---
title: コンス トラクター関数 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- constructor functions [XQuery]
ms.assetid: 98562d0e-d0e0-4f62-b001-90acbac67277
author: rothja
ms.author: jroth
ms.openlocfilehash: 7f64c9ff6664410983d9c3ce7ebdbf07e493ca03
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038993"
---
# <a name="constructor-functions-xquery"></a>コンストラクター関数 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  コンストラクター関数は、指定された入力から、XSD の組み込みのアトミック型またはユーザー定義のアトミック型のインスタンスを生成します。  
  
## <a name="syntax"></a>構文  
  
```  
  
TYP($atomicvalue as xdt:anyAtomicType?  
  
) as TYP?  
  
```  
  
## <a name="arguments"></a>引数  
 *$strval*  
 変換される文字列。  
  
 *TYP*  
 任意の組み込み XSD 型。  
  
## <a name="remarks"></a>コメント  
 コンストラクターは基本データ型、および派生されたアトミック XSD 型に対してサポートされています。 ただしのサブタイプ**xs:duration**、含む**xdt:yearMonthDuration と xdt:dayTimeDuration**と**xs:QName**、 **xs:NMTOKEN**、および**xs:NOTATION**はサポートされていません。 関連するスキーマ コレクションで利用可能なユーザー定義のアトミック型も使用できます。ただし、それらは次に示す型から直接または間接的に派生されている必要があります。  
  
#### <a name="supported-base-types"></a>サポートされている基本データ型  
 サポートされている基本データ型を次に示します。  
  
-   xs:string  
  
-   xs:boolean  
  
-   xs:decimal  
  
-   xs:float  
  
-   xs:double  
  
-   xs:duration  
  
-   xs:dateTime  
  
-   xs:time  
  
-   xs:date  
  
-   xs:gYearMonth  
  
-   xs:gYear  
  
-   xs:gMonthDay  
  
-   xs:gDay  
  
-   xs:gMonth  
  
-   xs:hexBinary  
  
-   xs:base64Binary  
  
-   xs:anyURI  
  
#### <a name="supported-derived-types"></a>サポートされている派生型  
 サポートされている派生型を次に示します。  
  
-   xs:normalizedString  
  
-   xs:token  
  
-   xs:language  
  
-   xs:Name  
  
-   xs:NCName  
  
-   xs:ID  
  
-   xs:IDREF  
  
-   xs:ENTITY  
  
-   xs:integer  
  
-   xs:nonPositiveInteger  
  
-   xs:negativeInteger  
  
-   xs:long  
  
-   xs:int  
  
-   xs:short  
  
-   xs:byte  
  
-   xs:nonNegativeInteger  
  
-   xs:unsignedLong  
  
-   xs:unsignedInt  
  
-   xs:unsignedShort  
  
-   xs:unsignedByte  
  
-   xs:positiveInteger  
  
 SQL Server では、次に示す方法で、コンストラクター関数の呼び出しの際に定数の組み合わせもサポートしています。  
  
-   引数が文字列リテラルの場合、式はコンパイル時に評価されます。 値が型に関する制約を満たしていない場合、静的エラーが発生します。  
  
-   引数が別の型のリテラルである場合、式はコンパイル時に評価されます。 値が型に関する制約を満たしていない場合、空のシーケンスが返されます。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列には、AdventureWorks データベース。  
  
### <a name="a-using-the-datetime-xquery-function-to-retrieve-older-product-descriptions"></a>A. dateTime() XQuery 関数を使用して、製品の説明の古いバージョンを取得する  
 サンプルの XML ドキュメントに最初に割り当てられている、この例では、 **xml**型の変数。 このドキュメントには 3 つのサンプル <`ProductDescription`> 要素が含まれます。各要素には <`DateCreated`> 子要素が含まれています。  
  
 次に、その変数がクエリされ、指定された日時より前に作成された製品の説明だけを取得します。 比較のために、クエリを使用して、 **xs:dateTime()** コンス トラクター関数を日付を入力します。  
  
```  
declare @x xml  
set @x = '<root>  
<ProductDescription ProductID="1" >  
  <DateCreated DateValue="2000-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription  ProductID="2" >  
  <DateCreated DateValue="2001-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
<ProductDescription ProductID="3" >  
  <DateCreated DateValue="2002-01-01T00:00:00Z" />  
  <Summary>Some Summary description</Summary>  
</ProductDescription>  
</root>'  
  
select @x.query('  
     for $PD in  /root/ProductDescription  
     where xs:dateTime(data( ($PD/DateCreated/@DateValue)[1] )) < xs:dateTime("2001-01-01T00:00:00Z")  
     return  
        element Product  
       {   
        ( attribute ProductID { data($PD/@ProductID ) },  
        attribute DateCreated { data( ($PD/DateCreated/@DateValue)[1] ) } )  
        }  
 ')  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   FOR ... WHERE ループ構造を使用して、取得、 \<ProductDescription > WHERE 句で指定された条件を満たす要素。  
  
-   **DateTime()** コンス トラクター関数が構築に使用される**dateTime**適切に比較できる型の値。  
  
-   この後、クエリは結果の XML を出力します。 一連の属性を構成しているため、XML の構造にコンマとかっこが使用されています。  
  
 結果を次に示します。  
  
```  
<Product   
   ProductID="1"   
   DateCreated="2000-01-01T00:00:00Z"/>  
```  
  
## <a name="see-also"></a>参照  
 [XML の構築&#40;XQuery&#41;](../xquery/xml-construction-xquery.md)   
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
