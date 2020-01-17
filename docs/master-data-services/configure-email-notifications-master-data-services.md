---
title: 電子メール通知を構成する
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- e-mail [Master Data Services], configuring
- notifications [Master Data Services], configuring notifications
ms.assetid: 4241a6ab-7465-471b-9890-57c6b572037e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2b49a2a9b52df3cf5364f0e4f86b4181439ff61b
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729644"
---
# <a name="configure-email-notifications-master-data-services"></a>電子メール通知を構成する (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] で電子メール メッセージを自動的に送信する場合は、通知電子メールを構成します。  
  
### <a name="to-configure-notifications"></a>通知を構成するには  
  
1.  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]の **[データベース]** ページで、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースを選択します。  
  
2.  **[システム設定]** セクションで、 **[プロファイルの作成]** をクリックします。  
  
3.  すべての必須フィールドを入力します。 詳細については、「[[データベース メール プロファイルとアカウントの作成] ダイアログ ボックス (マスター データ サービス構成マネージャー)](../master-data-services/create-database-mail-profile-and-account-dialog-box.md)」を参照してください。  
  
4.  クリックして **OK**です。  
  
    > [!NOTE]  
    >  通知を構成した後に [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] を使用して変更を加えることはできません。 変更は [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースで直接行う必要があります。 詳細については、「 [データベース メール構成オブジェクト](../relational-databases/database-mail/database-mail-configuration-objects.md)」を参照してください。  
  
## <a name="next-steps"></a>Next Steps  
  
-   [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] には、通知に影響を与える設定があります。 これらの設定は、 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] で調整するか、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの System Settings テーブルで直接調整することができます。 詳細については、「[システム設定 &#40;マスター データ サービス&#41;](../master-data-services/system-settings-master-data-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [通知 (マスター データ サービス)](../master-data-services/notifications-master-data-services.md)   
 [電子メール通知のトラブルシューティング (Master Data Services)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)   
 [通知を送信するようにビジネス ルールを構成する (マスター データ サービス)](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)  
  
  
