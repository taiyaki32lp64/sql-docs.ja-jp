---
title: '[Web アプリケーションの作成] ダイアログ ボックス (Master Data Services 構成マネージャー) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.createapp.f1
ms.assetid: e045b41a-4836-47f6-8e78-2b09494b461f
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 65e057224a8456f893b38e106e6b7f75d03d237a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65483230"
---
# <a name="create-web-application-dialog-box-master-data-services-configuration-manager"></a>[Web アプリケーションの作成] ダイアログ ボックス (Master Data Services 構成マネージャー)
  **[Web アプリケーションの作成]** ダイアログ ボックスを使用して、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションを作成します。 この Web アプリケーションは、 **[Web の構成]** ページで選択したサイトに作成されます。  
  
## <a name="web-application"></a>Web アプリケーション  
 Web サーバーでは、ファイル システム内の [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] **WebApplication** folder in the file system. セットアップ中に、この場所を指定し、既定のパスは*ドライブ*: \Program Files\Microsoft SQL server \120\master Data services \webapplication です。  
  
|コントロール名|説明|  
|------------------|-----------------|  
|[仮想パス]|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションを作成する仮想パスを選択します。 仮想パスは、Web アプリケーションへのアクセスに使用される URL の一部です。<br /><br /> この一覧は、 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションを作成できる、アプリケーションの仮想パスのみが表示されるようにフィルター選択されています。 別の [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションに [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションを作成することはできません。|  
|Alias|[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションの名前を入力するか、既定の名前を使用します。 この名前は、Web ブラウザーから Web アプリケーションにアクセスするための URL で使用されます。|  
  
## <a name="application-pool"></a>アプリケーション プール  
  
|コントロール名|説明|  
|------------------|-----------------|  
|**名前**|新しいアプリケーション プールの一意な表示名を入力するか、既定の名前を使用します。 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションは、このアプリケーション ツールに追加されます。<br /><br /> アプリケーション プールには、あるアプリケーション プール内のアプリケーションが別のアプリケーション プール内のアプリケーションに影響しないように境界が設けられています。|  
|**ユーザー名**|Active Directory のドメインおよびユーザー名を入力します。 このアカウントは、Web アプリケーションを実行するアプリケーション プールの ID です。 このアカウントは、 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの作成時にサービス アカウントとして指定したアカウントと同じにします。<br /><br /> このアカウントは、データベースにアクセスするために [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの mds_exec データベース ロールに追加されます。 詳細については、「[データベース ログイン、ユーザー、およびロール &#40;マスター データ サービス&#41;](database-logins-users-and-roles-master-data-services.md)」を参照してください。 また、このアカウントは、[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Windows グループ **MDS_ServiceAccounts** にも追加されます。このグループには、ファイル システムの一時コンパイル ディレクトリ **MDSTempDir** に対する権限が与えられています。 詳細については、「[フォルダーとファイルの権限 &#40;マスター データ サービス&#41;](../../2014/master-data-services/folder-and-file-permissions-master-data-services.md)」を参照してください。|  
|**Password**|指定したユーザー アカウントのパスワードを入力します。|  
|**[パスワードの確認入力]**|指定したユーザー アカウントのパスワードを再入力します。 **[パスワード]** フィールドと **[パスワードの確認入力]** フィールドには、同じパスワードを入力する必要があります。|  
  
## <a name="see-also"></a>参照  
 [[Web の構成] ページ &#40;マスター データ サービス構成マネージャー&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
 [マスター データ サービスのデータベースと web サイトの設定します。](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Web アプリケーションの要件&#40;マスター データ サービス&#41;](install-windows/web-application-requirements-master-data-services.md)   
 [マスター データ マネージャー Web アプリケーションの作成 &#40;マスター データ サービス&#41;](install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
