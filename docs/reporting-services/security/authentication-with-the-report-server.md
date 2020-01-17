---
title: レポート サーバーでの認証 | Microsoft Docs
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], configuring
- connections [Reporting Services], accounts
- Windows authentication [Reporting Services]
- authentication [Reporting Services]
- Forms authentication
ms.assetid: 753c2542-0e97-4d8f-a5dd-4b07a5cd10ab
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d3246b38461c1445f3335f42944480732ab583a0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65570895"
---
# <a name="authentication-with-the-report-server"></a>レポート サーバーでの認証

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) には、レポート サーバーに対してユーザーおよびクライアント アプリケーションを認証するための構成可能なオプションがいくつか用意されています。 既定では、レポート サーバーは Windows 統合認証を使用し、クライアントとネットワーク リソースが同じドメインまたは信頼されているドメインに属している場合は、信頼関係があると見なされます。 ネットワーク トポロジおよび組織のニーズに応じて、Windows 統合認証に使用される認証プロトコルをカスタマイズしたり、基本認証を使用したり、自分で提供したカスタムのフォームベースの認証拡張機能を使用したりすることができます。 認証の種類ごとに、個別にオンとオフを切り替えることができます。 レポート サーバーで複数の種類の要求を受け入れる場合は、複数の種類の認証を有効にすることができます。
  
 レポート サーバーのコンテンツまたは操作へのアクセスを要求するすべてのユーザーとアプリケーションは、事前に認証を受けないとアクセスを許可されません。  
  
## <a name="authentication-types"></a>認証の種類  
 レポート サーバーのコンテンツまたは操作へのアクセスを要求するすべてのユーザーとアプリケーションは、レポート サーバーで構成されている認証の種類を使用して事前に認証を受けないとアクセスを許可されません。 次の表では、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]でサポートされている認証の種類について説明します。  
  
|認証の種類の名前|HTTP 認証レイヤーの値|既定で使用|[説明]|  
|-----------------------------|-------------------------------------|---------------------|-----------------|  
|RSWindowsNegotiate|ネゴシエート|はい|Windows 統合認証に対して Kerberos が最初に試行されますが、レポート サーバーへのクライアント要求に対して Active Directory でチケットを付与できない場合は NTLM に戻ります。 ネゴシエートは、チケットが使用できない場合にのみ NTLM に戻ります。 チケットがないのではなく、最初の試行でエラーになった場合は、レポート サーバーで 2 回目の試行は行われません。|  
|RSWindowsNTLM|NTLM|はい|Windows 統合認証に NTLM を使用します。<br /><br /> 資格情報は、他の要求で委任または権限借用されません。 後続の要求は、新しい要求/応答シーケンスに従います。 ネットワークのセキュリティ設定によっては、ユーザーは資格情報または認証要求を透過的に処理するように要求される場合があります。|  
|RSWindowsKerberos|Kerberos|いいえ|Windows 統合認証に Kerberos を使用します。 サービス アカウントのセットアップ サービス プリンシパル名 (SPN) を設定して、Kerberos を構成する必要があります。そのためには、ドメイン管理者権限が必要です。 Kerberos での ID 委任を設定した場合は、レポートを要求したユーザーのトークンを使用して、レポート データを提供する別の外部データ ソースに接続することもできます。<br /><br /> RSWindowsKerberos を指定する前に、使用しているブラウザーの種類で実際にサポートされていることを確認してください。 Microsoft Edge、または Internet Explorer を使用している場合、Kerberos 認証はネゴシエートを通してのみサポートされます。 Microsoft Edge、または Internet Explorer では、Kerberos を直接指定する認証要求は作成されません。|  
|RSWindowsBasic|Basic|いいえ|基本認証は、HTTP プロトコルで定義され、レポート サーバーへの HTTP 要求の認証にのみ使用できます。<br /><br /> HTTP 要求で資格情報が base64 エンコードとして渡されます。 基本認証を使用した場合、ユーザー アカウント情報をネットワークで送信する前に Secure Sockets Layer (SSL) で暗号化できます。 SSL は、クライアントからレポート サーバーに接続要求を送信するための暗号化されたチャネルを HTTP TCP/IP 接続で提供します。 詳細については、 [TechNet Web サイトの「](https://go.microsoft.com/fwlink/?LinkId=71123) SSL を使用して資格情報データを暗号化する [!INCLUDE[msCoName](../../includes/msconame-md.md)] 」を参照してください。|  
|Custom|(Anonymous)|いいえ|匿名認証は、HTTP 要求の認証ヘッダーを無視するようにレポート サーバーに指示します。 レポート サーバーですべての要求が受け入れられますが、ユーザーを認証する場合は、カスタムの [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] フォーム認証を指定する必要があります。<br /><br /> **Custom** は、レポート サーバーにすべての認証要求を処理するカスタム認証モジュールを配置している場合にのみ指定します。 カスタム認証は、既定の Windows 認証拡張機能と共に使用することはできません。|  
  
## <a name="unsupported-authentication-methods"></a>サポートされない認証方法  
 以下の認証方法および要求はサポートされていません。  
  
|認証方法|説明|  
|---------------------------|-----------------|  
|匿名|レポート サーバーでは、配置にカスタム認証拡張機能が含まれている場合以外は、匿名ユーザーからの認証されていない要求は受け入れません。<br /><br /> 基本認証用に構成されたレポート サーバーでレポート ビルダーへのアクセスを有効にした場合、レポート ビルダーは認証されていない要求を受け入れます。<br /><br /> それ以外の場合、匿名の要求は [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]に到達する前に拒否され、HTTP ステータス 401 アクセス拒否エラーが発生します。 401 アクセス拒否を受信したクライアントは、有効な認証の種類を使用して要求を作成し直す必要があります。|  
|シングル サインオン テクノロジ (SSO)|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]には、シングル サインオン テクノロジに対するネイティブ サポートはありません。 シングル サインオン テクノロジを使用する場合は、カスタム認証拡張機能を作成する必要があります。<br /><br /> レポート サーバー ホスティング環境では、ISAPI フィルターはサポートされません。 使用している SSO テクノロジが ISAPI フィルターとして実装されている場合、RSASecueID または RADIUS プロトコルの ISA Server 組み込みサポートの使用を検討してください。 それ以外の場合は、RS 用に ISA Server ISAPI または HTTPModule を作成できますが、直接 ISA Server を使用することをお勧めします。|  
|Passport|SQL Server Reporting Services ではサポートされていません。|  
|ダイジェスト|SQL Server Reporting Services ではサポートされていません。|  
  
## <a name="configuration-of-authentication-settings"></a>認証設定の構成  
 認証設定は、レポート サーバーの URL が予約されたときに、既定のセキュリティを使用するように構成されます。 これらの設定を誤って変更すると、レポート サーバーは、認証できない HTTP 要求に対して HTTP 401 アクセス拒否エラーを返します。 認証の種類を選択する際は、ネットワークで Windows 認証がどのようにサポートされているかを理解している必要があります。 少なくとも 1 種類の認証を指定する必要があります。 RSWindows に対しては、複数の種類の認証を指定できます。 RSWindows 認証の種類 ( **RSWindowsBasic**、 **RSWindowsNTLM**、 **RSWindowsKerberos**、および **RSWindowsNegotiate**) は、カスタムと同時に指定することはできません。  
  
> [!IMPORTANT]  
>  Reporting Services では、指定した設定がコンピューティング環境に対して適切かどうかは検証されません。 インストールの状況によっては既定のセキュリティが機能しない場合や、指定した構成設定がセキュリティ インフラストラクチャに対して有効ではない場合があります。 そのため、レポート サーバーを配置する際は、大規模な組織で使用できるようにする前に、管理されたテスト環境で十分にテストすることが重要です。  
  
 レポート サーバー Web サービスと [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] は、常に同じ種類の認証を使用します。 レポート サーバー サービスの機能領域に別の種類の認証を構成することはできません。 スケールアウト配置の場合は、すべての変更を配置内の全ノードに同じように適用する必要があります。 同じスケールアウト内でノードごとに異なる種類の認証を使用するように構成することはできません。  
  
 バックグラウンド処理は、エンド ユーザーからの要求は受け入れませんが、自動実行用のすべての要求を認証します。 バックグラウンド処理では常に Windows 認証が使用され、レポート サーバー サービスを使用する要求、または自動実行アカウント (構成されている場合) が認証されます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [レポート サーバーで Windows 認証を構成する](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
  
-   [レポート サーバーで基本認証を構成する](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)  
  
-   [レポート サーバーでカスタム認証またはフォーム認証を構成する](../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスクの説明|リンク|  
|-----------------------|-----------|  
|Windows 統合認証の種類を構成します。|[レポート サーバーで Windows 認証を構成する](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)|  
|基本認証の種類を構成します。|[レポート サーバーで基本認証を構成する](../../reporting-services/security/configure-basic-authentication-on-the-report-server.md)|  
|フォーム認証、またはカスタム認証の種類を構成します。|[レポート サーバーでカスタム認証またはフォーム認証を構成する](../../reporting-services/security/configure-custom-or-forms-authentication-on-the-report-server.md)|  
|[!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] がカスタム認証のシナリオを処理できるようにします。|[カスタム認証クッキーを送信するように Web ポータルを構成する](configure-the-web-portal-to-pass-custom-authentication-cookies.md)|  

## <a name="next-steps"></a>次の手順

[ネイティブ モードのレポート サーバーに対する権限の許可](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
[RsReportServer.config 構成ファイル](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
[ロールの割り当てを作成および管理する](../../reporting-services/security/create-and-manage-role-assignments.md)   
[レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
[セキュリティ拡張機能の実装](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)   
[ネイティブ モードのレポート サーバーでの SSL 接続の構成](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)   
[セキュリティ拡張機能の概要](../../reporting-services/extensions/security-extension/security-extensions-overview.md)   
[Reporting Services での認証](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md)   
[Reporting Services での承認](../../reporting-services/extensions/security-extension/authorization-in-reporting-services.md)  

その他の質問 [Reporting Services のフォーラムに質問してみてください](https://go.microsoft.com/fwlink/?LinkId=620231)
