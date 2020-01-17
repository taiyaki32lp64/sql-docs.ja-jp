---
title: ファイルとファイル グループの復元 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restorefilesandfilegrps.general.f1
- sql13.swb.bselectfilegrpsfiles.f1
- sql13.swb.restorefilesandfilegrps.options.f1
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], restoring files and filegroups
- restoring [SQL Server], files
ms.assetid: 72603b21-3065-4b56-8b01-11b707911b05
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5398b371ea4c969fedf54502d160ebd183cc2bdb
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908858"
---
# <a name="restore-files-and-filegroups-sql-server"></a>ファイルとファイル グループの復元 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でファイルとファイル グループを復元する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
-   [セキュリティ](#Security)  
  
-   **ファイルおよびファイル グループを復元する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   ファイルとファイル グループの復元中は、復元作業を実行するシステム管理者以外は、復元されるデータベースを使用しないでください。  
  
-   RESTORE は、明示的または暗黙的なトランザクションでは使用できません。  
  
-   単純復旧モデルでは、ファイルは読み取り専用のファイル グループに属している必要があります。  
  
-   完全復旧モデルまたは一括ログ復旧モデルを使用する場合は、ファイルを復元する前に、ログの末尾と呼ばれるアクティブ トランザクション ログをバックアップする必要があります。 詳細については、「 [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)でファイルとファイル グループを復元する方法について説明します。  
  
-   暗号化されたデータベースを復元するには、データベースの暗号化に使用された証明書または非対称キーにアクセスできることが必要です。 証明書または非対称キーがないと、データベースは復元できません。 このため、バックアップが必要である間は、データベース暗号化キーの暗号化に使用する証明書を保持しておく必要があります。 詳細については、「 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 復元するデータベースが存在しない場合、ユーザーは RESTORE を実行できる CREATE DATABASE 権限を使用する必要があります。 データベースが存在する場合、既定では、RESTORE 権限は **sysadmin** 固定サーバー ロールおよび **dbcreator** 固定サーバー ロールのメンバーと、データベースの所有者 (**dbo**) に与えられています (FROM DATABASE_SNAPSHOT オプションを使用する場合、データベースは常に存在します)。  
  
 RESTORE 権限は、サーバーでメンバーシップ情報を常に確認できるロールに与えられます。 固定データベース ロールのメンバーシップは、データベースがアクセス可能で破損していない場合にのみ確認することができますが、RESTORE の実行時にはデータベースがアクセス可能で損傷していないことが必ずしも保証されないため、 **db_owner** 固定データベース ロールのメンバーには RESTORE 権限は与えられません。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-restore-files-and-filegroups"></a>ファイルおよびファイル グループを復元するには  
  
1.  オブジェクト エクスプローラーで適切な [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続した後、サーバー名をクリックしてサーバー ツリーを展開します。  
  
2.  **[データベース]** を展開します。 復元するデータベースに応じて、ユーザー データベースを選択するか、 **[システム データベース]** を展開してシステム データベースを選択します。  
  
3.  データベースを右クリックして **[タスク]** をポイントし、 **[復元]** をクリックします。  
  
4.  **[ファイルおよびファイル グループ]** をクリックして **[ファイルおよびファイル グループの復元]** ダイアログ ボックスを開きます。  
  
5.  **[全般]** ページの **[復元先データベース]** ボックスに、復元するデータベースの名前を入力します。 新しいデータベースを入力するか、ドロップダウン リストから既存のデータベースを選択します。 このリストには、システム データベース **master** および **tempdb**を除いた、サーバー上のすべてのデータベースが表示されます。  
  
6.  復元するバックアップ セットの復元元ファイルと場所を指定するには、次のいずれかのオプションをクリックします。  
  
    -   **[復元元データベース]**  
  
         ボックスにデータベース名を入力します。 このリストには、 **msdb** バックアップ履歴に従ってバックアップされたデータベースのみが含まれます。  
  
    -   **[復元元デバイス]**  
  
         参照ボタンをクリックします。 **[バックアップ デバイスの指定]** ダイアログ ボックスで、 **[バックアップ メディアの種類]** ボックスの一覧からいずれかのデバイスの種類を選択します。 **[バックアップ メディア]** ボックスに 1 つまたは複数のデバイスを選択するには、 **[追加]** をクリックします。  
  
         **[バックアップ メディア]** ボックスに目的のデバイスを追加したら、 **[OK]** をクリックして、 **[全般]** ページに戻ります。  
  
7.  **[復元するバックアップ セットの選択]** グリッドで、復元するバックアップを選択します。 このグリッドには、指定された場所に対して使用可能なバックアップが表示されます。 既定では、復旧計画が推奨されています。 推奨された復元計画をオーバーライドするには、グリッドの選択を変更します。 バックアップの選択を解除すると、それに依存するその他のバックアップも自動的に選択が解除されます。  
  
    |列見出し|値|  
    |-----------------|------------|  
    |**[復元]**|このチェック ボックスをオンにすると、バックアップ セットが復元されます。|  
    |**[名前]**|バックアップ セットの名前です。|  
    |**[ファイルの種類]**|バックアップのデータの種類を指定します。**データ**、**ログ**、または **Filestream データ**です。 テーブルに含まれるデータの種類は、 **データ** ファイルです。 トランザクション ログ データの種類は、 **ログ** ファイルです。 ファイル システムに格納されたバイナリ ラージ オブジェクト (BLOB) データの種類は、 **FILESTREAM データ** ファイルです。|  
    |**Type**|実行するバックアップの種類: **[完全]** 、 **[差分]** 、 **[トランザクション ログ]** 。|  
    |**[サーバー]**|バックアップ操作を実行するデータベース エンジン インスタンスの名前です。|  
    |**[ファイルの論理名]**|ファイルの論理名です。|  
    |**[データベース]**|バックアップ操作に呼び出されるデータベース名です。|  
    |**[開始日]**|バックアップ操作が開始した日時で、クライアントの地域設定で表示されます。|  
    |**完了日**|バックアップ操作が完了したときの日付と時刻。クライアントの地域設定で表示されます。|  
    |**[サイズ]**|バックアップ セットのサイズ (バイト単位) です。|  
    |**[ユーザー名]**|バックアップ操作を実行したユーザーの名前。|  
  
8.  詳細設定オプションの表示または選択を行うには、 **[ページの選択]** ペインの **[オプション]** をクリックします。  
  
9. 状況が適切であれば、 **[復元オプション]** パネルでは、次の任意のオプションを選択できます。  
  
     **[ファイル グループとして復元する]**  
     ファイル グループ全体が復元されることを示します。  
  
     **[既存のデータベースを上書きする]**  
     同じ名前を持つ別のデータベースまたはファイルが既に存在していても、復元操作で既存のデータベースおよび関連ファイルを上書きするように指定します。  
  
     このオプションを選択することは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE ステートメントで REPLACE オプションを使用することと同じです。  
  
     **[各バックアップを復元する前に確認する]**  
     各バックアップ セットを復元する前にユーザーに確認します。  
  
     このオプションは、サーバーのテープ デバイスが 1 台であるために、メディア セットごとにテープを入れ替える必要がある場合などに特に便利です。  
  
     **[復元するデータベースへのアクセスを制限する]**  
     復元するデータベースの使用を、 **db_owner**、 **dbcreator**、または **sysadmin**のメンバーだけに制限します。  
  
     このオプションを選択することは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE ステートメントで RESTRICTED_USER オプションを使用することと同じです。  
  
10. 新しい場所にデータベースを復元する場合、必要に応じて、 **[次のデータベース ファイルに復元]** グリッドで各ファイルの新しい復元先を指定できます。  
  
    |列見出し|値|  
    |-----------------|------------|  
    |**[元のファイル名]**|ソース バックアップ ファイルの完全なパスです。|  
    |**[ファイルの種類]**|バックアップのデータの種類を指定します。**データ**、**ログ**、または **Filestream データ**です。 テーブルに含まれるデータの種類は、 **データ** ファイルです。 トランザクション ログ データの種類は、 **ログ** ファイルです。 ファイル システムに格納されたバイナリ ラージ オブジェクト (BLOB) データの種類は、 **FILESTREAM データ** ファイルです。|  
    |**[復元先]**|復元されるデータベース ファイルのフル パスです。 新しい復元ファイルを指定するには、テキスト ボックスをクリックして、指定されているパスおよびファイル名を編集します。 **[復元先]** 列でパスまたはファイル名を変更することは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE ステートメントで MOVE オプションを使用することと同じです。|  
  
11. **[復旧状態]** パネルの選択内容により、復元操作後のデータベースの状態が決まります。  

  **[コミットされていないトランザクションをロールバックして、データベースを使用可能な状態にする。別のトランザクション ログは復元できません。(RESTORE WITH RECOVERY)]**  
  データベースを復旧します。 これは既定の動作です。 このオプションは、必要なすべてのバックアップをすべて復元する場合のみ選択します。 このオプションを選択することは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE ステートメントで WITH RECOVERY を使用することと同じです。  
  
  **データベースは操作不可状態のままで、コミットされていないトランザクションはロールバックしない。別のトランザクション ログは復元できます(RESTORE WITH NORECOVERY)**  
  データベースを復元状態のままにします。 データベースを復旧するには、RESTORE WITH RECOVERY オプションを使用して (上記を参照) 別の復元を実行する必要があります。 このオプションを選択することは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE ステートメントで WITH NORECOVERY を使用することと同じです。  
  
  このオプションを選択すると、 **[レプリケーションの設定を保存する]** オプションを選択できなくなります。  
  
  **[データベースを読み取り専用モードにする。コミットされていないトランザクションはロールバックされますが、復旧結果を元に戻せるようにロールバック操作をファイルに保存します。(RESTORE WITH STANDBY)]**  
  データベースをスタンバイ状態のままにします。 このオプションを選択することは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE ステートメントで WITH STANDBY を使用することと同じです。  
  
  このオプションを選択した場合は、スタンバイ ファイルを指定する必要があります。  
  
  **[ロールバック UNDO ファイル]**  
  **[ロールバック UNDO ファイル]** テキスト ボックスで、スタンバイ ファイル名を指定します。 データベースを読み取り専用モード (RECOVERY WITH STANDBY) にする場合は、このオプションが必要です。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-restore-files-and-filegroups"></a>ファイルおよびファイル グループを復元するには  
  
1.  RESTORE DATABASE ステートメントを実行して、ファイルとファイル グループのバックアップを復元します。そのとき、以下を指定します。  
  
    -   復元するデータベースの名前。  
  
    -   復元するデータベースの完全バックアップが格納されているバックアップ デバイス。  
  
    -   復元する各ファイルに対応する FILE 句。  
  
    -   復元する各ファイル グループに対応する FILEGROUP 句。  
  
    -   NORECOVERY 句。 バックアップ作成後にファイルが変更されていない場合は、RECOVERY 句を指定します。  
  
2.  ファイル バックアップの作成後にファイルが変更された場合は、RESTORE LOG ステートメントを実行して、トランザクション ログ バックアップを適用します。そのとき、以下を指定します。  
  
    -   トランザクション ログが適用されるデータベースの名前。  
  
    -   復元するトランザクション ログのバックアップが格納されているバックアップ デバイス。  
  
    -   NORECOVERY 句。現在のトランザクション ログ バックアップを適用した後、別のバックアップがある場合に指定します。それ以外の場合は RECOVERY 句を指定します。  
  
         トランザクション ログ バックアップを適用する場合、そのバックアップには、ファイルとファイル グループのバックアップが作成された時刻の情報が格納されている必要があります (すべてのデータベース ファイルを復元する場合を除く)。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 この例では、 `MyDatabase` データベースのファイルとファイル グループを復元します。 データベースを現在の時刻に復元するために、2 つのトランザクション ログが適用されます。  
  
```sql  
USE master;  
GO  
-- Restore the files and filesgroups for MyDatabase.  
RESTORE DATABASE MyDatabase  
   FILE = 'MyDatabase_data_1',  
   FILEGROUP = 'new_customers',  
   FILE = 'MyDatabase_data_2',  
   FILEGROUP = 'first_qtr_sales'  
   FROM MyDatabase_1  
   WITH NORECOVERY;  
GO  
-- Apply the first transaction log backup.  
RESTORE LOG MyDatabase  
   FROM MyDatabase_log1  
   WITH NORECOVERY;  
GO  
-- Apply the last transaction log backup.  
RESTORE LOG MyDatabase  
   FROM MyDatabase_log2  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [SSMS を使用してデータベース バックアップを復元する](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [ファイルおよびファイル グループのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [データベースの完全バックアップの作成 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)   
 [トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
