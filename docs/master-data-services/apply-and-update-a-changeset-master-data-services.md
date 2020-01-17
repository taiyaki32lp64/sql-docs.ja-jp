---
title: 変更セットの適用および更新
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 3a6a3cf2-1e77-43d3-a64a-855ae51258e7
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b0e937ff9222553c42eacefc173dfec90bb6ebc6
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728783"
---
# <a name="apply-and-update-a-changeset-master-data-services"></a>変更セットの適用および更新 (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  変更セットは、マスター データに対する保留中の変更のコレクションです。 変更セットをビューにローカルに適用したり、変更セット内の保留中の変更を追加、更新、削除したりできます。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。 詳細については、「[機能領域権限 (マスター データ サービス)](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
-   少なくとも、エンティティまたはその属性のいずれかに対する更新アクセス権が必要です。  
  
-   エンティティ管理者は、自分で所有する変更セットまたは承認のために送信された変更セットのみを表示できます。  
  
-   変更セットの状態がオープン状態または拒否状態のときは、自分で所有する変更セットのみを変更できます。  
  
## <a name="to-apply-and-update-a-changeset"></a>変更セットを適用および更新するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、モデルとバージョンを選択し、 **[エクスプローラー]** をクリックします。  
  
2.  **[エンティティ]** メニューでエンティティをクリックします。  
  
3.  右側のウィンドウで、 **[変更セット]** を選択し、表示および変更する変更セットをダブルクリックします。  
  
4.  **[適用]** をクリックします。  
  
     保留中の変更がグリッド内のエンティティ メンバーに適用されます。 保留中の変更が強調表示されます。  
  
     メンバーを作成、削除、更新すると、変更セットが変更されます。  
  
5.  保留中の変更に戻すには、 **[変更セット]** ウィンドウのグリッド内で右クリックし、 **[戻す]** をクリックします。  
  
## <a name="next-steps"></a>Next Steps  
 [変更セットのコミットまたは送信 (マスター データ サービス)](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [変更セットを作成する (マスター データ サービス)](../master-data-services/create-a-changeset-master-data-services.md)   
 [変更セットの承認または拒否 (マスター データ サービス)](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
