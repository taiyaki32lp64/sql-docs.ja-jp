---
title: '例: HIDE ディレクティブの指定 | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- HIDE directive
ms.assetid: 87504d87-1cbd-412a-9041-47884b6efcec
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22ee3e41d5792683dd73520bbeacb35fdc91d83e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006706"
---
# <a name="example-specifying-the-hide-directive"></a>例: HIDE ディレクティブの指定
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  この例では、 **HIDE** ディレクティブの使用方法を示します。 クエリから返されたユニバーサル テーブル内の行を並べ替える目的でクエリから属性を返し、最終的な結果の XML ドキュメントにはその属性を含めない場合に、このディレクティブが役立ちます。  
  
 このクエリでは、次の XML を生成します。  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
           <Summary> element from XML stored in CatalogDescription column  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 このクエリでは、求める XML を生成しています。 Tag 列に値 1 と 2 を持つ 2 つの列グループが識別されます。  
  
 このクエリでは、xml データ型の [query()](../../t-sql/xml/query-method-xml-data-type.md) メソッド ( **xml** データ型) を使用し、 **xml** 型の CatalogDescription 列に対するクエリを実行して、概要情報を取得します。 また、このクエリでは、 [xml](../../t-sql/xml/value-method-xml-data-type.md) データ型の **value() メソッド (xml データ型)** を使用して、CatalogDescription 列から ProductModelID 値を取得します。 この値は、結果の行セットを並べ替えるために必要ですが、結果の XML ドキュメントでは必要ありません。 そのため、列名 `[Summary!2!ProductModelID!HIDE]`には、 **HIDE** ディレクティブが含まれています。 この列が SELECT ステートメントに含まれていなければ、 `[ProductModel!1!ProdModelID]` xml `[Summary!2!SummaryDescription]` 型の **列と** 列で行セットを並べ替える必要がありますが、ORDER BY 句では **xml** 型を使用することはできません。 このため、 `[Summary!2!ProductModelID!HIDE]` 列を追加し、これを ORDER BY 句で指定しています。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID     as [ProductModel!1!ProdModelID],  
        Name               as [ProductModel!1!Name],  
        NULL               as [Summary!2!ProductModelID!hide],  
        NULL               as [Summary!2!SummaryDescription]  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        Name,  
        CatalogDescription.value('  
         declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       (/PD:ProductDescription/@ProductModelID)[1]', 'int'),  
        CatalogDescription.query('  
         declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
         /pd:ProductDescription/pd:Summary')  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
ORDER BY [ProductModel!1!ProdModelID],[Summary!2!ProductModelID!hide]  
FOR XML EXPLICIT  
go  
```  
  
 結果を次に示します。  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
      <pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription" xmlns="">  
        <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">Our top-of-the-line competition mountain bike. Performance-enhancing options include the innovative HL Frame, super-smooth front suspension, and traction for all terrain. </p1:p>  
      </pd:Summary>  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
## <a name="see-also"></a>参照  
 [FOR XML での EXPLICIT モードの使用](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
