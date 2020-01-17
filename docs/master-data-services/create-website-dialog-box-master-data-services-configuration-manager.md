---
title: '[Web サイトの作成] ダイアログ ボックス'
ms.custom: seo-lt-2019
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql13.mds.configmanager.createsite.f1
ms.assetid: 179c9c1e-3b06-421b-b71b-1cb64d104f5e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: b3251f4ef6d27d06f72717cd096d85048b4134f4
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729420"
---
# <a name="create-website-dialog-box-master-data-services-configuration-manager"></a>[Web サイトの作成] ダイアログ ボックス (マスター データ サービス構成マネージャー)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  **[Web サイトの作成]** ダイアログ ボックスを使用すると、ローカル コンピューター上に新しい Web サイトを作成できます。 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]で Web サイトを作成すると、作成したサイトは、[!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web アプリケーションとして構成されるルート アプリケーションを伴って、ローカル コンピューター上のインターネット インフォメーション サービス (IIS) に追加されます。 また、新しいアプリケーション プールが作成され、Web アプリケーションがそのアプリケーション プールに追加されます。  
  
## <a name="web-site"></a>Web サイト  
  
|コントロール名|[説明]|  
|------------------|-----------------|  
|**Web サイト名**|Web サイトの名前を入力するか、既定の名前を使用します。 これは、IIS でサイトを識別するためだけに使用される表示名です。 Web ブラウザーからサイトにアクセスするためには使用されません。<br /><br /> この名前は、ローカル コンピューター上の IIS にあるすべてのサイトで一意である必要があります。|  
|**[プロトコル]**|**http** が表示されます。 クライアントとサーバーとの間の通信を暗号化されたチャネルで行う必要がない場合には、ハイパーテキスト転送プロトコル (HTTP) を使用します。<br /><br /> **注**: [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]で HTTPS サイトを作成することはできません。 HTTPS は、SSL (Secure Sockets Layer) を使用する HTTP プロトコルで、機密情報や個人データをやり取りする場合や個人情報を送信する前にサーバーの ID を確認するようユーザーに要求する場合に役立ちます。 暗号化されたチャネルを介してサーバーとクライアントとの間で情報を転送する必要がある場合は、IIS マネージャーなどの IIS ツールを使用してサイトを HTTPS バインドで構成し、Web サイト バインドをサーバー証明書に関連付ける必要があります。これを行うと、Web サイトを Web ブラウザーで開くことができるようになります。 サーバー証明書の詳細については、[ TechNet の「](https://go.microsoft.com/fwlink/?LinkId=163220)Configuring Server Certificates in IIS 7[!INCLUDE[msCoName](../includes/msconame-md.md)]」 (IIS 7 でサーバー証明書を構成する) を参照してください。|  
|**IP アドレス (IP address)**|ユーザーがサイトへのアクセスに使用できる IP アドレスを選択します。 既定では、 **[すべて未割り当て]** が選択されています。 特定の IPv4 または IPv6 アドレスを使用する理由がなければ、既定値を使用してください。<br /><br /> **[すべて未割り当て]** を選択すると、このサイトは、指定したポートとオプションのホスト名のすべての IP アドレスに対する要求に応答します。 サーバー上の別のサイトが同じポートにバインドしていても、特定の IP アドレスを使用している場合、そのサイトでは、そのポートと特定の IP アドレスに対する HTTP 要求を受信します。また、IP アドレスが **[すべて未割り当て]** に設定されているサイトでは、そのポートと他の IP アドレスに対するその他の HTTP 要求もすべて受信します。|  
|**[ポート]**|この Web サイトに対する要求で使用されるポートを入力します。 HTTP プロトコルを選択すると、既定のポートが 80 になります。 既定のポート以外のポートを指定する場合、クライアントは、Web サイトに接続するためにポート番号を指定する必要があります。<br /><br /> **注**: IIS の **[既定の Web サイト]** は、IP アドレスがすべて未割り当てになっている、ポート 80 の HTTP プロトコルを使用するように構成されています。 既定のバインド情報を使用して [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]で Web サイトの作成を試みると、バインドが重複していることを示すエラーが表示されます。 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]でサイトのバインド情報を変更するか、IIS マネージャーなどの IIS ツールを使用して既定の Web サイトのバインド情報を変更する必要があります。 または、IIS で Web サイトを一意に識別できるようにホスト ヘッダーを指定することもできます。 指定したポートでトラフィックを受信するようにファイアウォールを構成してください。|  
|**[ホスト ヘッダー]**|省略可能な値。 ホスト ヘッダー名を入力します。 ホスト ヘッダー名は、1 つの IP アドレスまたはポートを使用するコンピューターにホスト名 (ドメイン名) を割り当てるときに使用します。 ホスト名を指定すると、クライアントは、Web サイトへのアクセスに、IP アドレスではなくその名前を使用する必要があります。 ホスト名を構成すると、DNS サーバーにそのホスト名のエントリが反映されるまで、Web ブラウザーでそのサイトを開くことはできません。<br /><br /> たとえば、ユーザーに `https://www.contoso.com/` のサイトへのアクセスを求める場合は、ホスト名として www.contoso.com を指定して、DNS サーバーにこのエントリが反映される必要があります。<br /><br /> Web サイトがイントラネット上で使用できる場合は、ユーザーがブラウザーでサーバー名 (`https://server_name` など) を入力すると、ホスト名を指定する必要はありません。 ただし、使用している環境の DNS サーバーがこの Web サーバーの他の名前を保存するよう構成されている場合は、ユーザーが DNS サーバーに保存されている他の名前を使用できるように、各ホスト名に個別のバインドを作成できます。 サイトに複数のホスト名を構成する必要がある場合は、IIS マネージャーなどの IIS ツールを使用して、別のサイト バインドを追加します。|  
  
## <a name="application-pool"></a>アプリケーション プール  
  
|コントロール名|[説明]|  
|------------------|-----------------|  
|**名前**|新しいアプリケーション プールの一意な表示名を入力するか、表示されている既定の名前を使用します。 この Web サイトのルート Web アプリケーションは、このアプリケーション プールで実行されます。<br /><br /> アプリケーション プールには、あるアプリケーション プール内のアプリケーションが別のアプリケーション プール内のアプリケーションに影響しないように境界が設けられています。|  
|**ユーザー名**|Active Directory のドメインおよびユーザー名を入力します。 このアカウントは、Web アプリケーションを実行するアプリケーション プールの ID です。<br /><br /> このアカウントは、データベースにアクセスするために [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] データベースの mds_exec データベース ロールに追加されます。 詳細については、「[データベース ログイン、ユーザー、およびロール &#40;マスター データ サービス&#41;](../master-data-services/database-logins-users-and-roles-master-data-services.md)」を参照してください。 また、このアカウントは、[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Windows グループ **MDS_ServiceAccounts** にも追加されます。このグループには、ファイル システムの一時コンパイル ディレクトリ **MDSTempDir** に対する権限が与えられています。 詳細については、「[フォルダーとファイルの権限 &#40;マスター データ サービス&#41;](../master-data-services/folder-and-file-permissions-master-data-services.md)」を参照してください。|  
|**パスワード**|指定したユーザー アカウントのパスワードを入力します。|  
|**[パスワードの確認入力]**|指定したユーザー アカウントのパスワードを再入力します。 **[パスワード]** フィールドと **[パスワードの確認入力]** フィールドには、同じパスワードを入力する必要があります。|  
  
## <a name="see-also"></a>参照  
 [[Web の構成] ページ &#40;マスター データ サービス構成マネージャー&#41;](../master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
[マスター データ サービスのインストールと構成](../master-data-services/master-data-services-installation-and-configuration.md) [Web アプリケーションの要件 &#40;マスター データ サービス&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [マスター データ マネージャー Web アプリケーションの作成 &#40;マスター データ サービス&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
