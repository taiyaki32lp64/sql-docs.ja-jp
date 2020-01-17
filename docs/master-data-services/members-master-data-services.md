---
title: メンバー
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- leaf members [Master Data Services]
- consolidated members [Master Data Services]
- consolidated members [Master Data Services], about consolidated members
- members [Master Data Services], about members
- leaf members [Master Data Services], about leaf members
- members [Master Data Services]
ms.assetid: 0fda32b9-677d-4ba2-bb28-f76f2383a30f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d6e663ef23c472b2a78ec71c58086824adae185e
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728007"
---
# <a name="members-master-data-services"></a>メンバー (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] では、メンバーは物理マスター データです。 たとえば、Product エンティティの Road-150 バイクや、Customer エンティティの特定の顧客をメンバーにすることができます。  
  
## <a name="how-members-relate-to-other-model-objects"></a>メンバーと他のモデル オブジェクトの関連付け  
 メンバーは、テーブルの行と考えることができます。 関連するメンバーはエンティティに含まれ、各メンバーは属性値によって定義されます。  
  
 この例では、テーブルはエンティティを、テーブルの行はメンバーを、テーブルの列は属性を、それぞれ表しています。 各セルは特定のメンバーの属性値を表します。  
  
 ![テーブルとして表されるマスターデータサービスエンティティ](../master-data-services/media/mds-conc-entity-table.gif "テーブルとして表されるマスターデータサービスエンティティ")  
  
## <a name="member-types"></a>メンバーの種類  
 メンバーには、リーフ メンバー、統合メンバー、およびコレクション メンバーという 2 種類があります。  
  
 リーフ メンバーは、エンティティの既定のメンバーです。  
  
-   派生階層では、リーフ メンバーは唯一の種類のメンバーです。 1 つのエンティティのリーフ メンバーは、別のエンティティのリーフ メンバーの親として使用されます。  
  
-   明示的階層では、リーフ メンバーは最下位レベルで、子を持つことができません。  
  
 統合メンバーは、エンティティの明示的階層およびコレクションが有効になっているときにのみ存在します。  
  
-   派生階層には、統合メンバーは含まれません。  
  
-   明示的階層では、統合メンバーは階層内の他のメンバーの親になることも、子になることもできます。  
  
## <a name="use-hierarchies-and-collections-to-organize-members"></a>階層とコレクションを使用したメンバーの整理  
 階層およびコレクションを使用して、レポートまたは分析のためにメンバーをグループ化できます。 詳細については、「[階層 (マスター データ サービス)](../master-data-services/hierarchies-master-data-services.md)」および「[コレクション (マスター データ サービス)](../master-data-services/collections-master-data-services.md)」を参照してください。  
  
## <a name="member-example"></a>メンバーの例  
 次の例では、各メンバーは、Name、Code、Subcategory、StandardCost、ListPrice、および FilePhoto という属性値で構成されています。  
  
 ![自転車製品エンティティテーブル](../master-data-services/media/mds-conc-entity-table-w-data.gif "自転車製品エンティティテーブル")  
  
## <a name="related-tasks"></a>関連タスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|新しいリーフ メンバーを作成する。|[リーフ メンバーを作成する (マスター データ サービス)](../master-data-services/create-a-leaf-member-master-data-services.md)|  
|新しい統合メンバーを作成する。|[統合メンバーを作成する (マスター データ サービス)](../master-data-services/create-a-consolidated-member-master-data-services.md)|  
|既存のメンバーまたはコレクションを削除する。|[メンバーまたはコレクションを削除する (マスター データ サービス)](../master-data-services/delete-a-member-or-collection-master-data-services.md)|  
|削除したメンバーまたはコレクションを再アクティブ化する。|[メンバーまたはコレクションを再アクティブ化する (マスター データ サービス)](../master-data-services/reactivate-a-member-or-collection-master-data-services.md)|  
|メンバーの属性値を更新する。|[属性の型の変更 (Excel 用 MDS アドイン)](../master-data-services/microsoft-excel-add-in/change-the-attribute-type-mds-add-in-for-excel.md)|  

  
## <a name="related-content"></a>関連コンテンツ  
  
-   [マスター データ サービスの概要 (MDS)](../master-data-services/master-data-services-overview-mds.md)  
  
-   [エンティティ (マスター データ サービス)](../master-data-services/entities-master-data-services.md)  
  
-   [属性 (マスター データ サービス)](../master-data-services/attributes-master-data-services.md)  
  
-   [階層 (マスター データ サービス)](../master-data-services/hierarchies-master-data-services.md)  
  
-   [コレクション (マスター データ サービス)](../master-data-services/collections-master-data-services.md)  
  
-   [リーフ権限 (マスター データ サービス)](../master-data-services/leaf-permissions-master-data-services.md)  
  
 
-   [フィルター演算子 (マスター データ サービス)](../master-data-services/filter-operators-master-data-services.md)  
  
  
