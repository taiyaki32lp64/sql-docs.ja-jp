---
title: 電子メール配信用にレポートサーバーを構成する (SSRS Configuration Manager) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], distributing
- report servers [Reporting Services], e-mail delivery
- remote SMTP service [Reporting Services]
- distributing reports [Reporting Services], e-mail
- CDO
- Collaboration Data Objects
- SMTP settings [Reporting Services]
- e-mail [Reporting Services]
- sending reports
- mail [Reporting Services]
- local SMTP service [Reporting Services]
ms.assetid: b838f970-d11a-4239-b164-8d11f4581d83
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c2e34258f10033c61f9966e62fa7c14025423613
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952332"
---
# <a name="configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager"></a>電子メール配信用にレポート サーバーを構成する (SSRS 構成マネージャー)


  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には電子メール配信拡張機能があり、電子メールを使用してレポートを配布できます。 電子メール サブスクリプションをどのように定義するかに応じて、配信は、通知、リンク、添付ファイル、または埋め込みレポートから構成されます。 電子メール配信拡張機能は、既存のメール サーバー テクノロジと連携して動作します。 メール サーバーは、SMTP サーバーまたはフォワーダーである必要があります。 レポート サーバーは、オペレーティング システムに用意されている Collaboration Data Objects (CDO) ライブラリ (cdosys.dll) を通じて SMTP サーバーに接続します。  
  
 既定では、レポート サーバーの電子メール配信拡張機能は構成されていません。 Reporting Services 構成マネージャーを使用して、この拡張機能の最低限の構成を行う必要があります。 詳細なプロパティを設定するには、 `RSReportServer.config` ファイルを編集します。 この拡張機能を使用するようにレポート サーバーを構成できない場合は、代わりに共有フォルダーにレポートを配信できます。 詳細については、「 [File Share Delivery in Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md)」を参照してください。  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード|  
  
 
  
##  <a name="bkmk_configuration_requirements"></a>構成の要件  
  
-   レポート サーバーの電子メール配信は Collaboration Data Objects (CDO) に実装されており、ローカルまたはリモートの簡易メール転送プロトコル (SMTP) サーバーまたは SMTP フォワーダーを必要とします。 SMTP は、一部の Windows オペレーティング システムではサポートされていません。 Itanium ベース エディションの Windows Server 2008 を使用している場合、SMTP はサポートされません。 CDO によって提供される構成オプションの詳細については、MSDN の「 [CoClass の構成](https://go.microsoft.com/fwlink/?LinkId=98237) 」を参照してください。  
  
-   レポート サーバー サービス アカウントには、メールを送信する SMTP サーバーに対する権限が必要です。  
  
-   電子メール配信拡張機能では、電子メール添付ファイルに UTF-8 エンコードが使用されます。 エンコードを変更することはできません。HTML 表示拡張機能では UTF-8 だけがサポートされます。  
  
> [!NOTE]  
>  既定の電子メール配信拡張機能では、送信するメール メッセージのデジタル署名および暗号化はサポートされていません。  
  
 
  
##  <a name="bkmk_configure_for_local_or_remote_SMTP"></a>ローカルまたはリモートの SMTP サービス用のレポートサーバーの構成  
 ローカルの SMTP サービス、あるいはリモートの SMTP サーバーまたは SMTP フォワーダーを使用して、電子メール配信をサポートできます。 既存のリモート SMTP サーバーにアクセスできる場合は、リモート SMTP サーバーを使用してください。 使用できる SMTP サーバーがない場合、または後でコンピューター接続の障害が原因と考えられるレポート配信エラーが発生した場合は、ローカル SMTP サービスを使用するように切り替える必要があります。 ローカル サービスまたはリモート サービス用にレポート サーバーを構成する方法の詳細については、このトピックでさらに説明します。  
  
  
  
##  <a name="bkmk_setting_email_delivery"></a>電子メール配信の構成オプションの設定  
 レポート サーバーの電子メール配信を使用するには、先に、使用する SMTP サーバーに関する情報を提供する構成値を設定する必要があります。  
  
 電子メール配信用にレポート サーバーを構成するには、次の操作を行います。  
  
-   SMTP サーバーと、電子メールを送信する権限のあるユーザー アカウントを指定するだけの場合は、Reporting Services 構成マネージャーを使用します。 これらは、レポート サーバーの電子メール配信拡張機能を構成するために最低限必要な設定です。 詳細については、「[電子メール&#40;の設定-&#41; Configuration Manager SSRS ネイティブモード](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)」と「 [Reporting Services での電子メール配信](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)」を参照してください。  
  
-   (省略可能) テキスト エディターを使用して、RSreportserver.config ファイルで追加の設定を指定します。 このファイルには、レポート サーバーの電子メール配信の構成設定がすべて含まれています。 ローカル SMTP サーバーを使用する場合や、電子メールの配信を特定のホストに限定する場合は、これらのファイルで追加の設定を指定する必要があります。 構成ファイルの検索と変更の詳細については、SQL Server オンラインブックの「 [Reporting Services 構成ファイル&#40;&#41;を変更する](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。  
  
> [!NOTE]  
>  レポート サーバーの電子メール設定は CDO に基づいています。 特定の設定に関する詳細については、CDO の製品マニュアルを参照してください。  
  

  
##  <a name="bkmk_example_config_file"></a>レポートサーバーの電子メール構成の例  
 次の例は、リモート SMTP サーバーに対する RSreportserver.config ファイルでの設定を示しています。 設定に関する説明と有効な値については、 [ssNoVersion](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) オンライン ブックの「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onlオンライン ブックの「e or the CDO product documentation.  
  
```  
<RSEmailDPConfiguration>  
     <SMTPServer>mySMTPServer.Adventure-Works.com</SMTPServer>  
     <SMTPServerPort></SMTPServerPort>  
     <SMTPAccountName></SMTPAccountName>  
     <SMTPConnectionTimeout></SMTPConnectionTimeout>  
     <SMTPServerPickupDirectory></SMTPServerPickupDirectory>  
     <SMTPUseSSL></SMTPUseSSL>  
     <SendUsing>2</SendUsing>  
     <SMTPAuthenticate></SMTPAuthenticate>  
     <From>my-rs-email-account@Adventure-Works.com</From>  
     <EmbeddedRenderFormats>  
          <RenderingExtension>MHTML</RenderingExtension>  
     </EmbeddedRenderFormats>  
     <PrivilegedUserRenderFormats></PrivilegedUserRenderFormats>  
     <ExcludedRenderFormats>  
          <RenderingExtension>HTMLOWC</RenderingExtension>  
          <RenderingExtension>NULL</RenderingExtension>  
     </ExcludedRenderFormats>  
     <SendEmailToUserAlias>True</SendEmailToUserAlias>  
     <DefaultHostName></DefaultHostName>  
     <PermittedHosts>  
          <HostName>Adventure-Works.com</HostName>  
          <HostName>hotmail.com</HostName>  
     </PermittedHosts>  
</RSEmailDPConfiguration>  
```  
  

  
##  <a name="bkmk_setting_TO_field"></a>をに設定するための構成オプション:フィールドを設定するための構成オプション  
 **"個別のサブスクリプションを管理"** タスクで与えられる権限に従って作成されたユーザー定義サブスクリプションには、ドメイン ユーザー アカウントに基づく定義済みのユーザー名が含まれます。 ユーザーがサブスクリプションを作成すると、 **[宛先]** フィールドの受信者名は、サブスクリプションの作成者のドメイン ユーザー アカウントを使用して自動的に指定されます。  
  
 使用している SMTP サーバーまたはフォワーダーで、ドメイン ユーザー アカウントとは別の電子メール アカウントを利用している場合、SMTP サーバーからそのユーザーにレポートの配信が試行されたときに配信が失敗します。  
  
 この問題に対処するには、ユーザーが **[宛先]** フィールドに名前を入力できるように構成設定を変更します。  
  
1.  テキスト エディターで RSReportServer.config を開きます。  
  
2.  `SendEmailToUserAlias` を `False` に設定します。  
  
3.  `DefaultHostName` を SMTP サーバーまたはフォワーダーのドメイン ネーム システム (DNS) 名または IP アドレスに設定します。  
  
4.  ファイルを保存します。  
  
  
  
##  <a name="bkmk_options_remote_SMTP"></a>リモート SMTP サービスの構成オプション  
 レポート サーバーと SMTP サーバーまたはフォワーダーの間の接続は、次の構成設定によって決まります。  
  
-   `SendUsing` メッセージを送信する方法を指定します。 ネットワーク SMTP サービスまたはローカル SMTP サービスのピックアップ ディレクトリを選択できます。 リモート SMTP サービスを使用するには、RSReportServer.config ファイルでこの値を **2** に設定する必要があります。  
  
-   `SMTPServer` リモート SMTP サーバーまたはフォワーダーを指定します。 リモート SMTP サーバーまたはフォワーダーを使用している場合には、この値は必須です。  
  
-   `From` メール メッセージの **[送信者]** 行に使用する値を設定します。 リモート SMTP サーバーまたはフォワーダーを使用している場合には、この値は必須です。  
  
 リモート SMTP サービスで使用する他の値としては、次のものがあります (既定値を変更するのでない限り、これらの値をオーバーライドする必要はありません)。  
  
-   **SMTPServerPort** は、ポート 25 に構成します。  
  
-   **SMTPAuthenticate** では、レポート サーバーがリモート SMTP サーバーに接続する方法を指定します。 既定値は 0 (認証なし) です。 この場合、接続は匿名アクセスをとおして行われます。 ドメインの構成によっては、レポート サーバーと SMTP サーバーが同じドメインのメンバーであることが必要になる場合があります。  
  
     制限付きの配信リスト (たとえば、認証されたアカウントからの着信メッセージだけを受け付ける配信リスト) に電子メールを送信するには、 **SMTPAuthenticate** を **2**に設定します。  
  

  
##  <a name="bkmk_options_local_SMTP"></a>ローカル SMTP サービスの構成オプション  
 レポート サーバー電子メール配信のテストまたはトラブルシューティングを行う場合は、ローカル SMTP サービスの構成が役に立ちます。 既定ではローカル SMTP サービスは無効になっています。 有効にする方法については、「[電子メール配信用にレポートサーバーを構成する (ssrs Configuration Manager)](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) 」および「[電子メールの設定-Configuration Manager &#40;ssrs ネイティブ&#41;モード](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md)」を参照してください。  
  
 レポート サーバーとローカル SMTP サーバーまたはフォワーダーの間の接続は、次の構成設定によって決まります。  
  
-   `SendUsing` は**1**に設定されます。  
  
-   **SMTPServerPickupDirectory** には、ローカル ドライブのフォルダーを設定します。  
  
    > [!NOTE]  
    >  ローカル SMTP サーバーを使用している場合は、`SMTPServer` に設定しないようにしてください。  
  
-   `From` メール メッセージの **[送信者]** 行に使用する値を設定します。 この値は必須です。  
  
 
  
##  <a name="bkmk_use_configuration_manager"></a>Reporting Services Configuration Manager を使用してレポートサーバーの電子メールを構成するには  
  
1.  レポート サーバー Windows サービスが SMTP サーバー上で `Send As` 権限を保持していることを確認します。  
  
2.  Reporting Services 構成マネージャーを起動して、レポート サーバー インスタンスに接続します。  
  
3.  [電子メールの設定] ページで、SMTP サーバーの名前を入力します。 この値は、IP アドレス、企業イントラネット上のコンピューターの UNC 名、または完全修飾ドメイン名にすることができます。  
  
4.  **[送信者アドレス]** で、SMTP サーバーから電子メールを送信する権限を保持しているアカウントの名前を入力します。  
  
5.  **[適用]** をクリックします。  
  

  
##  <a name="bkmk_confiugre_remote_SMTP"></a>リモート SMTP サービスをレポートサーバー用に構成するには  
  
1.  レポート サーバー Windows サービスが SMTP サーバー上で `Send As` 権限を保持していることを確認します。  
  
2.  テキスト エディターで RSReportServer.config ファイルを開きます。  
  
3.  <`UrlRoot`> がレポート サーバーの URL アドレスに設定されていることを確認します。 この値はレポート サーバーを構成するときに設定されるため、既に設定されているはずです。 設定されていない場合は、レポート サーバーの URL アドレスを入力します。  
  
4.  Delivery セクションで、<`ReportServerEmail`> を検索します。  
  
5.  <`SMTPServer`> で、SMTP サーバーの名前を入力します。 この値は、IP アドレス、企業イントラネット上のコンピューターの UNC 名、または完全修飾ドメイン名にすることができます。  
  
6.  <`SendUsing`> が 2 に設定されていることを確認します。 別の値に設定されている場合、レポート サーバーはリモート SMTP サービスを使用するように構成されていません。  
  
7.  <`From`> で、SMTP サーバーから電子メールを送信する権限を保持しているアカウントの名前を入力します。  
  
8.  ファイルを保存します。  
  
     レポート サーバーは新しい設定を自動的に使用します。サービスを再起動する必要はありません。 追加の SMTP 設定を指定し、レポート サーバー電子メール配信で SMTP サーバーを使用する方法をさらに細かく構成することもできます。 詳しくは、「 [ssNoVersion](../../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md) 」および「 [ssNoVersion](../../reporting-services/report-server/rsreportserver-config-configuration-file.md) オンライン ブックの「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Onlオンライン ブックの「e.  
  

  
##  <a name="bkmk_confiugre_local_SMTP"></a>レポートサーバーのローカル SMTP サービスを構成するには  
  
1.  コントロール パネルを開き、 **[プログラムの追加と削除]** をクリックします。  
  
2.  **[Windows コンポーネントの追加と削除]** をクリックして、Windows コンポーネント ウィザードを開始します。  
  
3.  **[アプリケーション サーバー]** を選択し、 **[詳細]** をクリックします。  
  
4.  **[インターネット インフォメーション サービス (IIS)]** を選択し、 **[詳細]** をクリックします。  
  
5.  **[SMTP サービス]** チェック ボックスをオンにして、 **[OK]** をクリックします。  
  
6.  Windows コンポーネント ウィザードの **[次へ]** をクリックし、 **[完了]** をクリックします。  
  
7.  **[サービス]** コンソールでサービスが実行されていることを確認します。  
  
8.  テキスト エディターで **RSReportServer.config** ファイルを開きます。  
  
9. `<UrlRoot>` がレポート サーバーの URL アドレスに設定されていることを確認します。 この値はレポート サーバーを構成するときに設定されるため、既に設定されているはずです。 設定されていない場合は、レポート サーバーの URL アドレスを入力します。  
  
10. Delivery セクションで、`<ReportServerEmail>.` を検索します。  
  
11. `<SMTPServer>`内で、この設定の値をすべて消去します。タグは削除しないでください。  
  
12. `<SendUsing>` を 1 に設定します。 1 以外の値に設定されている場合、レポート サーバーはローカル SMTP サービスを使用するように構成されていません。  
  
13. `<SMTPServerPickupDirectory>` に、ローカル ドライブ上のフォルダーを設定します。  
  
14. `<From>` に、SMTP サーバーから電子メールを送信する権限を保持しているアカウントを設定します。  
  
15. ファイルを保存します。  
  
 
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
