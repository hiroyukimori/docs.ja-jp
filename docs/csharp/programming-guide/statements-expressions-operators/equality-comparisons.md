---
title: "等価比較 (C# プログラミング ガイド)"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- object equality [C#]
ms.assetid: 10b865ea-4e7b-4127-9242-c9b8f57d9f04
caps.latest.revision: 14
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
ms.openlocfilehash: 948bbc1b5b8535cc31ea362497fa69a816b43edc
ms.contentlocale: ja-jp
ms.lasthandoff: 07/28/2017

---
# <a name="equality-comparisons-c-programming-guide"></a>等価比較 (C# プログラミング ガイド)
2 つの値が等しいかどうかを比較することが必要な場合があります。 そのような場合、*値が等価であること* (*等価性*と呼ばれる) をテストすることになります。等価性とは 2 つの変数に含まれる値が等しいことを意味します。 また、2 つの変数がメモリ内の同一の基になるオブジェクトを参照しているかどうかを確認する必要がある場合もあります。 このタイプの等価は、*参照の等価性*または*同一性*と呼ばれます。 ここでは、2 種類の等価について説明します。また、詳細について他のトピックへのリンクを示します。  
  
## <a name="reference-equality"></a>参照の等価性  
 参照の等価とは、2 つのオブジェクト参照が同一の基になるオブジェクトを参照していることを意味します。 次の例に示すように、これは簡単な代入によって生じます。  
  
 [!code-cs[csProgGuideStatements#18](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/equality-comparisons_1.cs)]  
  
 このコードでは、2 つのオブジェクトが作成されますが、代入ステートメント以降は、両方の参照が同一のオブジェクトを参照しています。 したがって、参照の等価性があります。 2 つの参照が同じオブジェクトを参照しているかどうかを判断するには、<xref:System.Object.ReferenceEquals%2A> メソッドを使用します。  
  
 参照の等価性の概念は参照型のみに適用されます。 値型オブジェクトには参照の等価性がありません。これは、値型のインスタンスが変数に代入される場合、値のコピーが作成されるためです。 そのため、ボックス化を解除した 2 つの構造体でメモリ内の同じ場所を参照することはできません。 さらに、<xref:System.Object.ReferenceEquals%2A> を使用して 2 つの値型を比較する場合、オブジェクトに含まれている値がすべて同一である場合でも、結果は常に `false` になります。 これは、各変数が個別のオブジェクト インスタンスにボックス化されているためです。 詳細については、「[方法: 参照の等価性 (同値) をテストする](../../../csharp/programming-guide/statements-expressions-operators/how-to-test-for-reference-equality-identity.md)」を参照してください。  
  
## <a name="value-equality"></a>値の等価性  
 値が等価であるとは、2 つのオブジェクトが同じ値を含むことを意味します。 [int](../../../csharp/language-reference/keywords/int.md)、[bool](../../../csharp/language-reference/keywords/bool.md) などのプリミティブ値型では、値が等価であることをテストするのは簡単です。 次の例に示すように、[==](../../../csharp/language-reference/operators/equality-comparison-operator.md) 演算子を使用できます。  
  
```csharp  
int a = GetOriginalValue();  
int b = GetCurrentValue();  
  
// Test for value equality.   
if( b == a)   
{  
    // The two integers are equal.  
}  
```  
  
 それ以外のほとんどの型については、値が等価であることをテストするのは、もっと複雑です。特定の型で等価性がどのように定義されるかを理解する必要があるからです。 複数のフィールドまたはプロパティを含むクラスおよび構造体では、多くの場合、値が等価であるとは、すべてのフィールドまたはプロパティが同一の値を含むことであると定義されます。 たとえば、pointA.X が pointB.X と等しく、pointA.Y が pointB.Y と等しい場合、2 つの `Point` オブジェクトは等価であると定義されます。  
  
 ただし、等価性を 1 つの型のすべてのフィールドに基づいて判断する必要はありません。 サブセットに基づいて判断できます。 所有していない型を比較する場合は、その型の等価性がどのように定義されるのかを明確に理解している必要があります。 独自のクラスおよび構造体で値が等しいかどうかを定義する方法の詳細については、「[方法: 型の値の等価性を定義する](../../../csharp/programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md)」を参照してください。  
  
### <a name="value-equality-for-floating-point-values"></a>浮動小数点値での値の等価性  
 バイナリのコンピューター上での浮動小数点演算には誤差があるため、浮動小数点値 ([double](../../../csharp/language-reference/keywords/double.md) および [float](../../../csharp/language-reference/keywords/float.md)) の等価比較には問題があります。 詳細については、<xref:System.Double?displayProperty=fullName> のトピックの「解説」を参照してください。  
  
## <a name="related-topics"></a>関連トピック  
  
|タイトル|説明|  
|-----------|-----------------|  
|[方法: 参照の等価性 (同値) をテストする](../../../csharp/programming-guide/statements-expressions-operators/how-to-test-for-reference-equality-identity.md)|2 つの変数に参照の等価性があるかどうかを確認する方法を説明します。|  
|[方法: 型の値の等価性を定義する](../../../csharp/programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md)|型の値の等価性にカスタムの定義を指定する方法を説明します。|  
|[C# プログラミング ガイド](../../../csharp/programming-guide/index.md)|C# 言語の重要な機能に関する詳細情報へのリンクを示します。また、.NET Framework 経由でアクセスできる C# の機能について説明します。|  
|[型](../../../csharp/programming-guide/types/index.md)|C# 型システムについて説明し、詳細情報へのリンクを示します。|  
  
## <a name="see-also"></a>関連項目  
 [C# プログラミング ガイド](../../../csharp/programming-guide/index.md)

