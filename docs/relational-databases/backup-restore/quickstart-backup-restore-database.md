---
title: クイック スタート:データベースのバックアップと復元
titleSuffix: SQL Server
description: このクイックスタートでは、オンプレミスの SQL Server データベースをバックアップおよび復元する方法について説明します。
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: backup-restore
ms.prod_service: backup-restore
ms.assetid: ''
ms.openlocfilehash: 97993d621de9b10d930feb2fc54f53bc83f00293
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258639"
---
# <a name="quickstart-backup-and-restore-a-sql-server-database-on-premises"></a>クイック スタート:SQL Server データベースのオンプレミスでのバックアップと復元
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

このクイック スタートでは、新しいデータベースを作成し、その単純なバックアップを取得して復元します。 

詳細な方法については、「[データベースの完全バックアップの作成](create-a-full-database-backup-sql-server.md)」と「[SSMS を使用してデータベース バックアップを復元する](restore-a-database-backup-using-ssms.md)」を参照してください。

## <a name="prerequisites"></a>前提条件
このクイック スタートを完了するには、次のものが必要です。 

- [SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads)
- [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)

## <a name="create-a-test-database"></a>テスト データベースを作成する 

1. [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md) を起動し、SQL Server インスタンスに接続します。
1. **[新しいクエリ]** ウィンドウを開きます。 
1. 次の Transact-SQL (T-SQL) コードを実行して、テスト データベースを作成します。 新しいデータベースを表示するには、**オブジェクト エクスプローラー**の **[データベース]** ノードを最新の情報に更新します。 

```sql
USE [master]
GO

CREATE DATABASE [SQLTestDB]
GO

USE [SQLTestDB]
GO
CREATE TABLE SQLTest (
    ID INT NOT NULL PRIMARY KEY,
    c1 VARCHAR(100) NOT NULL,
    dt1 DATETIME NOT NULL DEFAULT getdate()
)
GO


USE [SQLTestDB]
GO

INSERT INTO SQLTest (ID, c1) VALUES (1, 'test1')
INSERT INTO SQLTest (ID, c1) VALUES (2, 'test2')
INSERT INTO SQLTest (ID, c1) VALUES (3, 'test3')
INSERT INTO SQLTest (ID, c1) VALUES (4, 'test4')
INSERT INTO SQLTest (ID, c1) VALUES (5, 'test5')
GO

SELECT * FROM SQLTest
GO
```
 
## <a name="take-a-backup"></a>バックアップを取得する
データベースのバックアップを取得するには、次の操作を行います。 

1. [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md) を起動し、SQL Server インスタンスに接続します。
1. **オブジェクト エクスプローラー**で、 **[データベース]** ノードを展開します。  
1. データベースを右クリックし、 **[タスク]** にポインターを合わせ、 **[バックアップ]** を選択します。 
1. **[同期先]** の下の、バックアップのパスが正しいことを確認します。 これを変更する必要がある場合は、 **[削除]** を選択して既存のパスを削除してから、 **[追加]** で新しいパスを入力します。 省略記号を使用すると、特定のファイルに移動できます。 
1. **[OK]** を選択すると、データベースのバックアップが取得されます。 

![SQL のバックアップを取得する](media/quickstart-backup-restore-database/backup-db-ssms.png)

次の Transact-SQL コマンドを実行してデータベースをバックアップすることもできます。 

```sql
BACKUP DATABASE [SQLTestDB] 
TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\SQLTestDB.bak' 
WITH NOFORMAT, NOINIT,  
NAME = N'SQLTestDB-Full Database Backup', SKIP, NOREWIND, NOUNLOAD,  STATS = 10
GO
```


## <a name="restore-a-backup"></a>バックアップを復元する
データベースを復元するには、次の操作を行います。 

1. [SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md) を起動し、SQL Server インスタンスに接続します。
1. **オブジェクト エクスプローラー**の **[データベース]** ノードを右クリックして、 **[データベースの復元]** をクリックします。

    ![データベースを復元する](media/quickstart-backup-restore-database/restore-db-ssms1.png)

1. **[デバイス]** を選択し、省略記号 (...) を選択してバックアップ ファイルを探します。 
1. **[追加]** を選択して `.bak` ファイルが配置されている場所に移動します。 `.bak` ファイルを選択して、 **[OK]** を選択します。 
1. **[OK]** を選択すると **[バックアップ デバイスの選択]** ダイアログ ボックスが閉じます。 
1. **[OK]** を選択すると、データベースのバックアップが復元されます。 

    ![データベースを復元する](media/quickstart-backup-restore-database/restore-db-ssms2.png)

次の Transact-SQL スクリプトを実行してデータベースを復元することもできます。

```sql
USE [master]
RESTORE DATABASE [SQLTestDB] 
FROM DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\SQLTestDB.bak' WITH  FILE = 1,  NOUNLOAD,  STATS = 5
GO
```

### <a name="clean-up-resources"></a>リソースをクリーンアップする
次の Transact-SQL コマンドを実行すると、作成したデータベースが MSDB データベースにあるバックアップ履歴とともに削除されます。

```sql
EXEC msdb.dbo.sp_delete_database_backuphistory @database_name = N'SQLTestDB'
GO

USE [master]
DROP DATABASE [SQLTestDB]
GO
```

## <a name="see-more"></a>詳細情報
[バックアップと復元の概要](back-up-and-restore-of-sql-server-databases.md)
[URL へのバックアップ](sql-server-backup-to-url.md)
[完全バックアップの作成](create-a-full-database-backup-sql-server.md)
[データベース バックアップの復元](restore-a-database-backup-using-ssms.md)
