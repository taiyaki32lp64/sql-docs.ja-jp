---
title: レポート サーバー サービス アカウントの構成 (SSRS 構成マネージャー) | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: ''
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/10/2018
ms.openlocfilehash: cb867bfdfc8d9ecb686d3ecc52c48c80bc60d9cd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63261067"
---
# <a name="configure-the-report-server-service-account-ssrs-configuration-manager"></a>レポート サーバー サービス アカウントの構成 (SSRS 構成マネージャー)

  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、レポート サーバー Web サービス、レポート マネージャー、およびスケジュールされたレポート処理とサブスクリプションの配信に使用されるバックグラウンド処理アプリケーションを含んだ単一のサービスとして実装されます。 このトピックでは、サービス アカウントを最初に構成する方法と、Reporting Services 構成ツールを使用してアカウントやパスワードを変更する方法について説明します。  
  
## <a name="initial-configuration"></a>初期構成

 レポート サーバー サービスのアカウントは、セットアップ時に定義されます。 このサービスは、ドメイン ユーザー アカウントまたは `NetworkService` などのビルトイン アカウントで実行できます。 既定のアカウントはありません。指定した任意のアカウント、[サーバーの構成 - サービス アカウント](../../sql-server/install/server-configuration-service-accounts.md)インストール ウィザードのページがレポート サーバー サービスの初期アカウントになります。  
  
> [!IMPORTANT]
> レポート サーバー Web サービスとレポート マネージャーは [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] アプリケーションですが、[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] アカウントでは実行されません。 単一のサービス アーキテクチャによって、両方の ASP.NET アプリケーションが同じレポート サーバー プロセス ID で実行されます。 これは以前のリリースからの重要な変更です。以前のリリースでは、レポート サーバー Web サービスとレポート マネージャーの両方が、IIS で指定された [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] ワーカー プロセス ID で実行されていました。
  
## <a name="changing-the-service-account"></a>サービス アカウントの変更

 サービス アカウント情報の表示と再構成には、常に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを使用します。 サービス ID 情報は、内部の複数の場所に保存されています。 このツールを使用することで、アカウントまたはパスワードを変更するたびに、すべての参照がその変更に対応して確実に更新されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールは、次に示す追加手順を実行することで、レポート サーバーを利用可能な状態に維持します。  
  
- ローカル コンピューター上に作成されたレポート サーバー グループに、新しいアカウントを自動的に追加します。 このグループは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ファイルをセキュリティで保護するアクセス制御リスト (ACL) 内で指定されます。  
  
- レポート サーバー データベースをホストするために使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスのログイン権限を自動的に更新します。 新しいアカウントは **RSExecRole**に追加されます。  
  
     古いアカウントのデータベース ログインは自動的に削除されません。 使用されなくなったするアカウントは削除するようにしてください。 詳細については、SQL Server オンラインブックの「[レポート サーバー データベースの管理 &#40;SSRS ネイティブ モード&#41;](../report-server/report-server-database-ssrs-native-mode.md)」を参照してください。  
  
     新しいサービス アカウントにデータベース権限が与えられるのは、そのサービス アカウントを最初に使用するようにレポート サーバー データベース接続を構成した場合に限られます。 ドメイン ユーザー アカウントまたは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ログインを使用するようにレポート サーバー データベース接続を構成した場合は、サービス アカウントを更新しても接続情報には影響しません。  
  
- 暗号化キーを自動的に更新し、新しいアカウントのプロファイル情報を取り込みます。  
  
    > [!NOTE]  
    > レポート サーバーがスケールアウト配置の一部である場合、更新するレポート サーバーのみが影響を受けます。 配置内の他のレポート サーバーの暗号化キーは、サービス アカウントを変更しても影響を受けません。  
  
 アカウントを設定する方法の詳細については、次を参照してください。[サービス アカウントを構成&#40;SSRS 構成マネージャー&#41;](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md)します。  
  
## <a name="choosing-an-account"></a>アカウントの選択

 レポート サーバー サービスは、次に示すアカウントの種類のいずれかで実行するように構成できます。  
  
- 最も特権の少ない Windows ユーザー アカウント  
  
- NetworkService  
  
- LocalSystem  
  
- LocalService  
  
 アカウントの種類の選択については最適な方法が 1 つだけ存在するわけではなく、 アカウントごとに考慮する必要がある利点と欠点があります。 実稼働サーバーに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を配置する場合のベスト プラクティスは、共有アカウントが悪意のあるユーザーによって悪用された場合に被害が拡大しないように、サービスをドメイン ユーザー アカウントで実行することです。 これによって、このアカウントのログオンの利用状況も容易に監査できるようになります。 Windows ユーザー アカウントを使用する場合のトレードオフとして、Kerberos 認証を使用するネットワークに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] を配置する場合、このユーザー アカウントでサービスを登録する必要があります。 詳細については、「[レポート サーバーのサービス プリンシパル名 &#40;SPN&#41; の登録](../report-server/register-a-service-principal-name-spn-for-a-report-server.md)」を参照してください。  
  
 次に示すガイドラインとリンクは、配置に最適な方法を決定するのに役立ちます。  
  
- [サービス アカウント&#40;SSRS ネイティブ モード&#41;](../../sql-server/install/service-account-ssrs-native-mode.md)します。  
  
- SQL Server のオンライン ブックの「[Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) 」。  
  
- [サービスおよびサービス アカウントのセキュリティ計画ガイド](http://usergroup.doubletake.com/file_cabinet/download/0x000021733)。  
  
## <a name="updating-an-expired-password"></a>期限切れのパスワードの更新

 レポート サーバー サービスがドメイン アカウントで実行されている場合に、Reporting Services 構成ツールでパスワードを更新する前にパスワードの有効期限が切れると、新しいパスワードを指定するまでこのサービスが開始されなくなります。 サービスを開始できないと、Reporting Services 構成ツールを使用してサーバーに接続できなくなり、アカウントを更新できません。 この場合は、複数のツールを併用してサーバーをオンラインに戻す必要があります。  
  
 パスワードをリセットするには、次の操作を行います。  
  
1. **開始**メニューで、**コントロール パネルの** 、 をポイント**管理者ツール**、 をクリック**サービス**します。  
  
2. 右クリックして**SQL Server Reporting Services**、**プロパティ**します。  
  
3. クリックして**ログオン**、新しいパスワードを入力します。  
  
4. パスワードを変更したら、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成ツールを起動し、[サービス アカウント] ページでパスワードを更新します。 この追加の手順は、レポート サーバーによって内部的に保存されているアカウント情報を更新するために必要です。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のサービス アカウントのパスワードの有効期限が切れると、レポート サーバーへの接続時に `rsReportServerDatabaseUnavailable` エラーが発生します。 パスワードを再設定すると、このエラーは解決されます。  
  
## <a name="configuring-the-report-server-service-for-a-sharepoint-integrated-report-server"></a>SharePoint 統合レポート サーバーのレポート サーバー サービスの構成

 SharePoint 統合モードでレポート サーバーを実行している場合は、次のいずれかの状況のときに、SharePoint 構成データベースに保存されているサービス アカウント情報を更新する必要があります。  
  
- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アカウントを変更する場合 (たとえば、NetworkService からドメイン ユーザー アカウントに切り替える場合など)。  
  
- SharePoint ファームを拡張して追加の SharePoint Web アプリケーションを組み込む場合。 サーバー ファームがレポート サーバー統合用に構成されている場合に、新たに追加されたアプリケーションがファーム内の他のアプリケーションとは異なるユーザー アカウントで実行されるように構成されているときは、データベース アクセス情報を更新する必要があります。  
  
 データベース アクセス情報を再設定した後は、古い接続が引き続き使用されないように [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] サービスを再起動する必要があります。  
  
1. **管理ツール**、 をクリックして**SharePoint 2010 サーバーの全体管理**します。  
  
2. クリックして**アプリケーション管理**します。  
  
3. Reporting Services] セクションで [**データベース アクセスの許可**します。  
  
4. **[OK]** をクリックします。 [資格情報の入力] ダイアログ ボックスが表示されます。  
  
5. レポート サーバーをホストするコンピューター上のローカルの管理者グループに属しているユーザーの資格情報を入力します。 この資格情報は、サービス アカウント情報を取得する目的のために、レポート サーバー コンピューターへの一度だけの接続に使用されます。 各サービス アカウントに対して作成されたデータベース ログインは、SharePoint データベース内で更新されます。  
  
6. サービスを再起動するには、次のようにクリックします。**操作**します。  
  
7. トポロジおよびサービスでは、次のようにクリックします。**サーバーのサービスの**します。  
  
8. Windows SharePoint Services の Web アプリケーションをクリックして**停止**します。  
  
9. サービスが停止するまで待ちます。  
  
10. クリックして**開始**します。  
  
> [!NOTE]  
> SharePoint 製品とテクノロジは、reporting services SharePoint モードのようなサービスの構成にドメイン アカウントが必要です。  
  
## <a name="next-steps"></a>次の手順

 [サービス アカウントを構成&#40;SSRS 構成マネージャー&#41; ](../../sql-server/install/configure-a-service-account-ssrs-configuration-manager.md) [サービス アカウント&#40;SSRS ネイティブ モード&#41;](../../sql-server/install/service-account-ssrs-native-mode.md) [レポート サーバー Url の構成&#40;SSRS の構成Manager&#41; ](configure-report-server-urls-ssrs-configuration-manager.md) [Reporting Services 構成マネージャー&#40;ネイティブ モード&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)
