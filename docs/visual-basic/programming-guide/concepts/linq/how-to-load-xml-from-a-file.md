---
title: "方法: ファイル (Visual Basic の場合) から XML を読み込む |Microsoft ドキュメント"
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
ms.assetid: e2d337ad-8ac8-4671-b694-30e5ca1413b7
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
ms.openlocfilehash: 54755384eaf74fa008f93198f3de5e44fb095bda
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-load-xml-from-a-file-visual-basic"></a>方法: ファイル (Visual Basic の場合) から XML を読み込む
このトピックで説明を使用して、URI から XML を読み込む方法、<xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>メソッド</xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>。  
  
## <a name="example"></a>例  
 次の例では、ファイルから XML ドキュメントを読み込む方法を示します。 この例では、books.xml を読み込んで、XML ツリーをコンソールに出力します。  
  
 この例は、次の XML ドキュメントを使用して:[サンプル XML ファイル: 書籍 (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-books-linq-to-xml.md)します。  
  
```vb  
Dim booksFromFile As XElement = XElement.Load("books.xml")  
Console.WriteLine(booksFromFile)  
```  
  
 このコードを実行すると、次の出力が生成されます。  
  
```xml  
<Catalog>  
  <Book id="bk101">  
    <Author>Garghentini, Davide</Author>  
    <Title>XML Developer's Guide</Title>  
    <Genre>Computer</Genre>  
    <Price>44.95</Price>  
    <PublishDate>2000-10-01</PublishDate>  
    <Description>An in-depth look at creating applications   
      with XML.</Description>  
  </Book>  
  <Book id="bk102">  
    <Author>Garcia, Debra</Author>  
    <Title>Midnight Rain</Title>  
    <Genre>Fantasy</Genre>  
    <Price>5.95</Price>  
    <PublishDate>2000-12-16</PublishDate>  
    <Description>A former architect battles corporate zombies,   
      an evil sorceress, and her own childhood to become queen   
      of the world.</Description>  
  </Book>  
</Catalog>  
```  
  
## <a name="see-also"></a>関連項目  
 [(Visual Basic) の XML の解析](../../../../visual-basic/programming-guide/concepts/linq/parsing-xml.md)
