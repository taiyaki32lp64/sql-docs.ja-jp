---
title: モデル権限とメンバー権限の重複
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], effective permissions
- permissions [Master Data Services], model and member overlaps
- members [Master Data Services], effective permissions
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: e12489cc490c5b8ee9f363e329da9a057fac8f3f
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728983"
---
# <a name="overlapping-model-and-member-permissions-master-data-services"></a>モデル権限とメンバー権限の重複 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  メンバーに割り当てられている権限は、モデル オブジェクトに割り当てられている権限と重複している可能性があります。 重複が発生すると、より制限の厳しい権限が有効になります。  
  
 メンバーに割り当てられている権限が、対応するモデル オブジェクトの権限とは異なる場合、次のルールが適用されます。  
  
-   **拒否** が他のどの権限をオーバーライドします。  
  
-   モデル レベルの**管理者** 権限はすべての権限をオーバーライドし、サブ レベルで ALL (CRUD) アクセス権限に変更されます。  
  
-   有効なアクセス権限は、メンバーと属性のアクセス権限と交差します。  
  
     たとえば、メンバーの権限に **作成** と **更新**が含まれる場合、属性の権限は **更新**になります。 有効な権限は **更新**です。  
  
 次の図は、属性の権限がメンバーの権限とは異なる場合に、個々の属性値に対して有効な権限を示しています。  
  
 ![mds_conc_security_member_overlap_table](../master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## <a name="example-1"></a>例 1  
 ![mds_conc_overlap_model_1](../master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 **[モデル]** タブで、Product エンティティに **更新** 権限が割り当てられています。 エンティティのすべての属性がこの権限を継承しています。  
  
 **[階層メンバー]** タブで、派生階層の Mountain Bikes サブカテゴリ ノードに **更新** 権限が割り当てられています。  
  
 結果: **[エクスプローラー]** で、Mountain Bikes ノード内のすべてのメンバーについて、すべての属性値に対する **更新** 権限がユーザーに与えられます。 その他のメンバーと属性は、すべて非表示になります。  
  
 ![mds_conc_overlap_model_example_1](../master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## <a name="example-2"></a>例 2  
 ![mds_conc_overlap_model_2](../master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 **[モデル]** タブで、Subcategory 属性に **更新** 権限が割り当てられています。  
  
 **[階層メンバー]** タブで、派生階層の Mountain Bikes サブカテゴリ ノードに **読み取り** 権限が明示的に割り当てられています。  
  
 結果: **[エクスプローラー]** で、Mountain Bikes ノード内のメンバーについて、Subcategory 属性値に対する **読み取り** 権限がユーザーに与えられます。 その他のメンバーと属性は、すべて非表示になります。  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="example-3"></a>例 3  
 ![mds_conc_overlap_model_3](../master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 **[モデル]** タブで、Subcategory 属性に **読み取り** 権限が割り当てられています。  
  
 **[階層メンバー]** タブで、派生階層の Mountain Bikes サブカテゴリに **更新** 権限が明示的に割り当てられています。  
  
 結果: **[エクスプローラー]** で、属性値に対する **読み取り** 権限がユーザーに与えられます。 その他のメンバーと属性は、すべて非表示になります。  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="see-also"></a>参照  
 [権限の決定方法 (マスター データ サービス)](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [ユーザー アクセス許可とグループ アクセス許可の重複 (マスター データ サービス)](../master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  
