---
title: string-length 関数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- string-length function
- fn:string-length function
ms.assetid: 7cd69c8b-cf2c-478c-b9a3-e0e14e1aa8aa
author: rothja
ms.author: jroth
ms.openlocfilehash: 12ae1efbf900a505a5f257f9684842a0ad9ff21f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004654"
---
# <a name="functions-on-string-values---string-length"></a>文字列値に使用する関数 - string-length
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  文字列の長さを文字数として返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:string-length() as xs:integer  
fn:string-length($arg as xs:string?) as xs:integer  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 長さを計算する対象となるソース文字列です。  
  
## <a name="remarks"></a>コメント  
 場合の値 *$arg*は空のシーケンス、 **xs:integer** 0 の値が返されます。  
  
 XQuery 関数におけるサロゲート ペアの動作は、データベースの互換性レベルに左右されます。 互換性レベルが 110 以上の場合、各サロゲート ペアは 1 文字としてカウントされます。 互換性レベルがこれ未満の場合は、2 文字としてカウントされます。 詳細については、次を参照してください。 [ALTER DATABASE 互換性レベル&#40;TRANSACT-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)と[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)します。  
  
 値にサロゲート文字 2 文字で表される 4 バイトの Unicode 文字が含まれている場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] はサロゲート文字 1 つを 1 文字として計算します。  
  
 **String-length()** せず、パラメーターは、述語内でのみ使用できます。 たとえば、次のクエリでは <`ROOT`> 要素が返されます。  
  
```  
DECLARE @x xml;  
SET @x='<ROOT>Hello</ROOT>';  
SELECT @x.query('/ROOT[string-length()=5]');  
```  
  
## <a name="supplementary-characters-surrogate-pairs"></a>補助文字 (サロゲート ペア)  
 XQuery 関数におけるサロゲート ペアの動作は、データベースの互換性レベルに左右されます。場合によっては、関数の既定の名前空間 URI に左右されることもあります。 詳細については、のトピックでは、「XQuery 関数はサロゲート対応」のセクションを参照してください。 [SQL Server 2016 におけるデータベース エンジン機能の重大な変更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md)します。 参照してください[ALTER DATABASE 互換性レベル&#40;TRANSACT-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)と[Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md)します。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列には、AdventureWorks データベース。  
  
### <a name="a-using-the-string-length-xquery-function-to-retrieve-products-with-long-summary-descriptions"></a>A. XQuery の string-length() 関数を使用して、長い概要説明のある製品を取得する  
 次のクエリでは、概要説明が 50 文字を超える製品の製品 ID、概要説明の長さ、概要自体 (<`Summary`> 要素) を取得します。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT CatalogDescription.query('  
      <Prod ProductID= "{ /pd:ProductDescription[1]/@ProductModelID }" >  
       <LongSummary SummaryLength =   
           "{string-length(string( (/pd:ProductDescription/pd:Summary)[1] )) }" >  
           { string( (/pd:ProductDescription/pd:Summary)[1] ) }  
       </LongSummary>  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.value('string-length( string( (/pd:ProductDescription/pd:Summary)[1]))', 'decimal') > 200;  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   WHERE 句の条件により、XML ドキュメントに保持されている概要説明が 200 文字を超える行のみが取得されます。 使用して、 [value() メソッド (XML データ型)](../t-sql/xml/value-method-xml-data-type.md)します。  
  
-   SELECT 句は、必要な XML のみを構築しています。 使用して、 [query() メソッド (XML データ型)](../t-sql/xml/query-method-xml-data-type.md) XML を構築し、XML ドキュメントからデータを取得するために必要な XQuery 式を指定します。  
  
 これは、結果の一部です。  
  
```  
Result  
-------------------  
<Prod ProductID="19">  
      <LongSummary SummaryLength="214">Our top-of-the-line competition   
             mountain bike. Performance-enhancing options include the  
             innovative HL Frame, super-smooth front suspension, and   
             traction for all terrain.  
      </LongSummary>  
</Prod>  
...  
```  
  
### <a name="b-using-the-string-length-xquery-function-to-retrieve-products-whose-warranty-descriptions-are-short"></a>B. XQuery の string-length() 関数を使用して、保証内容が短い製品を取得する  
 次のクエリは、保証内容の記述が 20 文字に満たない製品の製品 ID、長さ、保証内容の記述、および <`Warranty`> 要素自体を含む XML を取得します。  
  
 保証は製品の特徴の 1 つです。 <`Features`> 要素の後に、省略可能な <`Warranty`> 子要素が続きます。  
  
```  
WITH XMLNAMESPACES (  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd,  
'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for   $ProdDesc in /pd:ProductDescription,  
            $pf in $ProdDesc/pd:Features/wm:Warranty  
      where string-length( string(($pf/wm:Description)[1]) ) < 20  
      return   
          <Prod >  
             { $ProdDesc/@ProductModelID }  
             <ShortFeature FeatureDescLength =   
                             "{string-length( string(($pf/wm:Description)[1]) ) }" >  
                 { $pf }  
             </ShortFeature>  
          </Prod>  
     ') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/pd:ProductDescription')=1;  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   **pd**と**wm**はこのクエリで使用される名前空間プレフィックス。 これらは、クエリ対象のドキュメントで使用されている同じ名前空間を示します。  
  
-   XQuery では、入れ子になった FOR ループを指定しています。 外側の FOR ループが必要な場合は、取得するため、 **ProductModelID**の属性、<`ProductDescription`> 要素。 また、保証内容の記述が 20 文字未満の製品のみを取得するので、内部 FOR ループも必要です。  
  
 結果の一部を次に示します。  
  
```  
Result  
-------------------------  
<Prod ProductModelID="19">  
  <ShortFeature FeatureDescLength="15">  
    <wm:Warranty   
       xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
      <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
      <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
   </ShortFeature>  
</Prod>  
...  
```  
  
## <a name="see-also"></a>参照  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
