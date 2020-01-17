---
title: データベースの段階的な部分復元 - メモリ最適化テーブル
ms.custom: seo-dt-2019
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 732c9721-8dd4-481d-8ff9-1feaaa63f84f
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a546e2aeceb60e42f4fc9dc8b1170431fd581ef3
ms.sourcegitcommit: 384e7eeb0020e17a018ef8087970038aabdd9bb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2019
ms.locfileid: "74412579"
---
# <a name="piecemeal-restore-of-databases-with-memory-optimized-tables"></a>メモリ最適化テーブルを持つデータベースの段階的な部分復元

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  段階的な部分復元は、次に説明する 1 つの制限を除き、メモリ最適化テーブルを持つデータベースでサポートされています。 段階的なバックアップと部分復元の詳細については、「[RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)」および「 [段階的な部分復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)」を参照してください。  
  
 メモリ最適化ファイル グループは、プライマリ ファイル グループと共にバックアップおよび復元する必要があります。  
  
-   プライマリ ファイル グループをバックアップ (または復元) するときは、メモリ最適化ファイル グループを指定する必要があります。  
  
-   メモリ最適化ファイル グループをバックアップ (または復元) するときは、プライマリ ファイル グループを指定する必要があります。  
  
 段階的なバックアップと部分復元に関する主要なシナリオは、次のとおりです。  
  
-   段階的なバックアップを使用すると、バックアップのサイズを小さくすることができます。 次に例をいくつか示します。  
  
    -   異なる時刻または日にデータベースのバックアップを実行するように構成し、ワークロードに及ぼす影響を最小限に抑えます。 1 つの例は、割り当てられるデータベースのメンテナンス時間内にデータベースの完全バックアップを完了することができない、非常に大規模なデータベース (1 TB 以上) です。 この状況では、段階的なバックアップを使用し、データベース全体を分割して複数の段階的なバックアップの対象にすることができます。  
  
    -   ファイル グループに読み取り専用のマークが付けられている場合は、読み取り専用というマークを付けられた時点より後のトランザクション ログをバックアップする必要はありません。 読み取り専用というマークが付けられた後、そのファイル グループを 1 回だけバックアップする方針を選択することができます。  
  
-   段階的な部分復元  
  
    -   段階的な部分復元の目標は、すべてのデータを待つことなく、データベースの重要な部分のみをオンライン状態にすることです。 1 つの例は、データベース内にパーティション化されたデータが存在していて、古いパーティションはほとんど使用されていない状況です。 そのようなパーティションは、必要な場合のみ復元することができます。 同様に、履歴データを含むファイル グループもこれに似ています。  
  
    -   ページ修復機能を使用して、特定のページを復元することにより、ページ破損を修正することもできます。 詳細については、「[ページ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)」を参照してください。  
  
## <a name="samples"></a>サンプル  
 次の例では、以下のスキーマを使用します。  
  
```sql
CREATE DATABASE imoltp
    ON PRIMARY (
        name = imoltp_primary1,
        filename = 'c:\data\imoltp_data1.mdf')
    LOG ON (
        name = imoltp_log,
        filename = 'c:\data\imoltp_log.ldf');
    GO  
  
ALTER DATABASE imoltp
    ADD FILE (
        name = imoltp_primary2,
        filename = 'c:\data\imoltp_data2.ndf');
GO  
  
ALTER DATABASE imoltp
    ADD FILEGROUP imoltp_secondary;

ALTER DATABASE imoltp
    ADD FILE (
        name = imoltp_secondary,
        filename = 'c:\data\imoltp_secondary.ndf')
            TO FILEGROUP imoltp_secondary;
GO  
  
ALTER DATABASE imoltp
    ADD FILEGROUP imoltp_mod
    CONTAINS MEMORY_OPTIMIZED_DATA;

ALTER DATABASE imoltp
    ADD FILE (
        name = 'imoltp_mod1',
        filename = 'c:\data\imoltp_mod1')
            TO FILEGROUP imoltp_mod;

ALTER DATABASE imoltp
    ADD FILE (
        name = 'imoltp_mod2',
        filename = 'c:\data\imoltp_mod2')
            TO FILEGROUP imoltp_mod;
GO  
```  
  
### <a name="backup"></a>バックアップ  
 このサンプルでは、プライマリ ファイル グループとメモリ最適化ファイル グループをバックアップする方法を示します。 プライマリ ファイル グループとメモリ最適化ファイル グループの両方を共に指定する必要があります。  
  
```sql
BACKUP database imoltp
    filegroup = 'primary',
    filegroup = 'imoltp_mod'
    to disk = 'c:\data\imoltp.dmp'
    with init;
```
  
 次のサンプルでは、プライマリ ファイル グループとメモリ最適化ファイル グループのどちらでもないファイル グループのバックアップが、メモリ最適化テーブルの存在しないデータベースを操作する状況に似ていることを示します。 次のコマンドを使用すると、セカンダリ ファイル グループがバックアップされます  
  
```sql
BACKUP database imoltp
    filegroup = 'imoltp_secondary'
    to disk = 'c:\data\imoltp_secondary.dmp'
    with init;
```
  
### <a name="restore"></a>[復元]  
 次のサンプルでは、プライマリ ファイル グループとメモリ最適化ファイル グループを共に復元する方法を示します。  

```sql
RESTORE database imoltp
    filegroup = 'primary',
    filegroup = 'imoltp_mod'
    from disk = 'c:\data\imoltp.dmp'
    with
        partial,
        norecovery;

-- Restore the transaction log.

RESTORE LOG [imoltp]
    FROM DISK = N'c:\data\imoltp_log.dmp'
    WITH
        FILE = 1,
        NOUNLOAD,
        STATS = 10;
GO
```
  
 次のサンプルでは、プライマリ ファイル グループとメモリ最適化ファイル グループのどちらでもないファイル グループの復元が、メモリ最適化テーブルの存在しないデータベースを操作する状況に似ていることを示します。  
  
```sql
RESTORE DATABASE [imoltp]
    FILE = N'imoltp_secondary'
    FROM DISK = N'c:\data\imoltp_secondary.dmp'
    WITH
        FILE = 1,
        RECOVERY,
        NOUNLOAD,
        STATS = 10;
GO
```

## <a name="see-also"></a>参照  
 [メモリ最適化テーブルのバックアップ、復元、復旧](https://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  

