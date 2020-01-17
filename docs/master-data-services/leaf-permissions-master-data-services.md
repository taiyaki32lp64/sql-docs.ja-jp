---
title: リーフ権限
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
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
ms.openlocfilehash: 4e01c6773ce28694e95f992f1af49a7cce19e969
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728079"
---
# <a name="leaf-permissions-master-data-services"></a>リーフ権限 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  リーフ権限は、エンティティのすべてのリーフ メンバーの属性値に適用されます。  
  
 明示的階層が有効になっていないエンティティの場合、 **リーフ** への権限の割り当ては、エンティティへの権限の割り当てと同じです。  
  
 **Notes:**  
  
-   リーフ権限は、ユーザー インターフェイスの **[エクスプローラー]** 機能領域にのみ適用されます。  
  
-   **Name** 属性および **Code** 属性に割り当てられる権限は適用されません。  
  
|権限|[説明]|  
|----------------|-----------------|  
|**読み取り**|ユーザーはリーフ メンバーと属性を読み取ることができます。|  
|**作成**|ユーザーはリーフ メンバーを作成し、作成時に属性値を割り当てることができます。|  
|**Update**|ユーザーはリーフ メンバーと属性を更新できます。|  
|**[削除]**|ユーザーはリーフ メンバーを削除できます。|  
|**拒否**|リーフ メンバーに対するすべてのアクセスを拒否します。|  
  
 読み取り、作成、更新、削除の各権限は組み合わせることができます。 作成、更新、削除が割り当てられると、読み取り権限が自動的に割り当てられます。  
  
## <a name="attribute-permissions"></a>属性の権限  
 属性の権限は、特定のエンティティの属性の値に適用されます。 属性の権限のみを持つユーザーは、メンバーを追加または削除できません。  
  
|権限|[説明]|  
|----------------|-----------------|  
|**読み取り**|ユーザーは属性の読み取ることができます。|  
|**作成**|ユーザーはメンバーを作成するときに値を割り当てることができます。|  
|**Update**|ユーザーは属性を更新できます。|  
|**[削除]**|影響しません。|  
|**拒否**|属性が表示されません。<br /><br /> 注: Name 属性と Code 属性へのアクセスを明示的に拒否することはできません。|  
  
### <a name="example"></a>例  
 Product エンティティの場合、Subcategory 属性に **更新** 権限を割り当てます。 他のすべての属性に対しては権限を拒否します。  
  
|[オブジェクト名]|Code|Subcategory (更新)|  
|----------|----------|----------------------------|  
|Mountain-100|BK-M101|{5} マウンテンバイク|  
|Mountain-100|BK-M201|{5} マウンテンバイク|  
  
 **[エクスプローラー]** では、Subcategory 列の属性値を更新できます。 属性に対する権限がない場合、その属性は表示されません。  
  
> [!NOTE]  
>  この例では、Subcategory は、SubcategoryList エンティティに基づくドメイン ベースの属性です。 Mountain-100 に対して別のサブカテゴリを選択することはできますが、SubcategoryList エンティティへのメンバーの追加または SubcategoryList エンティティからのメンバーの削除を行うことはできません。  
  
## <a name="see-also"></a>参照  
 [モデル オブジェクト権限を割り当てる (マスター データ サービス)](../master-data-services/assign-model-object-permissions-master-data-services.md)   
    
 [モデル オブジェクト権限 (マスター データ サービス)](../master-data-services/model-object-permissions-master-data-services.md)   
 [メンバー (マスター データ サービス)](../master-data-services/members-master-data-services.md)   
 [属性 (マスター データ サービス)](../master-data-services/attributes-master-data-services.md)  
  
  
