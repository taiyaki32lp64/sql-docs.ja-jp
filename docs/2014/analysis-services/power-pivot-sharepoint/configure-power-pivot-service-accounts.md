---
title: PowerPivot サービス アカウントの構成 |Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 76a85cd0-af93-40c9-9adf-9eb0f80b30c1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b90944c3260af69f29fbae8a93f5865c1f3c6d1e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66071858"
---
# <a name="configure-powerpivot-service-accounts"></a>PowerPivot サービス アカウントの構成
  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] のインストールには、サーバー処理をサポートする 2 つのサービスが含まれます。 **SQL Server Analysis Services (PowerPivot)** サービスは、アプリケーション サーバー上の PowerPivot データの処理およびクエリのサポートを提供する Windows サービスです。 このサービスのログイン アカウントは、SharePoint 統合モードで Analysis Services をインストールするときに、SQL Server セットアップで必ず指定します。  
  
 SharePoint ファームのアプリケーション プール ID で実行される共有 Web サービスである PowerPivot サービス アプリケーション用に、アカウントをもう 1 つ指定する必要があります。 このアカウントは、PowerPivot 構成ツールまたは PowerShell を使用して [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] インストールを構成するときに指定します。  
  
 接続を監査したり、ファームで Kerberos 認証プロトコルを有効にしたりできるように、それぞれのサービスは、専用のアカウントで実行する必要があります。  
  
 サービス アカウントを設定した後で、いずれかのアカウントに変更を加える場合は、SharePoint サーバーの全体管理を使用する必要があります。 別のツール (Services コンソール アプリケーション、IIS マネージャー、SQL Server 構成マネージャーなど) を使用すると、ファーム内でのデータベース アクセス、または物理サーバー上でのファイル アクセスに必要な権限が更新されません。  
  
 このトピックには、次のセクションが含まれます。  
  
 [SQL Server Analysis Services (PowerPivot) インスタンスの有効期限切れのパスワードを更新します。](#bkmk_passwordssas)  
  
 [PowerPivot サービス アプリケーションの有効期限が切れたパスワードを更新します。](configure-power-pivot-service-accounts.md#bkmk_passwordapp)  
  
 [各サービスの実行に使用するアカウントの変更](#bkmk_newacct)  
  
 [作成するか、PowerPivot サービス アプリケーションのアプリケーション プールの変更](#bkmk_appPool)  
  
 [アカウント要件と権限](#requirements)  
  
 [トラブルシューティング: 手動で管理アクセス許可を付与します。](#updatemanually)  
  
 [トラブルシューティング: 解決するには HTTP 503 エラー中央管理サイトまたは SharePoint Foundation の有効期限が切れたパスワードによる Web アプリケーション サービス](#expired)  
  
##  <a name="bkmk_passwordssas"></a> SQL Server Analysis Services (PowerPivot) インスタンスの有効期限切れのパスワードを更新します。  
  
1.  [スタート] ボタンをクリックし、 **[管理ツール]** 、 **[サービス]** の順にクリックします。 ダブルクリック**SQL Server Analysis Services (PowerPivot)** します。 **[ログオン]** をクリックし、アカウントの新しいパスワードを入力します。  
  
2.  サーバーの全体管理で、[セキュリティ] セクションの **[管理アカウントの構成]** をクリックします。  
  
3.  **[編集]** をクリックして指定のアカウントを変更します。  
  
4.  **[今すぐパスワードを変更]** をクリックします。  
  
5.  **[アカウント パスワードを新しい値に設定する]** をクリックします。 管理アカウントで実行されるすべてのサービスで、更新された資格情報が使用されます。  
  
##  <a name="bkmk_passwordapp"></a> PowerPivot サービス アプリケーションの有効期限が切れたパスワードを更新します。  
  
1.  サーバーの全体管理で、[セキュリティ] セクションの **[管理アカウントの構成]** をクリックします。  
  
2.  **[編集]** をクリックして指定のアカウントを変更します。  
  
3.  **[今すぐパスワードを変更]** をクリックします。  
  
4.  **[アカウント パスワードを新しい値に設定する]** をクリックします。 管理アカウントで実行されるすべてのサービスで、更新された資格情報が使用されます。  
  
##  <a name="bkmk_newacct"></a> 各サービスの実行に使用するアカウントの変更  
  
1.  サーバーの全体管理で、[セキュリティ] セクションの **[サービス アカウントの構成]** をクリックします。  
  
2.  **[Windows サービス - SQL Server Analysis Services]** を選択して、Analysis Services サービス アカウントを変更します。  
  
3.  **[このサービスのアカウントを選択する]** で、既存の管理アカウントを選択するか、新規に作成します。 このアカウントは、ドメイン ユーザー アカウントであることが必要です。  
  
4.  選択**サービス アプリケーション プール - SharePoint Web サービスのシステム**既定の PowerPivot サービス アプリケーションのアプリケーション プール id を変更します。 インストールの構成によっては、SharePoint サービス用に作成された既存のサービス アプリケーション プールでサービスが実行されている場合があります。 既定では、PowerPivot 構成ツールは、サービスを登録します**既定の PowerPivot サービス アプリケーション (PowerPivot サービス アプリケーション)** します。  
  
     サービスが SharePoint 管理者によって手動で構成された場合、サービスにはほとんどの場合に自身のサービス アプリケーション プールがあります。  
  
5.  **[このサービスのアカウントを選択する]** で、既存の管理アカウントを選択するか、新規に作成します。 このアカウントは、ドメイン ユーザー アカウントであることが必要です。  
  
6.  **[OK]** をクリックします。  
  
##  <a name="bkmk_appPool"></a> 作成するか、PowerPivot サービス アプリケーションのアプリケーション プールの変更  
  
1.  サーバーの全体管理で、[アプリケーション構成の管理] の **[サービス アプリケーションの管理]** をクリックします。  
  
2.  PowerPivot サービス アプリケーションを選択します (クリックはしないでください)。 アプリケーション名をクリックすると、PowerPivot 管理ダッシュボードが開きます。このダッシュボードには、アプリケーション プールを指定するプロパティ ページへのリンクはありません。  行の空白部分をクリックするか、種類名をクリックして、PowerPivot サービス アプリケーションを選択できます。  
  
3.  リボンの **[プロパティ]** をクリックします。  
  
4.  **[新しいアプリケーション プールの作成]** をクリックします。 アプリケーション プールの名前を指定し、その ID の管理アカウントを指定します。  
  
##  <a name="requirements"></a> アカウント要件と権限  
 PowerPivot for SharePoint の配置を計画するときには、次のサービス アカウントについて計画する必要があります。  
  
-   Analysis Services サービス アカウント。 Analysis Services は、PowerPivot のクエリおよびデータ更新のジョブをファームで処理します。 このアカウントは、SQL Server のセットアップ中に、PowerPivot for SharePoint をインストールするときに必ず指定します。  
  
-   PowerPivot サービス アプリケーション プール。 PowerPivot サービス アプリケーションは、PowerPivot System サービスに関連付けられ、ファーム内の PowerPivot クエリ処理に SharePoint 統合と SharePoint インフラストラクチャを提供します。 PowerPivot サービス アプリケーションに対して指定するアプリケーション プールは、PowerPivot System サービスのサービス ID です。 1 つのファームに複数の PowerPivot サービス アプリケーションを作成できますが、 それぞれのサービス アプリケーションを、固有のアプリケーション プールで実行する必要があります。  
  
#### <a name="analysis-services-service-account"></a>Analysis Services サービス アカウント  
  
|要件|説明|  
|-----------------|-----------------|  
|プロビジョニングの要件|このアカウントは、SQL Server セットアップ中に指定する必要がありますを使用して、 **Analysis Services - 構成ページ**インストール ウィザード (または`ASSVCACCOUNT`コマンド ライン セットアップのインストール パラメーター)。<br /><br /> ユーザー名やパスワードは、サーバーの全体管理、PowerShell、または PowerPivot 構成ツールを使用して変更できます。 その他のツールでのアカウントやパスワードの変更はサポートされていません。|  
|ドメイン ユーザー アカウントの要件|このアカウントは Windows ドメイン ユーザー アカウントであることが必要です。 ビルトイン コンピューター アカウント (Network Service や Local Service など) は禁止されています。 SQL Server セットアップは、コンピューター アカウントが指定された場合にインストールをブロックすることで、ドメイン ユーザー アカウント要件を適用します。|  
|権限の要件|このアカウントは SQLServerMSASUser$ のメンバーである必要があります\<server > $PowerPivot セキュリティ グループとローカル コンピューターの WSS_WPG セキュリティ グループ。 これらの権限は自動的に付与されます。 確認するか、アクセス許可を付与する方法の詳細については、次を参照してください[、PowerPivot サービス アカウント管理のアクセス許可を手動で付与](#updatemanually)このトピックの「と[初期構成&#40;PowerPivot for SharePoint。&#41;](../../sql-server/install/initial-configuration-powerpivot-for-sharepoint.md).|  
|スケールアウトの要件|ファームに複数の PowerPivot for SharePoint サーバー インスタンスをインストールする場合は、すべての Analysis Services サーバー インスタンスが同じドメイン ユーザー アカウントで実行されている必要があります。 たとえば、最初の [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] インスタンスが Contoso\ssas-srv01 として実行されるように構成した場合は、それ以降に同じファームに配置したその他のすべての [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] インスタンスも Contoso\ssas-srv01 (または現在の任意のアカウント) として実行される必要があります。<br /><br /> すべてのサービス インスタンスが同じアカウントで実行されるように構成すると、PowerPivot System サービスで、クエリ処理やデータ更新のジョブをファーム内の任意の Analysis Services サービス インスタンスに割り当てられるようになります。 また、Analysis Services サーバー インスタンスに対してサーバーの全体管理の管理アカウント機能を使用できるようになります。 すべての [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] インスタンスに同じアカウントを使用すると、アカウントまたはパスワードを 1 回変更するだけで、これらの資格情報を使用するすべてのサービス インスタンスを自動的に更新できます。<br /><br /> SQL Server セットアップでは、同一アカウント要件が適用されます。 PowerPivot for SharePoint インスタンスが既に SharePoint ファームにインストールされているスケールアウト配置では、指定した [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] アカウントとファーム内で既に使用されているアカウントが異なる場合、セットアップによって新規インストールがブロックされます。|  
  
#### <a name="powerpivot-service-application-pool"></a>PowerPivot サービス アプリケーション プール  
  
|要件|説明|  
|-----------------|-----------------|  
|プロビジョニングの要件|PowerPivot System サービスは、ファーム上の共有リソースで、サービス アプリケーションを作成すると使用できるようになります。 サービス アプリケーション プールは、サービス アプリケーションの作成時に指定する必要があります。 サービス アプリケーション プールを指定する方法には、PowerPivot 構成ツールを使用する方法と PowerShell コマンドを使用する方法の 2 つがあります。<br /><br /> アプリケーション プール ID を一意のアカウントで実行されるように構成 いない場合は、別のアカウントで実行するように変更を検討してください。|  
|ドメイン ユーザー アカウントの要件|アプリケーション プール ID は Windows ドメイン ユーザー アカウントであることが必要です。 ビルトイン コンピューター アカウント (Network Service や Local Service など) は禁止されています。|  
|権限の要件|このアカウントには、コンピューターのローカルのシステム管理者権限は必要ありません。 ただし、同じコンピューターにインストールされているローカル [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] に対する Analysis Services のシステム管理者権限が必要です。 これらの権限は、SQL Server セットアップを実行したり、サーバーの全体管理でアプリケーション プール ID を設定または変更したりすると、自動的に付与されます。<br /><br /> 管理権限は、 [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]にクエリを転送する場合に必要です。 また、状態の監視、非アクティブなセッションの終了、およびトレース イベントのリッスンにも必要です。<br /><br /> このアカウントには、PowerPivot サービス アプリケーション データベースに対する接続、読み取り、および書き込みの権限が必要です。 これらの権限は、アプリケーションの作成時に自動的に付与され、サーバーの全体管理でアカウントやパスワードを変更した場合にも自動的に更新されます。<br /><br /> PowerPivot サービス アプリケーションでは、ファイルの取得前に、データを表示する権限が SharePoint ユーザーにあるかどうかを確認しますが、ユーザーの権限の借用は行いません。 そのため、権限の借用に関する権限の要件はありません。|  
|スケールアウトの要件|[なし] :|  
  
##  <a name="updatemanually"></a> トラブルシューティング。手動で管理アクセス許可を付与します。  
 資格情報を更新するユーザーがコンピューターのロカール管理者でない場合、管理者権限は更新されません。 この場合は、管理者権限を手動で付与できます。 最も簡単な方法でこの操作を行うには、サーバーの全体管理で PowerPivot の構成タイマー ジョブを実行します。 この方法を使用すると、ファーム内のすべての PowerPivot サーバーの権限をリセットできます。 この方法は、SharePoint タイマー ジョブがファームの管理者およびコンピューターのローカル管理者の両方として実行されている場合にのみ使用できる点に注意してください。  
  
1.  [監視] で、 **[ジョブ定義の確認]** をクリックします。  
  
2.  選択**PowerPivot 構成タイマー ジョブ**します。  
  
3.  **[今すぐ実行]** をクリックします。  
  
 最後の手段として、PowerPivot サービス アプリケーションへの Analysis Services システム管理アクセス許可を付与することで適切なアクセス許可を確認および具体的には、サービス アプリケーションの id を SQLServerMSASUser$ に追加\<servername > $PowerPivot Windows セキュリティ グループ。 SharePoint ファームに統合された各 Analysis Services インスタンスに対してこれらの手順を繰り返す必要があります。  
  
 Windows セキュリティ グループを更新するには、ローカル管理者である必要があります。  
  
1.  SQL Server Management studio で、Analysis Services インスタンスに接続します。\<サーバー名 > \POWERPIVOT します。  
  
2.  サーバー名を右クリックし、 **[プロパティ]** をクリックします。  
  
3.  **[セキュリティ]** をクリックします。  
  
4.  **[追加]** をクリックします。  
  
5.  PowerPivot サービス アプリケーション プールを使用するアカウントの名前を入力し、クリックして**OK**します。  
  
6.  [管理ツール] で、 **[コンピューターの管理]** をクリックします。  
  
7.  **[ローカル ユーザーとグループ]** を開きます。  
  
8.  **[グループ]** を開きます。  
  
9. SQLServerMSASUser$ をダブルクリックして\<servername > $PowerPivot します。  
  
10. **[追加]** をクリックします。  
  
11. PowerPivot サービス アプリケーション プールを使用するアカウントの名前を入力し、クリックして**OK**します。  
  
##  <a name="expired"></a> トラブルシューティング。解決するには HTTP 503 エラー中央管理サイトまたは SharePoint Foundation の有効期限が切れたパスワードによる Web アプリケーション サービス  
 アカウントのリセットまたはパスワードの期限切れが原因で、サーバーの全体管理サービスまたは SharePoint Foundation Web アプリケーション サービスが停止する場合は、SharePoint サーバーの全体管理あるいは SharePoint サイトを開こうとすると、"サービスを利用できません" という HTTP 503 エラー メッセージが表示されます。 サーバーをオンラインに戻すには、次の手順を実行します。 サーバーの全体管理を使用できる場合は、続行して期限切れのアカウント情報を更新できます。  
  
1.  [管理ツール] で、 **[インターネット インフォメーション サービス マネージャー]** をクリックします。  
  
2.  サイトまたはサーバーの全体管理アプリケーション プールの ID が、期限切れのパスワードを持つドメイン ユーザー アカウントである場合は、次の手順を実行します。  
  
    1.  アプリケーション プール名を右クリックし、 **[詳細設定]** をクリックします。  
  
    2.  選択**Identity**  をクリックし、... をアプリケーション プール Id ダイアログ ボックスを開きます。  
  
    3.  **[設定]** をクリックします。  
  
    4.  ユーザー名とパスワードを入力します。  
  
3.  IISRESET を実行します。 この操作を行うには、管理者コマンド プロンプトを開き、コマンドで「`iisreset`」と入力します。  
  
4.  SharePoint サーバーの全体管理で、[セキュリティ] の **[管理アカウントの構成]** をクリックします。  
  
5.  **[編集]** をクリックして、期限切れのパスワードを持つ管理アカウントの情報を更新します。  
  
6.  **[今すぐパスワードを変更]** をクリックします。  
  
7.  **[既存のパスワードを使用]** をクリックします。  
  
8.  パスワードを入力し、 **[OK]** をクリックします。  
  
 Reporting Services がインストールされている場合は、Reporting Services 構成マネージャーを使用して、レポート サーバーのパスワードとレポート サーバー データベースへの接続に使用するパスワードを更新します。 詳細については、「[レポート サーバーの構成と管理 (Reporting Services SharePoint モード)](../../reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [開始または PowerPivot を SharePoint サーバーの停止](start-or-stop-a-power-pivot-for-sharepoint-server.md)   
 [構成、PowerPivot 自動データ更新アカウント&#40;PowerPivot for SharePoint&#41;](../configure-unattended-data-refresh-account-powerpivot-sharepoint.md)  
  
  
