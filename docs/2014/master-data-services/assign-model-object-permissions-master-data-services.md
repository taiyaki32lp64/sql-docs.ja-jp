---
title: モデル オブジェクト アクセス許可を割り当てる (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], assigning object permissions
- permissions [Master Data Services], assigning model object permissions
ms.assetid: 4b80148d-2318-415c-9479-28c240e48bcd
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a1477f934dfa8a23fa5498124b74c9a150b24a33
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480072"
---
# <a name="assign-model-object-permissions-master-data-services"></a>モデル オブジェクト権限を割り当てる (Master Data Services)
  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]では、 **の** [エクスプローラー] [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]機能領域内のデータにユーザーまたはグループがアクセスできるようにする必要があるとき、またはユーザーまたはグループを管理者にする必要があるときは、モデル オブジェクトに権限を割り当てます。  
  
> [!NOTE]  
>  モデルに権限を割り当てると、その他のすべてのモデルへの権限は暗黙的に拒否されます。 モデル オブジェクト権限を割り当てない場合、ユーザーまたはグループは **[エクスプローラー]** のデータにアクセスできません。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   **[ユーザー/グループの権限]** 機能領域にアクセスするための権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「 [管理者 &#40;マスター データ サービス&#41;](administrators-master-data-services.md)にアクセスすることなくグループに対してユーザーの追加または削除を行うことができます。  
  
### <a name="to-assign-model-object-permissions"></a>モデル オブジェクト権限を割り当てるには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[ユーザー/グループの権限]** をクリックします。  
  
2.  **[ユーザー]** または **[グループ]** ページで、編集するユーザーまたはグループの行を選択します。  
  
3.  **[選択したユーザーの編集]** をクリックします。  
  
4.  **[モデル]** タブをクリックします。  
  
5.  **[モデル]** ボックスの一覧からモデルを選択します (オプション)。  
  
6.  **[編集]** をクリックします。  
  
7.  ツリーを展開して、権限を割り当てるモデル オブジェクトをクリックします。  
  
8.  メニューから、次のように選択します。**読み取り専用**、 **Update**、または**Deny**します。  
  
9. **[保存]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
  
-   (省略可能) [階層メンバーの権限を割り当てる (マスター データ サービス)](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [モデル オブジェクト権限を削除する (マスター データ サービス)](../../2014/master-data-services/delete-model-object-permissions-master-data-services.md)   
 [モデル オブジェクト権限 (マスター データ サービス)](../../2014/master-data-services/model-object-permissions-master-data-services.md)   
 [モデル管理者を作成する (マスター データ サービス)](../../2014/master-data-services/create-a-model-administrator-master-data-services.md)  
  
  
