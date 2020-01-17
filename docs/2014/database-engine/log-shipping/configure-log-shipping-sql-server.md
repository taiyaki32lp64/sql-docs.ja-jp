---
title: ログ配布の構成 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], enabling
- log shipping [SQL Server], configuring
ms.assetid: c42aa04a-4945-4417-b4c7-50589d727e9c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f7533eb253ba32dd8ef2d57c3182096b36a6e47b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62774586"
---
# <a name="configure-log-shipping-sql-server"></a>ログ配布の構成 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、ログ配布を構成する方法を説明します。  
  
> [!NOTE]  
>  [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 以降のバージョンでは、バックアップの圧縮がサポートされています。 ログ配布構成の作成時に、ログ バックアップのバックアップ圧縮動作を制御できます。 詳細については、「[バックアップの圧縮 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-compression-sql-server.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [前提条件](#Prerequisites)  
  
     [Security](#Security)  
  
-   **以下を使用してログ配布を構成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
  
-   プライマリ データベースでは、完全復旧モデルか一括ログ復旧モデルを使用する必要があります。単純復旧モデルにデータベースを切り替えると、ログ配布が機能しなくなります。  
  
-   ログ配布を構成する前に、セカンダリ サーバーからトランザクション ログ バックアップを使用できるようにするための共有を作成する必要があります。 この共有は、トランザクション ログ バックアップを生成するディレクトリにします。 たとえば、トランザクション ログをディレクトリ c:\data\tlogs\\にバックアップする場合は、このディレクトリを基に \\\\*primaryserver*\tlogs という共有を作成します。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 ログ配布ストアド プロシージャには、 **sysadmin** 固定サーバー ロールのメンバーシップが必要です。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-configure-log-shipping"></a>ログ配布を構成するには  
  
1.  ログ配布構成のプライマリ データベースとして使用するデータベースを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[ページの選択]** の **[トランザクション ログの配布]** をクリックします。  
  
3.  **[ログ配布構成のプライマリ データベースとして有効にする]** チェック ボックスをオンにします。  
  
4.  **[トランザクション ログのバックアップ]** で **[バックアップの設定]** をクリックします。  
  
5.  **[バックアップ フォルダーのネットワーク パスを指定する]** ボックスに、トランザクション ログ バックアップ フォルダー用に作成した共有へのネットワーク パスを入力します。  
  
6.  バックアップ フォルダーがプライマリ サーバー上にある場合は、 **[バックアップ フォルダーがプライマリ サーバーに存在する場合は、バックアップ フォルダーのローカル パスを入力 (例: c:\\backup)]** ボックスに、バックアップ フォルダーへのローカル パスを入力します (バックアップ フォルダーが、プライマリ サーバー上にない場合は、このボックスは空のままでかまいません)。  
  
    > [!IMPORTANT]  
    >  プライマリ サーバーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントがローカル システム アカウントで実行されている場合、バックアップ フォルダーはプライマリ サーバー上に作成し、このフォルダーへのローカル パスを指定する必要があります。  
  
7.  **[次の期間を経過したファイルを削除する]** と **[バックアップが次の期間内に行われない場合は警告する]** の各パラメーターを構成します。  
  
8.  **[バックアップ ジョブ]** の **[スケジュール]** ボックスに、バックアップ スケジュールの一覧が表示されます。 スケジュールをカスタマイズする場合は、 **[スケジュール]** をクリックし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのスケジュールを必要に応じて調整します。  
  
9. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [バックアップの圧縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)がサポートされています。 ログ配布構成を作成する際には、次のオプションのいずれかを選択して、ログ バックアップのバックアップ圧縮動作を制御することができます: **既定のサーバー設定を使用する**、**バックアップを圧縮する**、**バックアップを圧縮しない**。 詳細については、「 [Log Shipping Transaction Log Backup Settings](../../relational-databases/databases/log-shipping-transaction-log-backup-settings.md)」をご覧ください。  
  
10. **[OK]** をクリックします。  
  
11. **[セカンダリ サーバー インスタンスとデータベース]** の **[追加]** をクリックします。  
  
12. **[接続]** をクリックし、セカンダリ サーバーとして使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。  
  
13. **[セカンダリ データベース]** ボックスで、一覧からデータベースを選択するか、作成するデータベースの名前を入力します。  
  
14. **[セカンダリ データベースの初期化]** タブで、セカンダリ データベースを初期化するためのオプションを選択します。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] によりセカンダリ データベースをデータベース バックアップから初期化することを選択した場合、セカンダリ データベースのデータとログ ファイルは **master** データベースのデータとログ ファイルと同じ場所に配置されます。 この場所は、多くの場合、プライマリ データベースのデータとログ ファイルの場所とは異なります。  
  
15. **[ファイルのコピー]** タブの **[ファイルのコピー先フォルダー]** ボックスに、トランザクション ログ バックアップのコピー先となるフォルダーのパスを入力します。 多くの場合、セカンダリ サーバー上のフォルダーを指定します。  
  
16. **[復元ジョブ]** の **[スケジュール]** ボックスにコピー スケジュールの一覧が表示されます。 スケジュールをカスタマイズする場合、 **[スケジュール]** をクリックして、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのスケジュールを必要に応じて調整します。 このスケジュールはバックアップ スケジュールに近い設定にします。  
  
17. **[復元]** タブの **[バックアップ復元時のデータベース状態]** で、 **[復旧モードなし]** または **[スタンバイ モード]** を選択します。  
  
18. **[スタンバイ モード]** を選択する場合は、復元操作の進行中にセカンダリ データベースからユーザーを切断するかどうかを選択します。  
  
19. セカンダリ サーバーの復元処理を遅延させる場合、 **[バックアップの復元を最低限次の期間遅延する]** で遅延時間を選択します。  
  
20. **[復元が次の期間内に行われない場合は警告する]** で警告のしきい値を選択します。  
  
21. **[復元ジョブ]** の **[スケジュール]** ボックスに表示される復元スケジュールを確認します。 スケジュールをカスタマイズする場合、 **[スケジュール]** をクリックして、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのスケジュールを必要に応じて調整します。 このスケジュールはバックアップ スケジュールに近い設定にします。  
  
22. **[OK]** をクリックします。  
  
23. **[監視サーバー インスタンス]** の **[監視サーバー インスタンスを使用する]** チェック ボックスをオンにし、 **[設定]** をクリックします。  
  
    > [!IMPORTANT]  
    >  このログ配布構成を監視するには、ここで監視サーバーを追加する必要があります。 監視サーバーを後で追加するには、このログ配布構成を削除して、代わりに監視サーバーを含む新しい構成を用意します。  
  
24. **[接続]** をクリックして、監視サーバーとして使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに接続します。  
  
25. **[モニター接続]** で、バックアップ、コピー、復元の各ジョブで監視サーバーへの接続に使用する接続方法を指定します。  
  
26. **[履歴の保有期間]** で、ログ配布の履歴レコードを保持する期間を指定します。  
  
27. **[OK]** をクリックします。  
  
28. **[データベースのプロパティ]** ダイアログ ボックスで **[OK]** をクリックし、構成処理を開始します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-configure-log-shipping"></a>ログ配布を構成するには  
  
1.  プライマリ データベースの完全バックアップをセカンダリ サーバーに復元して、セカンダリ データベースを初期化します。  
  
2.  プライマリ サーバーで [sp_add_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-database-transact-sql) を実行して、プライマリ データベースを追加します。 このストアド プロシージャからは、バックアップ ジョブ ID とプライマリ ID が返されます。  
  
3.  プライマリ サーバーで [sp_add_jobschedule](/sql/relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql) を実行して、バックアップ ジョブのスケジュールを追加します。  
  
4.  監視サーバーで [sp_add_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-alert-job-transact-sql) を実行して、警告ジョブを追加します。  
  
5.  プライマリ サーバーでバックアップ ジョブを有効にします。  
  
6.  セカンダリ サーバーで [sp_add_log_shipping_secondary_primary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-primary-transact-sql) を実行します。このとき、プライマリ サーバーとプライマリ データベースの詳細情報を指定します。 このストアド プロシージャからは、セカンダリ ID、コピー ジョブ ID、および復元ジョブ ID が返されます。  
  
7.  セカンダリ サーバーで [sp_add_jobschedule](/sql/relational-databases/system-stored-procedures/sp-add-jobschedule-transact-sql) を実行して、コピー ジョブと復元ジョブのスケジュールを設定します。  
  
8.  セカンダリ サーバーで [sp_add_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-secondary-database-transact-sql) を実行して、セカンダリ データベースを追加します。  
  
9. プライマリ サーバーで [sp_add_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-add-log-shipping-primary-secondary-transact-sql) を実行して、新しいセカンダリ データベースに関する必要な情報をプライマリ サーバーに追加します。  
  
10. セカンダリ サーバーでコピー ジョブと復元ジョブを有効にします。 詳細については、「 [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)」をご覧ください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [SQL Server 2014 へのログ配布のアップグレード&#40;TRANSACT-SQL&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [ログ配布構成へのセカンダリ データベースの追加 &#40;SQL Server&#41;](add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [ログ配布構成からのセカンダリ データベースの削除 &#40;SQL Server&#41;](remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [ログ配布の削除 &#40;SQL Server&#41;](remove-log-shipping-sql-server.md)  
  
-   [ログ配布レポートの表示 &#40;SQL Server Management Studio&#41;](view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [ログ配布の監視 &#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
-   [ログ配布のセカンダリへのフェールオーバー &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [ログ配布について &#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [ログ配布テーブルとストアド プロシージャ](log-shipping-tables-and-stored-procedures.md)  
  
  
