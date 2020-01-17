---
title: メモリ最適化テーブルを持つデータベースのリソース プールへのバインド | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f222b1d5-d2fa-4269-8294-4575a0e78636
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d64b5bf6b60f37bf386840031c304dd5b13faaeb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63158802"
---
# <a name="bind-a-database-with-memory-optimized-tables-to-a-resource-pool"></a>メモリ最適化テーブルを持つデータベースのリソース プールへのバインド
  リソース プールは、管理できる物理リソースのサブセットを表します。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースは既定のリソース プールにバインドされてリソースを使用します。 1 つ以上のメモリ最適化テーブルによって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のリソースが消費されたり、メモリ最適化テーブルに必要なメモリが他のメモリ ユーザーによって消費されたりするのを防ぐために、別のリソース プールを作成して、メモリ最適化テーブルを持つデータベースのメモリ消費量を管理することをお勧めします。  
  
 1 つのデータベースをバインドできるのは、1 つのリソース プールだけです。 ただし、同じプールに複数のデータベースをバインドすることは可能です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、メモリ最適化テーブルを持たないデータベースをリソース プールにバインドすることはできますが、バインドしても何も効果はありません。 将来的にデータベースにメモリ最適化テーブルを作成する可能性がある場合は、データベースを名前付きリソース プールにバインドすることができます。  
  
 データベースをリソース プールにバインドするには、事前にデータベースとリソース プールの両方が存在している必要があります。 バインドは、データベースが次にオンラインになったときに有効になります。 詳細については、「 [データベースの状態](../databases/database-states.md) 」を参照してください。  
  
 リソース プールについては、「 [リソース ガバナー リソース プール](../resource-governor/resource-governor-resource-pool.md)」を参照してください。  
  
  
## <a name="create-the-database-and-resource-pool"></a>データベースとリソース プールを作成する  
 データベースとリソース プールは、任意の順序で作成できます。 重要なのは、データベースをリソース プールにバインドする前に、両方が存在することです。  
  
### <a name="create-the-database"></a>データベースの作成  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] は、IMOLTP_DB という名前のデータベースを作成します。このデータベースに、1 つ以上のメモリ最適化テーブルを格納します。 パス \<driveAndPath> は、このコマンドを実行する前に存在している必要があります。  
  
```sql  
CREATE DATABASE IMOLTP_DB  
GO  
ALTER DATABASE IMOLTP_DB ADD FILEGROUP IMOLTP_DB_fg CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP_DB ADD FILE( NAME = 'IMOLTP_DB_fg' , FILENAME = 'c:\data\IMOLTP_DB_fg') TO FILEGROUP IMOLTP_DB_fg;  
GO  
```  
  
### <a name="determine-the-minimum-value-for-minmemorypercent-and-maxmemorypercent"></a>MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT の最小値の決定  
 メモリ最適化テーブルに必要なメモリを確認したら、使用可能なメモリの何パーセントが必要になるかを特定し、メモリの割合をその値以上に設定する必要があります。  
  
 **例:**    
この例では、計算の結果、メモリ最適化テーブルおよびインデックスに 16 GB のメモリが必要であると確認されたものとします。 また、使用できるメモリとして 32 GB がコミットされていると想定します。  
  
 一見すると、MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT は 50 (16 は 32 の 50%) に設定する必要があるように思われます。  しかし、それではメモリ最適化テーブルに十分なメモリが与えられません。 後に示す表 (「[メモリ最適化テーブルおよびインデックスで使用可能なメモリの割合](#percent-of-memory-available-for-memory-optimized-tables-and-indexes)」) によると、コミットされたメモリが 32 GB の場合、メモリ最適化テーブルとインデックスで使用できるのはその 80% だけです。  このため、最小と最大の割合は、コミットされたメモリではなく使用可能なメモリに基づいて計算します。  
  
 `memoryNeedeed = 16`   
 `memoryCommitted = 32`   
 `availablePercent = 0.8`   
 `memoryAvailable = memoryCommitted * availablePercent`   
 `percentNeeded = memoryNeeded / memoryAvailable`  
  
 実際の数値の算出:   
`percentNeeded = 16 / (32 * 0.8) = 16 / 25.6 = 0.625`  
  
 したがって、メモリ最適化テーブルとインデックスに 16 GB という要件を満たすには、使用可能なメモリの少なくとも 62.5% が必要です。  MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT の値は整数にする必要があるため、少なくとも 63% として設定します。  
  
### <a name="create-a-resource-pool-and-configure-memory"></a>リソース プールの作成とメモリの構成  
 メモリ最適化テーブルのメモリを構成するときは、MAX_MEMORY_PERCENT ではなく MIN_MEMORY_PERCENT に基づいてキャパシティ プランニングを実施する必要があります。  MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT については、「[ALTER RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-pool-transact-sql)」を参照してください。 この結果、メモリ最適化テーブルが使用できるメモリをより適切に予測することができます。MIN_MEMORY_PERCENT を指定すると、他のリソース プールにメモリの制約を加えて、この値に応じたメモリが確保されるためです。 メモリを確実に使用できるようにし、さらにメモリ不足が発生しないようにするには、MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT を同じ値にします。 コミットされたメモリの量に対してメモリ最適化テーブルで使用できるメモリの割合については、後の「 [メモリ最適化テーブルおよびインデックスで使用可能なメモリの割合](#percent-of-memory-available-for-memory-optimized-tables-and-indexes) 」をご覧ください。  
  
 参照してください[ベスト プラクティス。VM 環境でのインメモリ OLTP を使用して](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)詳細については、VM 環境で作業する場合。  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コードでは、使用可能なメモリを 50% に指定して、Pool_IMOLTP という名前のリソース プールを作成します。  プールが作成された後、Pool_IMOLTP が含まれるようにリソース ガバナーが再構成されます。  
  
```sql  
-- set MIN_MEMORY_PERCENT and MAX_MEMORY_PERCENT to the same value  
CREATE RESOURCE POOL Pool_IMOLTP   
  WITH   
    ( MIN_MEMORY_PERCENT = 63,   
    MAX_MEMORY_PERCENT = 63 );  
GO  
  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="bind-the-database-to-the-pool"></a>データベースをプールにバインドする  
 システム関数 `sp_xtp_bind_db_resource_pool` を使用して、データベースをリソース プールにバインドします。 この関数は、パラメーターとしてデータベース名とリソース プール名を受け取ります。  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] では、リソース プール Pool_IMOLTP へのデータベース IMOLTP_DB のバインドを定義しています。 このバインドは、データベースをオンラインにするまで有効になりません。  
  
```sql  
EXEC sp_xtp_bind_db_resource_pool 'IMOLTP_DB', 'Pool_IMOLTP'  
GO  
```  
  
 システム関数 sp_xtp_bind_db_resourece_pool は、2 つの文字列パラメーター (database_name と pool_name) を受け取ります。  
  
## <a name="confirm-the-binding"></a>バインドを確認する  
 バインドを確認します。このとき、IMOLTP_DB のリソース プール ID に注意してください。 NULL にすることはできません。  
  
```sql  
SELECT d.database_id, d.name, d.resource_pool_id  
FROM sys.databases d  
GO  
```  
  
## <a name="make-the-binding-effective"></a>バインドを有効にする  
 バインドを有効にするには、リソース プールにバインドした後で、データベースをいったんオフラインにしてからオンラインに戻す必要があります。 データベースが以前に別のプールにバインドされていた場合は、これによって以前のリソース プールから割り当て済みのメモリが削除され、新しくデータベースにバインドされたリソース プールから、メモリ最適化テーブルおよびインデックス用のメモリが割り当てられます。  
  
```sql  
USE master  
GO  
  
ALTER DATABASE IMOLTP_DB SET OFFLINE  
GO  
ALTER DATABASE IMOLTP_DB SET ONLINE  
GO  
  
USE IMOLTP_DB  
GO  
```  
  
 これで、データベースがリソース プールにバインドされました。  
  
## <a name="change-min-memory-percent-and-max-memory-percent-on-an-existing-pool"></a>最小メモリの割合と、既存のプールの最大メモリの割合を変更します。  
 サーバーにメモリを追加した場合や、メモリ最適化テーブルに必要なメモリの量が変わった場合は、MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT の値を変更する必要があることがあります。 次の手順では、リソース プールで MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT の値を変更する方法を示します。 MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT に使用する値については、以下のセクションをご覧ください。  トピックを参照して[ベスト プラクティス。VM 環境でのインメモリ OLTP を使用して](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)詳細についてはします。  
  
1.  `ALTER RESOURCE POOL` を使用して MIN_MEMORY_PERCENT と MAX_MEMORY_PERCENT の両方の値を変更します。  
  
2.  新しい値を使用してリソース ガバナーを再構成するには、 `ALTER RESURCE GOVERNOR` を使用します。  
  
 **サンプル コード**  
  
```sql  
ALTER RESOURCE POOL Pool_IMOLTP  
WITH  
     ( MIN_MEMORY_PERCENT = 70,  
       MAX_MEMORY_PERCENT = 70 )   
GO  
  
-- reconfigure the Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
## <a name="percent-of-memory-available-for-memory-optimized-tables-and-indexes"></a>メモリ最適化テーブルおよびインデックスで使用可能なメモリの割合  
 メモリ最適化テーブルを持つデータベースと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ワークロードを同じリソース プールにマップした場合は、プールのユーザー間でプール使用に関する競合が生じないように、リソース ガバナーによって [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 用の内部しきい値が設定されます。 一般に、 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 用のしきい値はプールの約 80% です。 さまざまなメモリ サイズに対する実際のしきい値を次の表に示します。  
  
 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] データベースの専用リソース プールを作成するときは、行のバージョンとデータの増加を確認した後で、インメモリ テーブルに必要な物理メモリ量を推定する必要があります。 必要なメモリ量を推定したら、DMV の `sys.dm_os_sys_info` の列 "committed_target_kb" を反映する SQL インスタンスのコミット ターゲット メモリの割合でリソース プールを作成します ([sys.dm_os_sys_info](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql) を参照)。 たとえば、インスタンスで使用できる合計メモリ量の 40% を含むリソース プール P1 を作成できます。 この 40% から、 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] エンジンは [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] データを格納するためにこれより少ない割合のメモリを取得します。  この処理は、 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] がこのプールのすべてのメモリを消費しないようにするために行います。  この少ない割合の値は、ターゲットのコミット済みメモリによって異なります。 次の表に、OOM のエラーが発生する前にリソース プール (既定または名前付き) の [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] データベースに使用可能なメモリを示します。  
  
|ターゲットのコミット済みメモリ|インメモリ テーブルで使用可能な割合|  
|-----------------------------|---------------------------------------------|  
|<= 8 GB|70%|  
|<= 16 GB|75%|  
|<= 32 GB|80%|  
|\<= 96 GB|85%|  
|>96 GB|90%|  
  
 たとえば、"ターゲットのコミット済みメモリ" が 100 GB で、メモリ最適化テーブルおよびインデックスに 60 GB のメモリが必要であると推定した場合は、MAX_MEMORY_PERCENT = 67 (必要な 60 GB/0.90 = 66.667 GB – 67 GB に切り上げ、67 GB/インストール済みの 100 GB = 67%) でリソース プールを作成して、[!INCLUDE[hek_2](../../../includes/hek-2-md.md)] オブジェクトで必要な 60 GB を確実に使用できるようにします。  
  
 データベースが名前付きリソース プールにバインドされている場合は、次のクエリを使用して異なるリソース プールにわたるメモリ割り当てを確認します。  
  
```sql  
SELECT pool_id  
     , Name  
     , min_memory_percent  
     , max_memory_percent  
     , max_memory_kb/1024 AS max_memory_mb  
     , used_memory_kb/1024 AS used_memory_mb   
     , target_memory_kb/1024 AS target_memory_mb  
   FROM sys.dm_resource_governor_resource_pools  
```  
  
 このサンプル出力は、メモリ最適化オブジェクトによって使用されたメモリがリソース プール、PoolIMOLTP の 1356 MB であり、上限が 2307 MB であることを示しています。 この上限によって、ユーザーとこのプールにマップされるシステムのメモリ最適化オブジェクトが使用できるメモリの合計が制御されます。  
  
 **サンプル出力**   
この出力は、上で作成したデータベースおよびテーブルからのものです。  
  
```  
pool_id     Name        min_memory_percent max_memory_percent max_memory_mb used_memory_mb target_memory_mb  
----------- ----------- ------------------ ------------------ ------------- -------------- ----------------   
1           internal    0                  100                3845          125            3845  
2           default     0                  100                3845          32             3845  
259         PoolIMOLTP 0                  100                3845          1356           2307  
```  
  
 詳細については、「 [sys.dm_resource_governor_resource_pools (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql)」を参照してください。  
  
 ご利用のデータベースを名前付きリソース プールにバインドしない場合、そのデータベースは "既定の" プールにバインドされます。 既定のリソース プールは他のほとんどの割り当ての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用されるため、正確に対象のデータベースに対して DMV sys.dm_resource_governor_resource_pools を使用して、メモリ最適化テーブルで消費されたメモリを監視することはできません。  
  
## <a name="see-also"></a>参照  
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql)   
 [sys.sp_xtp_unbind_db_resource_pool &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-unbind-db-resource-pool-transact-sql)   
 [リソース ガバナー](../resource-governor/resource-governor.md)   
 [リソース ガバナー リソース プール](../resource-governor/resource-governor-resource-pool.md)   
 [リソース プールの作成](../resource-governor/create-a-resource-pool.md)   
 [リソース プールの設定の変更](../resource-governor/change-resource-pool-settings.md)   
 [リソース プールの削除](../resource-governor/delete-a-resource-pool.md)  
  
  
