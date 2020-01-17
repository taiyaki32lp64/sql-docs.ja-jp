---
title: メンバー リビジョン履歴
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 113069c5-12e6-48ec-b443-b42e14f77308
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4bc3d2a084f7f1ec3abcf9e3d3bbcaf82e4749e8
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729113"
---
# <a name="member-revision-history-master-data-services"></a>メンバー リビジョン履歴 (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  メンバー リビジョン履歴は、エンティティのトランザクション ログの種類がメンバーの場合、メンバーに変更が加えられるたびに記録されます。  
  
 トランザクション ログの種類については、「[エンティティのトランザクション ログの種類の変更 (マスター データ サービス)](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)」を参照してください。  
  
 メンバー リビジョン履歴は、次の変更が行われた場合に記録されます。  
  
-   メンバーが作成、削除、再アクティブ化、またはパージされた。  
  
-   属性値が変更された。  
  
-   メンバーが階層内またはコレクション内で移動された。  
  
## <a name="view-and-manage-revision-history-by-entity"></a>エンティティ単位でのリビジョン履歴の表示と管理  
 [エクスプローラー] 機能領域で、エンティティ内のすべてのメンバーのリビジョンを表示できます。 更新権限を持っている場合、メンバーを以前のリビジョンにロールバックできます。  
  
 **リビジョン履歴を表示して管理するには**  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]でモデルとバージョンを選択し、 **[エクスプローラー]** をクリックします。  
  
2.  **[エンティティ]** メニューからエンティティを選択します。  
  
3.  **[履歴の表示]** をクリックして、エンティティの履歴データをすべて表示します。  
  
4.  **[フィルター]** をクリックしてデータをフィルター処理します。  
  
5.  列ヘッダーをクリックしてデータを並べ替えます。  
  
6.  更新権限を持っている場合、 **[Revert Member]** (メンバーを元に戻す) をクリックして、選択したバージョンにロールバックします。  
  
## <a name="view-and-manage-revision-history-by-member"></a>メンバー単位でのリビジョン履歴の表示と管理  
 メンバーに対する読み取り権限を持っている場合、[エクスプローラー] 機能領域でメンバーのリビジョンを表示できます。 更新権限を持っている場合、メンバーをロールバックして以前のバージョンに戻したり、リビジョンに注釈を追加したりできます。  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]でモデルとバージョンを選択し、 **[エクスプローラー]** をクリックします。  
  
2.  **[エンティティ]** メニューからエンティティを選択します。  
  
3.  メンバーを選択します。  
  
4.  右側のペインで **[履歴の表示]** をクリックします。  
  
## <a name="log-retention-setting"></a>ログの保有期間の設定  
 **データベースのシステム設定の** [Log retention in Days] [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] (ログ保有期間日数) プロパティを設定することで、履歴データが保持される期間を構成できます。または、モデルを作成または編集するときに、 **[Log Retention Days]** (ログ保有期間の日数) を設定して保有期間を構成できます。  
  
## <a name="related-task"></a>関連タスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|メンバー リビジョン履歴のロールバック|[メンバー リビジョン履歴のロールバック (マスター データ サービス)](../master-data-services/rollback-member-revision-history-master-data-services.md)|  
  
## <a name="see-also"></a>参照  
 [モデルを作成する (マスター データ サービス)](../master-data-services/create-a-model-master-data-services.md)   
 [システム設定 (マスター データ サービス)](../master-data-services/system-settings-master-data-services.md)  
  
  
