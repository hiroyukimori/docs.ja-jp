---
title: "動的言語ランタイムの概要 | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dynamic language runtime
- IronPython
- DLR
- IronRuby
ms.assetid: f769a271-8aff-4bea-bfab-6160217ce23d
caps.latest.revision: 26
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Machine Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 0930cd01af6af3f00aae070e712e5a758fd99090
ms.contentlocale: ja-jp
ms.lasthandoff: 06/02/2017

---
# <a name="dynamic-language-runtime-overview"></a>動的言語ランタイムの概要
*動的言語ランタイム* (DLR) とは、動的言語の一連のサービスを共通言語ランタイム (CLR) に追加するランタイム環境です。 DLR により、.NET Framework 上で実行される動的言語の開発や、静的に型指定された言語への動的機能の追加が簡単になります。  
  
 静的に型指定された言語である C# や Visual Basic (`Option Explicit On` を使用する場合) では、オブジェクトの型をデザイン時に指定する必要があるのに対して、動的言語では、オブジェクトの型を実行時に識別できます。 動的言語の例には、Lisp、Smalltalk、JavaScript、PHP、Ruby、Python、ColdFusion、Lua、Cobra、Groovy などがあります。  
  
 動的言語の多くには、開発者に次の利点があります。  
  
-   高速フィードバック ループ (REPL、つまり Read-Evaluate-Print Loop) を使用する機能。 この機能により、いくつかのステートメントを入力し、すぐに実行して結果を表示できます。  
  
-   トップダウン式の開発と従来のボトムアップ式の開発の両方に対するサポート。 たとえば、トップダウン アプローチを使用する場合は、まだ実装されていない関数を呼び出し、後で必要なときに基になる実装を追加できます。  
  
-   リファクタリングとコード変更の容易さ。コード全体で静的な型宣言を変更する必要がありません。  
  
 動的言語は、優れたスクリプト言語です。 動的言語使用して作成されたアプリケーションは、新しいコマンドや機能を追加してユーザーが簡単に拡張できます。 動的言語は、Web サイトやテスト ハーネスの作成、サーバー ファームの管理、さまざまなユーティリティの開発、データ変換の実行にもよく使用されます。  
  
 DLR の目的は、動的言語のシステムを .NET Framework 上で実行でき、.NET と相互運用できるようにすることです。 DLR は、Visual Studio 2010 の C# と Visual Basic に動的オブジェクトを導入して、これらの言語での動的な動作をサポートし、動的言語との相互運用を可能にします。  
  
 DLR は、動的な操作をサポートするライブラリを作成する場合にも役立ちます。 たとえば、XML オブジェクトまたは JavaScript Object Notation (JSON) オブジェクトを使用するライブラリがある場合、DLR を使用する言語では、それらのオブジェクトを動的オブジェクトとして利用できます。 このため、ライブラリ ユーザーは、構文的に簡単でわかりやすいコードを作成して、オブジェクトの操作やオブジェクト メンバーへのアクセスを行うことができます。  
  
 たとえば、C# では、XML のカウンターをインクリメントするために次のコードを使用します。  
  
 `Scriptobj.SetProperty("Count", ((int)GetProperty("Count")) + 1);`  
  
 DLR を使用すると、次のコードを代わりに使用して同じ操作を実行できます。  
  
 `scriptobj.Count += 1;`  
  
 CLR と同様に、DLR は .NET Framework の一部であり、.NET Framework および Visual Studio のインストール パッケージに付属しています。 オープン ソース バージョンの DLR は、[CodePlex](http://go.microsoft.com/fwlink/?LinkId=141028) の Web サイトからダウンロードすることもできます。  
  
> [!NOTE]
>  オープン ソース バージョンの DLR には、Visual Studio および .NET Framework に含まれている DLR の機能がすべて組み込まれています。 また、言語実装者向けの追加サポートも用意されています。 詳細については、[CodePlex](http://go.microsoft.com/fwlink/?LinkId=141028) の Web サイトのドキュメントを参照してください。  
  
 以下は、DLR を使用して開発された言語の例です。  
  
-   IronPython。 [CodePlex](http://go.microsoft.com/fwlink/?LinkId=141040) の Web サイトから、オープン ソース ソフトウェアとして入手できます。  
  
-   IronRuby。 [RubyForge](http://go.microsoft.com/fwlink/?LinkId=141044) の Web サイトから、オープン ソース ソフトウェアとして入手できます。  
  
## <a name="primary-dlr-advantages"></a>DLR の主な利点  
 DLR には、次の利点があります。  
  
### <a name="simplifies-porting-dynamic-languages-to-the-net-framework"></a>動的言語の .NET Framework への移植を簡略化  
 DLR により、言語実装者は、構文アナライザー、パーサー、セマンティクス アナライザー、コード ジェネレーター、および従来は自身で作成する必要があったその他のツールを作成せずに済みます。 DLR を使用する言語では、言語レベルのコードをツリー状の構造で表す*式ツリー*、ランタイム ヘルパー ルーチン、およびオプションとして <xref:System.Dynamic.IDynamicMetaObjectProvider> インターフェイスを実装する動的オブジェクトを生成する必要があります。 DLR と .NET Framework により、コード分析タスクやコード生成タスクの多くの部分が自動化されます。 このため、言語実装者は固有の言語機能に集中できます。  
  
### <a name="enables-dynamic-features-in-statically-typed-languages"></a>静的に型指定された言語での動的機能を使用が可能  
 C# や Visual Basic などの既存の .NET Framework 言語では、動的オブジェクトを作成し、静的に型指定されたオブジェクトと一緒に使用できます。 たとえば、C# や Visual Basic で、HTML、ドキュメント オブジェクト モデル (DOM)、および .NET リフレクションの動的オブジェクトを使用できます。  
  
### <a name="provides-future-benefits-of-the-dlr-and-net-framework"></a>DLR と .NET Framework の将来的な利点の活用  
 DLR を使用して実装された言語は、DLR と .NET Framework で将来的に強化される機能を活用できます。 たとえば、ガベージ コレクターの強化やアセンブリの読み込み時間の高速化が盛り込まれた .NET Framework の新しいバージョンがリリースされた場合、DLR を使用して実装された言語は、その恩恵をすぐに受けます。 同様に、コンパイルの向上など、DLR の最適化が行われた場合は、DLR を使用して実装されたすべての言語でもパフォーマンスが向上します。  
  
### <a name="enables-sharing-of-libraries-and-objects"></a>ライブラリとオブジェクトの共有が可能  
 ある言語で実装されたオブジェクトとライブラリを、他の言語で使用できます。 また、DLR では、静的に型指定された言語と動的言語の間の相互運用も可能になります。 たとえば、動的言語で記述されたライブラリを使用する動的オブジェクトを C# で宣言できます。 同時に、.NET Framework のライブラリを動的言語で使用できます。  
  
### <a name="provides-fast-dynamic-dispatch-and-invocation"></a>迅速な動的ディスパッチと呼び出しの実現  
 DLR では、高度なポリモーフィック キャッシュをサポートすることで、迅速な動的操作を提供します。 DLR は、オブジェクトを使用する操作を必要なランタイムの実装にバインドする規則を作成し、それらの規則をキャッシュします。これにより、同じ型のオブジェクトで同じコードが連続的に実行されるときに、リソースを大量に消費するバインド計算の発生を防ぎます。  
  
## <a name="dlr-architecture"></a>DLR のアーキテクチャ  
 動的言語ランタイムのアーキテクチャを次の図に示します。  
  
 ![動的言語ランタイム アーキテクチャの概要](../../../docs/framework/reflection-and-codedom/media/dlr-archoverview.png "DLR_ArchOverview")  
DLR のアーキテクチャ  
  
 DLR は、動的言語のサポートを強化するために一連のサービスを CLR に追加します。 これらのサービスには、次のようなものが含まれます。  
  
-   式ツリー。 DLR では、式ツリーを使用して言語のセマンティクスを表します。 この目的から、DLR では LINQ の式ツリーが拡張され、制御フロー、代入、およびその他の言語モデリング ノードが追加されています。 詳細については、「[式ツリー](http://msdn.microsoft.com/library/fb1d3ed8-d5b0-4211-a71f-dd271529294b)」を参照してください。  
  
-   呼び出しサイトのキャッシュ。 *動的呼び出しサイト*とは、動的オブジェクトに `a + b` や `a.b()` などの操作を実行するコード内の場所です。 DLR は、`a` と `b` の特性 (通常はこれらのオブジェクトの型) や操作に関する情報をキャッシュします。 同様の操作が以前に実行されていた場合、DLR は、必要なすべての情報をキャッシュから取得して、高速なディスパッチを実現します。  
  
-   動的オブジェクトの相互運用性。 DLR には、動的オブジェクトと操作を表し、言語実装者や動的ライブラリの作成者が使用できるクラスとインターフェイスのセットが用意されています。 このようなクラスやインターフェイスには、<xref:System.Dynamic.IDynamicMetaObjectProvider><xref:System.Dynamic.DynamicMetaObject><xref:System.Dynamic.DynamicObject> および <xref:System.Dynamic.ExpandoObject> があります。  
  
 DLR では、呼び出しサイトのバインダーを使用して、.NET Framework だけでなく、Silverlight や COM などの他のインフラストラクチャやサービスとも通信します。 バインダーは、言語のセマンティクスをカプセル化し、式ツリーを使用して呼び出しサイトの操作を実行する方法を指定します。 これにより、DLR を使用する動的言語および静的に型指定された言語で、ライブラリを共有し、DLR がサポートするすべてのテクノロジを利用できるようになります。  
  
## <a name="dlr-documentation"></a>DLR に関するドキュメント  
 言語に動的な動作を追加するためにオープン ソース バージョンの DLR を使用する方法、および .NET Framework で動的言語の使用を有効にする方法については、[CodePlex](http://go.microsoft.com/fwlink/?LinkId=141028) の Web サイトを参照してください。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Dynamic.ExpandoObject>   
 <xref:System.Dynamic.DynamicObject>   
 [共通言語ランタイム (CLR)](../../../docs/standard/clr.md)   
 [Expression Trees](http://msdn.microsoft.com/library/fb1d3ed8-d5b0-4211-a71f-dd271529294b)   
 [チュートリアル: 動的オブジェクトの作成と使用](~/docs/csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)