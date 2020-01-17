---
title: not 関数 (XQuery) |Microsoft Docs
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
- effective Boolean value [XQuery]
- fn:not function
- not function [XQuery]
- EBV
ms.assetid: 93dfc377-45f1-4384-9392-560d9331a915
author: rothja
ms.author: jroth
ms.openlocfilehash: 8711190a6d3cbae0c716f7f62af478b70b9473e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038912"
---
# <a name="functions-on-boolean-values---not-function"></a>ブール値に対する関数 - 機能しない 
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  True の場合の有効なブール値 *$arg*が false になり、FALSE を返しますの有効なブール値 *$arg*は true。  
  
## <a name="syntax"></a>構文  
  
```  
  
fn:not($arg as item()*) as xs:boolean  
```  
  
## <a name="arguments"></a>引数  
 *$arg*  
 有効なブール値が指定されているアイテムのシーケンス。  
  
## <a name="examples"></a>使用例  
 このトピックではさまざまなに格納されている XML インスタンスに対して XQuery の例について**xml**型の列には、AdventureWorks データベース。  
  
### <a name="a-using-the-not-xquery-function-to-find-product-models-whose-catalog-descriptions-do-not-include-the-specifications-element"></a>A. 製品モデル カタログの説明の検索に not() XQuery 関数を使用するは含めないでください、\<仕様 > 要素。  
 次のクエリは、カタログの説明は含めないでください製品モデルの製品モデル Id を含む XML を構築、<`Specifications`> 要素。  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
       <Product   
           ProductModelID="{ sql:column("ProductModelID") }"  
        />  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications/*)]  '  
     ) = 0  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   ドキュメントは、名前空間を使用しているため、サンプルは、WITH NAMESPACES ステートメントを使用します。 使用することも、**名前空間を宣言**キーワード、 [XQuery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md)プレフィックスを定義しています。  
  
-   クエリを含む XML を構築し、<`Product`> 要素とその**ProductModelID**属性。  
  
-   WHERE 句を使用して、 [exist() メソッド (XML データ型)](../t-sql/xml/exist-method-xml-data-type.md)行をフィルター選択します。 **Exist()** メソッドがある場合、True を返します\<ProductDescription > 要素を持たない\<Specification > 子要素。 使用に注意してください、 **not()** 関数。  
  
 各製品モデル カタログの説明が含まれているために、この結果セットが空で、\<仕様 > 要素。  
  
### <a name="b-using-the-not-xquery-function-to-retrieve-work-center-locations-that-do-not-have-a-machinehours-attribute"></a>B. not() XQuery 関数を使用して、MachineHours 属性を持たないワーク センターの場所を取得する  
 Instructions 列に対しては、次のクエリを指定します。 この列には、製品モデルの製造手順が格納されています。  
  
 特定の製品モデルの場合は、クエリは、MachineHours を指定しないワーク センターの場所を取得します。 属性は、 **MachineHours**が指定されていない、\<場所 > 要素。  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in /AWMI:root/AWMI:Location[not(@MachineHours)]  
     return  
       <Location LocationID="{ $i/@LocationID }"   
                   LaborHrs="{ $i/@LaborHours }" >  
        </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7   
```  
  
 上記のクエリでは、次に注意してください。  
  
-   **Declarenamespace**で[XQuery プロローグ](../xquery/modules-and-prologs-xquery-prolog.md)Adventure Works の製造手順の名前空間プレフィックスを定義します。 この定義は、製造手順ドキュメントで使用されているのと同じ名前空間を表しています。  
  
-   クエリで、**されません (@MachineHours)** がある場合、述語が True を返すありません**MachineHours**属性。  
  
 結果を次に示します。  
  
```  
ProductModelID Result   
-------------- --------------------------------------------  
7              <Location LocationID="30" LaborHrs="1"/>  
               <Location LocationID="50" LaborHrs="3"/>  
               <Location LocationID="60" LaborHrs="4"/>  
```  
  
### <a name="implementation-limitations"></a>実装の制限事項  
 制限事項を次に示します。  
  
-   **Not()** 関数には、xs:boolean 型、node() *、または空のシーケンスの引数のみサポートされています。  
  
## <a name="see-also"></a>関連項目  
 [xml データ型に対する XQuery 関数](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
