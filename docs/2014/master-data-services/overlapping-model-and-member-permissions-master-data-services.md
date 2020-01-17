---
title: モデル アクセス許可とメンバー アクセス許可の重複 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: ca57d34a3dda2880f3882d1940c6852af0729fb7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482728"
---
# <a name="overlapping-model-and-member-permissions-master-data-services"></a>モデル権限とメンバー権限の重複 (Master Data Services)
  メンバーに割り当てられている権限は、モデル オブジェクトに割り当てられている権限と重複している可能性があります。 重複が発生すると、より制限の厳しい権限が有効になります。  
  
 メンバーに割り当てられている権限が、対応するモデル オブジェクトの権限とは異なる場合、次のルールが適用されます。  
  
-   **拒否** が他のどの権限をオーバーライドします。  
  
-   **読み取り専用**オーバーライド**Update**します。  
  
 次の図は、属性の権限がメンバーの権限とは異なる場合に、個々の属性値に対して有効な権限を示しています。  
  
 ![mds_conc_security_member_overlap_table](../../2014/master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## <a name="example-1"></a>例 1  
 ![mds_conc_overlap_model_1](../../2014/master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 **[モデル]** タブで、Product エンティティに **更新** 権限が割り当てられています。 エンティティのすべての属性がこの権限を継承しています。  
  
 **[階層メンバー]** タブで、派生階層の Mountain Bikes サブカテゴリ ノードに **更新** 権限が割り当てられています。  
  
 結果: **[エクスプローラー]** で、Mountain Bikes ノード内のすべてのメンバーについて、すべての属性値に対する **更新** 権限がユーザーに与えられます。 その他のメンバーと属性は、すべて非表示になります。  
  
 ![mds_conc_overlap_model_example_1](../../2014/master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## <a name="example-2"></a>例 2  
 ![mds_conc_overlap_model_2](../../2014/master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 **[モデル]** タブで、Subcategory 属性に **更新** 権限が割り当てられています。  
  
 **階層メンバー**  タブで、派生階層の Mountain Bikes サブカテゴリ ノードが割り当てられて明示的に**読み取り専用**権限。  
  
 結果:**エクスプ ローラー**、ユーザーが**読み取り専用**Mountain Bikes ノード内のメンバーについて、Subcategory 属性値にアクセスを許可します。 その他のメンバーと属性は、すべて非表示になります。  
  
 ![mds_conc_overlap_model_example_2](../../2014/master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="example-3"></a>例 3  
 ![mds_conc_overlap_model_3](../../2014/master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 **モデル**タブで、Subcategory 属性に**読み取り専用**権限が割り当てられています。  
  
 **[階層メンバー]** タブで、派生階層の Mountain Bikes サブカテゴリに **更新** 権限が明示的に割り当てられています。  
  
 結果:**エクスプ ローラー**、ユーザーが**読み取り専用**属性値にアクセスを許可します。 その他のメンバーと属性は、すべて非表示になります。  
  
 ![mds_conc_overlap_model_example_2](../../2014/master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## <a name="see-also"></a>参照  
 [権限の決定方法 (マスター データ サービス)](how-permissions-are-determined-master-data-services.md)   
 [ユーザー アクセス許可とグループ アクセス許可の重複 (マスター データ サービス)](../../2014/master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  
