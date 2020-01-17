---
title: マスター データ サービスのデータベースと web サイトのセットアップ |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.general.f1
ms.assetid: d50863e7-50d9-4ab8-aabb-fd68e2d132a1
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 478dea9095fe22a437aecf138c22374b5a70885b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054102"
---
# <a name="set-up-the-database-and-website-for-master-data-services"></a>マスター データ サービスのデータベースと Web サイトの設定
  [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] を使って、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] のデータベースと Web サイトを設定する (MDS)  
  
 データベースと Web サイトを設定するには、次のタスクを実行してください。  
  
1.  **の** [データベース構成] [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]ページで、データベースを作成します。  
  
     詳しくは、次を参照してください[データベース構成 ページ&#40;Master Data Services 構成マネージャー&#41; ](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)と[データベース生成ウィザード&#40;Master Data Services 構成マネージャー&#41; 。](../../2014/master-data-services/create-database-wizard-master-data-services-configuration-manager.md).  
  
2.  **の** [Web 構成] [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]ページで、新しい Web サイトを作成するか、既定の Web サイトを選ぶか、別の既存の Web サイトを選びます。 その後、MDS データベースを、選んだ Web アプリケーションや作成した Web アプリケーションに関連付けます。  
  
     詳しくは、次を参照してください[Web 構成 ページ&#40;Master Data Services 構成マネージャー&#41; ](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)と[web サイトの作成 ダイアログ ボックス&#40;Master Data Services 構成マネージャー&#41; 。](../../2014/master-data-services/create-website-dialog-box-master-data-services-configuration-manager.md).  
  
3.  (省略可能) **の** [Web 構成] [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]ページで、Data Quality Services との統合を有効にします。  
  
     詳細については、次を参照してください。 [Web 構成 ページ&#40;Master Data Services 構成マネージャー&#41; ](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)と[マスター データ サービスと Data Quality Services 統合を有効にする](install-windows/enable-data-quality-services-integration-with-master-data-services.md)します。  
  
 また、 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] を使って、MDS データベースに関連付けられている Web アプリケーションとサービスの設定値を指定できます。 たとえば、データの読み込み頻度や検証メールの送信頻度を指定できます。 詳細については、「[システム設定 &#40;マスター データ サービス&#41;](../../2014/master-data-services/system-settings-master-data-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マスター データ サービス データベース](../../2014/master-data-services/master-data-services-database.md)   
 [マスター データ マネージャー Web アプリケーション](../../2014/master-data-services/master-data-manager-web-application.md)  
  
  
