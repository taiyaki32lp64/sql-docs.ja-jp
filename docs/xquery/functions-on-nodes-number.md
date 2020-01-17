---
title: number 関数 (XQuery) |Microsoft Docs
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
- number function
- fn:number function
ms.assetid: dff6d19b-765c-4df9-afff-9a0e7be9b91b
author: rothja
ms.author: jroth
ms.openlocfilehash: 31a52f86692d5769fe22f4cf0b5a04ad324c3ac0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67930115"
---
# <a name="functions-on-nodes---number"></a>ノードの関数 - number
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  によって示されるノードの数値の値を返します *$arg*します。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:number() as xs:double?   
fn:number($arg as node()?) as xs:double?  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 ノードの値は数値として返されます。  
  
## <a name="remarks"></a>コメント  
 場合 *$arg*が指定されていない、double 型に変換された、コンテキスト ノードの数値の値が返されます。 SQL Server で**fn:number()** せず、引数は、コンテキストに依存する述語のコンテキストでのみ使用できます。 具体的にのみ使用できます角かっこ () 内で。 たとえば、次の式を返します、<`ROOT`> 要素。  
  
```  
declare @x xml  
set @x='<ROOT>111</ROOT>'  
select @x.query('/ROOT[number()=111]')  
```  
  
 ノードの値でない場合、数値の単純型の有効な字句表現で定義されている**XML Schema Part 2: datatypes,、W3C 勧告**関数は空のシーケンスを返します。 NaN はサポートされません。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列には、AdventureWorks データベース。  
  
### <a name="a-using-the-number-xquery-function-to-retrieve-the-numeric-value-of-an-attribute"></a>A. Number() XQuery 関数を使用して、属性の数値の値を取得するには  
 次のクエリでは、製品モデル 7 の製造プロセス内で最初の作業のセンターの場所から、ロット サイズ属性の数値の値を取得します。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in (//AWMI:root//AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"   
                   LotSizeA="{  $i/@LotSize }"  
                   LotSizeB="{  number($i/@LotSize) }"  
                   LotSizeC="{ number($i/@LotSize) + 1 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   **Number()** 関数のためのクエリで示すように必須ではありません、 **LotSizeA**属性。 これは XPath 1.0 関数で、主に旧バージョンとの互換性上の理由で含まれています。  
  
-   XQuery では**LotSizeB** number 関数を指定し、冗長です。  
  
-   クエリを**LotSizeD**算術演算の番号の値の使用方法を示します。  
  
 結果を次に示します。  
  
```  
ProductModelID   Result  
----------------------------------------------  
7              <Location LocationID="10"   
                         LotSizeA="100"   
                         LotSizeB="100"   
                         LotSizeC="101" />  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   **Number()** 関数ノードのみを受け取ります。 アトミック値を受け取ることはできません。  
  
-   値は、数値として返すことができないときに、 **number()** 関数が NaN ではなく空のシーケンスを返します。  
  
## <a name="see-also"></a>関連項目  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
