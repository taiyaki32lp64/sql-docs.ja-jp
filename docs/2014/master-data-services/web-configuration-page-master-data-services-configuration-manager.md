---
title: '[Web の構成] ページ (マスター データ サービス構成マネージャー) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.webconfigpg.f1
ms.assetid: 7b900778-0169-4e42-9faf-98dc1c01313e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 12ba4a2d03e98d5f2dac79917e23a93c0a24cdb0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481217"
---
# <a name="web-configuration-page-master-data-services-configuration-manager"></a>[Web の構成] ページ (マスター データ サービス構成マネージャー)
  **[Web の構成]** ページを使用すると、Web サイトまたは Web アプリケーションを新規作成できます。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションを選択すると、アプリケーションの [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースを指定して、Data Quality Services を有効にすることができます。  
  
## <a name="configure-the-web-application"></a>Web アプリケーションの構成  
  
|コントロール名|説明|  
|------------------|-----------------|  
|**[Web サイト]**|新しい Web サイトを作成するか、既定の Web サイトを選択するか、または (リストされている場合は) 利用可能な別のサイトを選択します。 この一覧には、ローカル コンピューター上のインターネット インフォメーション サービス (IIS) で定義されている Web サイトが表示されます。 新しい Web サイトを作成すると、新しい Web アプリケーションが自動的に作成されます。 既定または別の既存サイトを選択した場合は、手動でアプリケーションを作成する必要があります。|  
|**[Web アプリケーション]**|構成する [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションを選択します。 このボックスには、選択した Web サイト内の [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションのみが表示されます。<br /><br /> 何も表示されない場合は、 **[アプリケーションの作成]** をクリックして Web サイトを作成します。|  
|**アプリケーションを作成します。**|選択したサイト内の **Web アプリケーションを作成するための** [Web アプリケーションの作成] [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ダイアログ ボックスを開きます。 このボタンは、選択したサイトに [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションとして構成されたルート Web アプリケーションが存在しない場合のみ、有効になります。|  
  
## <a name="associate-application-with-database"></a>アプリケーションとデータベースの関連付け  
  
|コントロール名|説明|  
|------------------|-----------------|  
|**Select**|**[サーバーへの接続]** ダイアログ ボックスを開きます。このダイアログ ボックスから [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスに接続して、選択した [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web アプリケーションに関連付ける [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] データベースを選択します。|  
|**SQL Server インスタンス (SQL Server instance)**|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースをホストする、選択した [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] インスタンスの名前が表示されます。 これは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスに接続してデータベースを選択するまで、空白になります。|  
|**[データベース]**|選択した [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Web アプリケーションに関連付けられている [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] データベースの名前が表示されます。 これは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスに接続してデータベースを選択するまで、空白になります。|  
  
## <a name="enable-dqs-integration"></a>DQS 統合の有効化  
  
|コントロール名|説明|  
|------------------|-----------------|  
|**[Data Quality Services との統合を有効化]**|このオプションを選択すると、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]で使用可能な Data Quality 機能が有効になります。 詳細については、「 [マスター データ サービスを使用した Data Quality Services 統合の有効化](install-windows/enable-data-quality-services-integration-with-master-data-services.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [マスター データ サービスのデータベースと web サイトの設定します。](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Web アプリケーションの要件&#40;マスター データ サービス&#41;](install-windows/web-application-requirements-master-data-services.md)   
 [マスター データ マネージャー Web アプリケーションの作成 &#40;マスター データ サービス&#41;](install-windows/create-a-master-data-manager-web-application-master-data-services.md)   
 [MDS 2014 と「サービス利用不可」エラー](https://blogs.msdn.com/b/womeninanalytics/archive/2015/08/19/mds-2014-and-service-unavailable-error.aspx)  
  
  
