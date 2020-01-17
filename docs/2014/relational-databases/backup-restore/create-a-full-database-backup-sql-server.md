---
title: データベースの完全バックアップの作成 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d4c750f4230cc83467cc5993d2a6ab571a06d2f5
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798034"
---
# <a name="create-a-full-database-backup-sql-server"></a>データベースの完全バックアップの作成 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、または PowerShell を使用して、データベースの完全バックアップを作成する方法について説明します。  
  
> [!NOTE]  
>  Azure Blob ストレージサービスへの SQL Server のバックアップの詳細については、「」 SQL Server、「 [Azure Blob Storage サービスを使用したバックアップと復元](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」を参照してください。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [推奨事項](#Recommendations)  
  
     [セキュリティ](#Security)  
  
-   **次のものを使用してデータベースの完全バックアップを作成するには:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [PowerShell](#PowerShellProcedure)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   BACKUP ステートメントは、明示的または暗黙的なトランザクションでは使用できません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって作成されたバックアップは、それより前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では復元できません。  
  
-   詳細については、「 [バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)」を参照してください。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   データベース サイズが大きくなると、データベースの完全バックアップにかかる時間は長くなり、必要な記憶領域も増加します。 このため、大きなデータベースの場合は、データベースの完全バックアップを一連の *差分データベース バックアップ*で補完することができます。 詳細については、「[差分バックアップ &#40;SQL Server&#41;](differential-backups-sql-server.md)」を参照してください。  
  
-   データベースの完全バックアップのサイズは、[sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) システム ストアド プロシージャを使用して推計することができます。  
  
-   既定では、バックアップ操作が成功するたびに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログおよびシステム イベント ログにエントリが 1 つ追加されます。 ログを頻繁にバックアップすると、これらの成功メッセージがすぐに蓄積され、他のメッセージを探すのが困難になるほどエラー ログが大きくなることがあります。 そのような場合、これらのエントリに依存するスクリプトがなければ、トレース フラグ 3226 を使用することによってこれらのログ エントリを除外できます。 詳細については、「[トレース フラグ &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
 データベースをバックアップすると、TRUSTWORTHY は OFF に設定されます。 TRUSTWORTHY を ON に設定する方法については「[ALTER DATABASE の SET オプション &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)」を参照してください。  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では、バックアップの作成で `PASSWORD` と `MEDIAPASSWORD` のオプションは廃止されました。 パスワード付きで作成されたバックアップを復元することは、引き続き可能です。  
  
####  <a name="Permissions"></a> アクセス許可  
 BACKUP DATABASE 権限と BACKUP LOG 権限は、既定では、 **sysadmin** 固定サーバー ロール、 **db_owner** 固定データベース ロール、および **db_backupoperator** 固定データベース ロールのメンバーに与えられています。  
  
 バックアップ デバイスの物理ファイルに対する所有と許可の問題によって、バックアップ操作が妨げられることがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、デバイスに対して読み書きを実行できる必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスが実行されているアカウントには書き込み権限が必要です。 ただし、システム テーブルにバックアップ デバイスのエントリを追加する [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)では、ファイル アクセスの権限は確認されません。 バックアップ デバイスの物理ファイルに関するこのような問題は、バックアップや復元が試行され、物理リソースがアクセスされるまで、表面化しない可能性があります。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してバックアップ タスクを指定する場合、[!INCLUDE[tsql](../../includes/tsql-md.md)][スクリプト][ ボタンをクリックしてスクリプトの保存先を選択することにより、対応する ](/sql/t-sql/statements/backup-transact-sql) **BACKUP** スクリプトを生成できます。  
  
#### <a name="to-back-up-a-database"></a>データベースをバックアップするには  
  
1.  オブジェクト エクスプローラーで適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[データベース]** を展開し、目的のデータベースに応じて、任意のユーザー データベースを選択するか、または **[システム データベース]** を展開して任意のシステム データベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** をポイントし、 **[バックアップ]** をクリックします。 **[データベースのバックアップ]** ダイアログ ボックスが表示されます。  
  
4.  [`Database`] ボックスの一覧で、データベース名を確認します。 必要に応じて、このボックスの一覧から別のデータベースを選択することもできます。  
  
5.  どの復旧モデル ( **[FULL]** 、 **[BULK_LOGGED]** 、 **[SIMPLE]** ) でも、データベースのバックアップを実行できます。  
  
6.  **[バックアップの種類]** ボックスの一覧の **[完全]** をクリックします。  
  
     データベースの完全バックアップを作成すると、データベースの差分バックアップを作成できるようになります。詳細については、「[データベースの差分バックアップの作成 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)」を参照してください。  
  
7.  必要に応じて、 **[コピーのみのバックアップ]** を選択して、コピーのみのバックアップを作成します。 *コピーのみのバックアップ*は、従来の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップのシーケンスから独立した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップです。 詳細については、「[コピーのみのバックアップ &#40;SQL Server&#41;](copy-only-backups-sql-server.md)」を参照してください。  
  
    > [!NOTE]  
    >  **[差分]** オプションが選択されている場合、コピーのみのバックアップは作成できません。  
  
8.  **[バックアップコンポーネント]** で、[`Database`] をクリックします。  
  
9. **[名前]** ボックスに表示された既定のバックアップ セット名をそのまま使用するか、または別のバックアップ セット名を入力します。  
  
10. 必要に応じて、 **[説明]** ボックスに、バックアップ セットの説明を入力します。  
  
11. **[ディスク]** 、 **[テープ]** 、または **[URL]** をクリックして、バックアップ先を選択します。 1 つのメディア セットを含んでいる最大 64 個のディスク ドライブまたはテープ ドライブのパスを選択するには、 **[追加]** をクリックします。 選択したパスは、 **[バックアップ先]** ボックスの一覧に表示されます。  
  
     バックアップ先を削除するには、バックアップ先を選択して **[削除]** をクリックします。 バックアップ先の内容を表示するには、バックアップ先を選択して **[内容]** をクリックします。  
  
12. メディア オプションを表示または選択するには、 **[ページの選択]** ペインの **[メディア オプション]** をクリックします。  
  
13. 次のいずれかをクリックして、 **[メディアに上書きします]** オプションを選択します。  
  
    -   **[既存のメディア セットにバックアップする]**  
  
         このオプションでは、 **[既存のバックアップ セットに追加する]** または **[既存のすべてのバックアップ セットを上書きする]** をクリックします。 詳細については、「[メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)」を参照してください。  
  
         必要に応じて、 **[メディア セット名とバックアップ セットの有効期限を確認する]** チェック ボックスをオンにします。これにより、バックアップ操作で、メディア セットとバックアップ セットの有効期限が切れる日付と時刻の確認が行われます。  
  
         必要に応じて、 **[メディア セット名]** ボックスに名前を入力します。 名前を指定しなかった場合、空の名前でメディア セットが作成されます。 メディア セット名を指定した場合は、メディア (テープまたはディスク) の実際の名前がここで入力した名前と一致しているかどうかが確認されます。  
  
        > [!IMPORTANT]  
        >  **[全般]** ページでバックアップ先として **[URL]** を選択した場合、このオプションは無効になります。 詳細については、「[[データベースのバックアップ] &#40;[メディア オプション] ページ&#41;](back-up-database-media-options-page.md)」を参照してください。  
        >   
        >  暗号化を使用する場合は、このオプションを選択しないでください。 このオプションを選択すると、 **[バックアップ オプション]** ページの暗号化オプションが無効になります。 既存のバックアップ セットに追加するときには、暗号化はサポートされません。  
  
    -   **[新しいメディア セットにバックアップし、すべての既存のバックアップ セットを消去する]**  
  
         このオプションでは、 **[新しいメディア セット名]** ボックスに名前を入力し、必要に応じて **[新しいメディア セットの説明]** ボックスにメディア セットの説明を入力します。  
  
        > [!IMPORTANT]  
        >  **[全般]** ページで **[URL]** を選択した場合、このオプションは無効になります。 これらのアクションは、Azure storage へのバックアップ時にはサポートされません。  
  
14. **[信頼性]** セクションで、必要に応じて以下のチェック ボックスをオンにします。  
  
    -   **[完了時にバックアップを検証する]** 。  
  
    -   **[メディアに書き込む前にチェックサムを行う]** 、および、必要に応じて、 **[チェックサム エラーのまま続行する]** 。 チェックサムの詳細については、「[バックアップ中および復元中に発生する可能性があるメディア エラー &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)」をご覧ください。  
  
15. **[全般]** ページの **[バックアップ先]** セクションで、テープ ドライブにバックアップするように指定した場合は、 **[バックアップ後にテープをアンロードする]** チェック ボックスがアクティブになります。 このオプションをオンにすると、 **[アンロードの前にテープを巻き戻す]** オプションがアクティブになります。  
  
    > [!NOTE]  
    >  **[全般]** ページの **[バックアップの種類]** で、トランザクション ログをバックアップするように指定しなかった場合、 **[トランザクション ログ]** セクションの各オプションは無効になっています。  
  
16. バックアップ オプションを表示または選択するには、 **[ページの選択]** ペインの **[バックアップ オプション]** をクリックします。  
  
17. バックアップ セットの有効期限と、有効期限が過ぎたデータを明示的に確認せずに上書きできるかどうかを指定します。  
  
    -   バックアップ セットが指定の日数後に期限切れになるようにするには、 **[期間指定]** (既定のオプション) をクリックし、セットを作成してからセットが期限切れになるまでの日数を入力します。 0 ～ 99,999 日の値を指定できます。0 日を指定すると、バックアップ セットの有効期限は無期限になります。  
  
         既定値は、 **[サーバーのプロパティ]** ダイアログ ボックス ([データベースの設定] ページ) の **[バックアップ メディアの既定の保有期間 (日)]** オプションで設定されています。 このオプションを表示するには、オブジェクト エクスプローラーでサーバー名を右クリックし、[プロパティ] をクリックします。次に、 **[データベースの設定]** ページをクリックします。  
  
    -   バックアップ セットが特定の日付に期限切れになるようにするには、 **[日時指定]** をクリックし、セットの有効期限が切れる日付を入力します。  
  
         バックアップの有効期限の詳細については、「[BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)」を参照してください。  
  
18. [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] 以降では、 [バックアップの圧縮](backup-compression-sql-server.md)がサポートされています。 既定では、バックアップが圧縮されるかどうかは、 **backup-compression default** サーバー構成オプションの値によって決まります。 ただし、現在のサーバー レベルの既定の設定にかかわらず、 **[バックアップを圧縮する]** をオンにしてバックアップを圧縮することも、 **[バックアップを圧縮しない]** をオンにして圧縮しないようにすることもできます。  
  
     **現在のバックアップの圧縮の既定値を表示または変更するには**  
  
    -   [backup compression default サーバー構成オプションの表示または構成](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
19. バックアップに暗号化を使用するかどうかを指定します。 暗号化手順に使用する暗号化アルゴリズムを選択し、既存の証明書または非対称キーの一覧から証明書または非対称キーを指定します。 暗号化は SQL Server 2014 以降でサポートされます。 暗号化オプションの詳細については、「[[データベースのバックアップ] &#40;[バックアップ オプション] ページ&#41;](back-up-database-backup-options-page.md)」を参照してください。  
  
> [!NOTE]  
>  メンテナンス プラン ウィザードを使用して、データベースのバックアップを作成することもできます。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-create-a-full-database-backup"></a>データベースの完全バックアップを作成するには  
  
1.  次の項目を指定した BACKUP DATABASE ステートメントを実行し、データベースの完全バックアップを作成します。  
  
    -   バックアップするデータベースの名前。  
  
    -   データベースの完全バックアップを書き込むバックアップ デバイス。  
  
     データベースの完全バックアップのための [!INCLUDE[tsql](../../includes/tsql-md.md)] の基本構文を次に示します。  
  
     BACKUP DATABASE *database*  
  
     TO *backup_device* [ **,** ...*n* ]  
  
     [ WITH *with_options* [ **,** ...*o* ] ] ;  
  
    |オプション|[説明]|  
    |------------|-----------------|  
    |*database*|バックアップするデータベースです。|  
    |*backup_device* [ **,** ...*n* ]|バックアップ操作に使用する 1 ～ 64 個のバックアップ デバイスの一覧を指定します。 物理バックアップ デバイスを指定したり、対応する論理バックアップ デバイス (既に定義されている場合) を指定したりできます。 物理バックアップ デバイスを指定するには、DISK オプションまたは TAPE オプションを使用します。<br /><br /> { DISK &#124; TAPE } **=** _physical_backup_device_name_<br /><br /> 詳細については、「 [バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md)のインスタンスが動作しているコンピューターにテープ ドライブが装着されている場合のみ使用できます。|  
    |WITH *with_options* [ **,** ...*o* ]|必要に応じて、1 つ以上の追加オプション ( *o*) を指定します。 基本的な with オプションについては、手順 2. を参照してください。|  
  
2.  必要に応じて、1 つ以上の WITH オプションを指定します。 ここでは、一部の基本的な WITH オプションについて説明します。 すべての WITH オプションについては、「 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)」を参照してください。  
  
    -   基本的なバックアップ セット WITH オプション  
  
         { COMPRESSION | NO_COMPRESSION }  
         [!INCLUDE[ssEnterpriseEd10](../../../includes/ssenterpriseed10-md.md)] 以降でのみ、このバックアップで [バックアップの圧縮](backup-compression-sql-server.md) を実行するかどうかを指定し、サーバー レベルの既定値をオーバーライドできます。  
  
         ENCRYPTION (ALGORITHM,  SERVER CERTIFICATE |ASYMMETRIC KEY)  
         SQL Server 2014 以降でのみ、使用する暗号化アルゴリズムと暗号化の保護に使用する証明書または非対称キーを指定します。  
  
         DESCRIPTION **=** { **' *`text`* '**  |  **@** _text_variable_ }  
         バックアップ セットを記述したテキストを自由な形式で指定します。 文字列の長さは最大 255 文字です。  
  
         名前 **=** { *backup_set_name* |  **@** _backup_set_name_var_ }  
         バックアップ セットの名前を指定します。 名前の長さは最大 128 文字です。 NAME を指定しないと、名前は空白になります。  
  
    -   基本的なバックアップ セット WITH オプション  
  
         既定では、BACKUP はバックアップを既存のメディア セットに追加し、既存のバックアップ セットを保持します。 これを明示的に指定するには、NOINIT オプションを使用します。 既存のバックアップ セットへの追加については、「 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)」を参照してください。  
  
         また、FORMAT オプションを使用して、バックアップ メディアをフォーマットすることもできます。  
  
         FORMAT [ **,** MEDIANAME **=** { *media_name* |  **@** _media_name_variable_ } ] [ **,** MEDIADESCRIPTION **=** { *text* |  **@** _text_variable_ } ]  
         FORMAT 句は、バックアップ メディアを初めて使用する場合や既存のデータをすべて上書きする場合に使用します。 必要に応じて、新しいメディアにメディア名と説明を割り当てます。  
  
        > [!IMPORTANT]  
        >  BACKUP ステートメントで FORMAT 句を使用すると、バックアップ メディアに格納されているバックアップが破棄されるので、十分注意して使用してください。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
  
#### <a name="a-backing-up-to-a-disk-device"></a>A. ディスク デバイスへのバックアップ  
 次の例では、新しいメディア セットを作成する [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] を使用して、 `FORMAT` データベース全体をディスクにバックアップします。  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="b-backing-up-to-a-tape-device"></a>b. テープ デバイスへのバックアップ  
 次の例では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]データベース全体をテープにバックアップし、以前のバックアップに追加します。  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="c-backing-up-to-a-logical-tape-device"></a>C. 論理テープ デバイスへのバックアップ  
 次の例では、テープ ドライブ用の論理バックアップ デバイスを作成した後、 作成したデバイスに [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース全体をバックアップします。  
  
```sql  
-- Create a logical backup device,   
-- AdventureWorks2012_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'AdventureWorks2012_Bak_Tape', '\\.\tape0'; USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO AdventureWorks2012_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'AdventureWorks2012_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell の使用  
  
1.  `Backup-SqlDatabase` コマンドレットを使用します。 これがデータベースの完全バックアップであることを明示するには、 **-backupaction**パラメーターに既定値の `Database`を指定します。 このパラメーターは、データベースの完全バックアップでは省略可能です。  
  
     次の例では、 `MyDB` データベースの完全なバックアップを、サーバー インスタンス `Computer\Instance`の既定のバックアップ場所に作成します。 オプションで、`-BackupAction Database` を指定します。  
  
    ```powershell
    Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
    ```  
  
 **SQL Server PowerShell プロバイダーを設定して使用するには**  
  
-   [SQL Server PowerShell プロバイダー](../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データベースのバックアップ (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [データベースの差分バックアップの作成 &#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [データベースバックアップ&#40;の復元 SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [単純復旧モデルでのデータベース バックアップの復元 &#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [完全復旧モデルで障害発生時点までデータベースを復元する &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [データベースを新しい場所に復元する &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
-   [メンテナンス プラン ウィザードの使用](../maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>参照  
 [バックアップの概要 &#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [トランザクション ログのバックアップ &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [データベースのバックアップ &#40;全般ページ&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [データベースのバックアップ &#40;バックアップ オプション ページ&#41;](back-up-database-backup-options-page.md)   
 [差分バックアップ &#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [データベースの完全バックアップ &#40;SQL Server&#41;](full-database-backups-sql-server.md)  
