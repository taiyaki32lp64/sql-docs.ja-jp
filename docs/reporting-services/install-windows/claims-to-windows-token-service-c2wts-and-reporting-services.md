---
title: Claims to Windows Token Service (C2WTS) と Reporting Services | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.date: 09/15/2017
ms.openlocfilehash: 2ed9c2a5070a1034970f2f34f5e7bf88a77e8533
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264998"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Claims to Windows Token Service (C2WTS) と Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

[SQL Server Reporting Services レポート ビューアー Web パーツ](../report-server-sharepoint/deploy-report-viewer-web-part.md)内でネイティブ モード レポートを表示するには、SharePoint Claims to Windows Token Service (C2WTS) が必要です。

SQL Server Reporting Services SharePoint モードで SharePoint ファームの外部にあるデータ ソースに対して Windows 認証を使用する場合にも、C2WTS が必要です。 C2WTS は、データ ソースが共有サービスと同じコンピューター上にある場合でも必要です。 ただし、このシナリオでは、制約付き委任は必要ありません。

> [!NOTE]
> SharePoint と Reporting Services の統合は、SQL Server 2016 以降では使用できません。

## <a name="report-viewer-native-mode-web-part-configuration"></a>レポート ビューアー (ネイティブ モード) Web パーツの構成

レポート ビューアー Web パーツを使用すると、SharePoint サイト内に SQL Server Reporting Services ネイティブ モード レポートを埋め込むことができます。 この Web パーツは、SharePoint 2013 と SharePoint 2016 に使用できます。 SharePoint 2013 と SharePoint 2016 のどちらも、要求認証を利用します。 結果として、C2WTS を適切に構成する必要があり、レポートを正しく表示するには Reporting Services を Kerberos 認証用に構成する必要があります。

1. RSWindowsNegotiate 認証タイプを使用するために SSRS サービス アカウントを決定し、SPN を設定し、rsreportserver.config ファイルを更新して、Kerberos 認証用の Reporting Services (ネイティブ モード) インスタンスを構成します。 [レポート サーバーのサービス プリンシパル名 (SPN) の登録](https://docs.microsoft.com/sql/reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server)

2. [C2WTS の構成に必要な手順](https://docs.microsoft.com/sql/reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services?view=sql-server-2017#steps-needed-to-configure-c2wts)に従います
 

## <a name="sharepoint-mode-integration"></a>SharePoint モードの統合

**このセクションは、SQL Server 2016 Reporting Services 以前にのみ適用されます。**

SharePoint ファームの外部にあるデータ ソースに対して Windows 認証を使用する場合、SQL Server Reporting Services SharePoint モードでは SharePoint Claims to Windows Token Service (C2WTS) が必要です。 これは、Web フロントエンド (WFE) と Reporting Services 共有サービス間の通信が常に要求認証になるため、ユーザーが Windows 認証を使用してデータ ソースにアクセスする場合にも当てはまります。

## <a name="steps-needed-to-configure-c2wts"></a>C2WTS の構成に必要な手順

C2WTS によって作成されたトークンは、制約付き委任 (特定のサービスへの制約) と "認証プロトコルの使用" (プロトコル遷移) 構成オプションでのみ機能します。

Kerberos の制約付き委任を使用する環境では、SharePoint Server サービスと外部データ ソースが同じ Windows ドメインに属している必要があります。 Claims to Windows Token Service (c2WTS) に依存する任意のサービスでは、Kerberos の **制約付き** 委任を使用して、c2WTS が Kerberos プロトコル遷移を使用して要求を Windows 資格情報に変換できるようにする必要があります。 これらの要件は、すべての SharePoint 共有サービスに共通です。 詳細については、「 [SharePoint 2013 で Kerberos 認証を計画する](https://technet.microsoft.com/library/ee806870.aspx)」を参照してください。  

1. C2WTS サービス ドメイン アカウントを構成します。 

    **ベスト プラクティスとしては、C2WTS を独自のドメイン ID で実行する必要があります。**

    * Active Directory アカウントを作成し、SharePoint サーバーの管理アカウントとしてアカウントを登録します。 マネージド アカウントの詳細については、[SharePoint のマネージド アカウント](https://blog.wbaer.net/2010/04/11/managed-accounts-in-sharepoint-2010/)に関する記事を参照してください
   
    * [SharePoint サーバーの全体管理] > [セキュリティ] > [サービス アカウントの構成] > [Windows サービス - Claims to Windows Token Service] から、マネージド アカウントを使用するための C2WTS サービスを構成します

    C2WTS を使用する各サーバーのローカルの Administrators グループに C2WTS サービス アカウントを追加します。 **レポート ビューアー Web パーツ**の場合は Web Front End (WFE) サーバーです。 **SharePoint 統合モード**の場合は、Reporting Services サービスが実行されているアプリケーション サーバーです。
    * [ローカル ポリシー] > [ユーザー権利の割り当て] のローカル セキュリティ ポリシーで、C2WTS アカウントに次のアクセス許可を付与します。
        * オペレーティング システムの一部として機能
        * 認証後にクライアントを借用する
        * サービスとしてログオン

    
2. C2WTS サービス アカウントの委任を構成します。

    アカウントには、プロトコル遷移を使用した制限付き委任に加え、通信に必要なサービス (SQL Server Database Engine、SQL Server Analysis Services など) に委任するアクセス許可も必要です。 委任を構成するには、Active Directory ユーザーとコンピューターのスナップインを使用できます。また、ドメイン管理者である必要があります。

    > [!IMPORTANT]
    > C2WTS サービス アカウントにどのような設定を構成するとしても、[委任] タブで、使用されているメイン サービス アカウントと同じにする必要があります。 **レポート ビューアー Web パーツ**の場合は、SharePoint Web アプリケーションのサービス アカウントです。 **SharePoint 統合モード**の場合は、Reporting Services サービス アカウントです。
    >
    > たとえば、C2WTS サービス アカウントを SQL Service に委任できるようにした場合、SharePoint 統合モードの Reporting Services サービス アカウントでも同様にする必要があります。

    * 各サービス アカウントを右クリックして、プロパティ ダイアログを開きます。 ダイアログで **[委任]** タブをクリックします。

        委任タブは、オブジェクトにサービス プリンシパル名 (SPN) が割り当てられている場合にのみ表示されます。 C2WTS では、C2WTS アカウントに SPN は必要ありませんが、SPN がない場合は、 **[委任]** タブは表示されません。 制約付き委任を構成する別の方法として、 **ADSIEdit**などのユーティリティを使用するという方法もあります。

    * 委任タブで重要な構成オプションは、次のとおりです。

        * **[指定されたサービスへの委任でのみこのユーザーを信頼する]** を選択する
        * **[任意の認証プロトコルを使う]** を選択する

    * **[追加]** を選択して、委任するサービスを追加します。

    * **[ユーザーまたはコンピューター...&#42;]** を選択し、サービスをホストするアカウントを入力します。 たとえば、SQL Server が *sqlservice* というアカウントで実行されている場合は、`sqlservice` と入力します。 
      **レポート ビューアー Web パーツ**の場合は、Reporting Services (ネイティブ モード) インスタンスのサービス アカウントです。

    * サービス一覧を選択します。 そのアカウントで使用できる SPN が表示されます。 そのアカウントのサービス一覧が表示されない場合は、サービスがないか、別のアカウントのサービスの可能性があります。 SPN の調整には、SetSPN ユーティリティを使用できます。 **レポート ビューアー Web パーツ**の場合は、「[レポート ビューアー Web パーツの構成](https://docs.microsoft.com/sql/reporting-services/install-windows/claims-to-windows-token-service-c2wts-and-reporting-services?view=sql-server-2017#report-viewer-native-mode-web-part-configuration)」で構成した http SPN が表示されます。

    * [OK] を選択してダイアログを閉じます。

3. C2WTS *AllowedCallers* を構成します。

    C2WTS では、"呼び出し元" の ID が構成ファイル **C2WTShost.exe.config** で明示されている必要があります。C2WTS は、そのように構成されていない限り、システム内のすべての認証ユーザーからの要求を受け入れません。 この場合、"呼び出し元" は WSS_WPG Windows グループです。 C2WTShost.exe.confi ファイルは次の場所に保存されます。

    C2WTS サービスについて、SharePoint サーバーの全体管理内でサービス アカウントを変更すると、そのアカウントが WSS_WPG グループに追加されます。

    **\Program Files\Windows Identity Foundation\v3.5\c2WTShost.exe.config**

    構成ファイルの例を次に示します。

    ```
    <configuration>
      <windowsTokenService>
        <!--  
            By default no callers are allowed to use the Windows Identity Foundation Claims To NT Token Service.  
            Add the identities you wish to allow below.  
          -->
        <allowedCallers>
          <clear/>
          <add value="WSS_WPG" />
        </allowedCallers>
      </windowsTokenService>
    </configuration>
    ```

4. **[サーバーのサービスの管理]** ページの [SharePoint サーバーの全体管理] から Claims to Windows Token Service を起動します (既に開始している場合は停止して起動します)。 このサービスは、アクションを実行するサーバーで起動する必要があります。 たとえば、WFE サーバーと SQL Server Reporting Services 共有サービスを実行しているアプリケーション サーバーを持っている場合は、アプリケーション サーバーで C2WTS を起動するだけでかまいません。 レポート ビューアー Web パーツを実行している場合、C2WTS は WFE サーバー上でのみ必要です。

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
