---
title: FOR XML クエリと入れ子になった FOR XML クエリの比較 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML query
- queries [XML in SQL Server], comparing query types
ms.assetid: 19225b4a-ee3f-47cf-8bcc-52699eeda32c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3cccb676574fe4b767d567fbe48cdb887baddf8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205055"
---
# <a name="for-xml-query-compared-to-nested-for-xml-query"></a>FOR XML クエリと入れ子になった FOR XML クエリの比較
  ここでは、単一レベルの FOR XML クエリと入れ子になった FOR XML クエリを比較します。 入れ子になった FOR XML クエリを使用すると、たとえば、属性中心の XML と要素中心の XML の組み合わせをクエリの結果に指定できるなどの利点があります。 次の例はこのことを示しています。  
  
## <a name="example"></a>例  
 次の `SELECT` クエリでは、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの製品カテゴリとサブカテゴリの情報を取得します。 このクエリには入れ子になった FOR XML はありません。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   ProductCategory.ProductCategoryID,   
         ProductCategory.Name as CategoryName,  
         ProductSubCategory.ProductSubCategoryID,   
         ProductSubCategory.Name  
FROM     Production.ProductCategory, Production.ProductSubCategory  
WHERE    ProductCategory.ProductCategoryID = ProductSubCategory.ProductCategoryID  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
GO  
```  
  
 結果の一部を次に示します。  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory ProductSubCategoryID="1" Name="Mountain Bike"/>  
  <ProductSubCategory ProductSubCategoryID="2" Name="Road Bike"/>  
  <ProductSubCategory ProductSubCategoryID="3" Name="Touring Bike"/>  
</ProductCategory>  
...  
```  
  
 クエリに `ELEMENTS` ディレクティブを指定すると、次のフラグメントに示すように、要素中心の結果が得られます。  
  
```  
<ProductCategory>  
  <ProductCategoryID>1</ProductCategoryID>  
  <CategoryName>Bike</CategoryName>  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <Name>Mountain Bike</Name>  
  </ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  </ProductSubCategory>  
</ProductCategory>  
```  
  
 次に示すように、生成する XML 階層が属性中心の XML と要素中心の XML の組み合わせだとします。  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 上のフラグメントに示した結果で、カテゴリ ID やカテゴリ名などの製品カテゴリの情報は属性です。 ただし、サブカテゴリの情報は要素中心です。 <`ProductCategory`> 要素を構築するには、次に示すような `FOR XML` クエリを記述できます。  
  
```  
SELECT ProductCategoryID, Name as CategoryName  
FROM Production.ProductCategory ProdCat  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 結果を次に示します。  
  
```  
< ProdCat ProductCategoryID="1" CategoryName="Bikes" />  
< ProdCat ProductCategoryID="2" CategoryName="Components" />  
< ProdCat ProductCategoryID="3" CategoryName="Clothing" />  
< ProdCat ProductCategoryID="4" CategoryName="Accessories" />  
```  
  
 XML 内に入れ子構造の <`ProductSubCategory`> 要素を構築するには、次に示すような入れ子構造の `FOR XML` クエリを追加します。  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName  
        FROM   Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 上のクエリに関して、次の点に注意してください。  
  
-   内側の `FOR XML` クエリは、製品サブカテゴリの情報を取得しています。 要素中心の XML を生成するために、内側の `ELEMENTS` に `FOR XML` ディレクティブを追加しています。ここで生成した XML は外側のクエリで生成される XML に追加されます。 既定では、外側のクエリで属性中心の XML が生成されます。  
  
-   結果を `TYPE` xml **型にするために、内側のクエリに** ディレクティブを指定しています。 `TYPE` ディレクティブを指定しないと、結果は `nvarchar(max)` 型で返され、XML データはエンティティ化されます。  
  
-   外側のクエリでも `TYPE` ディレクティブを指定しています。 そのため、このクエリの結果は **xml** 型でクライアントに返されます。  
  
 結果の一部を次に示します。  
  
```  
<ProductCategory ProductCategoryID="1" CategoryName="Bike">  
  <ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bike</SubCategoryName></ProductSubCategory>  
  <ProductSubCategory>  
     ...  
  <ProductSubCategory>  
     ...  
</ProductCategory>  
```  
  
 次のクエリは単に上記のクエリを拡張したものです。 これによって、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに格納されている完全な製品階層が示されます。 これには、次の内容が含まれます。  
  
-   製品カテゴリ  
  
-   各カテゴリの製品サブカテゴリ  
  
-   各サブカテゴリの製品モデル  
  
-   各モデルの製品  
  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースを理解するために、次のクエリが役に立ちます。  
  
```  
SELECT ProductCategoryID, Name as CategoryName,  
       (SELECT ProductSubCategoryID, Name SubCategoryName,  
               (SELECT ProductModel.ProductModelID,   
                       ProductModel.Name as ModelName,  
                       (SELECT ProductID, Name as ProductName, Color  
                        FROM   Production.Product  
                        WHERE  Product.ProductModelID =   
                               ProductModel.ProductModelID  
                        FOR XML AUTO, TYPE)  
                FROM   (SELECT distinct ProductModel.ProductModelID,   
                               ProductModel.Name  
                        FROM   Production.ProductModel,   
                               Production.Product  
                        WHERE  ProductModel.ProductModelID =   
                               Product.ProductModelID  
                        AND    Product.ProductSubCategoryID =   
                               ProductSubCategory.ProductSubCategoryID)   
                                  ProductModel  
                FOR XML AUTO, type  
               )  
        FROM Production.ProductSubCategory  
        WHERE ProductSubCategory.ProductCategoryID =   
              ProductCategory.ProductCategoryID  
        FOR XML AUTO, TYPE, ELEMENTS  
       )  
FROM Production.ProductCategory  
ORDER BY ProductCategoryID  
FOR XML AUTO, TYPE  
```  
  
 結果の一部を次に示します。  
  
```  
<Production.ProductCategory ProductCategoryID="1" CategoryName="Bikes">  
  <Production.ProductSubCategory>  
    <ProductSubCategoryID>1</ProductSubCategoryID>  
    <SubCategoryName>Mountain Bikes</SubCategoryName>  
    <ProductModel ProductModelID="19" ModelName="Mountain-100">  
      <Production.Product ProductID="771"   
                ProductName="Mountain-100 Silver, 38" Color="Silver" />  
      <Production.Product ProductID="772"   
                ProductName="Mountain-100 Silver, 42" Color="Silver" />  
      <Production.Product ProductID="773"   
                ProductName="Mountain-100 Silver, 44" Color="Silver" />  
        ...  
    </ProductModel>  
     ...  
```  
  
 製品サブカテゴリを生成している入れ子構造の `ELEMENTS` クエリから `FOR XML` ディレクティブを削除すると、結果全体が属性中心になります。 このクエリは入れ子にしないでも記述できます。 `ELEMENTS` を追加することで、結果として一部が属性中心で、一部が要素中心の XML が得られます。 この結果は単一レベルの FOR XML クエリでは生成できません。  
  
## <a name="see-also"></a>参照  
 [入れ子になった FOR XML クエリの使用](use-nested-for-xml-queries.md)  
  
  
