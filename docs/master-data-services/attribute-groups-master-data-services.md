---
title: 属性グループ
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services]
- attribute groups [Master Data Services], about attribute groups
ms.assetid: 648b3d0b-e15a-45f9-8292-3a54a072e62c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2b5cefb3548886cc26e55a9f408ac68e2bd30620
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729770"
---
# <a name="attribute-groups-master-data-services"></a>属性グループ (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] では、属性グループがエンティティ内の属性の整理に役立ちます。 エンティティ内に多数の属性がある場合、属性グループを使用すると、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションでのエンティティの表示が見やすくなります。  
  
## <a name="how-attribute-groups-change-the-display"></a>属性グループによる表示の変更  
 属性グループは、 **の** [エクスプローラー] [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]機能領域のグリッドの上部にタブとして表示されます。  
  
 1 つのエンティティに多くの属性がある場合、 **[エクスプローラー]** のグリッド内でエンティティのすべての属性を表示するには、右にスクロールする必要があります。 このスクロールを回避するために、属性グループを作成できます。  
  
-   属性グループには必ず、Name 属性と Code 属性が含まれます。  
  
-   エンティティの各属性は、1 つまたは複数の属性グループに属する場合があります。  
  
-   すべての属性が、 **エクスプローラー** の **[すべての属性]** タブに自動的に表示されます。  
  
-   **[すべての属性]** タブを非表示にすることはできません。  
  
 属性グループは、 **の** [システム管理] [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]機能領域で管理します。  
  
## <a name="show-or-hide-attribute-groups"></a>属性グループの表示と非表示  
 属性グループを作成すると、作成者以外のすべてのユーザーに対して自動的に非表示に設定されます。 グループを表示する方法の詳細については、「 [属性グループのユーザーへの表示 (マスター データ サービス)](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)機能領域のグリッドの上部にタブとして表示されます。  
  
 グループ内の特定の属性を非表示にするために、その属性に **[拒否]** の権限を割り当てることができます。 詳細については、「[リーフ アクセス許可 &#40;マスター データ サービス&#41;](../master-data-services/leaf-permissions-master-data-services.md)」を参照してください。  
  
## <a name="related-tasks"></a>関連タスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|新しい属性グループを作成して属性を追加する。|[属性グループを作成する (マスター データ サービス)](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|属性グループがユーザーに表示されるようにする。|[属性グループのユーザーへの表示 (マスター データ サービス)](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)|  
|既存の属性グループの名前を変更する。|[属性グループ名を変更する (マスター データ サービス)](../master-data-services/change-an-attribute-group-name-master-data-services.md)|  
|既存の属性グループを削除する。|[属性グループを削除する (マスター データ サービス)](../master-data-services/delete-an-attribute-group-master-data-services.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [属性 (マスター データ サービス)](../master-data-services/attributes-master-data-services.md)  
  
  
