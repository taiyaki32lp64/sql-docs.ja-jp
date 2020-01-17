---
title: DAC を使用したデータベースの配置 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.dbdeployment.settings.f1
- sql13.swb.dbdeployment.progress.f1
- sql13.swb.dbdeployment.summary.f1
- sql13.swb.dbdeployment.results.f1
- sql13.swb.dbdeployment.welcome.f1
helpviewer_keywords:
- deploy database wizard
- database deploy [SQL Server]
ms.assetid: 08c506e8-4ba0-4a19-a066-6e6a5c420539
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1fae39a6cd0fcd61b18419f8e46786067a4a69dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134805"
---
# <a name="deploy-a-database-by-using-a-dac"></a>DAC を使用したデータベースの配置
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **のインスタンスと** サーバー間、または 2 つの [!INCLUDE[ssDE](../../includes/ssde-md.md)] サーバー間でデータベースを配置するには、 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] SQL Azure へのデータベースの配置ウィザード [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]を使用します。  
  
##  <a name="BeforeBegin"></a> はじめに  
 このウィザードでは、データ層アプリケーション (DAC) の BACPAC アーカイブ ファイルを使用して、データおよびデータベース オブジェクトの定義を配置します。 ウィザードでは、ソース データベースからの DAC エクスポート操作と、配置先への DAC インポート操作を実行します。  
  
###  <a name="DBOptSettings"></a> データベースのオプションと設定  
 既定では、配置中に作成されるデータベースには、CREATE DATABASE ステートメントの既定の設定が適用されます。 ただし、データベースの照合順序と互換性レベルはソース データベースの値に設定されます。  
  
 TRUSTWORTHY、DB_CHAINING、HONOR_BROKER_PRIORITY などのデータベース オプションは、配置プロセスで調整できません。 ファイル グループの数、ファイルの数やサイズなどの物理プロパティは、配置作業中に変更することはできません。 配置が完了すれば、ALTER DATABASE ステートメント、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell を使用して、データベースを調整できます。  
  
###  <a name="LimitationsRestrictions"></a> 制限事項と制約事項  
 **データベース配置** ウィザードでサポートされるデータベースの配置は次のとおりです。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスから [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]  
  
-   [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] から [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンス  
  
-   2 つの [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] サーバー間  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の 2 つのインスタンス間でのデータベースの配置はサポートされません。  
  
 ウィザードを使用するには、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスで [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) 以降を実行している必要があります。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンス上のデータベースに [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]でサポートされていないオブジェクトが含まれている場合、ウィザードを使用して [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]にデータベースを配置することはできません。 また、 [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] 上のデータベースに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でサポートされていないオブジェクトが含まれている場合、ウィザードを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスにデータベースを配置することはできません。  
  
###  <a name="Security"></a> セキュリティ  
 セキュリティを強化するために、SQL Server 認証のログインは、パスワードなしで DAC BACPAC ファイルに格納されます。 BACPAC をインポートすると、ログインはパスワードが生成された無効なログインとして作成されます。 ログインを有効にするには、ALTER ANY LOGIN 権限を持つユーザーとしてログインし、ALTER LOGIN を使用してログインを有効にします。さらに、新しいパスワードを割り当て、そのパスワードを該当ユーザーに通知します。 Windows 認証ログインの場合、ログインのパスワードは SQL Server で管理されていないため、この操作は必要ありません。  
  
#### <a name="permissions"></a>アクセス許可  
 ウィザードでは、ソース データベースに対する DAC エクスポート権限が必要となります。 ログインには、ALTER ANY LOGIN 権限とデータベース スコープの VIEW DEFINITION 権限、および **sys.sql_expression_dependencies**に対する SELECT 権限が少なくとも必要です。 DAC をエクスポートできるのは、DAC をエクスポートするデータベースの database_owner 固定データベース ロールのメンバーでもある、securityadmin 固定サーバー ロールのメンバーです。 sysadmin 固定サーバー ロールのメンバーまたは **sa** という組み込みの SQL Server システム管理者アカウントも DAC をエクスポートできます。  
  
 ウィザードでは、配置先インスタンスまたはサーバーに対する DAC インポート権限が必要となります。 ログインは、 **sysadmin** または **serveradmin** 固定サーバー ロールのメンバーであるか、 **dbcreator** 固定サーバー ロールに属し、ALTER ANY LOGIN 権限を持っている必要があります。 あらかじめ登録された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システム管理者アカウント ( **sa** ) も DAC をインポートできます。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] へのログインが含まれる DAC をインポートするには、loginmanager ロールまたは serveradmin ロールのメンバーシップが必要です。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] へのログインが含まれない DAC をインポートするには、dbmanager ロールまたは serveradmin ロールのメンバーシップが必要です。  
  
##  <a name="UsingDeployDACWizard"></a> データベース配置ウィザードの使用  
 **データベース配置ウィザードを使用してデータベースを移行するには**  
  
1.  データベースの配置先に接続します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスまたは [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] サーバーを指定できます。  
  
2.  **オブジェクト エクスプローラー**で、データベースがあるインスタンスのノードを展開します。  
  
3.  **[データベース]** ノードを展開します。  
  
4.  配置するデータベースを右クリックして **[タスク]** を選択し、 **[SQL Azure へのデータベースの配置...]** をクリックします。  
  
5.  ウィザードの各ダイアログを完了します。  
  
    -   [[説明] ページ](#Introduction)  
  
    -   [配置の設定](#Deployment_settings)  
  
    -   [[概要] ページ](#Summary)  
  
    -   [[進行状況]](#Progress)  
    
    -   [結果](#Results)  
  
##  <a name="Introduction"></a> [説明] ページ  
 このページには、 **データベース配置** ウィザードの手順が示されています。  
  
 **[オプション]**  
  
-   **[次回からこのページを表示しない]** : 今後 [説明] ページを表示しないようにするには、このチェック ボックスをオンにします。  
  
-   **[次へ]** : **[配置設定]** ページに進みます。  
  
-   **[キャンセル]** : 操作を取り消し、ウィザードを閉じます。  
  
##  <a name="Deployment_settings"></a> [配置設定] ページ  
 このページを使用して、配置先サーバーと、新しいデータベースの詳細を指定します。  
  
 **[ローカル ホスト]**  
  
-   **[サーバー接続]** : サーバー接続の詳細を指定し、 **[接続]** をクリックして接続を検証します。  
  
-   **[新しいデータベース名]** : 新しいデータベースの名前を指定します。  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)] データベースの設定:**  
  
-   **[!INCLUDE[ssSDS](../../includes/sssds-md.md)] のエディション**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] のエディションをドロップダウン メニューから選択します。  
  
-   **[データベースの最大サイズ (GB)]** : データベースの最大サイズをドロップダウン メニューから選択します。  
  
 **その他の設定:**  
  
-   一時ファイル (BACPAC アーカイブ ファイル) のローカル ディレクトリを指定します。 このファイルは指定した場所に作成され、操作の完了後もそのまま残されます。  
  
##  <a name="Summary"></a> [概要] ページ  
 このページを使用すると、操作の指定ソースとターゲットの設定を確認できます。 指定した設定で配置操作を実行するには、 **[完了]** をクリックします。 配置操作をキャンセルしてウィザードを終了するには、 **[キャンセル]** をクリックします。  
  
##  <a name="Progress"></a> [進行状況] ページ  
 このページには、操作の進行状況を示す進行状況バーが表示されます。 詳細な状態を表示するには、 **[詳細表示]** をクリックします。  
  
##  <a name="Results"></a> [結果] ページ  
 このページでは、配置操作の成功と失敗が報告され、各アクションの結果が示されます。 エラーが発生したアクションには、 **[結果]** 列にリンクが表示されます。 そのアクションのエラーのレポートを表示するには、リンクをクリックします。  
  
 **[完了]** をクリックして、ウィザードを終了します。  
  
## <a name="using-a-net-framework-application"></a>.Net Framework アプリケーションの使用  
 **.Net Framework アプリケーションで DacStoreExport() メソッドおよび Import() メソッドを使用してデータベースを配置するには**  
  
 コード例を参照するには、 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=219575)上の DAC サンプル アプリケーションをダウンロードしてください。  
  
1.  SMO サーバー オブジェクトを作成し、配置するデータベースがあるインスタンスまたはサーバーに設定します。  
  
2.  **ServerConnection** オブジェクトを開いて、同じインスタンスに接続します。  
  
3.  **Microsoft.SqlServer.Management.Dac.DacStore** 型の **Export** メソッドを使用して、データベースを BACPAC ファイルにエクスポートします。 エクスポートするデータベースの名前と、BACPAC ファイルの出力先となるフォルダーのパスを指定します。  
  
4.  SMO サーバー オブジェクトを作成し、配置先インスタンスまたはサーバーに設定します。  
  
5.  **ServerConnection** オブジェクトを開いて、同じインスタンスに接続します。  
  
6.  **Microsoft.SqlServer.Management.Dac.DacStore** 型の **Import** メソッドを使用して、BACPAC をインポートします。 エクスポートによって作成された BACPAC ファイルを指定します。  
  
## <a name="see-also"></a>参照  
 [データ層アプリケーション](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [データ層アプリケーションのエクスポート](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)   
 [BACPAC ファイルのインポートによる新しいユーザー データベースの作成](../../relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)  
  
  
