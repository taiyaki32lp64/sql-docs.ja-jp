---
title: レポート サーバーで基本認証を構成する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, configuration
- Basic authentication
ms.assetid: 8faf2938-b71b-4e61-a172-46da2209ff55
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 32b46265b5da376bc974b55c48bf54bad88917d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102163"
---
# <a name="configure-basic-authentication-on-the-report-server"></a>レポート サーバーで基本認証を構成する
  Reporting Services は、既定では、ネゴシエート認証および NTLM 認証を指定する要求を受け入れます。 基本認証を使用するクライアント アプリケーションやブラウザーが配置に含まれる場合は、サポートされる種類の一覧に基本認証を追加する必要があります。 また、レポート ビルダーを使用する場合は、レポート ビルダーのファイルへの匿名アクセスを有効にする必要もあります。  
  
 レポート サーバーで基本認証を構成するには、RSReportServer.config ファイルの XML 要素と値を編集する必要があります。 既定値を置き換える際に、このトピックの例をコピーして貼り付けることもできます。  
  
 基本認証を有効にする前に、セキュリティ インフラストラクチャで基本認証がサポートされていることを確認します。 基本認証では、レポート サーバー Web サービスがローカル セキュリティ機関に資格情報を渡します。 資格情報でローカル ユーザー アカウントが指定されていた場合は、ユーザーはレポート サーバー コンピューター上のローカル セキュリティ機関によって認証されて、ローカル リソースに対して有効なセキュリティ トークンを受け取ります。 ドメイン ユーザー アカウントの資格情報は、ドメイン コントローラーに転送されて認証されます。 この場合は、認証が完了すると、ネットワーク リソースに対して有効なチケットが渡されます。  
  
 資格情報がネットワークのドメイン コントローラーに転送される間に傍受されるリスクを軽減するには、チャネルの暗号化 (Secure Sockets Layer (SSL) など) を使用する必要があります。 基本認証のみを使用した場合、ユーザー名はクリア テキストで転送され、パスワードは Base64 エンコード形式で転送されます。 チャネルの暗号化を追加すると、パケットが読み取り不可能になります。 詳細については、「 [ネイティブ モードのレポート サーバーでの SSL 接続の構成](configure-ssl-connections-on-a-native-mode-report-server.md)」を参照してください。  
  
 基本認証を有効にすると、レポートにデータを提供する外部データ ソースへの接続のプロパティをユーザーが設定するときに **[Windows 統合セキュリティ]** オプションを選択できなくなることに注意してください。 このオプションは、データ ソース プロパティ ページでグレー表示されます。  
  
> [!NOTE]  
>  次に示す手順は、ネイティブ モードのレポート サーバーを対象としています。 レポート サーバーを SharePoint 統合モードで配置する場合は、Windows 統合セキュリティを指定する既定の認証設定を使用する必要があります。 レポート サーバーでは、既定の Windows 認証拡張機能の内部機能を使用して、SharePoint 統合モードのレポート サーバーがサポートされます。  
  
### <a name="to-configure-a-report-server-to-use-basic-authentication"></a>レポート サーバーを構成して基本認証を使用するには  
  
1.  テキスト エディターで RSReportServer.config を開きます。  
  
     ファイルがある *\<ドライブ >:* \Program Files\Microsoft SQL Server\MSRS12 します。MSSQLSERVER\Reporting services \reportserver にあります。  
  
2.  検索 <`Authentication`>。  
  
3.  次に示す XML 構造の中でニーズに最も合うものをコピーします。 最初の XML 構造には、次のセクションで説明するすべての要素を指定するためのプレースホルダーが含まれています。  
  
    ```  
    <Authentication>  
          <AuthenticationTypes>  
                 <RSWindowsBasic>  
                       <LogonMethod>3</LogonMethod>  
                       <Realm></Realm>  
                       <DefaultDomain></DefaultDomain>  
                 </RSWindowsBasic>  
          </AuthenticationTypes>  
          <EnableAuthPersistence>true</EnableAuthPersistence>  
    </Authentication>  
    ```  
  
     既定値を使用する場合は、次に示す最小限の要素構造をコピーしてください。  
  
    ```  
          <AuthenticationTypes>  
                 <RSWindowsBasic/>  
          </AuthenticationTypes>  
    ```  
  
4.  既存のエントリを貼り付けます <`Authentication`>。  
  
     複数の認証の種類を使用する場合は、`RSWindowsBasic` 要素を追加するだけにして、`RSWindowsNegotiate`、`RSWindowsNTLM`、および `RSWindowsKerberos` の各エントリは削除しないでください。  
  
     Safari ブラウザーをサポートする場合は、複数の認証の種類を使用できるようにレポート サーバーを構成することはできません。 `RSWindowsBasic` のみを指定して、その他のエントリを削除する必要があります。  
  
     `Custom` は他の認証の種類と併用できないので注意してください。  
  
5.  空の値を置き換える <`Realm`> または <`DefaultDomain`> の環境で有効な値にします。  
  
6.  ファイルを保存します。  
  
7.  スケールアウト配置を構成した場合は、配置内の他のレポート サーバーに対して上記の手順を繰り返します。  
  
8.  レポート サーバーを再起動して、現在開いているセッションを消去します。  
  
## <a name="rswindowsbasic-reference"></a>RSWindowsBasic リファレンス  
 基本認証を構成するときには次の要素を指定できます。  
  
|要素|必須|有効な値|  
|-------------|--------------|------------------|  
|LogonMethod|はい<br /><br /> 値を指定しない場合は 3 が使用されます。|`2` = プレーン テキスト パスワードを認証する高パフォーマンス サーバー向けネットワーク ログオン。<br /><br /> `3` = クリア テキスト ログオン。各 HTTP 要求と一緒に送信される認証パッケージにログオン資格情報が保持されます。これにより、ネットワーク内の他のサーバーに接続する際に、サーバーがユーザーの権限を借用できます。 EnterprisePublishing<br /><br /> 注:値 0 (対話型ログオン) と値 1 (バッチ ログオン) は、[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] ではサポートされません。|  
|Realm|省略可|組織内の保護されたリソースへのアクセスを制御するための承認機能や認証機能を含んだリソース パーティションを指定します。|  
|DefaultDomain|省略可|サーバーがユーザーを認証する際のドメインを指定します。 この値はオプションです。ただし、省略した場合、レポート サーバーでは、コンピューター名がドメインとして使用されます。 コンピューターがドメインのメンバーになっている場合は、そのドメインが既定のドメインです。 レポート サーバーをドメイン コントローラーにインストールした場合、そのコンピューターによって制御されるドメインを指定します。|  
  
## <a name="enabling-anonymous-access-to-report-builder-application-files"></a>レポート ビルダー アプリケーション ファイルへの匿名アクセスの有効化  
 レポート ビルダーは、ClickOnce テクノロジを使用して、アプリケーション ファイルをクライアント コンピューターにダウンロードおよびインストールします。 クライアント コンピューターでレポート ビルダーを起動すると、ClickOnce アプリケーション ランチャーがレポート サーバー コンピューター上の追加のアプリケーション ファイルを要求します。 レポート サーバーが基本認証用に構成されている場合、ClickOnce アプリケーション ランチャーは基本認証をサポートしていないため、認証チェックが失敗します。  
  
 この問題を回避するには、レポート ビルダーのプログラム ファイルへの匿名アクセスを構成します。 これにより、ClickOnce がファイルを取得するときに認証チェックを省略できるようになります。 匿名アクセスを有効にするには、次の操作を行います。  
  
-   レポート サーバーが基本認証用に構成されていることを確認します。  
  
-   ReportBuilder フォルダーの下に bin フォルダーを作成し、そのフォルダーに 4 つのアセンブリをコピーします。  
  
-   RSReportServer.config に `IsReportBuilderAnonymousAccessEnabled` 要素を追加して、`True` に設定します。 ファイルを保存すると、レポート ビルダーへの新しいエンドポイントがレポート サーバーによって作成されます。 このエンドポイントは、プログラム ファイルにアクセスするために内部で使用されるものであり、コードで使用できるプログラマティック インターフェイスはありません。 別のエンドポイントを使用することにより、レポート サーバー サービス プロセス境界内の独自のアプリケーション ドメインでレポート ビルダーを実行することが可能になります。  
  
-   必要に応じて最小特権のアカウントを指定して、レポート サーバーとは別のセキュリティ コンテキストで要求を処理することもできます。 このアカウントは、レポート サーバー上のレポート ビルダー ファイルにアクセスするための匿名アカウントになります。 このアカウントによって ASP.NET ワーカー プロセスのスレッドの ID が設定され、 そのスレッドで実行される要求は認証チェックなしでレポート サーバーに渡されます。 このアカウントは、iusr _\<machine > アカウントでインターネット インフォメーション サービス (IIS)、ASP.NET のワーカーのセキュリティ コンテキストを設定するために使用する処理の匿名アクセスと権限借用が有効にするとします。 アカウントを指定するには、レポート ビルダーの Web.config ファイルにそのアカウントを追加します。  
  
 レポート ビルダーのプログラム ファイルへの匿名アクセスを有効にする場合は、レポート サーバーが基本認証用に構成されている必要があります。 レポート サーバーが基本認証用に構成されていない場合、匿名アクセスを有効にしようとするとエラーが発生します。  
  
 レポート ビルダーと認証の問題の詳細については、「[レポート ビルダーへのアクセスの構成](../report-server/configure-report-builder-access.md)」を参照してください。  
  
#### <a name="to-configure-report-builder-access-on-a-report-server-configured-for-basic-authentication"></a>基本認証用に構成されたレポート サーバーでレポート ビルダーへのアクセスを構成するには  
  
1.  RSReportServer.config ファイルの認証設定をチェックして、レポート サーバーが基本認証用に構成されていることを確認します。  
  
2.  ReportBuilder フォルダーの下に BIN フォルダーを作成します。 既定では、このフォルダーは \Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\ReportServer\ReportBuilder にあります。  
  
3.  ReportServer\Bin フォルダーから ReportBuilder\BIN フォルダーに次のアセンブリをコピーします。  
  
     Microsoft.ReportingServices.Diagnostics.dll  
  
     Microsoft.ReportingServices.Interfaces.dll  
  
     ReportingServicesAppDomainManager.dll  
  
     RSHttpRuntime.dll  
  
4.  必要に応じて、レポート ビルダーの要求を匿名アカウントで処理するための Web.config ファイルを作成します。  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
    <system.web>  
    <authentication mode="Windows" />    
    <identity impersonate="true " userName="username" password="password"/>  
    </system.web>  
    </configuration>  
    ```  
  
     Web.config ファイルを含める場合は、認証モードを `Windows` に設定する必要があります。  
  
     `Identity impersonate` には、`True` または `False` を指定できます。  
  
    -   ASP.NET がセキュリティ トークンを読み取らないようにする場合は、`False` に設定します。 この場合、要求はレポート サーバー サービスのセキュリティ コンテキストで実行されます。  
  
    -   ASP.NET がホスト層からセキュリティ トークンを読み取るようにする場合は、`True` に設定します。 `True` に設定した場合は、`userName` と `password` を指定して匿名アカウントを指定する必要もあります。 指定する資格情報により、要求が発行されるセキュリティ コンテキストが決まります。  
  
5.  Web.config ファイルを ReportBuilder\bin フォルダーに保存します。  
  
6.  RSReportServer.config ファイルを開き、Services セクションで `IsReportManagerEnabled` を見つけて、その下に次の設定を追加します。  
  
    ```  
    <IsReportBuilderAnonymousAccessEnabled>True</IsReportBuilderAnonymousAccessEnabled>  
    ```  
  
7.  RSReportServer.config ファイルを保存して閉じます。  
  
8.  レポート サーバーを再起動します。  
  
## <a name="see-also"></a>参照  
 [レポート サーバー アプリケーションのアプリケーション ドメイン](../report-server/application-domains-for-report-server-applications.md)   
 [Reporting Services のセキュリティと保護](reporting-services-security-and-protection.md)  
  
  
