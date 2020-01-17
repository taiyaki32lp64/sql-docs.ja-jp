---
title: メモリ最適化テーブルを持つデータベースの段階的な部分復元 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 732c9721-8dd4-481d-8ff9-1feaaa63f84f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3c9ee00a81dd64ea1fa6093eaccc8d9b96e0aa59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62806694"
---
# <a name="piecemeal-restore-of-databases-with-memory-optimized-tables"></a>メモリ最適化テーブルを持つデータベースの段階的な部分復元
  段階的な部分復元は、次に説明する 1 つの制限を除き、メモリ最適化テーブルを持つデータベースでサポートされています。 段階的なバックアップと部分復元の詳細については、「[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)」および「 [段階的な部分復元 &#40;SQL Server&#41;](../backup-restore/piecemeal-restores-sql-server.md)」を参照してください。  
  
 メモリ最適化ファイル グループは、プライマリ ファイル グループと共にバックアップおよび復元する必要があります。  
  
-   プライマリ ファイル グループをバックアップ (または復元) するときは、メモリ最適化ファイル グループを指定する必要があります。  
  
-   メモリ最適化ファイル グループをバックアップ (または復元) するときは、プライマリ ファイル グループを指定する必要があります。  
  
 段階的なバックアップと部分復元に関する主要なシナリオは、次のとおりです。  
  
-   段階的なバックアップを使用すると、バックアップのサイズを小さくすることができます。 いくつかの例を挙げます。  
  
    -   異なる時刻または日にデータベースのバックアップを実行するように構成し、ワークロードに及ぼす影響を最小限に抑えます。 1 つの例は、割り当てられるデータベースのメンテナンス時間内にデータベースの完全バックアップを完了することができない、非常に大規模なデータベース (1 TB 以上) です。 この状況では、段階的なバックアップを使用し、データベース全体を分割して複数の段階的なバックアップの対象にすることができます。  
  
    -   ファイル グループに読み取り専用のマークが付けられている場合は、読み取り専用というマークを付けられた時点より後のトランザクション ログをバックアップする必要はありません。 読み取り専用というマークが付けられた後、そのファイル グループを 1 回だけバックアップする方針を選択することができます。  
  
-   段階的な部分復元  
  
    -   段階的な部分復元の目標は、すべてのデータを待つことなく、データベースの重要な部分のみをオンライン状態にすることです。 1 つの例は、データベース内にパーティション化されたデータが存在していて、古いパーティションはほとんど使用されていない状況です。 そのようなパーティションは、必要な場合のみ復元することができます。 同様に、履歴データを含むファイル グループもこれに似ています。  
  
    -   ページ修復機能を使用して、特定のページを復元することにより、ページ破損を修正することもできます。 詳細については、「[ページ復元 &#40;SQL Server&#41;](../backup-restore/restore-pages-sql-server.md)」を参照してください。  
  
## <a name="samples"></a>サンプル  
 次の例では、以下のスキーマを使用します。  
  
```  
CREATE DATABASE imoltp  
ON PRIMARY (name = imoltp_primary1, filename = 'c:\data\imoltp_data1.mdf')  
LOG ON (name = imoltp_log, filename = 'c:\data\imoltp_log.ldf')  
GO  
  
ALTER DATABASE imoltp ADD FILE (name = imoltp_primary2, filename = 'c:\data\imoltp_data2.ndf')  
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_secondary  
ALTER DATABASE imoltp ADD FILE (name = imoltp_secondary, filename = 'c:\data\imoltp_secondary.ndf') TO FILEGROUP imoltp_secondary  
GO  
  
ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod   
ALTER DATABASE imoltp ADD FILE (name='imoltp_mod2', filename='c:\data\imoltp_mod2') TO FILEGROUP imoltp_mod   
GO  
```  
  
### <a name="backup"></a>バックアップ  
 このサンプルでは、プライマリ ファイル グループとメモリ最適化ファイル グループをバックアップする方法を示します。 プライマリ ファイル グループとメモリ最適化ファイル グループの両方を共に指定する必要があります。  
  
```  
backup database imoltp filegroup='primary', filegroup='imoltp_mod' to disk='c:\data\imoltp.dmp' with init  
```  
  
 次のサンプルでは、プライマリ ファイル グループとメモリ最適化ファイル グループのどちらでもないファイル グループのバックアップが、メモリ最適化テーブルの存在しないデータベースを操作する状況に似ていることを示します。 次のコマンドを使用して、セカンダリ ファイル グループをバックアップします。  
  
```  
backup database imoltp filegroup='imoltp_secondary' to disk='c:\data\imoltp_secondary.dmp' with init  
```  
  
### <a name="restore"></a>[復元]  
 次のサンプルでは、プライマリ ファイル グループとメモリ最適化ファイル グループを共に復元する方法を示します。  
  
```  
restore database imoltp filegroup = 'primary', filegroup = 'imoltp_mod'   
from disk='c:\data\imoltp.dmp' with partial, norecovery  
  
--restore the transaction log  
 RESTORE LOG [imoltp] FROM DISK = N'c:\data\imoltp_log.dmp' WITH  FILE = 1,  NOUNLOAD,  STATS = 10  
GO  
```  
  
 次のサンプルでは、プライマリ ファイル グループとメモリ最適化ファイル グループのどちらでもないファイル グループの復元が、メモリ最適化テーブルの存在しないデータベースを操作する状況に似ていることを示します。  
  
```  
RESTORE DATABASE [imoltp] FILE = N'imoltp_secondary'   
FROM  DISK = N'c:\data\imoltp_secondary.dmp' WITH  FILE = 1,  RECOVERY,  NOUNLOAD,  STATS = 10  
GO  
```  
  
## <a name="see-also"></a>参照  
 [メモリ最適化テーブルのバックアップ、復元、復旧](../../database-engine/backup-restore-and-recovery-of-memory-optimized-tables.md)  
  
  
