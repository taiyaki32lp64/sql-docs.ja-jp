---
title: 通知
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- notifications [Master Data Services]
- notifications [Master Data Services], about notifications
- e-mail [Master Data Services]
- e-mail [Master Data Services], about e-mail notifications
ms.assetid: d7ad32d5-9fe5-48fd-8c61-0b00c0aff082
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ec76228a4f8307813a2bb098b648133e065c5cd5
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727959"
---
# <a name="notifications-master-data-services"></a>通知 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] を構成できます。  
  
## <a name="how-notifications-are-sent"></a>通知の送信方法  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]の通知を構成します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] のインスタンスでデータベース メールを使用することで、通知により電子メール メッセージが送信されます。 データベース メールの詳細については、 [オンライン ブックの「](../relational-databases/database-mail/database-mail-configuration-objects.md) データベース メール構成オブジェクト [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 」を参照してください。  
  
## <a name="when-notifications-are-sent"></a>通知の送信タイミング  
 通知を構成すると、以降は次のインスタンスで自動の電子メール通知を送信できます。  
  
|インスタンス|説明|  
|--------------|-----------------|  
|データがビジネス ルール検証に失敗した場合|属性値がビジネス ルールの検証に失敗した場合に電子メールを送信するように、個々のビジネス ルールを構成する必要があります。 通知には次の情報が含まれます。<br /><br /> [モデル]<br /><br /> バージョン<br /><br /> Entity<br /><br /> メンバー コード<br /><br /> 失敗したビジネス ルール<br /><br /> その属性値によってビジネス ルールが失敗したメンバーへのリンク<br /><br /> 通知発行時間<br /><br /> 詳細については、「[通知を送信するようにビジネス ルールを構成する (マスター データ サービス)](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)」を参照してください。|  
|モデル バージョンの状態が変わった場合|モデル バージョンの状態が変わるたびに、モデル管理者であるユーザーは自動的に通知を受け取ります。 通知には次の情報が含まれます。<br /><br /> [モデル]<br /><br /> バージョン<br /><br /> バージョンの前の状態と新しい状態<br /><br /> 通知発行時間<br /><br /> 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../master-data-services/administrators-master-data-services.md)」を参照してください。|  
|変更セットの状態の変更|承認を必要とするエンティティに対する変更セットの状態が変更されるたびに、エンティティの管理者または変更セットの所有者、あるいはその両方が自動的に通知を受信します。 通知には次の情報が含まれます。<br /><br /> [モデル]<br /><br /> バージョン<br /><br /> 変更セットの名前<br /><br /> 前の状態<br /><br /> 新しい状態<br /><br /> 保留中の変更内容を表示および変更するために変更セットを適用するリンク<br /><br /> 詳細については、「[変更セット (マスター データ サービス)](../master-data-services/changesets-master-data-services.md)」を参照してください。|  
  
## <a name="system-settings"></a>システム設定  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] には、通知に影響を与える設定があります。 これらの設定は、 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] で調整するか、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの System Settings テーブルで直接調整することができます。 詳細については、「[システム設定 &#40;マスター データ サービス&#41;](../master-data-services/system-settings-master-data-services.md)」を参照してください。  
  
## <a name="related-tasks"></a>関連タスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|電子メールの通知を送信するように [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] を構成する。|[電子メール通知を構成する (マスター データ サービス)](../master-data-services/configure-email-notifications-master-data-services.md)|  
|属性値の変更時に通知を送信するように、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] を構成する。|[通知を送信するようにビジネス ルールを構成する (マスター データ サービス)](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   [ビジネス ルール (マスター データ サービス)](../master-data-services/business-rules-master-data-services.md)  
  
-   [バージョン (マスター データ サービス)](../master-data-services/versions-master-data-services.md)  
  
-   [電子メール通知のトラブルシューティング (Master Data Services)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)  
  
  
