---
title: "構造体の使用 (C# プログラミング ガイド)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- structs [C#], using
ms.assetid: cea4a459-9eb9-442b-8d08-490e0797ba38
caps.latest.revision: 28
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 67fa4f764e6e40041e4b8e37eccbd1adb2b509d3
ms.contentlocale: ja-jp
ms.lasthandoff: 07/28/2017

---
# <a name="using-structs-c-programming-guide"></a>構造体の使用 (C# プログラミング ガイド)
`struct` 型は、 `Point`、 `Rectangle`、 `Color`などの軽量のオブジェクトを表すのに適しています。 点を表すには [自動実装プロパティ](../../../csharp/language-reference/keywords/class.md) がある [クラス](../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md)を使用するのと同じくらい便利ですが、シナリオによっては [構造体](../../../csharp/language-reference/keywords/struct.md) を使用する方がより効率的です。 たとえば、1,000 個の `Point` オブジェクトから成る配列を宣言する場合は、各オブジェクトの参照用に追加のメモリを割り当てます。この場合、構造体であれば処理上の負荷を抑えることができます。 [!INCLUDE[dnprdnshort](~/includes/dnprdnshort-md.md)] には <xref:System.Drawing.Point>という名前のオブジェクトが含まれているため、この例の構造体には代わりに "CoOrds" という名前が付けられています。  
  
 [!code-cs[csProgGuideObjects#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-structs_1.cs)]  
  
 構造体に既定の (パラメーターなしの) コンストラクターを定義するとエラーになります。 また、構造体の本体のインスタンス フィールドを初期化した場合もエラーになります。 構造体メンバーを初期化するには、パラメーター化されたコンストラクターを使用するか、構造体を宣言した後で個別にメンバーにアクセスする必要があります。 プライベート メンバーや、その他のアクセスできないメンバーは、コンストラクター内でのみ初期化できます。  
  
 [new](../../../csharp/language-reference/keywords/new.md) 演算子を使用して struct オブジェクトを作成すると、オブジェクトが作成されて適切なコンストラクターが呼び出されます。 クラスとは異なり、構造体は `new` 演算子を使用せずにインスタンス化できます。 このような場合、コンストラクターの呼び出しが行われないため、割り当てがより効率的になります。 ただし、各フィールドは未割り当てのままになり、すべてのフィールドが初期化されるまではオブジェクトを使用できません。  
  
 構造体に参照型がメンバーとして含まれている場合は、メンバーの既定のコンストラクターを明示的に呼び出す必要があります。そうしないと、メンバーは未割り当てのままになり、構造体は使用できません (結果として、コンパイル エラー CS0171 が発生します)。  
  
 クラスには継承がありますが、構造体には継承がありません。 構造体は、他の構造体やクラスから継承できず、基本クラスになることはできません。 ただし、構造体は、基本クラス <xref:System.Object>から継承します。 構造体は、クラスの場合とまったく同じ方法でインターフェイスを実装できます。  
  
 `struct`キーワードを使用してクラスを宣言することはできません。 C# では、クラスと構造体は、意味が異なります。 構造体は値型ですが、クラスは参照型です。 詳細については、「 [Value Types (値型)](../../../csharp/language-reference/keywords/value-types.md)」を参照してください。  
  
 参照型の機能が必要な場合以外は、小さいクラスを構造体として宣言した方が、システムによってより効率的に処理される可能性があります。  
  
## <a name="example-1"></a>例 1  
  
### <a name="description"></a>説明  
 既定のコンストラクターとパラメーター化されたコンストラクターの両方を使用した `struct` の初期化の例を次に示します。  
  
### <a name="code"></a>コード  
 [!code-cs[csProgGuideObjects#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-structs_1.cs)]  
  
 [!code-cs[csProgGuideObjects#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-structs_2.cs)]  
  
## <a name="example-2"></a>例 2  
  
### <a name="description"></a>説明  
 構造体に固有の機能を次の例に示します。 この例では、 `new` 演算子を使用せずに CoOrds オブジェクトを作成しています。 `struct` を `class`という単語に置き換えた場合、プログラムはコンパイルされません。  
  
### <a name="code"></a>コード  
 [!code-cs[csProgGuideObjects#1](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-structs_1.cs)]  
  
 [!code-cs[csProgGuideObjects#3](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/using-structs_3.cs)]  
  
## <a name="see-also"></a>関連項目  
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)   
 [クラスと構造体](../../../csharp/programming-guide/classes-and-structs/index.md)   
 [構造体](../../../csharp/programming-guide/classes-and-structs/structs.md)

