---
title: "NavigationProperty 要素 (CSDLBI) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: a36b4d3b-6a6c-489b-8a46-2e6b925b568f
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5b1af93e52bc1a2fbd95059c86f73a0481572399
ms.contentlocale: ja-jp
ms.lasthandoff: 09/01/2017

---
# <a name="navigationproperty-element-csdlbi"></a>NavigationProperty 要素 (CSDLBI)
  NavigationProperty 要素は、CSDL Member の種類を拡張する複合型で、ビジネス インテリジェンス データ モデルでの移動をサポートします。  
  
> [!WARNING]  
>  この要素は報告用であり、変更または操作することはできません。  
  
## <a name="elements-and-attributes"></a>要素と属性  
 次の表に、NavigationProperty 要素を定義する要素と属性を示します。  
  
|名前|必須かどうか|Description|  
|----------|-----------------|-----------------|  
|CollectionCaption|いいえ|ナビゲーション プロパティのインスタンスのセットを参照するための複数形の名前。<br /><br /> この属性が省略されると、ベース メンバーの Caption 属性が使用されます。|  
  
## <a name="example"></a>例  
 **テーブル**  
  
 次の例では、テーブル モデルの Product SubCategory テーブルと Product テーブルの間のリンクを記述するナビゲーション プロパティを CSDLBI Version 1.1 で示します。  
  
```  
  
<NavigationProperty   
    Name="Product_Sub_Category_ProductSubcategoryKey"      
    Relationship="Sandbox.Product_Product_Sub_Category_Product_Sub_Category_ProductSubcategoryKey"  
     FromRole="Product_ProductSubcategoryKey"   
    ToRole="Product_Sub_Category_ProductSubcategoryKey">  
<bi:NavigationProperty   
     ReferenceName="Product Sub-Category_ProductSubcategoryKey" />  
</NavigationProperty>  
```  
  
## <a name="example"></a>例  
 **多次元**  
  
 次の例では、Contoso Operations キューブで 2 つのテーブル間のリレーションシップを記述するナビゲーション プロパティを CSDLBI Version 1.1 で示します。 このリレーションシップが、Bike Category テーブルと Product Subcategory テーブルを接続しています。  
  
```  
  
<NavigationProperty   
     Name="BikeSubcategory_ProductSubcategoryKey"   
     Relationship="Sandbox.Bike_BikeSubcategory_BikeSubcategory_ProductSubcategoryKey"   
     FromRole="Bike_ProductSubcategoryKey"   
     ToRole="BikeSubcategory_ProductSubcategoryKey">  
   <bi:NavigationProperty />  
</NavigationProperty>  
```  
  
## <a name="see-also"></a>参照  
 [レベルを 1050 から 1103 表形式オブジェクト モデルの互換性を理解します。](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  