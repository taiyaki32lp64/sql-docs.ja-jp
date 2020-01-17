---
title: データベースと web アプリケーションの関連付け
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ccb25672-f71d-4135-b548-f50eb45d8fa5
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d82bee5e275365b72adb3700cae8c11e6e67c9e7
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75253079"
---
# <a name="associate-a-master-data-services-database-and-web-application"></a>Master Data Services データベースと Web アプリケーションの関連付け

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  
  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションを [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースに関連付け、Web 操作に使用するデータベースを指定します。  
  
## <a name="prerequisites"></a>前提条件  
  
-   
  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] がローカル コンピューターにインストールされている必要があります。 詳細については、「 [マスター データ サービスのインストール](../../master-data-services/install-windows/install-master-data-services.md)」を参照してください。  
  
-   ローカルの [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションが存在している必要があります。 詳細については、「[マスター データ マネージャー Web アプリケーションを作成する方法 &#40;マスター データ サービス&#41;](../../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)」を参照してください。  
  
-   ローカルまたはリモートの [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースのどちらかが存在している必要があります。 詳細については、「 [マスター データ サービス データベースの作成](../../master-data-services/install-windows/create-a-master-data-services-database.md)」をご覧ください。  
  
### <a name="to-associate-a-master-data-services-database-and-web-application"></a>Master Data Services データベースと Web アプリケーションを関連付けるには  
  
1.  
  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
2.  左ペインで **[Web の構成]** をクリックします。  
  
3.  
  **[Web の構成]** ページで、 **[Web アプリケーション]** の下の **[Web サイト]** ボックスの一覧から [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションを含む Web サイトを選択します。  
  
4.  
  **[Web アプリケーション]** ボックスで、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]をホストする Web アプリケーションを選択します。  
  
5.  
  **[アプリケーションとデータベースの関連付け]** で、 **[選択]** をクリックします。 
  **[データベースへの接続]** ダイアログ ボックスが開きます。  
  
6.  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースをホストする [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] のインスタンスの接続情報を指定し、 **[接続]** をクリックします。  
  
7.  
  **[Master Data Services データベース]** ボックスの一覧から、Web アプリケーションに関連付けるデータベースを選択し、 **[OK]** をクリックします。  
  
8.  
  **[アプリケーションとデータベースの関連付け]** で、インスタンスおよびデータベースの情報が正しいことを確認し、 **[適用]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
  
-   Web アプリケーションが作成されると、プログラムによる [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web サービスへのアクセスが自動的に有効になります。 開発者がサービス メタデータにアクセスし、プログラムからプロキシ クラスを簡単に生成するには、メタデータ パブリッシュを有効にします。 詳細については、「 [マスター データ マネージャー Web サービス プロキシ クラスの作成](../../master-data-services/develop/create-master-data-manager-web-service-proxy-classes.md)」を参照してください。  
  
-   ユーザーおよびグループを [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]に追加します。 どのユーザーまたはグループも [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]へのアクセス権が付与されていない場合は、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] システム管理者の資格情報を使用して、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] を開く必要があります。 詳細については、「[Administrators &#40;Master Data Services&#41; (管理者 &#40;マスター データ サービス&#41;)](../../master-data-services/administrators-master-data-services.md)」および「[Users and Groups &#40;Master Data Services&#41; (ユーザーおよびグループ &#40;Master Data Services&#41;)](../../master-data-services/users-and-groups-master-data-services.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [マスターデータサービスのインストール](../../master-data-services/install-windows/install-master-data-services.md)   
 [[Web 構成] ページ &#40;マスターデータサービス構成マネージャー&#41;](../../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)  
  
  
