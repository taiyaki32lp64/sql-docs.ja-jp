---
title: 電子メールの設定 - Reporting Services のネイティブ モード (Configuration Manager) | Microsoft Docs
ms.date: 06/01/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
f1_keywords:
- SQL13.rsconfigtool.emailsettings.F1
helpviewer_keywords:
- SQL11.rsconfigtool.emailsettings.F1
ms.assetid: cdad1529-bfa6-41fb-9863-d9ff1b802577
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 872c7e4d501017627fcc64eca7ed48204c9d3533
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73593816"
---
# <a name="e-mail-settings---reporting-services-native-mode-configuration-manager"></a>電子メールの設定 - Reporting Services のネイティブ モード (構成マネージャー)
Reporting Services にはメール配信拡張機能があり、メールを使用してレポートを配布できます。 電子メール サブスクリプションをどのように定義するかに応じて、配信は、通知、リンク、添付ファイル、または埋め込みレポートから構成されます。 電子メール配信拡張機能は、既存のメール サーバー テクノロジと連携して動作します。 メール サーバーは、SMTP サーバーまたはフォワーダーである必要があります。 レポート サーバーは、オペレーティング システムに用意されている Collaboration Data Objects (CDO) ライブラリ (cdosys.dll) を通じて SMTP サーバーに接続します。

既定では、レポート サーバーの電子メール配信拡張機能は構成されていません。 Reporting Services 構成マネージャーを使用して、この拡張機能の最低限の構成を行う必要があります。 詳細なプロパティを設定するには、RSReportServer.config ファイルを編集します。 この拡張機能を使用するようにレポート サーバーを構成できない場合は、代わりに共有フォルダーにレポートを配信できます。 詳細については、「Reporting Services でのファイル共有の配信」をご覧ください。

## <a name="configuration-requirements"></a>構成要件

- レポート サーバーの電子メール配信は Collaboration Data Objects (CDO) に実装されており、ローカルまたはリモートの簡易メール転送プロトコル (SMTP) サーバーまたは SMTP フォワーダーを必要とします。 SMTP は、一部の Windows オペレーティング システムではサポートされていません。 Itanium ベース エディションの Windows Server 2008 を使用している場合、SMTP はサポートされません。 CDO によって提供される構成オプションの詳細については、MSDN の「 [CoClass の構成](https://go.microsoft.com/fwlink/?LinkId=98237) 」を参照してください。

構成された認証アカウントには、メールを送信する SMTP サーバーに対するアクセス許可が必要です。

- 電子メール配信拡張機能では、電子メール添付ファイルに UTF-8 エンコードが使用されます。 エンコードを変更することはできません。HTML 表示拡張機能では UTF-8 だけがサポートされます。

> [!NOTE] 
> 既定の電子メール配信拡張機能では、送信するメール メッセージのデジタル署名および暗号化はサポートされていません。

## <a name="setting-configuration-options-for-e-mail-delivery"></a>電子メール配信用の構成オプションの設定
レポート サーバーの電子メール配信を使用するには、先に、使用する SMTP サーバーに関する情報を提供する構成値を設定する必要があります。

電子メール配信用にレポート サーバーを構成するには、次の操作を行います。

- SMTP サーバーと、電子メールを送信する権限のあるユーザー アカウントを指定するだけの場合は、Reporting Services 構成マネージャーを使用します。 これらは、レポート サーバーの電子メール配信拡張機能を構成するために最低限必要な設定です。

- (省略可能) テキスト エディターを使用して、RSreportserver.config ファイルで追加の設定を指定します。 このファイルには、レポート サーバーの電子メール配信の構成設定がすべて含まれています。 ローカル SMTP サーバーを使用する場合や、電子メールの配信を特定のホストに限定する場合は、これらのファイルで追加の設定を指定する必要があります。 構成ファイルの検索と変更の詳細については、「[Reporting Services の構成ファイル (RSreportserver.config) の変更](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)」を参照してください。

> [!NOTE] 
> レポート サーバーの電子メール設定は CDO に基づいています。 特定の設定に関する詳細については、CDO の製品マニュアルを参照してください。

## <a name="a-namersconfigmanconfigure-report-server-e-mail-using-the-reporting-services-configuration-manager"></a><a name="rsconfigman"/>Reporting Services 構成マネージャーを使用してレポート サーバーのメールを構成する

1. Reporting Services 構成マネージャーを起動して、レポート サーバー インスタンスに接続します。

2. **[送信者アドレス]** に、生成されるメールの **[送信者]** フィールドに使用するメール アドレスを入力します。 

     SMTP サーバーからメールを送信する権限のあるユーザー アカウントを指定する必要があります。 **[送信者アドレス]** に入力した値は、rsreportserver.config ファイルの `<From>` フィールドに保存されます。  

3.  **SMTP Server**で、使用する SMTP サーバーまたはゲートウェイを指定します。 

     この値は、IP アドレス、企業イントラネット上のコンピューターの NetBIOS 名、または完全修飾ドメイン名にすることができます。 **SMTP Server** に入力した値は、rsreportserver.config ファイルの `<SMTPServer>` フィールドに保存されます。

4. **[認証]** ドロップダウンを使用して、SMTP サーバーの認証方法を指定します。 This 

     - **[認証なし]** は、指定されたメール サーバーに匿名で接続することを意味します。
     
          このオプションを選ぶと、rsreportserver.config で `<SendUsing>` の値が **2** に、 `<SMTPAuthenticate>` の値が **0** に設定されます。
     
     - **[ユーザー名とパスワード (基本)]** では、メール サーバーに接続するためのユーザー名とパスワードを指定できます。 **[セキュリティで保護された接続を使用]** を選んで、暗号化された接続でメール サーバーに接続することもできます。
     
          このオプションを選ぶと、rsreportserver.config で `<SendUsing>` の値が **2** に、 `<SMTPAuthenticate>` の値が **1** に設定されます。 **[セキュリティで保護された接続を使用]** を選ぶと、`SMTPUseSSL` が **True** に設定されます。 **[ユーザー名]** は暗号化された値として `<SendUserName>` に設定されます。 **[パスワード]** は暗号化された値として `<SendPassword>` に設定されます。
     
     - **[レポート サーバー サービス アカウント (NTLM)]** では、レポート サーバー用に指定したサービス アカウントが使用されます。 認証用にレポート サーバー サービス アカウントを使用する場合は、そのサービス アカウントに SMTP サーバー上での **Send As** アクセス許可があることを確認します。
     
          このオプションを選ぶと、rsreportserver.config で `<SendUsing>` の値が **2** に、 `<SMTPAuthenticate>` の値が **2** に設定されます。

5. **[適用]** を選択します。

6. 必要に応じて、rsreportserver.config 内でメール構成用に追加フィールドを調整することもできます。

## <a name="example-report-server-e-mail-configuration"></a>レポート サーバーの電子メール構成の例
次の例は、リモート SMTP サーバーに対する RSreportserver.config ファイルでの設定を示しています。 設定に関する説明と有効な値を読み取るには、「[Rsreportserver.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)」を参照してください。

```
<RSEmailDPConfiguration>
     <SMTPServer>mySMTPServer.Adventure-Works.com</SMTPServer>
     <SMTPServerPort></SMTPServerPort>
     <SMTPAccountName></SMTPAccountName>
     <SMTPConnectionTimeout></SMTPConnectionTimeout>
     <SMTPServerPickupDirectory></SMTPServerPickupDirectory>
     <SMTPUseSSL>False</SMTPUseSSL>
     <SendUsing>2</SendUsing>
     <SMTPAuthenticate>2</SMTPAuthenticate>
     <From>my-rs-email-account@Adventure-Works.com</From>
     <EmbeddedRenderFormats>
          <RenderingExtension>MHTML</RenderingExtension>
     </EmbeddedRenderFormats>
     <PrivilegedUserRenderFormats></PrivilegedUserRenderFormats>
     <ExcludedRenderFormats>
          <RenderingExtension>HTMLOWC</RenderingExtension>
          <RenderingExtension>NULL</RenderingExtension>
          <RenderingExtension>RGDI</RenderingExtension>
     </ExcludedRenderFormats>
     <SendEmailToUserAlias>True</SendEmailToUserAlias>
     <DefaultHostName></DefaultHostName>
     <PermittedHosts>
          <HostName>Adventure-Works.com</HostName>
          <HostName>hotmail.com</HostName>
     </PermittedHosts>
     <SendUserName></SendUserName>
     <SendPassword></SendPassword>
</RSEmailDPConfiguration>
```
## <a name="configuration-options-for-setting-the-to-field-in-a-message"></a>メッセージの [宛先] フィールドを設定するための構成オプション
"個別のサブスクリプションを管理" タスクで与えられるアクセス許可に従って作成されたユーザー定義サブスクリプションには、ドメイン ユーザー アカウントに基づく設定済みのユーザー名が含まれます。 ユーザーがサブスクリプションを作成すると、 **[宛先]** フィールドの受信者名は、サブスクリプションの作成者のドメイン ユーザー アカウントを使用して自動的に指定されます。

使用している SMTP サーバーまたはフォワーダーで、ドメイン ユーザー アカウントとは別の電子メール アカウントを利用している場合、SMTP サーバーからそのユーザーにレポートの配信が試行されたときに配信が失敗します。

この問題に対処するには、ユーザーが **[宛先]** フィールドに名前を入力できるように構成設定を変更します。

1. テキスト エディターで RSReportServer.config を開きます。

2. `<SendEmailToUserAlias>` を **False**に設定します。

3. `<DefaultHostName>` を SMTP サーバーまたはフォワーダーのドメイン ネーム システム (DNS) 名または IP アドレスに設定します。

4. ファイルを保存します。

## <a name="configuration-options-for-remote-smtp-service"></a>リモート SMTP サービスの構成オプション
レポート サーバーと SMTP サーバーまたはフォワーダーの間の接続は、次の構成設定によって決まります。

- `<SendUsing>` メッセージを送信する方法を指定します。 ネットワーク SMTP サービスまたはローカル SMTP サービスのピックアップ ディレクトリを選択できます。 リモート SMTP サービスを使用するには、RSReportServer.config ファイルでこの値を **2** に設定する必要があります。
- `<SMTPServer>` リモート SMTP サーバーまたはフォワーダーを指定します。 リモート SMTP サーバーまたはフォワーダーを使用している場合には、この値は必須です。
- `<From>` メール メッセージの **[送信者]** 行に使用する値を設定します。 リモート SMTP サーバーまたはフォワーダーを使用している場合には、この値は必須です。

リモート SMTP サービスで使用する他の値としては、次のものがあります (既定値を変更するのでない限り、これらの値をオーバーライドする必要はありません)。

- `<SMTPServerPort>` 既定ではポート 25 に構成されます。
- `<SMTPAuthenticate>` レポート サーバーがリモート SMTP サーバーに接続する方法を指定します。 既定値は **0** (認証なし) です。 この場合、接続は匿名アクセスをとおして行われます。 ドメインの構成によっては、レポート サーバーと SMTP サーバーが同じドメインのメンバーであることが必要になる場合があります。
- 制限付きの配信リスト (たとえば、認証されたアカウントからの着信メッセージだけを受け付ける配信リスト) にメールを送信するには、 `<SMTPAuthenticate>` を **1** または **2**に設定します。 **1**に設定すると、 `<SendUserName>` と `<SendPassword>`も設定する必要があります。 Reporting Services 構成マネージャーからこれを行うことをお勧めします。そうすることにより、 `<SendUserName>` と `<SendPassword>`の値が暗号化されるためです。

### <a name="to-configure-a-remote-smtp-service-for-the-report-server"></a>リモート SMTP サービスをレポート サーバー用に構成するには

> [!NOTE] 
> メール サーバーは Reporting Services 構成マネージャーで構成することをお勧めします。

1. レポート サーバー Windows サービスが SMTP サーバー上で **Send As** 権限を保持していることを確認します。

2. テキスト エディターで RSReportServer.config ファイルを開きます。

3. `<UrlRoot>` がレポート サーバーの URL アドレスに設定されていることを確認します。 この値はレポート サーバーを構成するときに設定されるため、既に設定されているはずです。 設定されていない場合は、レポート サーバーの URL アドレスを入力します。

4. Delivery セクションで、 `<RSEmailDPConfiguration>`を検索します。
     
5. `<SMTPServer>`で、SMTP サーバーの名前を入力します。 この値は、IP アドレス、企業イントラネット上のコンピューターの UNC 名、または完全修飾ドメイン名にすることができます。

6. レポート サーバーのサービス アカウントを使用するには、 `<SendUsing>` の値を **2** に設定します。 基本認証の場合は、 `<SendUsing>` の値を **1** に設定します。 **1**に設定すると、さらに `<SendUserName>` と `<SendPassword>`の値を指定する必要があります。 これらの値を暗号化する場合は、Reporting Services 構成マネージャー内で認証を設定します。

7. `<SMTPAuthenticate>` を 1 または 2 に設定する場合は、 **の値を** 1 `<SendUsing>` に設定します。

7. `<From>` を設定します。 SMTP サーバーからメールを送信する権限のあるユーザー アカウントを指定する必要があります。

8. ファイルを保存します。

     レポート サーバーは新しい設定を自動的に使用します。サービスを再起動する必要はありません。 追加の SMTP 設定を指定し、レポート サーバー電子メール配信で SMTP サーバーを使用する方法をさらに細かく構成することもできます。

## <a name="configuration-options-for-local-smtp-service"></a>ローカル SMTP サービスの構成オプション
レポート サーバー電子メール配信のテストまたはトラブルシューティングを行う場合は、ローカル SMTP サービスの構成が役に立ちます。 既定ではローカル SMTP サービスは無効になっています。

レポート サーバーとローカル SMTP サーバーまたはフォワーダーの間の接続は、次の構成設定によって決まります。

- **SendUsing** は **1**に設定します。
- **SMTPServerPickupDirectory** には、ローカル ドライブのフォルダーを設定します。

  > [!NOTE] 
  > ローカル SMTP サーバーを使用する場合は、SMTPServer を設定しないでください。

- **From** には、メール メッセージの **[送信者]** 行に使用する値を設定します。 この値は必須です。

### <a name="to-configure-a-local-smtp-service-for-the-report-server"></a>ローカル SMTP サービスをレポート サーバー用に構成するには

1. コントロール パネルで、 **[Windows の機能の有効化または無効化]** を選び、 **[役割と機能の追加ウィザード]** を開始します。

2. **[役割ベースまたは機能ベースのインストール]** 、 **[次へ]** の順に選びます。

3. インターネット インフォメーション サーバー (IIS) 上にインストールするサーバーを選んで、 **[次へ]** を選びます。

4. **[サーバーの役割]** ページで *[次へ]* を選びます。
     
5. *[機能]* ページで、 **[SMTP サーバー]** 、 **[次へ]** の順に選びます。

     SMTP サーバーに必要な機能を追加するよう求めるメッセージが表示されたら、 **[機能の追加]** を選びます。

6. **[Web サーバーの役割 (IIS)]** ページで、 *[次へ]* を選びます。

7. **[役割サービス]** ページで、 *[次へ]* を選びます。

8. **[確認]** ページで **[インストール]** を選びます。

9. **簡易メール転送プロトコル (SMTP)** の Windows サービスが実行されていることを [サービス] コンソールで確認します。

     ローカル SMTP サーバーを構成するには、管理ツールにある IIS 6.0 マネージャーを使用する必要があります。

10. テキスト エディターで RSReportServer.config ファイルを開きます。

11. `<UrlRoot>` がレポート サーバーの URL アドレスに設定されていることを確認します。 この値はレポート サーバーを構成するときに設定されるため、既に設定されているはずです。 設定されていない場合は、レポート サーバーの Web サービスの URL アドレスを入力します。

12. Delivery セクションで、 `<RSEmailDPConfiguration>`を検索します。
     
13. 空の `<SMTPServer>` が存在していることを確認します。
     
14. `<SendUsing>` を 1 に設定します。
     
14. `<SMTPAuthenticate>` を 0 に設定します。
     
15. `<SMTPServerPickupDirectory>` を SMTP サービスの Pickup フォルダーに設定します。
     
     既定の場所は、 *C:\inetpub\mailroot\Pickup*になります。
     
16. `<From>`を設定します。 これには、メール メッセージの **[送信者]** 行に使用する値を設定します。
     
17. ファイルを保存します。
  
## <a name="see-also"></a>参照  
[Reporting Services 構成マネージャー (ネイティブ モード)](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
[Modify a Reporting Services Configuration File (rsreportserver.config)](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
[Rsreportserver.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)
  
  
