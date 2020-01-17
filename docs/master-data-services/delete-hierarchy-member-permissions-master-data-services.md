---
title: 階層メンバーの権限を削除する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting member permissions [Master Data Services]
- members [Master Data Services], deleting permissions
- permissions [Master Data Services], deleting member permissions
ms.assetid: 7f22d5e2-70c1-422c-99c2-e995a47d812a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c441545bc88ef28031815cecb2c0f441fa1ea6a4
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729357"
---
# <a name="delete-hierarchy-member-permissions-master-data-services"></a>階層メンバーの権限を削除する (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] でモデル オブジェクトの権限を削除して、作成されている割り当てを削除します。  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   **[ユーザー/グループの権限]** 機能領域にアクセスするための権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
### <a name="to-delete-hierarchy-member-permissions"></a>階層メンバーの権限を削除するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[ユーザー/グループの権限]** をクリックします。  
  
2.  **[ユーザー]** または **[グループ]** ページで、編集するユーザーまたはグループの行を選択します。  
  
3.  **[選択したユーザーの編集]** をクリックします。  
  
4.  **[階層メンバー]** タブをクリックします。  
  
5.  **[モデル]** ボックスの一覧からモデルを選択します。  
  
6.  **[バージョン]** ボックスの一覧からバージョンを選択します。  
  
7.  **[編集]** をクリックします。  
  
8.  **[階層メンバーの権限]** パネルで、該当する権限のツリー ノードを見つけます。  
  
9. ツリー ノードをクリックし、コンテキスト メニューで **[なし]** をクリックします。  
  
    > [!NOTE]  
    >  権限がグループから継承されている場合、ユーザーから権限を削除できません。 グループから権限を削除する必要があります。  
  
10. **[保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [階層メンバーの権限 (マスター データ サービス)](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [階層メンバーの権限を割り当てる (マスター データ サービス)](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
  
