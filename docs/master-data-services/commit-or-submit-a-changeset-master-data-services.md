---
title: 変更セットのコミットまたは送信
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d323bbac-c8d4-4d2f-a7d2-a597e8b53e2d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4f45d9ced6b22ec2b0cf7007eee4549e595ec697
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728569"
---
# <a name="commit-or-submit-a-changeset-master-data-services"></a>変更セットのコミットまたは送信 (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  変更セットは、マスター データに対する保留中の変更のコレクションです。 エンティティの変更が管理者の承認を必要としない場合は、変更セットをコミットできます。 エンティティの変更が管理者の承認を必要とする場合は、承認を受けるために変更セットを送信できます。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。 詳細については、「[機能領域権限 (マスター データ サービス)](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
-   エンティティの変更が管理者の承認を必要としない場合は、変更セットを自分が所有し、変更セットの状態がオープンである場合のみ、変更セットをコミットできます。  
  
-   エンティティの変更が管理者の承認を必要とする場合は、変更セットを自分が所有し、変更セットの状態がオープンまたは拒否である場合のみ、承認を受けるために変更セットを送信できます。  
  
## <a name="to-commit-a-local-changeset"></a>ローカルの変更セットをコミットするには  
 コミット オプションは、エンティティ管理者が承認の必要性を有効にしていないエンティティでローカルの変更セットにのみ使用できます。  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、モデルとバージョンを選択し、 **[エクスプローラー]** をクリックします。  
  
2.  **[エンティティ]** メニューでエンティティをクリックします。  
  
3.  右側のウィンドウで、 **[変更セット]** を選択し、コミットする変更セットをダブルクリックします。  
  
4.  **[コミット]** をクリックします。  
  
## <a name="to-submit-a-changeset"></a>変更セットを送信するには  
 送信オプションは、エンティティ管理者が承認の必要性を有効にしているエンティティの変更セットでのみ使用できます。  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、モデルとバージョンを選択し、 **[エクスプローラー]** をクリックします。  
  
2.  **[エンティティ]** メニューでエンティティをクリックします。  
  
3.  右側のウィンドウで、 **[変更セット]** を選択し、送信する変更セットをダブルクリックします。  
  
4.  **[送信]** をクリックします。  
  
## <a name="next-steps"></a>Next Steps  
 [変更セットの承認または拒否 (マスター データ サービス)](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [変更セットを作成する (マスター データ サービス)](../master-data-services/create-a-changeset-master-data-services.md)   
 [変更セットの適用および更新 (マスター データ サービス)](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [変更セットの承認または拒否 (マスター データ サービス)](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  
