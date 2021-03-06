---
title: "標準クエリ演算子 (Visual Basic) のクエリ式構文 |Microsoft ドキュメント"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: eb978d86-d3b5-497b-95ce-a054bea8f510
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 53f975855c4d740e0b0373d384a9383ded410bd9
ms.lasthandoff: 03/13/2017

---
# <a name="query-expression-syntax-for-standard-query-operators-visual-basic"></a>標準クエリ演算子 (Visual Basic) のクエリ式の構文
Visual Basic 言語のキーワード構文の一部として呼び出せるようにする専用の使用頻度の高い標準クエリ演算子の一部が、*クエリ式*します。 クエリ式が異なり、読み取りやすくよりもクエリを表現する形式、*メソッドに基づく*と同じです。 クエリ式の句は、コンパイル時にクエリ メソッドへの呼び出しに変換されます。  
  
## <a name="query-expression-syntax-table"></a>式の構文のテーブルを照会する.  
 次の表では、標準クエリ演算子と同等のクエリ式の句は一覧表示します。  
  
|メソッド|Visual Basic のクエリ式の構文|  
|------------|------------------------------------------|  
|<xref:System.Linq.Enumerable.All%2A></xref:System.Linq.Enumerable.All%2A>|`Aggregate … In … Into All(…)`<br /><br /> (詳細については、次を参照してください[Aggregate 句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Any%2A></xref:System.Linq.Enumerable.Any%2A>|`Aggregate … In … Into Any()`<br /><br /> (詳細については、次を参照してください[Aggregate 句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Average%2A></xref:System.Linq.Enumerable.Average%2A>|`Aggregate … In … Into Average()`<br /><br /> (詳細については、次を参照してください[Aggregate 句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Cast%2A></xref:System.Linq.Enumerable.Cast%2A>|`From … As …`<br /><br /> (詳細については、次を参照してください[From 句](../../../../visual-basic/language-reference/queries/from-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Count%2A></xref:System.Linq.Enumerable.Count%2A>|`Aggregate … In … Into Count()`<br /><br /> (詳細については、次を参照してください[Aggregate 句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Distinct%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29></xref:System.Linq.Enumerable.Distinct%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>|`Distinct`<br /><br /> (詳細については、次を参照してください[Distinct 句](../../../../visual-basic/language-reference/queries/distinct-clause.md)。)。|  
|<xref:System.Linq.Enumerable.GroupBy%2A></xref:System.Linq.Enumerable.GroupBy%2A>|`Group … By … Into …`<br /><br /> (詳細については、次を参照してください[グループ By 句](../../../../visual-basic/language-reference/queries/group-by-clause.md)。)。|  
|<xref:System.Linq.Enumerable.GroupJoin%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2C%60%603%7D%29></xref:System.Linq.Enumerable.GroupJoin%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2C%60%603%7D%29>|`Group Join … In … On …`<br /><br /> (詳細については、次を参照してください[Group Join 句](../../../../visual-basic/language-reference/queries/group-join-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%29></xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%29>|`From x In …, y In … Where x.a = b.a`<br /><br /> または<br /><br /> `Join … [As …]In … On …`<br /><br /> (詳細については、次を参照してください[Join 句](../../../../visual-basic/language-reference/queries/join-clause.md)。)。|  
|<xref:System.Linq.Enumerable.LongCount%2A></xref:System.Linq.Enumerable.LongCount%2A>|`Aggregate … In … Into LongCount()`<br /><br /> (詳細については、次を参照してください[Aggregate 句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Max%2A></xref:System.Linq.Enumerable.Max%2A>|`Aggregate … In … Into Max()`<br /><br /> (詳細については、次を参照してください[Aggregate 句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Min%2A></xref:System.Linq.Enumerable.Min%2A>|`Aggregate … In … Into Min()`<br /><br /> (詳細については、次を参照してください[Aggregate 句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)。)。|  
|<xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29></xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By`<br /><br /> (詳細については、次を参照してください[Order By 句](../../../../visual-basic/language-reference/queries/order-by-clause.md)。)。|  
|<xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29></xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By … Descending`<br /><br /> (詳細については、次を参照してください[Order By 句](../../../../visual-basic/language-reference/queries/order-by-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Select%2A></xref:System.Linq.Enumerable.Select%2A>|`Select`<br /><br /> (詳細については、次を参照してください[Select 句](../../../../visual-basic/language-reference/queries/select-clause.md)。)。|  
|<xref:System.Linq.Enumerable.SelectMany%2A></xref:System.Linq.Enumerable.SelectMany%2A>|複数`From`句<br /><br /> (詳細については、次を参照してください[From 句](../../../../visual-basic/language-reference/queries/from-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Skip%2A></xref:System.Linq.Enumerable.Skip%2A>|`Skip`<br /><br /> (詳細については、次を参照してください[Skip 句](../../../../visual-basic/language-reference/queries/skip-clause.md)。)。|  
|<xref:System.Linq.Enumerable.SkipWhile%2A></xref:System.Linq.Enumerable.SkipWhile%2A>|`Skip While`<br /><br /> (詳細については、次を参照してください[Skip While 句](../../../../visual-basic/language-reference/queries/skip-while-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Sum%2A></xref:System.Linq.Enumerable.Sum%2A>|`Aggregate … In … Into Sum()`<br /><br /> (詳細については、次を参照してください[Aggregate 句](../../../../visual-basic/language-reference/queries/aggregate-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Take%2A></xref:System.Linq.Enumerable.Take%2A>|`Take`<br /><br /> (詳細については、次を参照してください[Take 句](../../../../visual-basic/language-reference/queries/take-clause.md)。)。|  
|<xref:System.Linq.Enumerable.TakeWhile%2A></xref:System.Linq.Enumerable.TakeWhile%2A>|`Take While`<br /><br /> (詳細については、次を参照してください[を While 句](../../../../visual-basic/language-reference/queries/take-while-clause.md)。)。|  
|<xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29></xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By …, …`<br /><br /> (詳細については、次を参照してください[Order By 句](../../../../visual-basic/language-reference/queries/order-by-clause.md)。)。|  
|<xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29></xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%29>|`Order By …, … Descending`<br /><br /> (詳細については、次を参照してください[Order By 句](../../../../visual-basic/language-reference/queries/order-by-clause.md)。)。|  
|<xref:System.Linq.Enumerable.Where%2A></xref:System.Linq.Enumerable.Where%2A>|`Where`<br /><br /> (詳細については、次を参照してください[Where 句の](../../../../visual-basic/language-reference/queries/where-clause.md)。)。|  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Linq.Enumerable></xref:System.Linq.Enumerable>   
 <xref:System.Linq.Queryable></xref:System.Linq.Queryable>   
 [標準クエリ演算子の概要 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [(Visual Basic) の実行方法による標準クエリ演算子の分類](../../../../visual-basic/programming-guide/concepts/linq/classification-of-standard-query-operators-by-manner-of-execution.md)
