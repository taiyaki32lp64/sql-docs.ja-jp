---
title: 新しい場所へのファイルの復元 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring files [SQL Server], how-to topics
- restoring databases [SQL Server], moving
- restoring files [SQL Server], steps
- file restores [SQL Server], how-to topics
- filegroups [SQL Server], restoring
- restoring filegroups [SQL Server]
ms.assetid: b4f4791d-646e-4632-9980-baae9cb1aade
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b30322bb48cfff6e0bca092d72aa9d5ad0990948
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62875070"
---
# <a name="restore-files-to-a-new-location-sql-server"></a>新しい場所へのファイルの復元 (SQL Server)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] または [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して、 [!INCLUDE[tsql](../../includes/tsql-md.md)]で新しい場所にファイルを復元する方法について説明します。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **ファイルを新しい場所に復元する方法:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   ファイルの復元中は、復元作業を実行するシステム管理者以外は、復元されるデータベースを使用しないでください。  
  
-   RESTORE は、明示的または暗黙的なトランザクションでは使用できません。  
  
-   完全復旧モデルまたは一括ログ復旧モデルを使用する場合は、ファイルを復元する前に、ログの末尾と呼ばれるアクティブ トランザクション ログをバックアップする必要があります。 詳細については、「 [トランザクション ログのバックアップ &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)でファイルとファイル グループを復元する方法について説明します。  
  
-   暗号化されたデータベースを復元するには、データベースの暗号化に使用された証明書または非対称キーにアクセスできることが必要です。 証明書または非対称キーがないと、データベースは復元できません。 このため、バックアップが必要である間は、データベース暗号化キーの暗号化に使用する証明書を保持しておく必要があります。 詳細については、「 [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md)」を参照してください。  
  
###  <a name="Security"></a> セキュリティ  
  
####  <a name="Permissions"></a> Permissions  
 復元するデータベースが存在しない場合、ユーザーは RESTORE を実行できる CREATE DATABASE 権限を使用する必要があります。 データベースが存在する場合、既定では、RESTORE 権限は **sysadmin** 固定サーバー ロールおよび **dbcreator** 固定サーバー ロールのメンバーと、データベースの所有者 (**dbo**) に与えられています (FROM DATABASE_SNAPSHOT オプションを使用する場合、データベースは常に存在します)。  
  
 RESTORE 権限は、サーバーでメンバーシップ情報を常に確認できるロールに与えられます。 固定データベース ロールのメンバーシップは、データベースがアクセス可能で破損していない場合にのみ確認することができますが、RESTORE の実行時にはデータベースがアクセス可能で損傷していないことが必ずしも保証されないため、 **db_owner** 固定データベース ロールのメンバーには RESTORE 権限は与えられません。  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-restore-files-to-a-new-location"></a>ファイルを新しい場所に復元するには  
  
1.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]のインスタンスに接続して、そのインスタンスを展開します。次に、 **[データベース]** を展開します。  
  
2.  目的のデータベースを右クリックし、 **[タスク]** 、 **[復元]** の順にポイントし、 **[ファイルおよびファイル グループ]** をクリックします。  
  
3.  **[全般]** ページの **[復元先データベース]** ボックスに、復元するデータベースの名前を入力します。 新しいデータベースを入力するか、ドロップダウン リストから既存のデータベースを選択します。 このリストには、システム データベース **master** および **tempdb**を除いた、サーバー上のすべてのデータベースが表示されます。  
  
4.  復元するバックアップ セットの復元元ファイルと場所を指定するには、次のいずれかのオプションをクリックします。  
  
    -   **[復元元データベース]**  
  
         ボックスにデータベース名を入力します。 このリストには、 **msdb** バックアップ履歴に従ってバックアップされたデータベースのみが含まれます。  
  
    -   **[復元元デバイス]**  
  
         参照ボタンをクリックします。 **[バックアップ デバイスの指定]** ダイアログ ボックスで、 **[バックアップ メディアの種類]** ボックスの一覧からいずれかのデバイスの種類を選択します。 **[バックアップ メディア]** ボックスに 1 つまたは複数のデバイスを選択するには、 **[追加]** をクリックします。  
  
         **[バックアップ メディア]** ボックスに目的のデバイスを追加したら、 **[OK]** をクリックして、 **[全般]** ページに戻ります。  
  
5.  **[復元するバックアップ セットの選択]** グリッドで、復元するバックアップを選択します。 このグリッドには、指定された場所に対して使用可能なバックアップが表示されます。 既定では、復旧計画が推奨されています。 推奨された復元計画をオーバーライドするには、グリッドの選択を変更します。 バックアップの選択を解除すると、それに依存するその他のバックアップも自動的に選択が解除されます。  
  
    |列見出し|値|  
    |-----------------|------------|  
    |**[復元]**|このチェック ボックスをオンにすると、バックアップ セットが復元されます。|  
    |**名前**|バックアップ セットの名前です。|  
    |**[ファイルの種類]**|バックアップでは、データの種類を指定します。**データ**、**ログ**、または**Filestream データ**します。 テーブルに含まれるデータの種類は、 **データ** ファイルです。 トランザクション ログ データの種類は、 **ログ** ファイルです。 ファイル システムに格納されたバイナリ ラージ オブジェクト (BLOB) データの種類は、 **FILESTREAM データ** ファイルです。|  
    |**型**|実行するバックアップの種類: **[完全]** 、 **[差分]** 、 **[トランザクション ログ]** 。|  
    |**[サーバー]**|バックアップ操作を実行するデータベース エンジン インスタンスの名前です。|  
    |**[ファイルの論理名]**|ファイルの論理名です。|  
    |**[データベース]**|バックアップ操作に呼び出されるデータベース名です。|  
    |**[開始日]**|バックアップ操作が開始した日時で、クライアントの地域設定で表示されます。|  
    |**完了日**|バックアップ操作が完了したときの日付と時刻。クライアントの地域設定で表示されます。|  
    |**Size**|バックアップ セットのサイズ (バイト単位) です。|  
    |**[ユーザー名]**|バックアップ操作を実行したユーザーの名前。|  
  
6.  **[ページの選択]** ペインの **[オプション]** ページをクリックします。  
  
7.  **[次のデータベース ファイルに復元]** グリッドに、移動するファイルの新しい場所を指定します。  
  
    |列見出し|値|  
    |-----------------|------------|  
    |**[元のファイル名]**|ソース バックアップ ファイルの完全なパスです。|  
    |**[ファイルの種類]**|バックアップでは、データの種類を指定します。**データ**、**ログ**、または**Filestream データ**します。 テーブルに含まれるデータの種類は、 **データ** ファイルです。 トランザクション ログ データの種類は、 **ログ** ファイルです。 ファイル システムに格納されたバイナリ ラージ オブジェクト (BLOB) データの種類は、 **FILESTREAM データ** ファイルです。|  
    |**[復元先]**|復元されるデータベース ファイルのフル パスです。 新しい復元ファイルを指定するには、テキスト ボックスをクリックして、指定されているパスおよびファイル名を編集します。 **[復元先]** 列でパスまたはファイル名を変更することは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] RESTORE ステートメントで MOVE オプションを使用することと同じです。|  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-restore-files-to-a-new-location"></a>ファイルを新しい場所に復元するには  
  
1.  必要に応じて、RESTORE FILELISTONLY ステートメントを実行し、データベースの完全バックアップ内のファイル数とファイル名を特定します。  
  
2.  次の項目を指定した RESTORE DATABASE ステートメントを実行し、データベースの完全バックアップを復元します。  
  
    -   復元するデータベースの名前。  
  
    -   復元するデータベースの完全バックアップが格納されているバックアップ デバイス。  
  
    -   新しい場所に復元するファイルごとの MOVE 句。  
  
    -   NORECOVERY 句。  
  
3.  ファイル バックアップの作成後にファイルが変更された場合は、RESTORE LOG ステートメントを実行して、トランザクション ログ バックアップを適用します。そのとき、以下を指定します。  
  
    -   トランザクション ログが適用されるデータベースの名前。  
  
    -   復元するトランザクション ログのバックアップが格納されているバックアップ デバイス。  
  
    -   NORECOVERY 句。現在のトランザクション ログ バックアップを適用した後、別のバックアップがある場合に指定します。それ以外の場合は RECOVERY 句を指定します。  
  
         トランザクション ログ バックアップを適用する場合、そのバックアップには、ファイルとファイル グループのバックアップが作成された時刻の情報が格納されている必要があります。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 この例では、元は C ドライブに配置されていた `MyNwind` データベースの 2 つのファイルを D ドライブ上の新しい場所に復元します。データベースを現在の時刻に復元するために、2 つのトランザクション ログも適用されます。 `RESTORE FILELISTONLY` ステートメントは、復元するデータベース内のファイルの数、論理名、および物理名をするために使用します。  
  
```sql  
USE master;  
GO  
-- First determine the number and names of the files in the backup.  
RESTORE FILELISTONLY  
   FROM MyNwind_1;  
-- Restore the files for MyNwind.  
RESTORE DATABASE MyNwind  
   FROM MyNwind_1  
   WITH NORECOVERY,  
   MOVE 'MyNwind_data_1' TO 'D:\MyData\MyNwind_data_1.mdf',   
   MOVE 'MyNwind_data_2' TO 'D:\MyData\MyNwind_data_2.ndf';  
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
 [データベースのバックアップを復元&#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [バックアップと復元によるデータベースのコピー](../databases/copy-databases-with-backup-and-restore.md)   
 [ファイルおよびファイル グループの復元 &#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
  
