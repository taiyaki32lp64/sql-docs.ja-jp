---
title: レポート サーバーのサービス プリンシパル名 (SPN) の登録 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: dda91d4f-77cc-4898-ad03-810ece5f8e74
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 92c0943b17f22c63481f1dbfb0f76977a4b71381
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66500232"
---
# <a name="register-a-service-principal-name-spn-for-a-report-server"></a>レポート サーバーのサービス プリンシパル名 (SPN) の登録
  相互認証に Kerberos プロトコルを使用するネットワークに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を配置する場合に、レポート サーバー サービスをドメイン ユーザー アカウントとして実行するように構成するには、レポート サーバー サービスのサービス プリンシパル名 (SPN) を作成する必要があります。  
  
## <a name="about-spns"></a>SPN について  
 SPN は、Kerberos 認証を使用するネットワークでのサービスの一意識別子です。 サービス クラスとホスト名で構成されますが、ポートが含まれることもあります。 HTTP SPN の場合、ポートは不要です。 Kerberos 認証を使用するネットワークでは、ビルトイン コンピューター アカウント (NetworkService や LocalSystem など) またはユーザー アカウントにサーバーの SPN を登録する必要があります。 ビルトイン アカウントには、自動的に SPN が登録されます。 一方、ドメイン ユーザー アカウントでサービスを実行する場合は、使用するアカウントに手動で SPN を登録する必要があります。  
  
 SPN を作成するには、 **SetSPN** コマンド ライン ユーティリティを使用します。 詳細については、以下を参照してください。  
  
-   [Setspn](https://technet.microsoft.com/library/cc731241\(WS.10\).aspx) (https://technet.microsoft.com/library/cc731241(WS.10).aspx) 。  
  
-   [サービス プリンシパル名 (SPN) SetSPN の構文 (Setspn.exe)](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx) (https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx) 。  
  
 このユーティリティをドメイン コントローラーで実行するには、ドメイン管理者であることが必要です。  
  
## <a name="syntax"></a>構文  
 SetSPN ユーティリティを使用してレポート サーバーの SPN を作成する場合は、次のようなコマンド構文を使用します。  
  
```  
Setspn -s http/<computername>.<domainname> <domain-user-account>  
```  
  
 **SetSPN** は、Windows Server で使用できます。 **-s** 引数は、重複する SPN がないことを検証してから、SPN を追加します。 **注: -s** は Windows Server 2008 以降の Windows Server で使用できます。  
  
 **HTTP** はサービス クラスです。 レポート サーバー Web サービスは、HTTP.SYS で実行されます。 HTTP 用に SPN を作成すると、副次的に、HTTP.SYS で実行される同じコンピューター上のすべての Web アプリケーション (IIS でホストされるアプリケーションを含む) に対して、ドメイン ユーザー アカウントに基づいてチケットが付与されます。 これらのサービスを別のアカウントで実行すると、認証要求が失敗します。 この問題を回避するには、すべての HTTP アプリケーションが同じアカウントで実行されるように構成するか、またはアプリケーションごとにホスト ヘッダーを作成し、作成したホスト ヘッダーごとに個別の SPN を作成することを検討してください。 ホスト ヘッダーを構成する場合、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成にかかわらず DNS を変更する必要があります。  
  
 \<*computername*> と \<*domainname*> に指定した値で、レポート サーバーをホストするコンピューターのネットワーク アドレスが一意に識別されます。 これは、ローカル ホスト名にすることも、完全修飾ドメイン名 (FQDN) にすることもできます。 ドメインが 1 つしかない場合、コマンド ラインから \<*domainname*> を省略できます。 \<*domain-user-account*> は、レポート サーバー サービスが実行され、SPN を登録する必要があるユーザー アカウントです。  
  
## <a name="register-an-spn-for-domain-user-account"></a>ドメイン ユーザー アカウントに対する SPN の登録  
  
#### <a name="to-register-an-spn-for-a-report-server-service-running-as-a-domain-user"></a>ドメイン ユーザーとして実行されるレポート サーバー サービスの SPN を登録するには  
  
1.  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をインストールし、レポート サーバー サービスをドメイン ユーザー アカウントとして実行するように構成します。 この手順が完了しないと、ユーザーはレポート サーバーに接続できないので注意してください。  
  
2.  ドメイン コントローラーにドメイン管理者としてログオンします。  
  
3.  コマンド プロンプト ウィンドウを開きます。  
  
4.  次のコマンドをコピーし、プレースホルダーの値を実際のネットワークで有効な値で置き換えます。  
  
    ```  
    Setspn -s http/<computer-name>.<domain-name> <domain-user-account>  
    ```  
  
     例: `Setspn -s http/MyReportServer.MyDomain.com MyDomainUser`  
  
5.  コマンドを実行します。  
  
6.  **RsReportServer.config** ファイルを開き、 `<AuthenticationTypes>` セクションを探します。  
  
7.  このセクションの最初のエントリとして `<RSWindowsNegotiate/>` を追加し、Kerberos を有効にします。  
  
## <a name="see-also"></a>参照  
 [サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Reporting Services ネイティブ モードのレポート サーバーの管理](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
