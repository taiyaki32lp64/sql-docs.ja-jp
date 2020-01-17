---
title: SQL Server のインスタンスの登録 (SQL Server ユーティリティ) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.makemanaged.agentaccount.F1
- SQL12.SWB.makemanaged.Summary.F1
- SQL12.SWB.makemanaged.enrolling.F1
- SQL12.SWB.makemanaged.progress.F1
- SQL12.SWB.makemanaged.instancename.F1
- SQL12.SWB.makemanaged.welcome.F1
- SQL12.SWB.makemanaged.validation.F1
helpviewer_keywords:
- Enroll instance
ms.assetid: a801c619-611b-4e82-a8d8-d1e01691b7a1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 37a148393d66a7434fda4461b704ee81b7e05223
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798083"
---
# <a name="enroll-an-instance-of-sql-server-sql-server-utility"></a>SQL Server のインスタンスの登録 (SQL Server ユーティリティ)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに登録し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のマネージド インスタンスとしてそのパフォーマンスおよび構成を監視します。 ユーティリティ コントロール ポイント (UCP) では、15 分ごとに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスから構成情報およびパフォーマンス情報を収集します。 情報は UCP のユーティリティ管理データ ウェアハウス (UMDW) に格納されます。UMDW ファイル名は sysutility_mdw です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンス データはポリシーと比較され、リソース使用時のボトルネックおよび統合の可能性を特定するのに役立ちます。  
  
 このリリースでは、UCP および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのマネージド インスタンスが次の要件を満たしている必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は Version 10.50 以上である必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの型は [!INCLUDE[ssDE](../../includes/ssde-md.md)]であることが必要です。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティは、単一の Windows ドメイン、または双方向の信頼関係を持つドメイン内で操作する必要があります。  
  
-   SQL Server の UCP およびすべてのマネージド インスタンスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントには、Active Directory 内のユーザーに対する読み取り権限が必要です。  
  
-   SQL Azure を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスとして登録することはできません。  
  
 このリリースでは、UCP が次の要件を満たしている必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスはサポートされているエディションである必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされている機能の一覧については、「 [SQL Server 2014 の各エディションがサポートする機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」を参照してください。  
  
-   UCP は SQL Server の大文字と小文字が区別されるインスタンスでホストすることをお勧めします。  
  
-   UCP コンピューター上のキャパシティ プランニングについては、次の推奨事項を考慮してください。  
  
    -   一般的なシナリオでは、UCP の UMDW データベース (sysutility_mdw) で使用されるディスク領域は、SQL Server のマネージド インスタンス 1 つにつき年間約 2 GB です。 この推定値は、マネージド インスタンスによって収集されるデータベース オブジェクトおよびシステム オブジェクトの数に応じて変化します。 UMDW (sysutility_mdw) のディスク領域の増加率は、最初の 2 日間で最大になります。  
  
    -   一般的なシナリオでは、UCP の msdb に使用されるディスク領域は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のマネージド インスタンス 1 つにつき約 20 MB です。 この推定値は、リソース使用率のポリシーと、マネージド インスタンスによって収集されるデータベース オブジェクトおよびシステム オブジェクトの数に応じて変化します。 一般に、ポリシー違反の数が増加したり、変化しやすいリソースの移動期間が長くなるにつれて、使用されるディスク領域が増加します。  
  
    -   UCP からマネージド インスタンスを削除しても、マネージド インスタンスのデータ保持期間の有効期限が切れるまでは、UCP のデータベースで使用されているディスク領域は縮小されません。  
  
 このリリースでは、SQL Server のすべてのマネージド インスタンスが次の要件を満たしている必要があります。  
  
-   UCP をホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスが大文字と小文字を区別しない場合は、SQL Server のマネージド インスタンスでも大文字と小文字を区別しないことをお勧めします。  
  
-   FILESTREAM データは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの監視機能ではサポートされていません。  
  
 詳細については、 [SQL Server 2014 の各エディションがサポート](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)する SQL Server および機能[の最大容量仕様に](../../sql-server/maximum-capacity-specifications-for-sql-server.md)関する説明を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの概念の詳細については、「 [SQL Server ユーティリティの機能とタスク](sql-server-utility-features-and-tasks.md)」を参照してください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ コレクション セットは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ以外のコレクション セットとサイド バイ サイドで実行できます。 つまり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのメンバーであれば、他のコレクション セットによって監視できます。 ただし、マネージド インスタンスのすべてのコレクション セットは、そのデータをユーティリティ管理データ ウェアハウスにアップロードすることに注意してください。 詳細については、「[SQL Server の同じインスタンスでユーティリティ コレクション セットとユーティリティ以外のコレクション セットを実行する場合の考慮事項](run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)」、および「[ユーティリティ コントロール ポイント データ ウェアハウスの構成 &#40;SQL Server Utility&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md)」を参照してください。  
  
## <a name="wizard-steps"></a>ウィザードの手順  
 次のセクションでは、ウィザードのワークフローの各ページについて詳しく説明します。 リンクをクリックすると、ウィザードのページの詳細に移動できます。 この操作を実行する PowerShell スクリプトの詳細については、PowerShell の [例](#PowerShell_enroll)を参照してください。  
  
-   [インスタンスの登録ウィザードの概要](#Welcome)  
  
-   [SQL Server インスタンスの指定](#Instance_name)  
  
-   [接続ダイアログ](#Connection_dialog)  
  
-   [ユーティリティ コレクション セットのアカウント](#Proxy_configuration)  
  
-   [SQL Server インスタンスの検証](#Validation_rules)  
  
-   [インスタンス登録の概要](#Summary)  
  
-   [SQL Server インスタンスの登録](#Enrolling)  
  
##  <a name="Welcome"></a> インスタンスの登録ウィザードの概要  
 このウィザードを起動するには、ユーティリティ エクスプローラーのツリーでユーティリティ コントロール ポイントを展開し、 **[マネージド インスタンス]** ノードを右クリックして、 **[マネージド インスタンスの追加]** をクリックします。  
  
 続行するには、 **[次へ]** をクリックします。  
  
##  <a name="Instance_name"></a> SQL Server インスタンスの指定  
 [接続] ダイアログボックスから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを選択するには、 **[接続]** をクリックします。Computername\instancename の形式で、コンピューター名と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名を指定します。 詳細については、「[サーバーへの接続 &#40;データベース エンジン&#41;](../../ssms/f1-help/connect-to-server-database-engine.md)」を参照してください。  
  
 続行するには、 **[次へ]** をクリックします。  
  
##  <a name="Connection_dialog"></a> 接続ダイアログ  
 [サーバーへの接続] ダイアログ ボックスで、サーバーの種類、コンピューター名、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名の情報を確認します。 詳細については、「[サーバーへの接続 &#40;データベース エンジン&#41;](../../ssms/f1-help/connect-to-server-database-engine.md)」を参照してください。  
  
> [!NOTE]  
>  接続が暗号化されている場合、暗号化された接続が使用されます。 接続が暗号化されていない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティは暗号化された接続を使用して再接続します。  
  
 続行するには、 **[接続]** をクリックします。  
  
##  <a name="Proxy_configuration"></a> ユーティリティ コレクション セットのアカウント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ コレクション セットを実行する Windows ドメイン アカウントを指定します。 このアカウントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ コレクション セットの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシ アカウントとして使用されます。 また、既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントを使用することもできます。 検証の要件を満たすには、次のガイドラインに従ってアカウントを指定します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントのオプションを指定する場合は、次のガイドラインに従います。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントには、ビルトイン アカウント (LocalSystem、NetworkService、LocalService など) ではなく、Windows ドメイン アカウントを指定する必要があります。  
  
 続行するには、 **[次へ]** をクリックします。  
  
##  <a name="Validation_rules"></a> SQL Server インスタンスの検証  
 このリリースでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに登録する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで、次の条件が満たされている必要があります：  
  
|条件|修正措置|  
|---------------|-----------------------|  
|指定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスと UCP に対する管理者特権が必要です。|指定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス、および UCP の管理者特権を持つアカウントでログオンします。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエディションでインスタンスの登録がサポートされている必要があります。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされている機能の一覧については、「 [SQL Server 2014 の各エディションがサポートする機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」を参照してください。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP で TCP/IP が有効になっている必要があります。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP で TCP/IP を有効にします。|  
|別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP で登録されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは使用できません。|指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの一部として既に管理されている場合、そのインスタンスを別の UCP に登録することはできません。|  
|既に UCP である [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは使用できません。|指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが、接続先の UCP とは別の UCP の場合、インスタンスをこの UCP に登録することはできません。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ コレクション セットがインストールされている必要があります。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを再インストールします。|  
|指定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのコレクション セットを停止する必要があります。|指定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスの既存のコレクション セットを停止します。 データ コレクターが無効になっている場合は、それを有効にして、実行中のコレクション セットを停止し、UCP の作成操作に対して検証規則を再実行します。<br /><br /> データ コレクターを有効にするには :<br /><br /> オブジェクト エクスプローラーで、 **[管理]** ノードを展開します。<br /><br /> **[データ コレクション]** を右クリックし、 **[データ コレクションの有効化]** をクリックします。<br /><br /> コレクション セットを停止するには :<br /><br /> オブジェクト エクスプローラーで、[管理] ノード、 **[データ コレクション]** 、 **[システム データ コレクション セット]** の順に展開します。<br /><br /> 停止するコレクション セットを右クリックして **[データ コレクション セットの停止]** をクリックします。<br /><br /> メッセージ ボックスにはこのアクションの結果が表示され、コレクション セットのアイコンに赤い丸が付いている場合は、コレクション セットが停止していることを示します。|  
|指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを開始する必要があります。|指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント サービスを開始します。 指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターのインスタンスである場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを手動で開始するように構成します。 それ以外の場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスが自動的に開始されるように構成します。|  
|UCP の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを開始する必要があります。|UCP の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを開始します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターのインスタンスである場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを手動で開始するように構成します。 それ以外の場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスが自動的に開始されるように構成します。|  
|WMI が正しく構成されている必要があります。|WMI の構成をトラブルシューティングするには、「 [SQL Server ユーティリティのトラブルシューティング](../../database-engine/troubleshoot-the-sql-server-utility.md)」を参照してください。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシ アカウントは、UCP の有効な Windows ドメイン アカウントである必要があります。|有効な Windows ドメイン アカウントを指定します。 アカウントが有効であることを確認するには、Windows ドメイン アカウントを使用して UCP にログオンします。|  
|プロキシ アカウント オプションを選択した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシ アカウントは、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスの有効な Windows ドメイン アカウントである必要があります。|有効な Windows ドメイン アカウントを指定します。 アカウントが有効であることを確認するには、Windows ドメイン アカウントを使用して、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにログオンします。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントをビルトイン アカウント (Network Service など) にすることはできません。|アカウントを Windows ドメイン ユーザー アカウントに再割り当てします。 アカウントが有効であることを確認するには、Windows ドメイン アカウントを使用して、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにログオンします。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントは、UCP の有効な Windows ドメイン アカウントである必要があります。|有効な Windows ドメイン アカウントを指定します。 アカウントが有効であることを確認するには、Windows ドメイン アカウントを使用して UCP にログオンします。|  
|サービス アカウント オプションを選択した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントは、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスの有効な Windows ドメイン アカウントである必要があります。|有効な Windows ドメイン アカウントを指定します。 アカウントが有効であることを確認するには、Windows ドメイン アカウントを使用して、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにログオンします。|  
  
 検証結果に失敗した条件が示されている場合は、支障をきたす問題を解決した後、 **[検証の再実行]** をクリックして、コンピューターの構成を確認します。  
  
 検証レポートを保存するには、 **[レポートの保存]** をクリックし、ファイルの場所を指定します。  
  
 続行するには、 **[次へ]** をクリックします。  
  
##  <a name="Summary"></a> インスタンス登録の概要  
 概要ページには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに追加する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの情報が表示されます。  
  
 マネージド インスタンスの設定は次のとおりです。  
  
-   SQL Server インスタンス名: ComputerName\InstanceName  
  
-   ユーティリティ コレクション セットのアカウント: DomainName\UserName  
  
 続行するには、 **[次へ]** をクリックします。  
  
##  <a name="Enrolling"></a> SQL Server インスタンスの登録  
 登録ページでは、次のように、処理の進行状況が表示されます。  
  
-   インスタンスを登録する準備をしています。  
  
-   収集されたデータのキャッシュ ディレクトリを作成しています。  
  
-   ユーティリティ コレクション セットを構成しています。  
  
 登録処理に関するレポートを保存するには、 **[レポートの保存]** をクリックし、ファイルの場所を指定します。  
  
 ウィザードを完了するには、 **[完了]** をクリックします。  
  
> [!NOTE]  
>  登録する SQL Server のインスタンスに SQL Server 認証を使用して接続し、UCP があるドメインとは異なる Active Directory ドメインに属するプロキシ アカウントを指定した場合、インスタンスの検証には成功しますが、次のエラー メッセージが表示されて登録処理に失敗します。  
>   
>  Transact-SQL ステートメントまたはバッチの実行中に例外が発生しました。 (Microsoft.SqlServer.ConnectionInfo)  
>   
>  追加情報: Windows NT グループまたはユーザー '\<ドメイン名\アカウント名>' に関する情報を取得できませんでした。エラー コード 0x5。 (Microsoft SQL Server、エラー: 15404)  
>   
>  このエラーのトラブルシューティングの詳細については、「 [SQL Server ユーティリティのトラブルシューティング](../../database-engine/troubleshoot-the-sql-server-utility.md)」を参照してください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンス上の "ユーティリティ情報" コレクション セットのプロパティは一切変更しないでください。また、データ コレクションはユーティリティ エージェント ジョブによって制御されるため、データ コレクションのオン/オフを手動で切り替えることも避けてください。  
  
 インスタンスの登録ウィザードが完了したら、SSMS の **ユーティリティ エクスプローラーのナビゲーション** ウィンドウで、 **[マネージド インスタンス]** ノードをクリックします。 登録済みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスは、 **ユーティリティ エクスプローラー** のコンテンツ ウィンドウのリスト ビューに表示されます。  
  
 データ収集プロセスはすぐに開始されますが、ユーティリティ エクスプローラーのコンテンツ ウィンドウ内のダッシュボードとビューポイントに最初に表示されるまで最大 30 分かかる場合があります。 データの収集は 15 分間隔で続行されます。 データを更新するには、 **ユーティリティ エクスプローラーのナビゲーション** ウィンドウで **[マネージド インスタンス]** ノードを右クリックして **[更新]** をクリックするか、リスト ビューで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名を右クリックして **[更新]** をクリックします。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティからマネージド インスタンスを削除するには、 **ユーティリティ エクスプローラーのナビゲーション** ウィンドウで **[マネージド インスタンス]** を選択してマネージド インスタンスのリスト ビューを設定し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ エクスプローラーのコンテンツ **ウィンドウのリスト ビューで** インスタンス名を右クリックして、 **[マネージド インスタンスを削除]** を選択します。  
  
##  <a name="PowerShell_enroll"></a> PowerShell を使用した SQL Server インスタンスの登録  
 次の例を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに登録します:  
  
```powershell
$UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
$SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
$Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($SqlStoreConnection);  
$Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\ManagedInstanceName";  
$InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
$ManagedInstance = $Utility.EnrollInstance($InstanceConnection, "ProxyAccount", "ProxyPassword");  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server ユーティリティの機能とタスク](sql-server-utility-features-and-tasks.md)   
 [SQL Server ユーティリティでの SQL Server のインスタンスの監視](monitor-instances-of-sql-server-in-the-sql-server-utility.md)   
 [SQL Server ユーティリティのトラブルシューティング](../../database-engine/troubleshoot-the-sql-server-utility.md)  
  
  
