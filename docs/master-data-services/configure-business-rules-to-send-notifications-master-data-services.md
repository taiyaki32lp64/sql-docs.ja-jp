---
title: 通知を送信するようにビジネス ルールを構成する
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- business rules [Master Data Services], configuring notifications
- e-mail [Master Data Services], configuring business rules
- notifications [Master Data Services], configuring business rules
ms.assetid: b24f7b11-ab53-4642-999c-e17b543b3558
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4645b9faca312eb5bee12eef1130893785c327d5
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728565"
---
# <a name="configure-business-rules-to-send-notifications-master-data-services"></a>通知を送信するようにビジネス ルールを構成する (マスター データ サービス)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]で、属性値の変更をユーザーに通知する場合は、通知を送信するようにビジネス ルールを構成します。  
  
## <a name="prerequisites"></a>Prerequisites  
 この手順を実行するには  
  
-   **[システム管理]** および **[ユーザー/グループの権限]** 機能領域にアクセスする権限が必要です。 **[ユーザー/グループの権限]** 機能領域に対する権限がないと、通知を送信するユーザーおよびグループの一覧を表示できません。  
  
-   モデル管理者である必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。  
  
-   検証アクションを使用するビジネス ルールが既に存在している必要があります。 詳細については、「[ビジネス ルールを作成しパブリッシュする (マスター データ サービス)](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)」を参照してください。  
  
-   通知を受け取るユーザーまたはグループには、検証に失敗した属性に対する**読み取り専用**以上の権限が必要です。 属性に対する権限が明示的または暗黙的に拒否されるユーザーまたはグループは、電子メールを受け取りますが、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で属性にアクセスすることはできません。  
  
-   メールがグループに送信された場合は、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] にアクセスしたグループ メンバーのみが電子メールを受信します。  
  
### <a name="to-configure-business-rules-to-send-notifications"></a>通知を送信するようにビジネス ルールを構成するには  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]で **[システム管理]** をクリックします。  
  
2.  メニュー バーから **[管理]** をポイントして **[ビジネス ルール]** をクリックします。  
  
3.  **[ビジネス ルール]** ページの **[モデル]** ボックスの一覧からモデルを選択します。  
  
4.  **[エンティティ]** ドロップダウン リストから、エンティティを選択します。  
  
5.  **[メンバーの種類]** ドロップ ダウン リストから、メンバーの種類を選択します。  
  
6.  グリッドで、編集するビジネス ルールの行を選択し、 **[編集]** をクリックします。  
  
7.  **[通知を送信する]** チェックボックスをオンにし、ドロップダウン リストから、電子メール通知を送信するユーザーまたはグループを選択します。  
  
8.  **[保存]** をクリックします。  
  
9. **[すべてパブリッシュ]** をクリックします。  
  
10. 確認のダイアログ ボックスで **[OK]** をクリックします。 **[ビジネス ルールの状態]** 列の値が **[アクティブ]** に変わり、 **[通知]** 列に通知の送信先ユーザーまたはグループが表示されます。  
  
## <a name="next-steps"></a>Next Steps  
  
-   以下のいずれかの手順でビジネス ルールをデータに適用します。  
  
    -   [ビジネス ルールに対して特定のメンバーを検証する (マスター データ サービス)](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [ビジネス ルールに対してバージョンを検証する (マスター データ サービス)](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   電子メール プロトコルを次のように構成します。  
  
    -   [電子メール通知を構成する (マスター データ サービス)](../master-data-services/configure-email-notifications-master-data-services.md)  
  
## <a name="see-also"></a>参照  
 [通知 (マスター データ サービス)](../master-data-services/notifications-master-data-services.md)   
 [電子メール通知を構成する (マスター データ サービス)](../master-data-services/configure-email-notifications-master-data-services.md)  
  
  
