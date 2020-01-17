---
title: リーフ アクセス許可 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services], permissions
- members [Master Data Services], leaf member permissions
- permissions [Master Data Services], leaf members
- leaf members [Master Data Services], attribute permissions
- attributes [Master Data Services], leaf member attribute permissions
ms.assetid: bde16e8c-bcd4-4041-8130-55c5450e5f72
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: ee587881b95821c2ae23580b54d298fa496cec15
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479169"
---
# <a name="leaf-permissions-master-data-services"></a>リーフ権限 (Master Data Services)
  リーフ権限は、エンティティのすべてのリーフ メンバーの属性値に適用されます。  
  
 明示的階層が有効になっていないエンティティの場合、 **リーフ** への権限の割り当ては、エンティティへの権限の割り当てと同じです。  
  
 **注**  
  
-   リーフ権限は、ユーザー インターフェイスの **[エクスプローラー]** 機能領域にのみ適用されます。  
  
-   **Name** 属性および **Code** 属性に割り当てられる権限は適用されません。  
  
|権限|説明|  
|----------------|-----------------|  
|**読み取り専用です。**|リーフ メンバーが表示されますが、ユーザーはそれらのメンバーを追加、削除、または変更できません。<br /><br /> 統合メンバーが存在する場合は、名前とコードが表示されますが、ユーザーはそれらを追加、削除、または変更できません。|  
|**Update**|リーフ メンバーが表示され、ユーザーはそれらのメンバーを追加、削除、および変更できます。<br /><br /> 統合メンバーが存在する場合は、名前とコードが表示されますが、ユーザーはそれらを追加、削除、または変更できません。|  
|**Deny**|エンティティのリーフ メンバーが表示されません。|  
  
## <a name="attribute-permissions"></a>属性の権限  
 属性の権限は、特定のエンティティの属性の値に適用されます。 属性の権限のみを持つユーザーは、メンバーを追加または削除できません。  
  
|権限|説明|  
|----------------|-----------------|  
|**読み取り専用です。**|属性が表示されますが、ユーザーは属性の値を変更できません。|  
|**Update**|属性が表示され、ユーザーは属性の値を変更できます。|  
|**Deny**|属性が表示されません。<br /><br /> 注:Name および Code 属性へのアクセスを明示的に拒否することはできません。|  
  
### <a name="example"></a>例  
 Product エンティティの場合、Subcategory 属性に **更新** 権限を割り当てます。 他のすべての属性に対しては権限を拒否します。  
  
|名前|コード|Subcategory (更新)|  
|----------|----------|----------------------------|  
|Mountain-100|BK-M101|{5} マウンテン バイク|  
|Mountain-100|BK-M201|{5} マウンテン バイク|  
  
 **[エクスプローラー]** では、Subcategory 列の属性値を更新できます。 属性に対する権限がない場合、その属性は表示されません。  
  
> [!NOTE]  
>  この例では、Subcategory は、SubcategoryList エンティティに基づくドメイン ベースの属性です。 Mountain-100 に対して別のサブカテゴリを選択することはできますが、SubcategoryList エンティティへのメンバーの追加または SubcategoryList エンティティからのメンバーの削除を行うことはできません。  
  
## <a name="see-also"></a>参照  
 [モデル オブジェクト権限を割り当てる (マスター データ サービス)](assign-model-object-permissions-master-data-services.md)   
 [アクセス許可を統合&#40;マスター データ サービス&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md)   
 [モデル オブジェクト権限 (マスター データ サービス)](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [メンバー (マスター データ サービス)](../../2014/master-data-services/members-master-data-services.md)   
 [属性 (マスター データ サービス)](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
