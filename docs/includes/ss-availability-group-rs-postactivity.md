---
ms.openlocfilehash: bf755ccfe5a1a6816129173dcb6ad5050ea5e114
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68213318"
---

## <a name="add-a-database-to-the-availability-group"></a>可用性グループにデータベースを追加する

可用性グループに追加するデータベースが、完全回復モードであり、有効なログ バックアップがあることを確認します。 データベースがテスト データベースまたは新しく作成されたデータベースの場合は、データベース バックアップを実行します。 `db1` という名前のデータベースを作成してバックアップするには、プライマリ SQL Server インスタンスで、次の Transact-SQL スクリプトを実行します。

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1]
   TO DISK = N'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\db1.bak';
```

`db1` という名前のデータベースを `ag1` という名前の可用性グループに追加するには、プライマリ SQL Server レプリカで、次の Transact-SQL スクリプトを実行します。

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>セカンダリ サーバーにデータベースが作成されたことを確認する

`db1` データベースが作成されて同期されているかどうかを確認するには、各セカンダリ SQL Server レプリカで次のクエリを実行します。

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
