---
title: データベースを新しい場所に復元する (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring databases [SQL Server], moving
- database restores [SQL Server], creating new databases
- restoring [SQL Server], with move
- restoring databases [SQL Server], creating new databases
- database backups [SQL Server], creating new database from
- backing up databases [SQL Server], creating new database from
- restoring databases [SQL Server], renaming
- database creation [SQL Server], restoring with move
ms.assetid: 4da76d61-5e11-4bee-84f5-b305240d9f42
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7a50004cfb39b93ecd0c144fb0d92d37545c83ee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62921181"
---
# <a name="restore-a-database-to-a-new-location-sql-server"></a>データベースを新しい場所に復元する (SQL Server)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で [!INCLUDE[tsql](../../includes/tsql-md.md)]データベースを新しい場所に復元し、必要に応じてデータベースの名前を変更する方法について説明します。 新しいディレクトリ パスにデータベースを移動できるほか、同じサーバー インスタンスまたは別のサーバー インスタンスにデータベースのコピーを作成できます。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [前提条件](#Prerequisites)  
  
     [推奨事項](#Recommendations)  
  
     [Security](#Security)  
  
-   **データベースを新しい場所に復元して、必要に応じて、データベースの名前を変更するを使用します。**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 作業を開始する準備  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   データベースの完全バックアップの復元中は、復元作業を実行するシステム管理者以外は、復元中のデータベースを使用しないでください。  
  
###  <a name="Prerequisites"></a> 前提条件  
  
-   完全復旧モデルまたは一括ログ復旧モデルを使用する場合は、データベースを復元する前に、アクティブ トランザクション ログをバックアップする必要があります。 詳細については、「[トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)」を参照してください。  
  
###  <a name="Recommendations"></a> 推奨事項  
  
-   暗号化されたデータベースを復元するには、データベースの暗号化に使用された証明書または非対称キーにアクセスできることが必要です。 証明書または非対称キーがないと、データベースは復元できません。 このため、バックアップが必要である間は、データベース暗号化キーの暗号化に使用する証明書を保持しておく必要があります。 詳細については、「 [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md)」を参照してください。  
  
-   データベースの移行に関するその他の考慮事項については、「[バックアップと復元によるデータベースのコピー](../databases/copy-databases-with-backup-and-restore.md)」を参照してください。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のデータベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] に復元すると、データベースが自動的にアップグレードされます。 通常、データベースは直ちに使用可能になります。 ただし、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースにフルテキスト インデックスがある場合、アップグレード プロセスでは、  **upgrade_option** サーバー プロパティの設定に応じて、インポート、リセット、または再構築が行われます。 アップグレード オプションがインポート (**upgrade_option** = 2) または再構築 (**upgrade_option** = 0) に設定されている場合、アップグレード中はフルテキスト インデックスを使用できなくなります。 インデックスを作成するデータ量によって、インポートには数時間、再構築には最大でその 10 倍の時間がかかることがあります。 また、アップグレード オプションがインポートに設定されており、フルテキスト カタログが使用できない場合は、関連付けられたフルテキスト インデックスが再構築されます。 **upgrade_option** サーバー プロパティの設定を変更するには、 [sp_fulltext_service](/sql/relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql)を使用します。  
  
###  <a name="Security"></a> セキュリティ  
 セキュリティを確保するため、不明なソースや信頼されていないソースからのデータベースは、アタッチまたは復元しないことをお勧めします。 こうしたデータベースには、意図しない [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを実行したり、スキーマまたは物理データベース構造を変更してエラーを発生させるような、悪意のあるコードが含まれている可能性があります。 不明または信頼できないソースのデータベースを使用する前に、運用サーバー以外のサーバーでそのデータベースに対し [DBCC CHECKDB](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) を実行し、さらに、そのデータベースのストアド プロシージャやその他のユーザー定義コードなどのコードを調べます。  
  
####  <a name="Permissions"></a> Permissions  
 復元するデータベースが存在しない場合、ユーザーは RESTORE を実行できる CREATE DATABASE 権限を使用する必要があります。 データベースが存在する場合、既定では、RESTORE 権限は **sysadmin** 固定サーバー ロールおよび **dbcreator** 固定サーバー ロールのメンバーと、データベースの所有者 (**dbo**) に与えられています。  
  
 RESTORE 権限は、サーバーでメンバーシップ情報を常に確認できるロールに与えられます。 固定データベース ロールのメンバーシップは、データベースがアクセス可能で破損していない場合にのみ確認することができますが、RESTORE の実行時にはデータベースがアクセス可能で損傷していないことが必ずしも保証されないため、 **db_owner** 固定データベース ロールのメンバーには RESTORE 権限は与えられません。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-restore-a-database-to-a-new-location-and-optionally-rename-the-database"></a>新しい場所にデータベースを復元し、必要に応じて名前を変更するには  
  
1.  適切な [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、オブジェクト エクスプローラーでサーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[データベース]** を右クリックし、 **[データベースの復元]** をクリックします。 **[データベースの復元]** ダイアログ ボックスが表示されます。  
  
3.  **[全般]** ページの **復元元**のセクションを使用して、復元するバックアップ セットの復元元ファイルと場所を指定します。 以下のオプションの 1 つを選択します。  
  
    -   **[データベース]**  
  
         復元するデータベースをドロップダウン リストから選択します。 このリストには、 **msdb** バックアップ履歴に従ってバックアップされたデータベースのみが含まれます。  
  
    > [!NOTE]  
    >  別のサーバーで作成されたバックアップの場合、復元先のサーバーには指定されたデータベースのバックアップ履歴情報が存在しません。 この場合、 **[デバイス]** をクリックして、復元するファイルまたはデバイスを手動で指定します。  
  
    1.  **[デバイス]**  
  
         参照ボタン ( **[...]** ) をクリックし、 **[バックアップ デバイスの選択]** ダイアログ ボックスを開きます。 **[バックアップ メディアの種類]** ボックスから、デバイスの種類を 1 つ選択します。 **[バックアップ メディア]** ボックスにデバイスを追加するには、 **[追加]** をクリックします。  
  
         **[バックアップ メディア]** ボックスに目的のデバイスを追加したら、 **[OK]** をクリックして、 **[全般]** ページに戻ります。  
  
         **[ソース: デバイス: データベース]** リスト ボックスで、復元するデータベースの名前を選択します。  
  
         **メモ** この一覧は **[デバイス]** をクリックした場合にのみ使用できます。 選択されたデバイスにバックアップを持つデータベースのみが使用できるようになります。  
  
4.  **復元先のセクション**の **[データベース]** ボックスに、復元するデータベースの名前が自動的に表示されます。 データベースの名前を変更するには、 **[データベース]** ボックスに新しい名前を入力します。  
  
5.  **[復元先]** ボックスで、既定値の **[最後に作成されたバックアップ]** のままにするか、 **[タイムライン]** をクリックして、 **[バックアップのタイムライン]** ダイアログ ボックスにアクセスし、具体的にどの時点で復旧アクションを停止するかを手動で選択します。 特定の時点を指定する方法の詳細については、「 [Backup Timeline](backup-timeline.md) 」を参照してください。  
  
6.  **[復元するバックアップ セット]** グリッドで、復元するバックアップを選択します。 このグリッドには、指定された場所に対して使用可能なバックアップが表示されます。 既定では、復旧計画が推奨されています。 推奨された復元計画を変更するには、グリッドの選択を変更します。 以前のバックアップの選択を解除すると、以前のバックアップの復元に依存するバックアップは自動的に選択が解除されます。  
  
     **[復元するバックアップ セット]** グリッドの列の詳細については、「[データベースの復元 &#40;[全般] ページ&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)」を参照してください。  
  
7.  データベース ファイルの新しい場所を指定するには、 **[ファイル]** ページを選択し、 **[すべてのファイルをフォルダーに移動する]** をクリックします。 **[データ ファイルのフォルダー]** および **[ログ ファイルのフォルダー]** の新しい場所を指定します。 このグリッドの詳細については、「[データベースの復元 &#40;[ファイル] ページ&#41;](restore-database-files-page.md)」を参照してください。  
  
8.  **[オプション]** ページで必要に応じてオプションを調整します。 これらのオプションの詳細については、「[データベースの復元 &#40;[オプション] ページ&#41;](restore-database-options-page.md)」を参照してください。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-restore-a-database-to-a-new-location-and-optionally-rename-the-database"></a>新しい場所にデータベースを復元し、必要に応じて名前を変更するには  
  
1.  必要に応じて、復元するデータベースの完全バックアップを含んでいるバックアップ セット内のファイルの論理名と物理名を判断します。 このステートメントは、バックアップ セットに保存されているデータベースとログ ファイルのリストを返します。 基本構文は次のとおりです。  
  
     RESTORE FILELISTONLY FROM *<backup_device>* WITH FILE = *backup_set_file_number*  
  
     この *backup_set_file_number* は、メディア セット内のバックアップの位置を示します。 バックアップ セットの位置は、 [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql) ステートメントを使用して取得できます。 詳細については、「[RESTORE の引数 &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)」の「バックアップ セットの指定」を参照してください。  
  
     このステートメントは、多くの WITH オプションもサポートします。 詳細については、[RESTORE FILELISTONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql) を参照してください。  
  
2.  [RESTORE DATABASE](/sql/t-sql/statements/restore-statements-transact-sql) ステートメントを使用し、データベースの完全バックアップを復元します。 既定で、データとログ ファイルが元の場所に復元されます。 データベースを再配置するには、MOVE オプションを使用して、各データベース ファイルを再配置し、既存ファイルとの衝突が発生するのを防ぎます。  
  
     データベースを新しい場所と新しい名前に復元するための基本的な [!INCLUDE[tsql](../../includes/tsql-md.md)] 構文は以下のとおりです。  
  
     RESTORE DATABASE *new_database_name*  
  
     FROM *backup_device* [ ,...*n* ]  
  
     [ WITH  
  
     {  
  
     [ **RECOVERY** | NORECOVERY ]  
  
     [ , ] [ FILE ={ *backup_set_file_number* | @*backup_set_file_number* } ]  
  
     [ , ] MOVE '*logical_file_name_in_backup*' TO '*operating_system_file_name*' [ ,...*n* ]  
  
     }  
  
     ;  
  
    > [!NOTE]  
    >  データベースを別のディスクに再配置する準備をする場合は、容量が十分あるかどうか、および既存のファイルと衝突する可能性がないかどうかを確認してください。 この作業は、 [RESTORE VERIFYONLY](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql) ステートメントを使用して、RESTORE DATABASE ステートメントで使用するのと同じ MOVE パラメーターを指定する必要があります。  
  
     次の表で、データベースを新しい場所に復元するという点で、この RESTORE ステートメントの引数を説明します。 これらの引数の詳細については、「 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)データベースを新しい場所に復元し、必要に応じてデータベースの名前を変更する方法について説明します。  
  
     *new_database_name*  
     データベースの新しい名前。  
  
    > [!NOTE]  
    >  異なるサーバー インスタンスにデータベースを復元している場合は、新しい名前ではなく元のデータベース名を使用することができます。  
  
     *backup_device* [ `,`...*n* ]  
     データベース バックアップを復元する 1 ～ 64 個のバックアップ デバイスのコンマ区切りリストを指定します。 物理バックアップ デバイスを指定したり、対応する論理バックアップ デバイス (定義されている場合) を指定したりできます。 物理バックアップ デバイスを指定するには、DISK オプションまたは TAPE オプションを使用します。  
  
     { DISK | TAPE } `=`*physical_backup_device_name*  
  
     詳細については、「 [バックアップ デバイス &#40;SQL Server&#41;](backup-devices-sql-server.md)の別のインスタンスで作成された場合、これは必須です。  
  
     { **RECOVERY** | NORECOVERY }  
     データベースで完全復旧モデルを使用している場合は、データベースの復元後にトランザクション ログ バックアップを適用しなければならない場合があります。 この場合は、NORECOVERY オプションを指定します。  
  
     そうでない場合は、既定の RECOVERY オプションを使用します。  
  
     FILE = { *backup_set_file_number* | @*backup_set_file_number* }  
     復元するバックアップ セットを特定します。 たとえば、 *1* の **backup_set_file_number** は、バックアップ 目での最初のバックアップ セットを示し、2 の *backup_set_file_number* は **2** 番目のバックアップ セットを示します。 バックアップ セットの *backup_set_file_number* を取得するには、 [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql) ステートメントを使用します。  
  
     このオプションを指定しない場合、既定ではバックアップ デバイスの 1 番目のバックアップ セットを使用します。  
  
     詳細については、「[RESTORE の引数 &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)」の「バックアップ セットの指定」を参照してください。  
  
     MOVE **' *`logical_file_name_in_backup`* '** TO **' *`operating_system_file_name`* '** [ `,`...*n* ]  
     *logical_file_name_in_backup* で指定されるデータまたはログ ファイルが、 *operating_system_file_name*で指定される位置に復元されることを指定します。 バックアップ セットから新しい位置に復元する論理ファイルごとに、MOVE ステートメントを指定してください。  
  
    |オプション|Description|  
    |------------|-----------------|  
    |*logical_file_name_in_backup*|バックアップ セット内のデータまたはログ ファイルの論理名を指定します。 バックアップ セット内のデータ ファイルまたはログ ファイルの論理ファイル名は、バックアップ セットが作成されたときのデータベース内における論理名と同じです。<br /><br /> 注:バックアップ セットに含まれる論理ファイルの一覧を取得するには、[RESTORE FILELISTONLY](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql) を使用します。|  
    |*operating_system_file_name*|*logical_file_name_in_backup*で指定したファイルの新しい場所を指定します。 ファイルはこの場所に復元されます。<br /><br /> 必要に応じて、 *operating_system_file_name* に復元するファイルの新しいファイル名を指定します。 これは、同じサーバー インスタンスで既存のデータベースのコピーを作成する場合に必要です。|  
    |*n*|追加の MOVE ステートメントを指定できることを示すプレースホルダーです。|  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 この例では、 `MyAdvWorks` サンプル データベースのバックアップを復元して、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] という名前の新しいデータベースを作成します。このデータベースには、2 つのファイル、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Data と [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]_Log が含まれます。 このデータベースは、単純復旧モデルを使用しています。 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースはサーバー インスタンスに既に存在するため、バックアップ内のファイルを新しい場所に復元する必要があります。 RESTORE FILELISTONLY ステートメントは、復元するデータベース内のファイル数と名前を判断するために使用します。 データベース バックアップは、バックアップ デバイスの 1 番目のバックアップ セットです。  
  
> [!NOTE]  
>  特定日時への復元を含む、トランザクション ログのバックアップと復元の例では、次の `MyAdvWorks_FullRM` の例と同様、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] から作成した `MyAdvWorks` データベースを使用します。 ただし、作成された `MyAdvWorks_FullRM` データベースは、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使って、完全復旧モデルを使用するように変更する必要があります:ALTER DATABASE <データベース名> SET RECOVERY FULL。  
  
```sql  
USE master;  
GO  
-- First determine the number and names of the files in the backup.  
-- AdventureWorks2012_Backup is the name of the backup device.  
RESTORE FILELISTONLY  
   FROM AdventureWorks2012_Backup;  
-- Restore the files for MyAdvWorks.  
RESTORE DATABASE MyAdvWorks  
   FROM AdventureWorks2012_Backup  
   WITH RECOVERY,  
   MOVE 'AdventureWorks2012_Data' TO 'D:\MyData\MyAdvWorks_Data.mdf',   
   MOVE 'AdventureWorks2012_Log' TO 'F:\MyLog\MyAdvWorks_Log.ldf';  
GO  
  
```  
  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースの完全データベース バックアップを作成する方法の例については、「[データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データベースの完全バックアップの作成 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [データベースのバックアップを復元&#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
## <a name="see-also"></a>参照  
 [データベースを別のサーバー インスタンスで使用できるようにするときのメタデータの管理 &#40;SQL Server&#41;](../databases/manage-metadata-when-making-a-database-available-on-another-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [バックアップと復元によるデータベースのコピー](../databases/copy-databases-with-backup-and-restore.md)  
  
  
