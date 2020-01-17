---
title: レポート サーバーで Windows 認証を構成する | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Windows authentication [Reporting Services]
- Reporting Services, configuration
ms.assetid: 4de9c3dd-0ee7-49b3-88bb-209465ca9d86
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a575d2e0f366df452d37615c7d3076027f5c400a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102131"
---
# <a name="configure-windows-authentication-on-the-report-server"></a>レポート サーバーで Windows 認証を構成する
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、既定では、ネゴシエート認証または NTLM 認証を指定する要求を受け入れます。 これらのセキュリティ プロバイダーを使用するクライアント アプリケーションおよびブラウザーが配置に含まれている場合は、追加の構成なしで既定値を使用できます。 Windows 統合セキュリティの別のセキュリティ プロバイダーを使用する場合 (たとえば Kerberos を直接使用する場合)、または既定値を変更した後に元の設定を復元する場合は、このトピックの情報を使用して、レポート サーバーで認証設定を指定できます。  
  
 Windows 統合セキュリティを使用するには、レポート サーバーにアクセスする必要がある各ユーザーに、有効な Windows ローカル ユーザー アカウントまたはドメイン ユーザー アカウントを割り当てるか、そのユーザーを Windows ローカル グループ アカウントまたはドメイン グループ アカウントのメンバーにする必要があります。 信頼されている他のドメインのアカウントを含めることもできます。 このアカウントは、レポート サーバー コンピューターにアクセスできる必要があります。また、レポート サーバーの特定の操作を実行できるように、後でこのアカウントをロールに割り当てる必要があります。  
  
 次の追加要件も満たす必要があります。  
  
-   RSReportServer.config ファイルの `AuthenticationType` が、`RSWindowsNegotiate`、`RSWindowsKerberos`、または `RSWindowsNTLM` に設定されている必要があります。 レポート サーバー サービス アカウントが NetworkService または LocalSystem である場合、RSReportServer.config ファイルには、既定で `RSWindowsNegotiate` 設定が含まれます。それ以外の場合は、`RSWindowsNTLM` 設定が使用されます。 Kerberos 認証のみを使用するアプリケーションがある場合は、`RSWindowsKerberos` を追加できます。  
  
    > [!IMPORTANT]  
    >  レポート サーバー サービスをドメイン ユーザー アカウントで実行するように構成し、かつそのアカウントのサービス プリンシパル名 (SPN) を登録していない場合は、`RSWindowsNegotiate` を使用すると Kerberos 認証エラーが発生します。 詳細については、このトピックの「 [レポート サーバー接続時の Kerberos 認証エラーの解決](#proxyfirewallRSWindowsNegotiate) 」を参照してください。  
  
-   [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] で Windows 認証を構成する必要があります。 既定では、レポート サーバー Web サービスとレポート マネージャーの Web.config ファイルが含まれて、\<認証モード ="Windows"> 設定します。 この設定を \<authentication mode="Forms"> に変更すると、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の Windows 認証が失敗します。  
  
-   Web.config ファイルに、レポート サーバー Web サービスとレポート マネージャーである必要があります\<identity impersonate ="true"/>。  
  
-   クライアント アプリケーションまたはブラウザーが、Windows 統合セキュリティをサポートしている必要があります。  
  
 レポート サーバーの認証設定を変更するには、RSReportServer.config ファイルの XML 要素と値を編集する必要があります。 特定の組み合わせを実装するために、このトピックの例をコピーして貼り付けることもできます。  
  
 既定の設定は、すべてのクライアント コンピューターとサーバー コンピューターが同じドメインまたは信頼されているドメインにあり、かつレポート サーバーがイントラネット アクセス用に企業のファイアウォールの内側に配置されている場合に最も適しています。 Windows 資格情報を渡すには、ドメインが信頼されていて単一であることが必要です。 サーバーで Kerberos Version 5 プロトコルを有効にした場合は、資格情報を複数回渡すことができます。 それ以外の場合は、資格情報をその有効期限が切れる前に 1 回だけ渡すことができます。 複数のコンピューター接続に対する資格情報の構成の詳細については、「 [レポート データ ソースに関する資格情報と接続情報を指定する](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)」を参照してください。  
  
 次に示す手順は、ネイティブ モードのレポート サーバーを対象としています。 レポート サーバーを SharePoint 統合モードで配置する場合は、Windows 統合セキュリティを指定する既定の認証設定を使用する必要があります。 レポート サーバーでは、既定の Windows 認証拡張機能の内部機能を使用して、SharePoint 統合モードのレポート サーバーがサポートされます。  
  
## <a name="extended-protection-for-authentication"></a>認証の拡張保護 (Extended Protection for Authentication)  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]以降では、認証の拡張保護がサポートされています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 機能により、認証の拡張保護に対するチャネル バインドとサービス バインドの使用がサポートされます。 この [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 機能は、拡張保護がサポートされているオペレーティング システムで使用する必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の拡張保護に対する構成は、RSReportServer.config ファイルの設定によって決まります。 このファイルは、ファイルを編集するか WMI API を使用して更新できます。 詳細については、「 [Reporting Services での認証の拡張保護](extended-protection-for-authentication-with-reporting-services.md)」をご覧ください。  
  
### <a name="to-configure-a-report-server-to-use-windows-integrated-security"></a>レポート サーバーを構成して Windows 統合セキュリティを使用するには  
  
1.  テキスト エディターで RSReportServer.config を開きます。  
  
2.  検索 <`Authentication`>。  
  
3.  次に示す XML 構造の中でニーズに最も合うものをコピーします。 `RSWindowsNegotiate`、`RSWindowsNTLM`、および `RSWindowsKerberos` は、任意の順序で指定できます。 個々の要求ではなく接続を認証する場合は、認証の永続化を有効にする必要があります。 認証の永続化を有効にすると、接続が続いている間は、認証を必要とするすべての要求が許可されます。  
  
     1 番目の XML 構造は、レポート サーバー サービス アカウントが NetworkService または LocalSystem である場合の既定の構成です。  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsNegotiate />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     2 番目の XML 構造は、レポート サーバー サービス アカウントが NetworkService と LocalSystem のいずれにも該当しない場合の既定の構成です。  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    ```  
  
     \</Authentication>  
  
     3 番目の XML 構造は、Windows 統合セキュリティで使用されるすべてのセキュリティ パッケージを指定します。  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsNegotiate />  
                 <RSWindowsKerberos />  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
    ```  
  
     4 番目の XML 構造は、配置が Kerberos をサポートしていない場合、または Kerberos 認証エラーに対処する場合にのみ、NTLM を指定します。  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsNTLM />  
          </AuthenticationTypes>  
    ```  
  
4.  既存のエントリを貼り付けます <`Authentication`>。  
  
     `Custom` の各種類と `RSWindows` は併用できないので注意してください。  
  
5.  必要に応じて拡張保護の設定を変更します。 既定では、拡張保護は無効になっています。  これらのエントリが存在しない場合は、拡張保護がサポートされているバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] が現在のコンピューターで実行されていない可能性があります。 詳細については、「 [Extended Protection for Authentication with Reporting Services](extended-protection-for-authentication-with-reporting-services.md)」をご覧ください。  
  
    ```  
          <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>  
          <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>  
    ```  
  
6.  ファイルを保存します。  
  
7.  スケールアウト配置を構成した場合は、配置内の他のレポート サーバーに対して上記の手順を繰り返します。  
  
8.  レポート サーバーを再起動して、現在開いているセッションを消去します。  
  
##  <a name="proxyfirewallRSWindowsNegotiate"></a> レポート サーバーに接続するときに、Kerberos 認証エラーを解決します。  
 ネゴシエート認証または Kerberos 認証が構成されているレポート サーバーでは、Kerberos 認証エラーが発生すると、レポート サーバーへのクライアント接続が失敗します。 Kerberos 認証エラーは、次の場合に発生します。  
  
-   サービス プリンシパル名 (SPN) を登録していない Windows ドメイン ユーザー アカウントでレポート サーバー サービスが実行されたとき。  
  
-   レポート サーバーが `RSWindowsNegotiate` 設定で構成されているとき。  
  
-   ブラウザーがレポート サーバーに送信する要求の認証ヘッダーで、NTLM ではなく Kerberos が選択されたとき。  
  
 Kerberos のログ記録を有効にしていれば、エラーを検出できます。 資格情報の入力を複数回要求された後に空のブラウザー ウィンドウが表示された場合も、エラーが発生しています。  
  
 削除することで Kerberos 認証エラーが発生していることを確認することができます < `RSWindowsNegotiate` /> から、構成ファイルと、接続を再試行します。  
  
 問題を確認したら、次の方法で問題に対処できます。  
  
-   ドメイン ユーザー アカウントでレポート サーバー サービスの SPN を登録します。 詳細については、「[レポート サーバーのサービス プリンシパル名 &#40;SPN&#41; の登録](../report-server/register-a-service-principal-name-spn-for-a-report-server.md)」を参照してください。  
  
-   ネットワーク サービスなどのビルトイン アカウントで実行されるように、サービス アカウントを変更します。 ビルトイン アカウントは、HTTP SPN を Host SPN にマップします。これは、コンピューターをネットワークに追加するときに定義されます。 詳細については、「[サービス アカウントの構成 (SSRS 構成マネージャー)](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)」を参照してください。  
  
-   NTLM を使用します。 NTLM は一般に、Kerberos 認証が失敗した場合に機能します。 NTLM を使用するには、RSReportServer.config ファイルから `RSWindowsNegotiate` を削除し、`RSWindowsNTLM` のみが指定されていることを確認します。 この方法を選択すれば、SPN を定義していないドメイン ユーザー アカウントでも、引き続きレポート サーバー サービスに使用できます。  
  
#### <a name="logging-information"></a>ログ情報  
 ログ情報に、Kerberos 関連の問題の解決に役立つものがいくつかあります。  
  
##### <a name="user-account-control-attribute"></a>User-Account-Control 属性  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アカウントに Active Directory の十分な属性セットがあるかどうかを確認します。 Reporting Services サービスのトレース ログ ファイルで、ログに記録された UserAccountControl 属性の値を探します。 値は 10 進形式で記録されています。 10 進値を 16 進形式に変換し、その値を User-Account-Control 属性が記述された MSDN のトピックで検索する必要があります。  
  
-   Reporting Services サービスのトレース ログのエントリは、次のように表示されます。  
  
    ```  
    appdomainmanager!DefaultDomain!8f8!01/14/2010-14:42:28:: i INFO: The UserAccountControl value for the service account is 590336  
    ```  
  
-   10 進値を 16 進形式に変換する 1 つの方法として、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows の電卓を使用することができます。 Windows の電卓では、[10 進] オプションと [16 進] オプションを表示するいくつかのモードがサポートされています。 [10 進] オプションを選択し、ログ ファイルで見つけた 10 進値を貼り付けるか入力して、[16 進] オプションを選択します。  
  
-   次に、「 [User-Account-Control 属性](https://go.microsoft.com/fwlink/?LinkId=183366) 」を参照して、サービス アカウントの属性を取得します。  
  
##### <a name="spns-configured-in-active-directory-for-the-reporting-services-service-account"></a>Reporting Services サービス アカウントに対して Active Directory で構成された SPN  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスのトレース ログ ファイルに SPN が記録されるようにするために、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の拡張保護機能を一時的に有効にすることができます。  
  
-   構成ファイル `rsreportserver.config` を次のように設定して変更します。  
  
    ```  
    <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>   
    <RSWindowsExtendedProtectionScenario>Any</RSWindowsExtendedProtectionScenario>  
    ```  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービスを再開し、トレース ログ ファイルで次のようなエントリを探します。  
  
    ```  
    rshost!rshost!e44!01/14/2010-14:43:51:: i INFO: Registered valid SPNs list for endpoint 2: rshost!rshost!e44!01/14/2010-14:43:52:: i INFO: SPN Whitelist Added <Explicit> - <HTTP/sqlpod064-13.w2k3.net>.  
    ```  
  
-   \<Explicit> の下に、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アカウントに対して Active Directory で構成された SPN の値が表示されます。  
  
 拡張保護の使用を止める場合は、構成値を既定に戻し、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アカウントを再開します。  
  
```  
<RSWindowsExtendedProtectionLevel>Off</RSWindowsExtendedProtectionLevel>  
<RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionScenario>  
```  
  
 詳細については、「 [Reporting Services での認証の拡張保護](extended-protection-for-authentication-with-reporting-services.md)」をご覧ください。  
  
#### <a name="how-the-browser-chooses-negotiated-kerberos-or-negotiated-ntlm"></a>ネゴシエートされた Kerberos またはネゴシエートされた NTLM がブラウザーで選択されるしくみ  
 Internet Explorer を使用してレポート サーバーに接続すると、認証ヘッダーでネゴシエートされた Kerberos または NTLM が指定されます。 次の場合は、Kerberos に代わって NTLM が使用されます。  
  
-   要求がローカル レポート サーバーに送信された場合。  
  
-   要求が、ホスト ヘッダーまたはサーバー名ではなく、レポート サーバー コンピューターの IP アドレスに送信された場合。  
  
-   Kerberos 認証に使用されるポートがファイアウォール ソフトウェアでブロックされた場合。  
  
-   特定のサーバーのオペレーティング システムで Kerberos が有効になっていない場合。  
  
-   ドメインに含まれている古いバージョンの Windows クライアントおよびサーバー オペレーティング システムが、そのオペレーティング システムの新しいバージョンに組み込まれている Kerberos 認証機能をサポートしていない場合。  
  
 さらに Internet Explorer では、URL、LAN、およびプロキシの設定内容に応じて、ネゴシエートされた Kerberos または NTLM が選択されることがあります。  
  
###### <a name="report-server-url"></a>レポート サーバーの URL  
 URL に完全修飾ドメイン名が含まれている場合、Internet Explorer は NTLM を選択します。 URL で localhost が指定されている場合も、Internet Explorer は NTLM を選択します。 URL でコンピューターのネットワーク名が指定されている場合、Internet Explorer はネゴシエートを選択します。この認証は、レポート サーバー サービス アカウントに SPN が存在するかどうかによって成功または失敗します。  
  
###### <a name="lan-and-proxy-settings-on-the-client"></a>クライアントでの LAN とプロキシの設定  
 Internet Explorer での LAN とプロキシの設定によって、NTLM が Kerberos の代わりに選択されるかどうかが決まります。 ただし、LAN とプロキシの設定は組織間で異なるため、Kerberos 認証エラーがどの設定に起因するかを正確に特定することは不可能です。 たとえば所属する組織で、URL を、イントラネット URL から完全修飾ドメイン名 URL (インターネット接続経由で解決される URL) に変換するようなプロキシ設定が実施されているとします。 種類の異なる URL に種類の異なる認証プロバイダーが使用されると、失敗すると予想した接続が成功することがあります。  
  
 認証の失敗が原因と考えられる接続エラーが発生した場合は、問題の原因を特定するために、LAN とプロキシの設定の組み合わせを変えてみてください。 Internet Explorer では、LAN とプロキシの設定を **[ローカル エリア ネットワーク (LAN) の設定]** ダイアログ ボックスで行います。このダイアログ ボックスを開くには、 **[インターネット オプション]** の **[接続]** タブで **[LAN の設定]** をクリックします。  
  
## <a name="external-resources"></a>外部リソース  
  
-   Kerberos とレポート サーバーの詳細については、 [SharePoint、Reporting Services、PerformancePoint Monitoring Server と Kerberos を使用したビジネス インテリジェンス ソリューションの展開](https://go.microsoft.com/fwlink/?LinkID=177751)に関する記事を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [レポート サーバーでの認証](authentication-with-the-report-server.md)   
 [ネイティブ モードのレポート サーバーに対する権限の許可](granting-permissions-on-a-native-mode-report-server.md)   
 [RSReportServer 構成ファイル](../report-server/rsreportserver-config-configuration-file.md)   
 [レポート サーバーで基本認証を構成する](configure-basic-authentication-on-the-report-server.md)   
 [レポート サーバーでカスタム認証またはフォーム認証を構成する](configure-custom-or-forms-authentication-on-the-report-server.md)   
 [Reporting Services での認証の拡張保護](extended-protection-for-authentication-with-reporting-services.md)  
  
  
