---
title: ファイルとファイル グループをバックアップする | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2016
ms.prod: sql
ms.prod_service: backup-restore
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
ms.openlocfilehash: cf87d09eed5b955c1773c46270f25cb0a2d57eaa
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708684"
---
# <a name="back-up-files-and-filegroups"></a>ファイルおよびファイル グループのバックアップ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、または PowerShell を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でファイルとファイル グループをバックアップする方法について説明します。 データベースのサイズやパフォーマンスの要件によりデータベースの完全バックアップが不可能な場合は、代わりに、ファイル バックアップを作成できます。 *ファイル バックアップ* には、1 つ以上のファイル (またはファイル グループ) 内のすべてのデータが含まれます。
  
ファイルのバックアップの詳細については、「 [ファイルの完全バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md) 」および「 [差分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)」を参照してください。  

##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
- BACKUP ステートメントは、明示的または暗黙的なトランザクションでは使用できません。  
  
- 単純復旧モデルでは、読み取りと書き込みが可能なファイルはすべてまとめてバックアップする必要があります。 これにより、データベースを一貫性のある時点に復元できます。 読み取りと書き込みが可能なファイルまたはファイル グループを個別に指定するのではなく、READ_WRITE_FILEGROUPS オプションを使用します。 このオプションにより、読み取りと書き込みが可能なすべてのファイル グループがデータベースにバックアップされます。 READ_WRITE_FILEGROUPS を指定して作成されたファイル グループは、"*部分バックアップ*" と呼ばれます。「[部分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md)」を参照してください。  
  
この機能の制限および制約の詳細については、「 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)」を参照してください。  
  
###  <a name="Recommendations"></a> 推奨事項
  
既定では、バックアップ操作が成功するたびに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログおよびシステム イベント ログにエントリが 1 つ追加されます。 ログを頻繁にバックアップすると、これらの成功メッセージがすぐに蓄積され、他のメッセージを探すのが困難になるほどエラー ログが大きくなることがあります。 そのような場合、これらのエントリに依存するスクリプトがなければ、トレース フラグ 3226 を使用することによってこれらのログ エントリを除外できます。「[トレース フラグ &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)」を参照してください。  

###  <a name="Permissions"></a> Permissions

`BACKUP DATABASE` および `BACKUP LOG` アクセス許可は、既定では、**sysadmin** 固定サーバー ロール、**db_owner** 固定データベース ロール、および **db_backupoperator** 固定データベース ロールのメンバーに与えられます。  
  
 バックアップ デバイスの物理ファイルに対する所有と許可の問題によって、バックアップ操作が妨げられることがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、デバイスに対して読み書きを実行できる必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが実行されているアカウントには書き込み権限が必要です。 ただし、システム テーブルにバックアップ デバイスのエントリを追加する [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)では、ファイル アクセスの権限は確認されません。 バックアップ デバイスの物理ファイルに関するこのような問題は、バックアップや復元が試行され、物理リソースがアクセスされるまで、表面化しない可能性があります。

## <a name="using-sql-server-management-studio"></a>SQL Server Management Studio の使用   
  
1. 適切な [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスへの接続後、オブジェクト エクスプローラーでサーバー名をクリックしてサーバー ツリーを展開します。  
  
1. **[データベース]** を展開します。さらに、そのデータベースに応じて、ユーザー データベースを選択するか、または **[システム データベース]** を展開してシステム データベースを選択します。  
  
1. データベースを右クリックして **[タスク]** をポイントし、 **[バックアップ]** をクリックします。 **[データベースのバックアップ]** ダイアログ ボックスが表示されます。  
  
1. **[データベース]** ボックスの一覧で、適切なデータベース名が表示されていることを確認します。 必要に応じて、このボックスの一覧から別のデータベースを選択することもできます。  
  
1. **[バックアップの種類]** ボックスの一覧の **[完全]** または **[差分]** をクリックします。  
  
1. **[バックアップ コンポーネント]** の **[ファイルとファイル グループ]** をクリックします。  
  
1. **[ファイルおよびファイル グループの選択]** ダイアログ ボックスで、バックアップするファイルおよびファイル グループを選択します。 個別のファイルを 1 つ以上選択できるほか、ファイル グループのチェック ボックスをオンにすると自動的にファイル グループ内のすべてのファイルが選択されます。  
  
1. **[名前]** ボックスに表示された既定のバックアップ セット名をそのまま使用するか、または別のバックアップ セット名を入力します。  
  
1. (省略可能) **[説明]** テキスト ボックスに、バックアップ セットの説明を入力します。  
  
1. バックアップ セットの有効期限を指定します。  
  
    - バックアップ セットが指定の日数後に期限切れになるようにするには、 **[期間指定]** (既定のオプション) をクリックし、セットを作成してからセットが期限切れになるまでの日数を入力します。 0 ～ 99,999 日の値を指定できます。0 日を指定すると、バックアップ セットの有効期限は無期限になります。  
  
         既定値は、 **[サーバーのプロパティ]** ダイアログ ボックス ( **[データベースの設定]** ページ) の **[バックアップ メディアの既定の保有期間 (日)]** オプションで設定されています。 このオプションを表示するには、オブジェクト エクスプローラーでサーバー名を右クリックし、[プロパティ] をクリックします。次に、 **[データベースの設定]** ページをクリックします。  
  
    - バックアップ セットが特定の日付に期限切れになるようにするには、 **[日時指定]** をクリックし、セットの有効期限が切れる日付を入力します。  
  
1. **[ディスク]** または **[テープ]** をクリックして、バックアップ先を選択します。 1 つのメディア セットを含んでいる最大 64 個のディスク ドライブまたはテープ ドライブのパスを選択するには、 **[追加]** をクリックします。 選択したパスは、 **[バックアップ先]** ボックスの一覧に表示されます。  
  
    > [!NOTE]
    > バックアップ先を削除するには、バックアップ先を選択して **[削除]** をクリックします。 バックアップ先の内容を表示するには、バックアップ先を選択して **[内容]** をクリックします。  
  
1. 詳細設定オプションを表示または選択するには、 **[ページの選択]** ペインの **[オプション]** をクリックします。  
  
1. 次のいずれかをクリックして、 **[メディアに上書きします]** オプションを選択します。  
  
    - **[既存のメディア セットにバックアップする]**  
  
         このオプションでは、 **[既存のバックアップ セットに追加する]** または **[既存のすべてのバックアップ セットを上書きする]** をクリックします。 
         
         既存のメディア セットへのバックアップの詳細については、「[メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)」を参照してください。  
  
         - (省略可能) **[メディア セット名とバックアップ セットの有効期限を確認する]** チェック ボックスをオンにします。これにより、バックアップ操作で、メディア セットとバックアップ セットの有効期限が切れる日付と時刻の確認が行われます。  
  
         - (省略可能) **[メディア セット名]** テキスト ボックスに名前を入力します。 名前を指定しなかった場合、空の名前でメディア セットが作成されます。 メディア セット名を指定した場合は、メディア (テープまたはディスク) の実際の名前がここで入力した名前と一致しているかどうかが確認されます。  
  
         メディア名を指定せずに、このチェック ボックスをオンにしてこのメディアを確認するよう指定した場合は、実際のメディア名も空でないとエラーになります。  
  
    - **[新しいメディア セットにバックアップし、すべての既存のバックアップ セットを消去する]**  
  
         このオプションでは、 **[新しいメディア セット名]** ボックスに名前を入力し、必要に応じて **[新しいメディア セットの説明]** ボックスにメディア セットの説明を入力します。
         
         新しいメディア セットを詳細する方法の詳細については、「[メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)」を参照してください。  
  
1. (省略可能) **[信頼性]** セクションで、以下をオンにします。  
  
    - **[完了時にバックアップを検証する]** 。  
  
    - **[メディアに書き込む前にチェックサムを行う]** 、および (必要に応じて) **[Continue on checksum error]\(チェックサム エラーのまま続行する\)** 。
    
         チェックサムの詳細については、「[バックアップ中および復元中に発生する可能性があるメディア エラー &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)」を参照してください。  
  
1. **[全般]** ページの **[バックアップ先]** セクションで、テープ ドライブにバックアップするように指定した場合は、 **[バックアップ後にテープをアンロードする]** チェック ボックスがアクティブになります。 このオプションをオンにすると、 **[アンロードの前にテープを巻き戻す]** オプションが有効になります。  
  
    > [!NOTE]
    > **[全般]** ページの **[バックアップの種類]** で、トランザクション ログをバックアップするように指定しなかった場合、 **[トランザクション ログ]** セクションの各オプションは無効になっています。  
  
1. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 以降のバージョンでは、 [バックアップの圧縮](../../relational-databases/backup-restore/backup-compression-sql-server.md)がサポートされています。 既定では、バックアップが圧縮されるかどうかは、 **[バックアップ圧縮の既定]** サーバー構成オプションの値によって決まります。 ただし、現在のサーバー レベルの既定の設定にかかわらず、 **[バックアップを圧縮する]** をオンにしてバックアップを圧縮することも、 **[バックアップを圧縮しない]** をオンにして圧縮しないようにすることもできます。  
  
     現在の既定のバックアップ圧縮を確認する方法については、「[backup compression default サーバー構成オプションの表示または構成](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)」を参照してください  

## <a name="using-transact-sql"></a>Transact-SQL の使用
  
ファイルまたはファイル グループのバックアップを作成するには、[BACKUP DATABASE <file_or_filegroup>](../../t-sql/statements/backup-transact-sql.md) ステートメントを使用します。 このステートメントでは、少なくとも次の項目を指定する必要があります。  
  
  - データベース名です。  
  
  - ファイルまたはファイル グループごとに FILE 句または FILEGROUP 句。  
  
  - 完全バックアップが書き込まれるバックアップ デバイス。  
  
ファイル バックアップの基本的な [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文は次のとおりです。  
  
  BACKUP DATABASE *database*  
  
  { FILE _=_ *logical_file_name* | FILEGROUP _=_ *logical_filegroup_name* } [ **,** ...*f* ]  
  
  TO *backup_device* [ **,** ...*n* ]  
  
  [ WITH *with_options* [ **,** ...*o* ] ] ;  
  
|オプション|[説明]|  
|------------|-----------------|  
|*database*|トランザクション ログ、データベースの一部、またはデータベース全体をバックアップする場合の、バックアップ元となるデータベースを指定します。|  
|FILE _=_ *logical_file_name*|ファイル バックアップに含めるファイルの論理名を指定します。|  
|FILEGROUP _=_ *logical_filegroup_name*|ファイル バックアップに含めるファイル グループの論理名を指定します。 単純復旧モデルでは、ファイル グループのバックアップは、読み取り専用のファイル グループに対してのみ使用できます。|  
|[ **,** ...*f* ]|複数のファイルおよびファイル グループを指定できることを示すプレースホルダーです。 ファイルまたはファイル グループの数は無制限です。|  
|*backup_device* [ **,** ...*n* ]|バックアップ操作に使用する 1 ～ 64 個のバックアップ デバイスの一覧を指定します。 物理バックアップ デバイスを指定したり、対応する論理バックアップ デバイス (既に定義されている場合) を指定したりできます。 物理バックアップ デバイスを指定するには、DISK オプションまたは TAPE オプションを使用します。<br /><br /> { DISK &#124; TAPE } _=_ *physical_backup_device_name*<br /><br /> 詳細については、「 [バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)」を参照してください。|  
|WITH *with_options* [ **,** ...*o* ]|必要に応じて、1 つ以上の追加オプション (DIFFERENTIAL など) を指定します。 ファイルの差分バックアップを行うには、差分のベースとなる完全ファイル バックアップが必要です。 <br /><br />詳細については、「[データベースの差分バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)」を参照してください。|  
  
完全復旧モデルでは、トランザクション ログもバックアップする必要があります。 ファイルの完全バックアップの完全なセットを使用してデータベースを復元するには、最初のファイル バックアップの先頭から、すべてのファイル バックアップにわたって十分なログ バックアップが必要です。

詳細については、「[トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)」を参照してください。  
  
###  <a name="TsqlExample"></a> 使用例
次の例では、 `Sales` データベースのセカンダリ ファイル グループの 1 つ以上のファイルをバックアップします。 このデータベースでは、完全復旧モデルを使用し、次のセカンダリ ファイル グループが含まれています。  
  
- `SalesGroup1` ファイルと `SGrp1Fi1` ファイルを含む、 `SGrp1Fi2`という名前のファイル グループ。  
  
- `SalesGroup2` ファイルと `SGrp2Fi1` ファイルを含む、 `SGrp2Fi2`という名前のファイル グループ。  
  
#### <a name="a-create-a-file-backup-of-two-files"></a>A. 2 つのファイルのファイル バックアップを作成する  
次の例では、 `SGrp1Fi2` ファイル グループの `SalesGroup1` ファイルと `SGrp2Fi2` ファイル グループの `SalesGroup2` ファイルのみのファイルの差分バックアップを作成します。  
  
```sql  
--Backup the files in the SalesGroup1 secondary filegroup.  
BACKUP DATABASE Sales  
   FILE = 'SGrp1Fi2',   
   FILE = 'SGrp2Fi2'   
   TO DISK = 'G:\SQL Server Backups\Sales\SalesGroup1.bck';  
GO  
```  
  
#### <a name="b-create-a-full-file-backup-of-the-secondary-filegroups"></a>B. セカンダリ ファイル グループの完全ファイル バックアップを作成する  
次の例では、両方のセカンダリ ファイル グループ内のすべてのファイルについて、完全ファイル バックアップを作成します。  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck';  
GO  
```  
  
#### <a name="c-create-a-differential-file-backup-of-the-secondary-filegroups"></a>C. セカンダリ ファイル グループの差分ファイル バックアップを作成する  
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
  
## <a name="PowerShellProcedure"></a> PowerShell の使用

[SQL Server PowerShell プロバイダー](../../relational-databases/scripting/sql-server-powershell-provider.md)を設定して使用します。
  
**Backup-SqlDatabase** コマンドレットを使用して- **BackupAction** パラメーターの値の **ファイル** を指定します。 また、次のいずれかのパラメーターを指定します。  
  
- 特定のファイルをバックアップするには、 _-DatabaseFile_ *String* パラメーターを指定します。*String* はバックアップする 1 つ以上のデータベース ファイルです。  
  
- 特定のファイル グループにあるすべてのファイルを指定するには、 _-DatabaseFileGroup_*String* パラメーターを指定します。*String* は、バックアップする 1 つ以上のデータベース ファイル グループです。  
  
次の例では、 `<myDatabase>` データベースのセカンダリ ファイル グループである FileGroup1 および FileGroup2 のすべてのファイルの完全ファイル バックアップを作成します。 バックアップは、サーバー インスタンス `Computer\Instance`の既定のバックアップ先に作成されます。  

```powershell
Backup-SqlDatabase -ServerInstance Computer\Instance -Database <myDatabase> -BackupAction Files -DatabaseFileGroup "FileGroup1","FileGroup2" 
```
  
## <a name="see-also"></a>参照  
 [バックアップの概要 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [バックアップの履歴とヘッダーの情報 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [データベースのバックアップ &#40;全般ページ&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)   
 [データベースのバックアップ &#40;バックアップ オプション ページ&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)   
 [ファイルの完全バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [差分バックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [ファイル復元 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [ファイル復元 &#40;単純復旧モデル&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)  
