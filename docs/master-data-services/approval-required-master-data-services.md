---
title: 承認が必要
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b475a53d-269d-49f3-bb42-965c555f80be
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 61d03410e5217175335caf0ca37241b28c887989
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729758"
---
# <a name="approval-required-master-data-services"></a>承認が必要 (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、管理者はエンティティを「承認が必要」に設定できます。 このエンティティに対するすべての変更には、エンティティ管理者の確認と承認が必要になります。  
  
> [!NOTE]  
>  リーフ メンバーに加えられた変更には、承認が必要です。 非推奨の明示的階層とコレクションに加えられた変更は、承認がバイパスされます。  
>   
>  ステージング テーブルの処理によって行われた変更は、承認がバイパスされます。  
>   
>  ビジネス ルールによって行われた変更は、承認がバイパスされます。  
  
## <a name="prerequisites"></a>前提条件  
 この手順を実行するには  
  
-   [システム管理] 機能領域にアクセスする権限が必要です。  
  
-   モデル管理者である必要があります。 詳細については、「[管理者 (マスター データ サービス)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   エンティティが存在する必要があります。 詳細については、「[エンティティを作成する (マスター データ サービス)](../master-data-services/create-an-entity-master-data-services.md)」を参照してください。  
  
## <a name="to-enable-approval-required-for-an-entity"></a>エンティティに対して「承認が必要」を有効にするには  
  
1.  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で **[システム管理]** をクリックします。  
  
2.  **[モデルの管理]** ページでグリッドからモデルを選択し、 **[エンティティ]** をクリックします。  
  
3.  **[Manage Entity]** (エンティティの管理) ページで、  **[承認が必要]** を有効にするエンティティの行をグリッドから選択します。  
  
4.  **[編集]** をクリックし、 **[承認が必要]** を選択して **[保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [変更セット (マスター データ サービス)](../master-data-services/changesets-master-data-services.md)  
  
  
