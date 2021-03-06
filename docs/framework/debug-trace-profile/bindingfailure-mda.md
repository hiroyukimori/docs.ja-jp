---
title: bindingFailure MDA
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- binding failure
- binding, failures
- MDAs (managed debugging assistants), binding failures
- assemblies [.NET Framework], binding failures
- managed debugging assistants (MDAs), binding failures
- BindingFailure MDA
ms.assetid: 26ada5af-175c-4576-931a-9f07fa1723e9
caps.latest.revision: 13
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 4e78cdcc5bcf69902675fceacc9dac245bfec336
ms.contentlocale: ja-jp
ms.lasthandoff: 08/21/2017

---
# <a name="bindingfailure-mda"></a>bindingFailure MDA
`bindingFailure` マネージ デバッグ アシスタント (MDA) は、アセンブリの読み込みに失敗したときにアクティブになります。  
  
## <a name="symptoms"></a>症状  
 コードは、静的参照またはいずれかのローダー メソッド (<xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> や <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName> など) を使用して、アセンブリを読み込もうとしました。 アセンブリは読み込まれず、<xref:System.IO.FileNotFoundException> または <xref:System.IO.FileLoadException> 例外がスローされました。  
  
## <a name="cause"></a>原因  
 バインディング エラーは、ランタイムがアセンブリを読み込むことができない場合に発生します。 バインディング エラーは、次のいずれかの状況の結果として発生することもあります。  
  
-   共通言語ランタイム (CLR) は、要求されたアセンブリを見つけることができません。 考えられる理由は多数あります。たとえば、アセンブリがインストールされていない、あるいはアプリケーションがアセンブリを見つけるように正しく構成されていないなどです。  
  
-   一般的な問題のシナリオの場合、型は別のアプリケーション ドメインに渡されます。CLR は、他のアプリケーション ドメインにその型が含まれているアセンブリを読み込む必要があります。 他のアプリケーション ドメインが元のアプリケーション ドメインとは異なる構成の場合、ランタイムがアセンブリを読み込めないことがあります。 たとえば、2 つのアプリケーション ドメインで、<xref:System.AppDomain.BaseDirectory%2A> プロパティ値が異なる可能性があります。  
  
-   要求されたアセンブリは、破損しているか、アセンブリではありません。  
  
-   アセンブリを読み込もうとしているコードには、アセンブリを読み込むための適切なコード アクセス セキュリティのアクセス許可が指定されていません。  
  
-   ユーザー資格情報には、ファイルを読み取るために必要なアクセス許可が指定されていません。  
  
## <a name="resolution"></a>解決策  
 最初の手順は、要求されたアセンブリに CLR がバインドできなかった原因を特定することです。 たとえば、「原因」セクションに一覧表示されたシナリオのように、ランタイムが要求されたアセンブリを見つけられなかったり、読み込めなかったりする理由は多数あります。 バインディング エラーの原因を除去するには、次のアクションをお勧めします。  
  
-   `bindingFailure` MDA によって提供されるデータを使用して、原因を特定します。  
  
    -   アセンブリ バインダーによって生成されるエラー ログを読み取るために、[Fuslogvw.exe (アセンブリ バインディング ログ ビューアー)](../../../docs/framework/tools/fuslogvw-exe-assembly-binding-log-viewer.md) を実行します。  
  
    -   アセンブリが要求された位置にあるかどうかを確認します。 <xref:System.Reflection.Assembly.LoadFrom%2A> および <xref:System.Reflection.Assembly.LoadFile%2A> メソッドの場合は、要求された位置を簡単に確認できます。 <xref:System.Reflection.Assembly.Load%2A> メソッドの場合は、アセンブリ ID を使用してバインドするため、アプリケーション ドメインの <xref:System.AppDomain.BaseDirectory%2A> プロパティ プローブ パスおよびグローバル アセンブリ キャッシュで、アセンブリ ID と一致するアセンブリを検索する必要があります。  
  
-   前の手順で確認した内容に基づいて、原因を解決します。 使用できる解決オプションは、次のとおりです。  
  
    -   要求されたアセンブリをグローバル アセンブリ キャッシュにインストールし、 <xref:System.Reflection.Assembly.Load%2A> メソッドを呼び出して ID でアセンブリを読み込みます。  
  
    -   要求されたアセンブリをアプリケーション ディレクトリにコピーし、<xref:System.Reflection.Assembly.Load%2A> メソッドを呼び出して ID でアセンブリを読み込みます。  
  
    -   <xref:System.AppDomain.BaseDirectory%2A> プロパティを変更するか、プライベート プローブ パスを追加して、バインディング エラーが発生したアプリケーション ドメインがアセンブリ パスを含むように再構成します。  
  
    -   ログオンしているユーザーがファイルを読み取れるように、ファイルのアクセス制御リストを変更します。  
  
## <a name="effect-on-the-runtime"></a>ランタイムへの影響  
 この MDA は CLR に影響しません。 バインディング エラーに関するデータを報告するだけです。  
  
## <a name="output"></a>出力  
 MDA は、読み込みに失敗したアセンブリを報告します。これには、要求されたパスや表示名、バインディング コンテキスト、読み込みが要求されたアプリケーション ドメイン、エラーの理由などが含まれます。  
  
 表示名や要求されたパスは、そのデータが CLR で利用できなかった場合は空白である場合があります。 失敗した呼び出しが <xref:System.Reflection.Assembly.Load%2A> メソッドに対するものであった場合は、ランタイムがアセンブリの表示名を判別できなかったことが考えられます。  
  
## <a name="configuration"></a>構成  
  
```xml  
<mdaConfig>  
  <assistants>  
    <bindingFailure />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="example"></a>例  
 次のコードの例は、この MDA がアクティブ化されることのある状況を示しています。  
  
```  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Reflection;  
namespace ConsoleApplication1  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            // This call attempts to load a nonexistent assembly.  
            // The call will throw a System.IO.FileNotFound exception  
            // and cause the activation of the bindingFailure MDA   
            // if it is registered.  
            Assembly.Load("NonExistentAssembly");  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>関連項目  
 [マネージ デバッグ アシスタントによるエラーの診断](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)

