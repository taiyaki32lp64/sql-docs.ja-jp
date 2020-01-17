---
title: トランザクション ログ バックアップの復元 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoretlog.options.f1
- sql12.swb.restoretlog.general.f1
helpviewer_keywords:
- restore log
- backing up transaction logs [SQL Server], restoring
- transaction log backups [SQL Server], restoring
- restoring transaction logs [SQL Server], restoring backups
- transaction log restores [SQL Server], SQL Server Management Studio
ms.assetid: 1de2b888-78a6-4fb2-a647-ba4bf097caf3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a0cfc68f78ae9ca4022abfb59a33d756e82a6f2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62875670"
---
# <a name="restore-a-transaction-log-backup-sql-server"></a>トランザクション ログ バックアップの復元 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して、トランザクション ログ バックアップを復元する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [前提条件](#Prerequisites)  
  
     [Security](#Security)  
  
-   **トランザクション ログ バックアップを復元するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Prerequisites"></a> 前提条件  
  
-   バックアップは、作成された順序で復元する必要があります。 特定のトランザクション ログ バックアップを復元する前に、まず、次に示す以前のバックアップを復元する必要があります。ただし、コミットされていないトランザクションはロールバックしません (WITH NORECOVERY)。  
  
    -   データベース全体のバックアップおよび、特定のトランザクション ログ バックアップの前に行われた差分バックアップがある場合は、最後の差分バックアップ データベースの最新の完全バックアップまたは差分バックアップが作成される前に、データベースが完全復旧モデルまたは一括ログ復旧モデルを使用していた。  
  
    -   データベース全体のバックアップまたは差分バックアップ (差分バックアップを復元する場合) 以降、特定のトランザクション ログ バックアップ以前に行われたすべてのトランザクション ログ バックアップ ログ バックアップが、作成された順序で、ログ チェーンにギャップがないように、適用されている。  
  
         トランザクション ログ バックアップの詳細については、「[トランザクション ログ バックアップ &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)」および「[トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](apply-transaction-log-backups-sql-server.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 RESTORE 権限は、サーバーでメンバーシップ情報を常に確認できるロールに与えられます。 固定データベース ロールのメンバーシップは、データベースがアクセス可能で破損していない場合にのみ確認することができますが、RESTORE の実行時にはデータベースがアクセス可能で損傷していないことが必ずしも保証されないため、 **db_owner** 固定データベース ロールのメンバーには RESTORE 権限は与えられません。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
> [!WARNING]  
>  通常の復元処理では、データ バックアップおよび差分バックアップと共に、 **[データベースの復元]** ダイアログ ボックスでログ バックアップを選択します。  
  
#### <a name="to-restore-a-transaction-log-backup"></a>トランザクション ログ バックアップを復元するには  
  
1.  オブジェクト エクスプローラーで適切な [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[データベース]** を展開します。さらに、そのデータベースに応じて、ユーザー データベースを選択するか、または **[システム データベース]** を展開してシステム データベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** をポイントし、 **[復元]** をポイントします。次に、 **[トランザクション ログ]** をクリックし、 **[トランザクション ログの復元]** ダイアログ ボックスを開きます。  
  
    > [!NOTE]  
    >  **[トランザクション ログ]** がグレーで表示される場合は、最初に完全バックアップまたは差分バックアップを復元する必要があります。 **[データベース]** バックアップ ダイアログ ボックスを使用してください。  
  
4.  **[全般]** ページの **[データベース]** ボックスの一覧で、データベースの名前を選択します。 復元状態のデータベースだけが一覧表示されます。  
  
5.  復元するバックアップ セットの復元元ファイルと場所を指定するには、次のいずれかのオプションをクリックします。  
  
    -   **[データベースの以前のバックアップから]**  
  
         復元するデータベースをドロップダウン リストから選択します。 このリストには、 **msdb** バックアップ履歴に従ってバックアップされたデータベースのみが含まれます。  
  
    -   **[ファイルまたはテープから]**  
  
         参照ボタン ( **[...]** ) をクリックし、 **[バックアップ デバイスの選択]** ダイアログ ボックスを開きます。 **[バックアップ メディアの種類]** ボックスから、デバイスの種類を 1 つ選択します。 **[バックアップ メディア]** ボックスにデバイスを追加するには、 **[追加]** をクリックします。  
  
         **[バックアップ メディア]** ボックスに目的のデバイスを追加したら、 **[OK]** をクリックして、 **[全般]** ページに戻ります。  
  
6.  **[復元するトランザクション ログのバックアップを選択]** グリッドで、復元するバックアップを選択します。 このグリッドには、選択したデータベースで使用できるトランザクション ログ バックアップが一覧表示されます。 ログ バックアップは、データベースの **[最初の LSN]** が **[最後の LSN]** よりも大きい場合にのみ使用できます。 ログ バックアップは、含まれているログ シーケンス番号 (LSN) の順に一覧表示され、この順序で復元する必要があります。  
  
     次の表は、グリッドの列ヘッダーとその値を示しています。  
  
    |[ヘッダー]|値|  
    |------------|-----------|  
    |**[復元]**|チェック ボックスをオンにしたバックアップ セットが復元されます。|  
    |**名前**|バックアップ セットの名前。|  
    |**コンポーネント**|バックアップされるコンポーネント:**データベース**、**ファイル**、または\<空白 > (トランザクション ログ用)。|  
    |**[データベース]**|バックアップ操作に関係するデータベース名。|  
    |**[開始日]**|バックアップ操作の開始日時 (クライアントの地域設定に準拠)。|  
    |**完了日**|バックアップ操作の完了日時 (クライアントの地域設定に準拠)。|  
    |**[最初の LSN]**|バックアップ セット内の先頭のトランザクションのログ シーケンス番号。 ファイル バックアップの場合は空白。|  
    |**[最後の LSN]**|バックアップ セット内の最後のトランザクションのログ シーケンス番号。 ファイル バックアップの場合は空白。|  
    |**チェックポイントの LSN**|バックアップが作成された時点における最新チェックポイントのログ シーケンス番号。|  
    |**全 LSN**|データベース全体の最新バックアップのログ シーケンス番号。|  
    |**[サーバー]**|バックアップ操作を実行したデータベース エンジン インスタンスの名前。|  
    |**[ユーザー名]**|バックアップ操作を実行したユーザーの名前。|  
    |**サイズ**|バックアップ セットのサイズ (バイト単位)。|  
    |**[Position]**|ボリューム内でのバックアップ セットの位置。|  
    |**[有効期限]**|バックアップ セットの期限が切れる日付と時刻。|  
  
7.  次のいずれかを選択します。  
  
    -   **[特定の時点]**  
  
         既定値 ( **[最新の候補]** ) をそのまま使用するか、または参照ボタンをクリックして **[特定の時点に復元]** ダイアログ ボックスを開き、特定の日付と時刻を選択します。  
  
    -   **[マークされたトランザクション]**  
  
         以前にマークされたトランザクションにデータベースを復元します。 このオプションを選択すると、 **[マークされたトランザクションの選択]** ダイアログ ボックスが開いて、選択されたトランザクション ログ バックアップで使用できるマークされたトランザクションの一覧がグリッドに表示されます。  
  
         既定では、マークされたトランザクションの前まで復元され、マークされたトランザクションは復元されません。 マークされたトランザクションも復元するには、 **[マークされたトランザクションを含める]** チェック ボックスをオンにします。  
  
         次の表は、グリッドの列ヘッダーとその値を示しています。  
  
        |[ヘッダー]|値|  
        |------------|-----------|  
        |\<空白>|マークを選択するためのチェック ボックスを表示します。|  
        |**トランザクション マーク**|トランザクションがコミットされたときにユーザーによって指定された、マークされたトランザクションの名前。|  
        |**Date**|トランザクションがコミットされた日時。 トランザクションの日付と時刻は、クライアント コンピューターの日付と時刻ではなく、 **msdbgmarkhistory** テーブルに記録されたとおりに表示されます。|  
        |**[説明]**|トランザクションがコミットされたときにユーザーが指定したマークされたトランザクションの説明 (該当する場合)。|  
        |**LSN (LSN)**|マークされたトランザクションのログ シーケンス番号。|  
        |**[データベース]**|マークされたトランザクションがコミットされたデータベースの名前。|  
        |**[ユーザー名]**|マークされたトランザクションをコミットしたデータベース ユーザーの名前。|  
  
8.  詳細設定オプションを表示または選択するには、 **[ページの選択]** ペインの **[オプション]** をクリックします。  
  
9. **[復元オプション]** セクションには次の選択肢があります。  
  
    -   **[レプリケーションの設定を保存する (WITH KEEP_REPLICATION)]**  
  
         パブリッシュされたデータベースを、そのデータベースが作成されたサーバー以外のサーバーに復元するときに、レプリケーションの設定を保存します。  
  
         このオプションでのみ使用可能な**コミットされていないトランザクションをロールバックして使用できるように、データベースのままにしています.** オプション (後述)、これはバックアップの復元に相当、`RECOVERY`オプション。  
  
         このオプションをオンの場合を使用すると、`KEEP_REPLICATION`オプション、 [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE`ステートメント。  
  
    -   **[各バックアップを復元する前に確認する]**  
  
         このオプションは、各バックアップ セットの復元前 (最初のバックアップ セットでは、その後) に、復元シーケンスを続行するかどうかをたずねる **[復元の続行]** ダイアログ ボックスを表示します。 このダイアログには、次のメディア セットの名前 (使用可能な場合)、バックアップ セット名、およびバックアップ セットの説明が表示されます。  
  
         このオプションは、異なるメディア セットのテープを交換する必要がある場合に特に役立ちます。 たとえば、サーバーにテープ デバイスが 1 台しかない場合に使用できます。 続行する準備ができたら **[OK]** をクリックします。  
  
         **[いいえ]** をクリックすると、データベースは復元状態のままになります。 最後の復元が完了した後、都合のよいときに復元シーケンスを継続できます。 次のバックアップがデータまたは差分バックアップの場合は、 **[データベースの復元]** タスクを再度使用します。 次のバックアップがログ バックアップの場合は、 **[トランザクション ログの復元]** タスクを使用します。  
  
    -   **[復元するデータベースへのアクセスを制限する (WITH RESTRICTED_USER)]**  
  
         復元するデータベースの使用を、 **db_owner**、 **dbcreator**、または **sysadmin**のメンバーだけに制限します。  
  
         このオプションをオンの場合を使用すると、`RESTRICTED_USER`オプション、 [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE`ステートメント。  
  
10. **[復旧状態]** オプションでは、復元操作後のデータベースの状態を指定します。  
  
    -   **[コミットされていないトランザクションをロールバックして、データベースを使用可能な状態にする。別のトランザクション ログは復元できません。(RESTORE WITH RECOVERY)]**  
  
         データベースを復旧します。 このオプションは、`RECOVERY`オプション、 [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE`ステートメント。  
  
         このオプションは、復元するログ ファイルがない場合にのみ選択します。  
  
    -   **[データベースは操作不可状態のままで、コミットされていないトランザクションはロールバックしない。別のトランザクション ログは復元できます。(RESTORE WITH NORECOVERY)]**  
  
         データベースを `RESTORING` 状態で未復旧のままにします。 このオプションを使用すると、`NORECOVERY`オプション、 [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE`ステートメント。  
  
         このオプションを選択した場合は、 **[レプリケーションの設定を保存する]** オプションは使用できません。  
  
        > [!IMPORTANT]  
        >  ミラー データベースまたはセカンダリ データベースの場合は、常にこのオプションを選択します。  
  
    -   **[データベースを読み取り専用モードにする。コミットされていないトランザクションは元に戻されますが、復旧結果を元に戻せるように元に戻す操作をファイルに保存します。(RESTORE WITH STANDBY)]**  
  
         データベースをスタンバイ状態のままにします。 このオプションを使用すると、`STANDBY`オプション、 [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE`ステートメント。  
  
         このオプションを選択した場合は、スタンバイ ファイルを指定する必要があります。  
  
11. 必要に応じて、 **[スタンバイ ファイル]** ボックスで、スタンバイ ファイル名を指定します。 このオプションは、データベースを読み取り専用モードのままにする場合に必要です。 スタンバイ ファイルは参照して指定するか、またはテキスト ボックスにパス名を入力します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
> [!IMPORTANT]  
>  指定があいまいにならないよう、すべての RESTORE ステートメントにおいて WITH NORECOVERY または WITH RECOVERY を常に明示的に指定することをお勧めします。 これは、スクリプトを作成するときに特に重要です。  
  
#### <a name="to-restore-a-transaction-log-backup"></a>トランザクション ログ バックアップを復元するには  
  
1.  次の項目を指定して RESTORE LOG ステートメントを実行し、トランザクション ログ バックアップを適用します。  
  
    -   トランザクション ログが適用されるデータベースの名前。  
  
    -   適用するトランザクション ログ バックアップが格納されているバックアップ デバイス。  
  
    -   NORECOVERY 句。  
  
     このステートメントの基本構文は次のとおりです。  
  
     RESTORE LOG *database_name* FROM <backup_device> WITH NORECOVERY  
  
     *database_name* は、データベース名です。<backup_device> は、復元するログ バックアップを保持するデバイスの名前です。  
  
2.  適用する必要があるトランザクション ログ バックアップごとに、手順 1. を繰り返します。  
  
3.  復元シーケンスの最後のバックアップを復元した後、データベースを復旧するには、次のステートメントのいずれかを使用します。  
  
    -   最後の RESTORE LOG ステートメントの一部としてデータベースを復旧する。  
  
        ```  
        RESTORE LOG <database_name> FROM <backup_device> WITH RECOVERY;  
        GO  
        ```  
  
    -   個別の RESTORE DATABASE ステートメントを使用してデータベースの復旧を待機する。  
  
        ```  
        RESTORE LOG <database_name> FROM <backup_device> WITH NORECOVERY;   
        RESTORE DATABASE <database_name> WITH RECOVERY;  
        GO  
        ```  
  
         データベースの復旧を待機すると、必要なログ バックアップがすべて復元されていることを確認できます。 これは、特定の時点への復元を実行する際の操作として、多くの場合は推奨される方法です。  
  
    > [!IMPORTANT]  
    >  ミラー データベースを作成している場合は、復旧ステップを省略します。 ミラー データベースは、RESTORING 状態のままにする必要があります。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 既定では、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースは単純復旧モデルを使用します。 以下の例では、次に示すように、完全復旧モデルが使用されるようにデータベースを変更する必要があります。  
  
```sql  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
```  
  
#### <a name="a-applying-a-single-transaction-log-backup"></a>A. 1 つのトランザクション ログ バックアップの適用  
 次の例では、まず [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] というバックアップ デバイスに存在するデータベースの完全バックアップを使用して `AdventureWorks2012_1`データベースを復元します。 次に、 `AdventureWorks2012_log`というバックアップ デバイスにある最初のトランザクション ログ バックアップを適用します。 最後に、データベースを復旧します。  
  
```sql  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorks2012_1  
   WITH NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 1,  
   WITH NORECOVERY;  
GO  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
#### <a name="b-applying-multiple-transaction-log-backups"></a>B. 複数のトランザクション ログ バックアップの適用  
 次の例では、まず [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] というバックアップ デバイスに存在するデータベースの完全バックアップを使用して `AdventureWorks2012_1`データベースを復元します。 次に、 `AdventureWorks2012_log`という名前のバックアップ デバイスにある最初の 3 つのトランザクション ログ バックアップを、1 つずつ適用します。 最後に、データベースを復旧します。  
  
```sql  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorks2012_1  
   WITH NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 1,  
   NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 2,  
   WITH NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 3,  
   WITH NORECOVERY;  
GO  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [データベースのバックアップを復元&#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [完全復旧モデルで障害発生時点までデータベースを復元する &#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [SQL Server データベースを特定の時点に復元する &#40;完全復旧モデル&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   [マークされたトランザクションへのデータベースの復元 &#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
## <a name="see-also"></a>参照  
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](apply-transaction-log-backups-sql-server.md)  
  
  
