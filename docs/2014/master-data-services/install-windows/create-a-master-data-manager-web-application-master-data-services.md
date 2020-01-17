---
title: マスター データ マネージャー Web アプリケーションの作成 (マスター データ サービス) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 241d46d7-8008-47f6-bebd-0dfff1cc856a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 238cf52a52e53aa4ee2712e0bd6abf43a6c5e128
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479383"
---
# <a name="create-a-master-data-manager-web-application-master-data-services"></a>マスター データ マネージャー Web アプリケーションの作成 (マスター データ サービス)
  [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションは、マスター データを操作するためのユーザー用インターフェイスと、MDS を構成および管理するための管理者用インターフェイスを提供します。  
  
 Web アプリケーションは、必ず Web サイトに含める必要があります。 Web アプリケーションを作成するには、次のいずれかを実行する必要があります。  
  
-   既定の Web サイトを使用し、Web アプリケーションを作成する。  
  
-   既存の Web サイトを使用し、Web アプリケーションを作成する。  
  
-   新しい Web サイトを作成する (これにより Web アプリケーションが自動的に作成されます)。  
  
 Web アプリケーションを作成したら、それを [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースに関連付けます。  
  
## <a name="prerequisites"></a>前提条件  
  
-   データベースをホストするコンピューターの要件の詳細については、「[Web アプリケーションの要件 &#40;マスター データ サービス&#41;](web-application-requirements-master-data-services.md)」を参照してください。  
  
## <a name="to-create-a-master-data-manager-web-application-in-a-new-website"></a>新しい Web サイトにマスター データ マネージャー Web アプリケーションを作成するには  
 新しい Web サイトを作成した場合、ルート Web アプリケーションは [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションです。 また、作成された Web アプリケーションは新しいアプリケーション プールに追加されます。  
  
> [!NOTE]  
>  この手順を使用した場合、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションの仮想パスと別名を指定することはできません。 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]の仮想パスと別名を指定する場合は、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションとして構成されていない既存の Web サイトに Web アプリケーションを作成する必要があります。  
  
 また [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] では、HTTP バインドのみを含むサイトの作成もサポートされます。 HTTPS バインドを追加するには、 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] で新しいサイトとアプリケーションを作成します。詳細については、「 [マスター データ マネージャー Web アプリケーションのセキュリティ保護](secure-a-master-data-manager-web-application.md) 」を参照してください。  
  
#### <a name="to-create-a-master-data-manager-web-application-in-a-new-website"></a>新しい Web サイトにマスター データ マネージャー Web アプリケーションを作成するには  
  
1.  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
2.  左ペインで **[Web の構成]** をクリックします。  
  
3.  **[Web の構成]** ページにある Web サイトの一覧で、 **[新規 Web サイトの作成]** を選択します。  
  
4.  **[Web サイトの作成]** ダイアログ ボックスで、新しい Web サイトの情報を指定します。 ダイアログ ボックスのユーザー インターフェイス (UI) オプションの詳細については、「[[Web サイトの作成] ダイアログ ボックス &#40;マスター データ サービス構成マネージャー&#41;](../create-website-dialog-box-master-data-services-configuration-manager.md)」を参照してください。  
  
5.  **[OK]** をクリックします。  
  
## <a name="to-create-a-master-data-manager-web-application-in-an-existing-website"></a>既存の Web サイトにマスター データ マネージャー Web アプリケーションを作成するには  
 既存の Web サイトに Web アプリケーションを作成する場合は、Web アプリケーションの仮想パスと別名を選択できます。 作成された Web アプリケーションは新しいアプリケーション プールに追加されます。  
  
#### <a name="to-create-a-master-data-manager-web-application-in-an-existing-website"></a>既存の Web サイトにマスター データ マネージャー Web アプリケーションを作成するには  
  
1.  [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]を開きます。  
  
2.  左ペインで **[Web の構成]** をクリックします。  
  
3.  **[Web の構成]** ページで、 **[Web サイト]** ボックスの一覧から、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションを作成する Web サイトを選択します。  
  
4.  **[アプリケーションの作成]** をクリックします。  
  
5.  **[Web アプリケーションの作成]** ダイアログ ボックスで、新しい Web アプリケーションの情報を指定します。 ウィザードのユーザー インターフェイス (UI) オプションの詳細については、「[[Web アプリケーションの作成] ダイアログ ボックス &#40;マスター データ サービス構成マネージャー&#41;](../create-web-application-dialog-box-master-data-services-configuration-manager.md)」を参照してください。  
  
6.  **[OK]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
  
-   Web アプリケーションを [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースに関連付けます。 詳細については、「 [Master Data Services データベースと Web アプリケーションの関連付け](associate-a-master-data-services-database-and-web-application.md)」を参照してください。  
  
-   SSL (Secure Sockets Layer) を使用してコンテンツを暗号化する必要がある場合は、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションをホストする Web サイトで HTTPS バインドを使用するように構成します。 Web サーバー用にサーバー証明書を構成し、サイト用に HTTP バインドと SSL 設定を構成するには、IIS マネージャーなどのインターネット インフォメーション サービス (IIS) ツールを使用する必要があります。 詳細については、「 [マスター データ マネージャー Web アプリケーションのセキュリティ保護](secure-a-master-data-manager-web-application.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [マスター データ サービスのインストール](install-master-data-services.md)  
  
  
