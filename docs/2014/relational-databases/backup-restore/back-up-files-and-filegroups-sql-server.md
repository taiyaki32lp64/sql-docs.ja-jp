---
title: ファイルおよびファイル グループのバックアップ (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up filegroups [SQL Server]
- file backups [SQL Server], how-to topics
- backing up files [SQL Server]
- backups [SQL Server], creating
- filegroups [SQL Server], backing up
ms.assetid: a0d3a567-7d8b-4cfe-a505-d197b9a51f70
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c686e5eb9bb44517aa1636dc28c972f6782f8bfe
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782749"
---
# <a name="back-up-files-and-filegroups-sql-server"></a>ファイルおよびファイル グループのバックアップ (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、または PowerShell を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でファイルとファイル グループをバックアップする方法について説明します。 データベースのサイズやパフォーマンスの要件によりデータベースの完全バックアップが不可能な場合は、代わりに、ファイル バックアップを作成できます。 *ファイル バックアップ* には、1 つ以上のファイル (またはファイル グループ) 内のすべてのデータが含まれます。 ファイルのバックアップの詳細については、「[ファイルの完全バックアップ &#40;SQL Server&#41;](full-file-backups-sql-server.md)」および「[差分バックアップ &#40;SQL Server&#41;](differential-backups-sql-server.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   **次のものを使用してファイルとファイルグループをバックアップするには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   BACKUP ステートメントは、明示的または暗黙的なトランザクションでは使用できません。  
  
-   単純復旧モデルでは、読み取りと書き込みが可能なファイルはすべてまとめてバックアップする必要があります。 これにより、データベースを一貫性のある時点に復元できます。 読み取りと書き込みが可能なファイルまたはファイル グループを個別に指定するのではなく、READ_WRITE_FILEGROUPS オプションを使用します。 このオプションにより、読み取りと書き込みが可能なすべてのファイル グループがデータベースにバックアップされます。 READ_WRITE_FILEGROUPS を指定して作成されるバックアップは、*部分バックアップ*と呼ばれます。 詳細については、「[部分バックアップ &#40;SQL Server&#41;](partial-backups-sql-server.md)」を参照してください。  
  
-   この機能の制限および制約の詳細については、「[バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)」を参照してください。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   既定では、バックアップ操作が成功するたびに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログおよびシステム イベント ログにエントリが 1 つ追加されます。 ログを頻繁にバックアップすると、これらの成功メッセージがすぐに蓄積され、他のメッセージを探すのが困難になるほどエラー ログが大きくなることがあります。 そのような場合、これらのエントリに依存するスクリプトがなければ、トレース フラグ 3226 を使用することによってこれらのログ エントリを除外できます。 詳細については、「[トレース フラグ &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> アクセス許可  
 BACKUP DATABASE 権限と BACKUP LOG 権限は、既定では、 **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_backupoperator** 固定データベース ロールのメンバーに与えられています。  
  
 バックアップ デバイスの物理ファイルに対する所有と許可の問題によって、バックアップ操作が妨げられることがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、デバイスに対して読み書きを実行できる必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが実行されているアカウントには書き込み権限が必要です。 ただし、システム テーブルにバックアップ デバイスのエントリを追加する [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)では、ファイル アクセスの権限は確認されません。 バックアップ デバイスの物理ファイルに関するこのような問題は、バックアップや復元が試行され、物理リソースがアクセスされるまで、表面化しない可能性があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-back-up-database-files-and-filegroups"></a>データベース ファイルおよびファイル グループをバックアップするには  
  
1.  適切な [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスへの接続後、オブジェクト エクスプローラーでサーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[データベース]** を展開します。さらに、そのデータベースに応じて、ユーザー データベースを選択するか、または **[システム データベース]** を展開してシステム データベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** をポイントし、 **[バックアップ]** をクリックします。 **[データベースのバックアップ]** ダイアログ ボックスが表示されます。  
  
4.  **[データベース]** ボックスの一覧で、適切なデータベース名が表示されていることを確認します。 必要に応じて、このボックスの一覧から別のデータベースを選択することもできます。  
  
5.  **[バックアップの種類]** ボックスの一覧の **[完全]** または **[差分]** をクリックします。  
  
6.  **[バックアップ コンポーネント]** の **[ファイルとファイル グループ]** をクリックします。  
  
7.  **[ファイルおよびファイル グループの選択]** ダイアログ ボックスで、バックアップするファイルおよびファイル グループを選択します。 個別のファイルを 1 つ以上選択できるほか、ファイル グループのチェック ボックスをオンにすると自動的にファイル グループ内のすべてのファイルが選択されます。  
  
8.  **[名前]** ボックスに表示された既定のバックアップ セット名をそのまま使用するか、または別のバックアップ セット名を入力します。  
  
9. 必要に応じて、 **[説明]** ボックスに、バックアップ セットの説明を入力します。  
  
10. バックアップ セットの有効期限を指定します。  
  
    -   バックアップ セットが指定の日数後に期限切れになるようにするには、 **[期間指定]** (既定のオプション) をクリックします。 次に、セットを作成してから期限切れになるまでの日数を入力します。 0 ～ 99,999 日の値を指定できます。0 日を指定すると、バックアップ セットの有効期限は無期限になります。  
  
         既定値は、 **[サーバーのプロパティ]** ダイアログ ボックス ( **[データベースの設定]** ページ) の **[バックアップ メディアの既定の保有期間 (日)]** オプションで設定されています。 このオプションを表示するには、オブジェクト エクスプローラーでサーバー名を右クリックし、[プロパティ] をクリックします。次に、 **[データベースの設定]** ページをクリックします。  
  
    -   バックアップ セットが特定の日付に期限切れになるようにするには、 **[日時指定]** をクリックし、セットの有効期限が切れる日付を入力します。  
  
11. **[ディスク]** または **[テープ]** をクリックして、バックアップ先を選択します。 1 つのメディア セットを含んでいる最大 64 個のディスク ドライブまたはテープ ドライブのパスを選択するには、 **[追加]** をクリックします。 選択したパスは、 **[バックアップ先]** ボックスの一覧に表示されます。  
  
    > [!NOTE]  
    >  バックアップ先を削除するには、バックアップ先を選択して **[削除]** をクリックします。 バックアップ先の内容を表示するには、バックアップ先を選択して **[内容]** をクリックします。  
  
12. 詳細設定オプションを表示または選択するには、 **[ページの選択]** ペインの **[オプション]** をクリックします。  
  
13. 次のいずれかをクリックして、 **[メディアに上書きします]** オプションを選択します。  
  
    -   **[既存のメディア セットにバックアップする]**  
  
         このオプションでは、 **[既存のバックアップ セットに追加する]** または **[既存のすべてのバックアップ セットを上書きする]** をクリックします。 既存のメディア セットへのバックアップの詳細については、「[メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)」を参照してください。  
  
         必要に応じて、 **[メディア セット名とバックアップ セットの有効期限を確認する]** チェック ボックスをオンにします。これにより、バックアップ操作で、メディア セットとバックアップ セットの有効期限が切れる日付と時刻の確認が行われます。  
  
         必要に応じて、 **[メディア セット名]** ボックスに名前を入力します。 名前を指定しなかった場合、空の名前でメディア セットが作成されます。 メディア セット名を指定した場合は、メディア (テープまたはディスク) の実際の名前がここで入力した名前と一致しているかどうかが確認されます。  
  
         メディア名を指定せずに、このチェック ボックスをオンにしてこのメディアを確認するよう指定した場合は、実際のメディア名も空でないとエラーになります。  
  
    -   **[新しいメディア セットにバックアップし、すべての既存のバックアップ セットを消去する]**  
  
         このオプションでは、 **[新しいメディア セット名]** ボックスに名前を入力し、必要に応じて **[新しいメディア セットの説明]** ボックスにメディア セットの説明を入力します。 新しいメディア セットを詳細する方法の詳細については、「[メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)」を参照してください。  
  
14. **[信頼性]** セクションで、必要に応じて以下のチェック ボックスをオンにします。  
  
    -   **[完了時にバックアップを検証する]** 。  
  
    -   **[メディアに書き込む前にチェックサムを行う]** 、および、必要に応じて、 **[チェックサム エラーのまま続行する]** 。 チェックサムの詳細については、「[バックアップ中および復元中に発生する可能性があるメディア エラー &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)」を参照してください。  
  
15. **[全般]** ページの **[バックアップ先]** セクションで、テープ ドライブにバックアップするように指定した場合は、 **[バックアップ後にテープをアンロードする]** チェック ボックスがアクティブになります。 このオプションをオンにすると、 **[アンロードの前にテープを巻き戻す]** オプションが有効になります。  
  
    > [!NOTE]  
    >  **[全般]** ページの **[バックアップの種類]** で、トランザクション ログをバックアップするように指定しなかった場合、 **[トランザクション ログ]** セクションの各オプションは無効になっています。  
  
16. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 以降のバージョンでは、 [バックアップの圧縮](backup-compression-sql-server.md)がサポートされています。 既定では、バックアップが圧縮されるかどうかは、 **backup-compression default** サーバー構成オプションの値によって決まります。 ただし、現在のサーバー レベルの既定の設定にかかわらず、 **[バックアップを圧縮する]** をオンにしてバックアップを圧縮することも、 **[バックアップを圧縮しない]** をオンにして圧縮しないようにすることもできます。  
  
     **現在の backup compression default 値を表示するには**  
  
    -   [backup compression default サーバー構成オプションの表示または構成](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-back-up-files-and-filegroups"></a>ファイルおよびファイル グループをバックアップするには  
  
1.  ファイルまたはファイル グループのバックアップを作成するには、[BACKUP DATABASE <file_or_filegroup>](/sql/t-sql/statements/backup-transact-sql) ステートメントを使用します。 このステートメントでは、少なくとも次の項目を指定する必要があります。  
  
    -   データベース名です。  
  
    -   ファイルまたはファイル グループごとに FILE 句または FILEGROUP 句。  
  
    -   完全バックアップが書き込まれるバックアップ デバイス。  
  
     ファイル バックアップの基本的な [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文は次のとおりです。  
  
     BACKUP DATABASE *database*  
  
     { FILE **=** _logical_file_name_ | FILEGROUP **=** _logical_filegroup_name_ } [ **,** ...*f* ]  
  
     TO *backup_device* [ **,** ...*n* ]  
  
     [ WITH *with_options* [ **,** ...*o* ] ] ;  
  
    |オプション|[説明]|  
    |------------|-----------------|  
    |*database*|トランザクション ログ、データベースの一部、またはデータベース全体をバックアップする場合の、バックアップ元となるデータベースを指定します。|  
    |FILE **=** _logical_file_name_|ファイル バックアップに含めるファイルの論理名を指定します。|  
    |FILEGROUP **=** _logical_filegroup_name_|ファイル バックアップに含めるファイル グループの論理名を指定します。 単純復旧モデルでは、ファイル グループのバックアップは、読み取り専用のファイル グループに対してのみ使用できます。|  
    |[ **,** ...*f* ]|複数のファイルおよびファイル グループを指定できることを示すプレースホルダーです。 ファイルまたはファイル グループの数は無制限です。|  
    |*backup_device* [ **,** ...*n* ]|バックアップ操作に使用する 1 ～ 64 個のバックアップ デバイスの一覧を指定します。 物理バックアップ デバイスを指定したり、対応する論理バックアップ デバイス (既に定義されている場合) を指定したりできます。 物理バックアップ デバイスを指定するには、DISK オプションまたは TAPE オプションを使用します。<br /><br /> { DISK &#124; TAPE } **=** _physical_backup_device_name_<br /><br /> 詳細については、「 [バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md)のインスタンスが動作しているコンピューターにテープ ドライブが装着されている場合のみ使用できます。|  
    |WITH *with_options* [ **,** ...*o* ]|必要に応じて、1 つ以上の追加オプション (DIFFERENTIAL など) を指定します。<br /><br /> 注: ファイルの差分バックアップを行うには、差分のベースとなる完全ファイル バックアップが必要です。 詳細については、「[データベースの差分バックアップの作成 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)」を参照してください。|  
  
2.  完全復旧モデルでは、トランザクション ログもバックアップする必要があります。 ファイルの完全バックアップの完全なセットを使用してデータベースを復元するには、最初のファイル バックアップの先頭から、すべてのファイル バックアップにわたって十分なログ バックアップが必要です。 詳細については、「[トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)」を参照してください.  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、 `Sales` データベースのセカンダリ ファイル グループの 1 つ以上のファイルをバックアップします。 このデータベースでは、完全復旧モデルを使用し、次のセカンダリ ファイル グループが含まれています。  
  
-   `SalesGroup1` ファイルと `SGrp1Fi1` ファイルを含む、 `SGrp1Fi2`という名前のファイル グループ。  
  
-   `SalesGroup2` ファイルと `SGrp2Fi1` ファイルを含む、 `SGrp2Fi2`という名前のファイル グループ。  
  
#### <a name="a-creating-a-file-backup-of-two-files"></a>A. 2 つのファイルのファイル バックアップの作成  
 次の例では、 `SGrp1Fi2` ファイル グループの `SalesGroup1` ファイルと `SGrp2Fi2` ファイル グループの `SalesGroup2` ファイルのみのファイルの差分バックアップを作成します。  
  
```sql  
--Backup the files in the SalesGroup1 secondary filegroup.  
BACKUP DATABASE Sales  
   FILE = 'SGrp1Fi2',   
   FILE = 'SGrp2Fi2'   
   TO DISK = 'G:\SQL Server Backups\Sales\SalesGroup1.bck';  
GO  
```  
  
#### <a name="b-creating-a-full-file-backup-of-the-secondary-filegroups"></a>b. セカンダリ ファイル グループの完全ファイル バックアップを作成する  
 次の例では、両方のセカンダリ ファイル グループ内のすべてのファイルについて、完全ファイル バックアップを作成します。  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck';  
GO  
```  
  
#### <a name="c-creating-a-differential-file-backup-of-the-secondary-filegroups"></a>C. セカンダリ ファイル グループの差分ファイル バックアップを作成する  
 次の例では、両方のセカンダリ ファイル グループ内のすべてのファイルについて、差分ファイル バックアップを作成します。  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck'  
   WITH   
      DIFFERENTIAL;  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
  
`Backup-SqlDatabase` コマンドレットを使用して、`Files` パラメーターの値に `-BackupAction` を指定します。 また、次のいずれかのパラメーターを指定します。  
  
    -   特定のファイルをバックアップするには、`-DatabaseFile`*string*パラメーターを指定します。ここで、 *string*はバックアップする1つ以上のデータベースファイルです。  
  
    -   特定のファイルグループ内のすべてのファイルをバックアップするには、`-DatabaseFileGroup`*string*パラメーターを指定します。 *string*はバックアップする1つ以上のデータベースファイルグループです。  
  
     次の例では、 `MyDB` データベースのセカンダリ ファイル グループである FileGroup1 および FileGroup2 のすべてのファイルの完全ファイル バックアップを作成します。 バックアップは、サーバー インスタンス `Computer\Instance`の既定のバックアップ先に作成されます。  
  
    ```powershell
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Files -DatabaseFileGroup "FileGroup1","FileGroup2"  
    ```  
  
SQL Server PowerShell プロバイダーを設定して使用する方法については、「 [SQL Server PowerShell プロバイダー](../../powershell/sql-server-powershell-provider.md)」を参照してください。
  
## <a name="see-also"></a>参照  
 [バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [バックアップの履歴とヘッダーの情報 &#40;SQL Server&#41;](backup-history-and-header-information-sql-server.md)   
 [データベースのバックアップ &#40;全般ページ&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [データベースのバックアップ &#40;バックアップ オプション ページ&#41;](back-up-database-backup-options-page.md)   
 [ファイルの完全バックアップ &#40;SQL Server&#41;](full-file-backups-sql-server.md)   
 [差分バックアップ &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [ファイルの復元 &#40;完全復旧モデル&#41;](file-restores-full-recovery-model.md)   
 [ファイル復元 &#40;単純復旧モデル&#41;](file-restores-simple-recovery-model.md)  
  
  
