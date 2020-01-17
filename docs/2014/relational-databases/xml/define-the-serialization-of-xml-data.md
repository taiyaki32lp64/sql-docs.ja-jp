---
title: XML データのシリアル化の定義 | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- entitization rules [XML in SQL Server]
- serialization
- reparsing serialized XML structures
- encoding [XML in SQL Server]
- XML [SQL Server], serialization
- xml data type [SQL Server], serialization
- typed XML
ms.assetid: 42b0b5a4-bdd6-4a60-b451-c87f14758d4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39f3ccc462fb063ecb314b1e9968dcfa8a095cbb
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688884"
---
# <a name="define-the-serialization-of-xml-data"></a>XML データのシリアル化の定義
  XML データ型を SQL 文字列型やバイナリ型に明示的または暗黙にキャストすると、XML データ型のコンテンツはこのトピックで説明する規則に従ってシリアル化されます。  
  
## <a name="serialization-encoding"></a>シリアル化のエンコード  
 SQL の対象型が VARBINARY の場合、結果は UTF-16 バイト順マークを前に付け、XML 宣言を付けずに、UTF-16 でシリアル化されます。 対象型が小さすぎる場合は、エラーが発生します。  
  
 例 :  
  
```sql
select CAST(CAST(N'<Δ/>' as XML) as VARBINARY(MAX))  
```  
  
 結果を次に示します。  
  
```  
0xFFFE3C0094032F003E00  
```  
  
 SQL の対象型が NVARCHAR または NCHAR の場合、結果はバイト順マークを前に付けず、XML 宣言を付けずに、UTF-16 でシリアル化されます。 対象型が小さすぎる場合は、エラーが発生します。  
  
 例 :  
  
```sql
select CAST(CAST(N'<Δ/>' as XML) as NVARCHAR(MAX))  
```  
  
 結果を次に示します。  
  
```  
<Δ/>  
```  
  
 SQL の対象型が VARCHAR または NCHAR の場合、結果はバイト順マークまたは XML 宣言を付けずに、データベースの照合順序のコード ページに対応するエンコードでシリアル化されます。 対象型が小さすぎるか、または対象の照合順序のコード ページに値をマップできない場合、エラーが発生します。  
  
 例 :  
  
```sql
select CAST(CAST(N'<Δ/>' as XML) as VARCHAR(MAX))  
```  
  
 現在の照合順序のコードページが Unicode 文字&#x10300;を表すことができない場合、または特定のエンコードで表現される場合、エラーが発生する可能性があります。  
  
 XML の結果がクライアント側に返されるときは、UTF-16 エンコードでデータが送信されます。 クライアント側のプロバイダーでは、API の規則に従ってデータを公開します。  
  
## <a name="serialization-of-the-xml-structures"></a>XML 構造のシリアル化  
 **xml** データ型のコンテンツは、通常の方法でシリアル化されます。 具体的には、要素ノードは要素マークアップにマップされ、テキスト ノードはテキスト コンテンツにマップされます。 ただし、文字がエンティティに変換される状況、および型指定されたアトミック値がシリアル化される方法については、次に説明します。  
  
## <a name="entitization-of-xml-characters-during-serialization"></a>シリアル化中の XML 文字のエンティティ変換  
 シリアル化されたすべての XML 構造は再解析が可能である必要があります。 したがって、XML パーサーの正規化フェーズ中に引き続き文字を互いにやり取りできるようにするには、一部の文字をエンティティに変換する方法でシリアル化する必要があります。 ただし、一部の文字をエンティティに変換する場合は、ドキュメントが整形式になり、解析可能になるようにする必要があります。 次に、シリアル化中に適用されるエンティティ変換の規則を示します。  
  
-   &、\<、> の文字が属性値や要素のコンテンツ内に出現する場合、常に、それぞれ &amp;、&lt;、&gt; にエンティティ変換されます。  
  
-   SQL Server では属性値を囲むために引用符 (U+0022) が使用されるので、属性値の引用符は &quot; にエンティティ変換されます。  
  
-   サーバーのみでキャストする場合は、サロゲート ペアが 1 つの数字参照としてエンティティ変換されます。 たとえば、サロゲート ペア U+D800 U+DF00 は、数字参照 &\#x00010300; にエンティティ変換されます。  
  
-   タブ (TAB, U+0009) とラインフィード (LF, U+000A) は、解析時に正規化されないように、属性値の内部でそれぞれ数字参照 &\#x9; および &\#xA; にエンティティ変換されます。  
  
-   キャリッジ リターン (CR, U+000D) は、解析時に正規化されないように、属性値と要素のコンテンツの両方の内部で数字参照 &\#xD; にエンティティ変換されます。  
  
-   空白文字だけが含まれているテキスト ノードを保護するために、空白文字の 1 つ (通常は最後の空白文字) が数字参照としてエンティティ変換されます。 このようにすると、解析時の空白文字の処理の設定とは無関係に、再解析時に空白文字のテキスト ノードが保持されます。  
  
 例 :  
  
```sql
declare @u NVARCHAR(50)  
set @u = N'<a a="  
    '+NCHAR(0xD800)+NCHAR(0xDF00)+N'>">   '+NCHAR(0xA)+N'</a>'  
select CAST(CONVERT(XML,@u,1) as NVARCHAR(50))  
```  
  
 結果を次に示します。  
  
```  
<a a="  
    𐌀>">     
</a>  
```  
  
 最後の空白文字の保護規則を適用しない場合は、 **xml** から文字列型またはバイナリ型にキャストするときに、CONVERT オプションを明示的に 1 に設定できます。 たとえば、エンティティ変換が行われないように、次のように設定できます。  
  
```sql
select CONVERT(NVARCHAR(50), CONVERT(XML, '<a>   </a>', 1), 1)  
```  
  
 [query() メソッド (XML データ型)](/sql/t-sql/xml/query-method-xml-data-type) の結果は、XML データ型のインスタンスになることに注意してください。 したがって、文字列型またはバイナリ型にキャストされる **query()** メソッドの結果は、上記の規則に従ってエンティティに変換されます。 エンティティに変換されていない文字列値を取得する場合は、代わりに [value() メソッド (XML データ型)](/sql/t-sql/xml/value-method-xml-data-type) を使用する必要があります。 次に、 **query()** メソッドを使用する例を示します。  
  
```sql
declare @x xml  
set @x = N'<a>This example contains an entitized char: <.</a>'  
select @x.query('/a/text()')  
```  
  
 結果を次に示します。  
  
```  
This example contains an entitized char: <.  
```  
  
 次に、 **value()** メソッドを使用する例を示します。  
  
```sql
select @x.value('(/a/text())[1]', 'nvarchar(100)')  
```  
  
 結果を次に示します。  
  
```  
This example contains an entitized char: <.  
```  
  
## <a name="serializing-a-typed-xml-data-type"></a>型指定された XML データ型のシリアル化  
 型指定された **xml** データ型のインスタンスには、XML スキーマ型に従って型指定される値が含まれています。 このような値は、XQuery が xs:string にキャストするのと同じ形式で、XML スキーマ型に従ってシリアル化されます。 詳細については、「 [XQuery での型キャストの規則](/sql/xquery/type-casting-rules-in-xquery)」を参照してください。  
  
 たとえば、次の例で示すように、xs:double の値 1.34e1 は 13.4 にシリアル化されます。  
  
```sql
declare @x xml  
set @x =''  
select CAST(@x.query('1.34e1') as nvarchar(50))  
```  
  
 これは、文字列値 13.4 を返します。  
  
## <a name="see-also"></a>参照  
 [XQuery での型キャストの規則](/sql/xquery/type-casting-rules-in-xquery)   
 [CAST および CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)  
  
  
