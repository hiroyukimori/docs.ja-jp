---
title: "正規表現言語 - クイック リファレンス | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "VS.RegularExpressionBuilder"
helpviewer_keywords: 
  - ".NET Framework 正規表現, 言語要素"
  - "カンニング ペーパー"
  - "解析 (正規表現を使用したテキストを), 言語要素"
  - "パターン一致 (正規表現を使用した), 言語要素"
  - "regex カンニング ペーパー"
  - "正規表現 [.NET Framework]"
  - "正規表現, 言語要素"
  - "検索 (正規表現を使用した), 言語要素"
ms.assetid: 930653a6-95d2-4697-9d5a-52d11bb6fd4c
caps.latest.revision: 56
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 56
---
# 正規表現言語 - クイック リファレンス
<a name="top"></a> 正規表現とは、入力テキスト内で正規表現エンジンによる照合が試行されるパターンです。 パターンは、1 個以上の文字リテラル、演算子、または構成体で構成されます。  簡単な紹介については、「[.NET Framework の正規表現](../../../docs/standard/base-types/regular-expressions.md)」を参照してください。  
  
 このクイック リファレンスの各セクションでは、正規表現の定義に使用できる特定カテゴリの文字、演算子、および構成体を一覧表示します。  
  
 [文字のエスケープ](#character_escapes)  
 [文字クラス](#character_classes)  
 [アンカー](#atomic_zerowidth_assertions)  
 [グループ化構成体](#grouping_constructs)  
 [量指定子](#quantifiers)  
 [前方参照構成体](#backreference_constructs)  
 [代替構成体](#alternation_constructs)  
 [置換](#substitutions)  
 [正規表現のオプション](#options)  
 [その他の構成体](#miscellaneous_constructs)  
  
 また、ダウンロードして印刷し、簡単に参照できるように、この情報を 2 種類の形式で提供します  
  
 [Word \(.docx\) 形式でダウンロード](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)  
[PDF \(.pdf\) 形式でダウンロード](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)  
  
<a name="character_escapes"></a>   
## 文字のエスケープ  
 正規表現内の円記号 \(\\\) は、直後の文字が特殊文字 \(次の表を参照\) であるか、文字どおりに解釈する必要があることを示します。 詳細については、「[文字のエスケープ](../../../docs/standard/base-types/character-escapes-in-regular-expressions.md)」を参照してください。  
  
|エスケープ文字|説明|パターン|一致件数|  
|-------------|--------|----------|----------|  
|`\a`|ビープ音文字の \\u0007 と一致します。|`\a`|"Error\!" \+ '\\u0007'  の "\\u0007"|  
|`\b`|文字クラスでバックスペースの \\u0008 と一致します。|`[\b]{3,}`|"\\b\\b\\b\\b" の "\\b\\b\\b\\b"|  
|`\t`|タブの \\u0009 と一致します。|`(\w+)\t`|"item1\\titem2\\t" の "item1\\t"、"item2\\t"|  
|`\r`|キャリッジ リターンの \\u000D と一致します。 \(`\r` は改行文字 `\n` とは異なります。\)|`\r\n(\w+)`|"\\r\\nThese are\\ntwo lines." の "\\r\\nThese"|  
|`\v`|垂直タブの \\u000B と一致します。|`[\v]{2,}`|"\\v\\v\\v" の "\\v\\v\\v"|  
|`\f`|フォーム フィードの \\u000C と一致します。|`[\f]{2,}`|"\\f\\f\\f" の "\\f\\f\\f"|  
|`\n`|改行文字の \\u000A と一致します。|`\r\n(\w+)`|"\\r\\nThese are\\ntwo lines." の "\\r\\nThese"|  
|`\e`|エスケープ文字の \\u001B と一致します。|`\e`|"\\x001B" の "\\x001B"|  
|`\` *nnn*|8 進数表現で文字を指定します \(*nnn* は 2 桁または 3 桁で構成されます\)。|`\w\040\w`|"a bc d" の<br /><br /> "a b"、"c d"|  
|`\x` *nn*|16 進数表現で文字を指定します \(*nn* は 2 桁で構成されます\)。|`\w\x20\w`|"a bc d" の<br /><br /> "a b"、"c d"|  
|`\c` *X*<br /><br /> `\c` *x*|*X* または *x* で指定された ASCII の制御文字と一致します。*X* または *x* は制御文字です。|`\cC`|"\\x0003" \(Ctrl\-C\) の "\\x0003"|  
|`\u` *nnnn*|16 進数形式で表される Unicode 文字 \(*nnnn* で表される 4 桁の数字\) と一致します。|`\w\u0020\w`|"a bc d" の<br /><br /> "a b"、"c d"|  
|`\`|このトピック内の表に示されているエスケープ文字として認識されない文字が後ろに付いている場合は、その文字と一致します。 たとえば、`\*` は `\x2A` と同じであり、`\.` は `\x2E` と同じです。 これを使用すると、正規表現エンジンによって言語要素 \(\* や ? など\)  と文字リテラル \( や  で表されたもの\) のあいまいさが解消されます。|`\d+[\+-x\*]\d+`|"\(2\+2\) \* 3\*9" の "2\+2" および "3\*9"|  
  
 [ページのトップへ](#top)  
  
<a name="character_classes"></a>   
## 文字クラス  
 文字クラスは、文字セットのいずれかと一致します。 文字クラスに含まれる言語要素を次の表に示します。 詳細については、「[文字クラス](../../../docs/standard/base-types/character-classes-in-regular-expressions.md)」を参照してください。  
  
|文字クラス|説明|パターン|一致件数|  
|-----------|--------|----------|----------|  
|`[` *character\_group* `]`|*character\_group* 内の任意の 1 文字と一致します。 既定では、大文字と小文字が区別されます。|`[ae]`|"gray" の "a"<br /><br /> "lane" の "a"、"e"|  
|`[^` *character\_group* `]`|否定: *character\_group* 内にない任意の 1 文字と一致します。 既定では、*character\_group* の文字について、大文字と小文字が区別されます。|`[^aei]`|"reign" の "r"、"g"、"n"|  
|`[` *先頭* `-` *last* `]`|文字範囲: *first* から *last* までの範囲にある任意の 1 文字と一致します。|`[A-Z]`|"AB123" の "A"、"B"|  
|`.`|ワイルドカード: \\n を除く任意の 1 文字と一致します。<br /><br /> リテラルのピリオド文字 \(.  または `\u002E`\) と一致させるには、この文字の前にエスケープ文字 \(`\.`\) を指定します。|`a.e`|"nave" の "ave"<br /><br /> "water" の "ate"|  
|`\p{` *name* `}`|*name* で指定された名前付きブロックまたは Unicode 一般カテゴリ内の任意の 1 文字と一致します。|`\p{Lu}`<br /><br /> `\p{IsCyrillic}`|"City Lights" の "C"、"L"<br /><br /> "ДЖem" の "Д"、"Ж"|  
|`\P{` *name* `}`|*name* で指定された名前付きブロックまたは Unicode 一般カテゴリにない任意の 1 文字と一致します。|`\P{Lu}`<br /><br /> `\P{IsCyrillic}`|"City" の "i"、"t"、"y"<br /><br /> "ДЖem" の "e"、"m"|  
|`\w`|単語に使用される任意の文字と一致します。|`\w`|"ID A1.3" の "I"、"D"、"A"、"1"、"3"|  
|`\W`|単語に使用される文字以外の任意の文字と一致します。|`\W`|"ID A1.3" の " "、"."|  
|`\s`|空白文字と一致します。|`\w\s`|"ID A1.3" の "D "|  
|`\S`|空白以外の文字と一致します。|`\s\S`|"int \_\_ctr" の " \_"|  
|`\d`|10 進数字と一致します。|`\d`|"4 \= IV" の "4"|  
|`\D`|10 進数以外の任意の文字と一致します。|`\D`|"4 \= IV" の " "、"\="、" "、"I"、"V"|  
  
 [ページのトップへ](#top)  
  
<a name="atomic_zerowidth_assertions"></a>   
## アンカー  
 アンカー \(アトミック ゼロ幅アサーション\) を使用すると、文字列内での現在位置によって一致するかどうかが決まります。しかし、エンジンで後方の文字列が読み込まれたり、複数の文字と一致したりすることはありません。 アンカーであるメタ文字を次の表に示します。 詳細については、「[アンカー](../../../docs/standard/base-types/anchors-in-regular-expressions.md)」を参照してください。  
  
|アサーション|説明|パターン|一致件数|  
|------------|--------|----------|----------|  
|`^`|文字列または行の先頭で一致する必要があります。|`^\d{3}`|"901"<br /><br /> \("901\-333\-" の\)|  
|`$`|文字列の末尾で一致するか、行または文字列の末尾にある `\n` の前で一致する必要があります。|`-\d{3}$`|"\-333"<br /><br /> \("\-901\-333" の\)|  
|`\A`|文字列の先頭で一致する必要があります。|`\A\d{3}`|"901"<br /><br /> \("901\-333\-" の\)|  
|`\Z`|文字列の末尾で一致するか、文字列の末尾にある `\n` の前で一致する必要があります。|`-\d{3}\Z`|"\-333"<br /><br /> \("\-901\-333" の\)|  
|`\z`|文字列の末尾で一致する必要があります。|`-\d{3}\z`|"\-333"<br /><br /> \("\-901\-333" の\)|  
|`\G`|前回の一致が終了した位置で一致する必要があります。|`\G\(\d\)`|"\(1\)\(3\)\(5\)\[7\]\(9\)" の "\(1\)"、"\(3\)"、"\(5\)"|  
|`\b`|`\w` \(英数字\) と `\W` \(英数字以外\) 文字の境界位置で一致する必要があります。|`\b\w+\s\w+\b`|"them theme them them" の "them theme"|  
|`\B`|`\b` 境界以外で一致する必要があります。|`\Bend\w*\b`|"end sends endure lender" の "ends"、"ender"|  
  
 [ページのトップへ](#top)  
  
<a name="grouping_constructs"></a>   
## グループ化構成体  
 グループ化構成体は、正規表現の部分式を表し、通常は入力文字列の部分文字列をキャプチャします。 グループ化構成体に含まれる言語要素を次の表に示します。 詳細については、「[グループ化構成体](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)」を参照してください。  
  
|グループ化構成体|説明|パターン|一致件数|  
|--------------|--------|----------|----------|  
|`(` *subexpression* `)`|一致した部分式をキャプチャして、1 から始まる序数を代入します。|`(\w)\1`|"deep" の "ee"|  
|`(?<` *name* `>` *subexpression*`)`|一致した部分式を名前付きグループにキャプチャします。|`(?<double>\w)\k<double>`|"deep" の "ee"|  
|`(?<` *name1* `-` *name2* `>` *subexpression*`)`|グループ定義の均等化を定義します。 詳細については、「[グループ化構成体](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md)」の「グループ定義の均等化」を参照してください。|`(((?'Open'\()[^\(\)]*)+((?'Close-Open'\))[^\(\)]*)+)*(?(Open)(?!))$`|"3\+2^\(\(1\-3\)\*\(3\-1\)\)" の "\(\(1\-3\)\*\(3\-1\)\)"|  
|`(?:` *subexpression*`)`|非キャプチャ グループを定義します。|`Write(?:Line)?`|"Console.WriteLine\(\)" の "WriteLine"<br /><br /> "Console.Write\(value\)" の "Write"|  
|`(?imnsx-imnsx:` *subexpression*`)`|指定したオプションを *subexpression* に適用するか、または無効にします。 詳細については、「[正規表現のオプション](../../../docs/standard/base-types/regular-expression-options.md)」を参照してください。|`A\d{2}(?i:\w+)\b`|"A12xl A12XL a12xl" の "A12xl"、"A12XL"|  
|`(?=` *subexpression*`)`|ゼロ幅の肯定先読みアサーションです。|`\w+(?=\.)`|"He is. The dog ran. The sun is out." の "is"、"ran"、および "out"|  
|`(?!` *subexpression*`)`|ゼロ幅の否定先読みアサーションです。|`\b(?!un)\w+\b`|"unsure sure unity used" の "sure"、"used"|  
|`(?<=` *subexpression*`)`|ゼロ幅の正の後読みアサーションです。|`(?<=19)\d{2}\b`|"1851 1999 1950 1905 2003" の "99"、"50"、"05"|  
|`(?<!` *subexpression*`)`|ゼロ幅の負の後読みアサーションです。|`(?<!19)\d{2}\b`|"1851 1999 1950 1905 2003" の "51"、"03"|  
|`(?>` *subexpression*`)`|非バックトラッキング \("最長"\) 部分式です。|`[13579](?>A+B+)`|"1ABB 3ABBC 5AB 5AC" の "1ABB"、"3ABB"、および "5AB"|  
  
 [ページのトップへ](#top)  
  
<a name="quantifiers"></a>   
## 限定子  
 量指定子は、一致するために、入力文字列中に直前の要素 \(文字、グループ、または文字クラス\) がいくつ存在しなければならないかを指定します。 量指定子に含まれる言語要素を次の表に示します。 詳細については、「[限定子](../../../docs/standard/base-types/quantifiers-in-regular-expressions.md)」を参照してください。  
  
|量指定子|説明|パターン|一致件数|  
|----------|--------|----------|----------|  
|`*`|直前の要素と 0 回以上一致します。|`\d*\.\d`|".0"、"19.9"、"219.9"|  
|`+`|直前の要素と 1 回以上一致します。|`"be+"`|"been" の "bee"、"bent" の "be"|  
|`?`|直前の要素と 0 回または 1 回一致します。|`"rai?n"`|"ran"、"rain"|  
|`{` *n* `}`|直前の要素とちょうど *n* 回一致します。|`",\d{3}"`|"1,043.6" の ",043"、"9,876,543,210" の ",876"、",543"、および ",210"|  
|`{` *n* `,}`|直前の要素と *n* 回以上一致します。|`"\d{2,}"`|"166"、"29"、"1930"|  
|`{` *n* `,` *分* `}`|直前の要素と *n* 回以上 *m* 回以下で一致します。|`"\d{3,5}"`|"166"、"17668"<br /><br /> "193024" の "19302"|  
|`*?`|直前の要素と 0 回以上 \(ただし、できるだけ少ない回数\) 一致します。|`\d*?\.\d`|".0"、"19.9"、"219.9"|  
|`+?`|直前の要素と 1 回以上 \(ただし、できるだけ少ない回数\) 一致します。|`"be+?"`|"been" の "be"、"bent" の "be"|  
|`??`|直前の要素と 0 回または 1 回 \(ただし、できるだけ少ない回数\) 一致します。|`"rai??n"`|"ran"、"rain"|  
|`{` *n* `}?`|直前の要素とちょうど *n* 回一致します。|`",\d{3}?"`|"1,043.6" の ",043"、"9,876,543,210" の ",876"、",543"、および ",210"|  
|`{` *n* `,}?`|直前の要素と *n* 回以上 \(ただし、できるだけ少ない回数\) 一致します。|`"\d{2,}?"`|"166"、"29"、"1930"|  
|`{` *n* `,` *分* `}?`|直前の要素と *n* 回以上 *m* 回以下 \(ただし、できるだけ少ない回数\) 一致します。|`"\d{3,5}?"`|"166"、"17668"<br /><br /> "193024" の "193"、"024"|  
  
 [ページのトップへ](#top)  
  
<a name="backreference_constructs"></a>   
## 前方参照構成体  
 前方参照を使用すると、以前に一致した部分式を、同じ正規表現内で引き続き識別できます。 .NET Framework の正規表現でサポートされている前方参照構成体を、次の表に示します。 詳細については、「[前方参照構成体](../../../docs/standard/base-types/backreference-constructs-in-regular-expressions.md)」を参照してください。  
  
|前方参照構成体|説明|パターン|一致件数|  
|-------------|--------|----------|----------|  
|`\` *number*|前方参照。 番号付き部分式の値に一致します。|`(\w)\1`|"seek" の "ee"|  
|`\k<` *name* `>`|名前付き前方参照。 名前付きの式の値に一致します。|`(?<char>\w)\k<char>`|"seek" の "ee"|  
  
 [ページのトップへ](#top)  
  
<a name="alternation_constructs"></a>   
## 代替構成体  
 代替構成体は、OR 一致を有効にするように正規表現を変更します。 これらの構成体に含まれる言語要素を次の表に示します。 詳細については、「[代替構成体](../../../docs/standard/base-types/alternation-constructs-in-regular-expressions.md)」を参照してください。  
  
|代替構成体|説明|パターン|一致件数|  
|-----------|--------|----------|----------|  
|`&#124;`|縦棒 \(&#124;\) 文字で区切られた要素のいずれかと一致します。|`th(e&#124;is&#124;at)`|"this is the day." の "the"、"this "|  
|`(?(` *式* `)` *可* `&#124;` *no* `)`|*expression* で指定される正規表現パターンが一致する場合は *yes* と一致します。それ以外の場合は、*no* \(省略可能\) 部分と一致します。*expression* はゼロ幅アサーションとして解釈されます。|`(?(A)A\d{2}\b&#124;\b\d{3}\b)`|"A10 C103 910" の "A10"、"910"|  
|`(?(` *name* `)` *可* `&#124;` *no* `)`|名前付きまたは番号付きのキャプチャ グループ *name* に一致が見つかった場合は *yes* と一致します。それ以外の場合は *no* \(省略可能\) と一致します。|`(?<quoted>")?(?(quoted).+?"&#124;\S+\s)`|"Dogs.jpg "Yiska playing.jpg"" の Dogs.jpg、"Yiska playing.jpg"|  
  
 [ページのトップへ](#top)  
  
<a name="substitutions"></a>   
## 置換  
 置換は、置換パターンでサポートされる正規表現言語要素です。 詳細については、「[置換](../../../docs/standard/base-types/substitutions-in-regular-expressions.md)」を参照してください。 アトミック ゼロ幅アサーションであるメタ文字を次の表に示します。  
  
|文字|説明|パターン|置換パターン|入力文字列|結果文字列|  
|--------|--------|----------|------------|-----------|-----------|  
|`$` *number*|グループの *number* と一致した部分文字列に置換されます。|`\b(\w+)(\s)(\w+)\b`|`$3$2$1`|"one two"|"two one"|  
|`${` *name* `}`|名前付きグループの *name* と一致した部分文字列に置換されます。|`\b(?<word1>\w+)(\s)(?<word2>\w+)\b`|`${word2} ${word1}`|"one two"|"two one"|  
|`$$`|"$" リテラルに置換されます。|`\b(\d+)\s?USD`|`$$$1`|"103 USD"|"$103"|  
|`$&`|一致したパターン全体と同じパターンに置換されます。|`\$?\d*\.?\d+`|`**$&**`|"$1.30"|"\*\*$1.30\*\*"|  
|`$``|一致した場所より前にある入力文字列のすべてに置換されます。|`B+`|`$``|"AABBCC"|"AAAACC"|  
|`$'`|一致した場所より後にある入力文字列のすべてに置換されます。|`B+`|`$'`|"AABBCC"|"AACCCC"|  
|`$+`|キャプチャされた最後のグループに置換されます。|`B+(C+)`|`$+`|"AABBCCDD"|AACCDD|  
|`$_`|入力文字列全体に置換されます。|`B+`|`$_`|"AABBCC"|"AAAABBCCCC"|  
  
 [ページのトップへ](#top)  
  
<a name="options"></a>   
## 正規表現のオプション  
 正規表現エンジンで正規表現パターンを解釈する方法を制御するオプションを指定できます。 これらのオプションの多くは、インラインで \(正規表現パターンで\) 指定することも、1 つ以上の <xref:System.Text.RegularExpressions.RegexOptions> 定数として指定することもできます。 このクイック リファレンスでは、インライン オプションのみを示しています。 インライン オプションと <xref:System.Text.RegularExpressions.RegexOptions> オプションの詳細については、「[正規表現のオプション](../../../docs/standard/base-types/regular-expression-options.md)」を参照してください。  
  
 インライン オプションは、次の 2 種類の方法で指定できます。  
  
-   [その他の構成体](../../../docs/standard/base-types/miscellaneous-constructs-in-regular-expressions.md) `(?imnsx-imnsx)` の使用。オプションまたはオプション セットの前に負符号 \(\-\) がある場合、そのオプションが無効になります。 たとえば、`(?i-mn)` では、大文字と小文字を区別しない一致 \(`i`\) がオン、複数行モード \(`m`\) がオフ、名前のないグループ キャプチャ \(`n`\) がオフになります。 このオプションは、このオプションが定義されている位置から正規表現パターンに適用され、パターンの末尾まで、または別の構成体によってオプションが反転する位置まで有効になります。  
  
-   [グループ化構成体](../../../docs/standard/base-types/grouping-constructs-in-regular-expressions.md) `(?imnsx-imnsx:`*subexpression*`)` の使用。これは、指定されたグループのみに対するオプションを定義します。  
  
 .NET Framework 正規表現エンジンでは、次のインライン オプションがサポートされます。  
  
|オプション|説明|パターン|一致件数|  
|-----------|--------|----------|----------|  
|`i`|大文字と小文字を区別しない一致を使用します。|`\b(?i)a(?-i)a\w+\b`|"aardvark AAAuto aaaAuto Adam breakfast" の "aardvark"、"aaaAuto"|  
|`m`|複数行モードを使用します。`^` と `$` は、\(入力文字列の先頭および末尾ではなく\) 各行の先頭および末尾と一致します。|例については、「[正規表現のオプション](../../../docs/standard/base-types/regular-expression-options.md)」の「複数行モード」を参照してください。||  
|`n`|名前のないグループをキャプチャしません。|例については、「[正規表現のオプション](../../../docs/standard/base-types/regular-expression-options.md)」の「明示的なキャプチャのみ」を参照してください。||  
|`s`|単一行モードを使用します。|例については、「[正規表現のオプション](../../../docs/standard/base-types/regular-expression-options.md)」の「単一行モード」を参照してください。||  
|`x`|正規表現パターンでエスケープされていない空白を無視します。|`\b(?x) \d+ \s \w+`|"1 aardvark 2 cats IV centurions" の "1 aardvark"、"2 cats"|  
  
 [ページのトップへ](#top)  
  
<a name="miscellaneous_constructs"></a>   
## その他の構成体  
 その他の構成体は、正規表現パターンを変更するか、それに関する情報を指定します。 .NET Framework でサポートされているその他の構成体を、次の表に示します。 詳細については、「[その他の構成体](../../../docs/standard/base-types/miscellaneous-constructs-in-regular-expressions.md)」を参照してください。  
  
|構成体|定義|例|  
|---------|--------|-------|  
|`(?imnsx-imnsx)`|パターンの途中で、大文字と小文字の区別などのオプションを設定または無効化します。 詳細については、「[正規表現のオプション](../../../docs/standard/base-types/regular-expression-options.md)」を参照してください。|`\bA(?i)b\w+\b` は、"ABA Able Act" の "ABA"、"Able" に一致します。|  
|`(?#` *comment*`)`|インライン コメントです。 コメントは、最初の閉じかっこで終了します。|`\bA(?#Matches words starting with A)\w+\b`|  
|`#` \[to end of line\]|X モード コメントです。 コメントの先頭はエスケープされない `#` で、コメントは行末まで継続します。|`(?x)\bA\w+\b#Matches words starting with A`|  
  
## 参照  
 <xref:System.Text.RegularExpressions?displayProperty=fullName>   
 <xref:System.Text.RegularExpressions.Regex>   
 [.NET Framework の正規表現](../../../docs/standard/base-types/regular-expressions.md)   
 [正規表現クラス](../../../docs/standard/base-types/the-regular-expression-object-model.md)   
 [正規表現の例](../../../docs/standard/base-types/regular-expression-examples.md)   
 [正規表現 \- クイック リファレンス \(Word 形式でダウンロード\)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)   
 [正規表現 \- クイック リファレンス \(PDF 形式でダウンロード\)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)