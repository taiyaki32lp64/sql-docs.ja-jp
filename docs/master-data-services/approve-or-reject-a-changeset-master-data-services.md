---
title: 変更セットの承認または拒否
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 45bd01f9-ae15-4fc5-a2ba-eee565a26ef8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 401983aa2e5094560f7bcc852c839986ffe4234d
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728774"
---
# <a name="approve-or-reject-a-changeset-master-data-services"></a>変更セットの承認または拒否 (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  変更セットは、マスター データに対する保留中の変更のコレクションです。 エンティティを変更する場合に管理者による承認を必要とする場合、変更セットが承認のために送信されます。管理者は、変更セットを確認したうえで、承認または拒否します。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   **[エクスプローラー]** 機能領域にアクセスする権限が必要です。 詳細については、「[機能領域権限 (マスター データ サービス)](../master-data-services/functional-area-permissions-master-data-services.md)」を参照してください。  
  
-   エンティティに対する管理者権限が必要です。  
  
-   エンティティの変更は、管理者による承認を必要とする必要があります。  
  
-   変更セットの状態が保留中の場合は、管理者が変更セットを確認したうえで、変更セットを承認または拒否できます。  
  
-   ユーザーは、自分自身が加えた変更を承認することはできません。 エンティティ管理者は、自分自身が加えた変更セットを承認するために 2 人目の管理者を割り当てる必要があります。  
  
## <a name="to-approve-or-reject-a-changeset"></a>変更セットを承認または拒否するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] のホーム ページで、モデルとバージョンを選択し、 **[エクスプローラー]** をクリックします。  
  
2.  **[エンティティ]** メニューでエンティティをクリックします。  
  
3.  右側のウィンドウで、 **[Changesets]** (変更セット) を選択し、承認または拒否する変更セットをダブルクリックします。  
  
4.  **[適用]** をクリックして変更セットを適用し、保留中の変更を確認します。  
  
5.  変更セットを拒否して所有者に差し戻すには、 **[拒否]** をクリックします。  
  
6.  変更セットを承認するには、 **[承認]** をクリックします。 変更セットが自動的にコミットされます。  
  
## <a name="see-also"></a>参照  
 [変更セットを作成する (マスター データ サービス)](../master-data-services/create-a-changeset-master-data-services.md)   
 [変更セットの適用および更新 (マスター データ サービス)](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [変更セットのコミットまたは送信 (マスター データ サービス)](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
  
