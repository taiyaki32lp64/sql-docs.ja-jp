---
title: 既存のファイルにファイル (およびファイル グループ) を復元する
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring files [SQL Server], how-to topics
- restoring files [SQL Server], steps
- file restores [SQL Server], how-to topics
- filegroups [SQL Server], restoring
- restoring filegroups [SQL Server]
- overwriting filegroups
- overwriting files
ms.assetid: 517e07eb-9685-4b06-90af-b1cc496700b7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a237383f2bc36aa3e3dd1b74174e5fbdd455920a
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241873"
---
# <a name="restore-files-and-filegroups-over-existing-files-sql-server"></a>既存のファイルにファイルとファイル グループを復元する (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]でファイルとファイル グループを既存のファイルに復元する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [セキュリティ](#Security)  
  
-   **ファイルとファイル グループを既存のファイルに復元する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   復元するデータベースは、ファイルとファイル グループの復元作業を行うシステム管理者以外のユーザーによって使用されていない状態にしておく必要があります。  
  
-   RESTORE は、明示的または暗黙的なトランザクションでは使用できません。  
  
-   完全復旧モデルまたは一括ログ復旧モデルを使用する場合は、ファイルを復元する前に、ログの末尾と呼ばれるアクティブ トランザクション ログをバックアップする必要があります。 詳細については、「[トランザクション ログのバックアップ &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)」を参照してください。  
  
-   暗号化されたデータベースを復元するには、データベースの暗号化に使用された証明書または非対称キーにアクセスできることが必要です。 証明書または非対称キーがないと、データベースは復元できません。 このため、バックアップが必要である間は、データベース暗号化キーの暗号化に使用する証明書を保持しておく必要があります。 詳細については、「 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 復元するデータベースが存在しない場合、ユーザーは RESTORE を実行できる CREATE DATABASE 権限を使用する必要があります。 データベースが存在する場合、既定では、RESTORE 権限は **sysadmin** 固定サーバー ロールおよび **dbcreator** 固定サーバー ロールのメンバーと、データベースの所有者 (**dbo**) に与えられています (FROM DATABASE_SNAPSHOT オプションを使用する場合、データベースは常に存在します)。  
  
 RESTORE 権限は、サーバーでメンバーシップ情報を常に確認できるロールに与えられます。 固定データベース ロールのメンバーシップは、データベースがアクセス可能で破損していない場合にのみ確認することができますが、RESTORE の実行時にはデータベースがアクセス可能で損傷していないことが必ずしも保証されないため、 **db_owner** 固定データベース ロールのメンバーには RESTORE 権限は与えられません。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-restore-files-and-filegroups-over-existing-files"></a>ファイルとファイル グループを既存のファイルに復元するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続して、そのインスタンスを展開します。次に、 **[データベース]** を展開します。  
  
2.  目的のデータベースを右クリックし、 **[タスク]** 、 **[復元]** の順にポイントし、 **[ファイルおよびファイル グループ]** をクリックします。  
  
3.  **[全般]** ページの **[復元先データベース]** ボックスに、復元するデータベースの名前を入力します。 新しいデータベースを入力するか、ドロップダウン リストから既存のデータベースを選択します。 このリストには、システム データベース **master** および **tempdb**を除いた、サーバー上のすべてのデータベースが表示されます。  
  
4.  復元するバックアップ セットの復元元ファイルと場所を指定するには、次のいずれかのオプションをクリックします。  
  
    -   **[復元元データベース]**  
  
         ボックスにデータベース名を入力します。 このリストには、 **msdb** バックアップ履歴に従ってバックアップされたデータベースのみが含まれます。  
  
    -   **[復元元デバイス]**  
  
         参照ボタンをクリックします。 **[バックアップ デバイスの指定]** ダイアログ ボックスで、 **[バックアップ メディアの種類]** ボックスの一覧からいずれかのデバイスの種類を選択します。 **[バックアップ メディア]** ボックスに 1 つまたは複数のデバイスを選択するには、 **[追加]** をクリックします。  
  
         **[バックアップ メディア]** ボックスに目的のデバイスを追加したら、 **[OK]** をクリックして、 **[全般]** ページに戻ります。  
  
5.  **[復元するバックアップ セットの選択]** グリッドで、復元するバックアップを選択します。 このグリッドには、指定された場所に対して使用可能なバックアップが表示されます。 既定では、復旧計画が推奨されています。 推奨された復元計画を変更するには、グリッドの選択を変更します。 バックアップの選択を解除すると、それに依存するその他のバックアップも自動的に選択が解除されます。  
  
    |列見出し|値|  
    |-----------------|------------|  
    |**復元**|このチェック ボックスをオンにすると、バックアップ セットが復元されます。|  
    |**Name**|バックアップ セットの名前です。|  
    |**[ファイルの種類]**|バックアップのデータの種類を指定します。**データ**、**ログ**、または **Filestream データ**です。 テーブルに含まれるデータの種類は、 **データ** ファイルです。 トランザクション ログ データの種類は、 **ログ** ファイルです。 ファイル システムに格納されたバイナリ ラージ オブジェクト (BLOB) データの種類は、 **FILESTREAM データ** ファイルです。|  
    |**Type**|実行するバックアップの種類: **[完全]** 、 **[差分]** 、 **[トランザクション ログ]** 。|  
    |**[サーバー]**|バックアップ操作を実行するデータベース エンジン インスタンスの名前です。|  
    |**[ファイルの論理名]**|ファイルの論理名です。|  
    |**[データベース]**|バックアップ操作に呼び出されるデータベース名です。|  
    |**[開始日]**|バックアップ操作が開始した日時で、クライアントの地域設定で表示されます。|  
    |**完了日**|バックアップ操作が完了したときの日付と時刻。クライアントの地域設定で表示されます。|  
    |**[サイズ]**|バックアップ セットのサイズ (バイト単位) です。|  
    |**ユーザー名**|バックアップ操作を実行したユーザーの名前。|  
  
6.  **[ページの選択]** ペインの **[オプション]** ページをクリックします。  
  
7.  **[復元オプション]** パネルで、 **[既存のデータベースを上書きする (WITH REPLACE)]** をクリックします。 同じ名前を持つ別のデータベースまたはファイルが既に存在している場合でも、復元操作は、既存のデータベースおよび関連ファイルを上書きします。  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-restore-files-and-filegroups-over-existing-files"></a>ファイルとファイル グループを既存のファイルに復元するには  
  
1.  RESTORE DATABASE ステートメントを実行して、ファイルとファイル グループのバックアップを復元します。そのとき、以下を指定します。  
  
    -   復元するデータベースの名前。  
  
    -   復元するデータベースの完全バックアップが格納されているバックアップ デバイス。  
  
    -   復元する各ファイルに対応する FILE 句。  
  
    -   復元する各ファイル グループに対応する FILEGROUP 句。  
  
    -   REPLACE オプション。各ファイルを、同じ名前および同じ場所の既存のファイルに復元できるよう指定します。  
  
        > [!CAUTION]  
        >  REPLACE オプションは慎重に使用してください。 詳細については、「」を参照してください。  
  
    -   NORECOVERY オプション。 バックアップ作成後にファイルが変更されていない場合は、RECOVERY 句を指定します。  
  
2.  ファイル バックアップの作成後にファイルが変更された場合は、RESTORE LOG ステートメントを実行して、トランザクション ログ バックアップを適用します。そのとき、以下を指定します。  
  
    -   トランザクション ログが適用されるデータベースの名前。  
  
    -   復元するトランザクション ログのバックアップが格納されているバックアップ デバイス。  
  
    -   NORECOVERY 句。現在のトランザクション ログ バックアップを適用した後、別のバックアップがある場合に指定します。それ以外の場合は RECOVERY 句を指定します。  
  
         トランザクション ログ バックアップを適用する場合、そのバックアップには、ファイルとファイル グループのバックアップが作成された時刻の情報が格納されている必要があります。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、 `MyNwind` データベースのファイルとファイル グループを復元し、同じ名前の既存のファイルを置き換えます。 データベースを現在の時刻に復元するために、2 つのトランザクション ログも適用されます。  
  
```sql  
USE master;  
GO  
-- Restore the files and filesgroups for MyNwind.  
RESTORE DATABASE MyNwind  
   FILE = 'MyNwind_data_1',  
   FILEGROUP = 'new_customers',  
   FILE = 'MyNwind_data_2',  
   FILEGROUP = 'first_qtr_sales'  
   FROM MyNwind_1  
   WITH NORECOVERY,  
   REPLACE;  
GO  
-- Apply the first transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log1  
   WITH NORECOVERY;  
GO  
-- Apply the last transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log2  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [SSMS を使用してデータベース バックアップを復元する](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [ファイルおよびファイル グループの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)   
 [バックアップと復元によるデータベースのコピー](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)  
  
  
