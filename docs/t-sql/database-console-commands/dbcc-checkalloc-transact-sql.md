---
title: DBCC CHECKALLOC (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKALLOC_TSQL
- DBCC CHECKALLOC
- DBCC_CHECKALLOC_TSQL
- CHECKALLOC
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC CHECKALLOC statement
- checking database space allocation
- database space allocation [SQL Server]
- consistency [SQL Server], disk space allocations
- space allocation [SQL Server]
- allocation checks
- disk space [SQL Server], allocation consistency checks
- space allocation [SQL Server], checking
ms.assetid: bc1218eb-ffff-44ce-8122-6e4fa7d68a79
author: pmasl
ms.author: umajay
ms.openlocfilehash: d1735a107f0510deaf062ce28bdc1a8db2acbae1
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056349"
---
# <a name="dbcc-checkalloc-transact-sql"></a>DBCC CHECKALLOC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

指定したデータベース用のディスク領域の割り当て構造について一貫性をチェックします。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```
DBCC CHECKALLOC   
[  
    ( database_name | database_id | 0   
      [ , NOINDEX   
      | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]  
    )  
    [ WITH   
        {   
          [ ALL_ERRORMSGS ]  
          [ , NO_INFOMSGS ]   
          [ , TABLOCK ]   
          [ , ESTIMATEONLY ]   
        }  
    ]  
]  
```  
  
## <a name="arguments"></a>引数  
 *database_name* | *database_id* | 0   
 割り当てとページの使用状況を確認するデータベースの名前または ID。
値を指定しないか 0 を指定した場合は、現在のデータベースが使用されます。
データベース名は、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。

 NOINDEX  
 ユーザー テーブルの非クラスター化インデックスをチェックしません。<br>NOINDEX は旧バージョンとの互換性のためにだけ用意されており、DBCC CHECKALLOC には影響しません。

 REPAIR_ALLOW_DATA_LOSS \| REPAIR_FAST \| REPAIR_REBUILD  
 検出されたエラーを DBCC CHECKALLOC で修復します。 *database_name* はシングル ユーザー モードになっている必要があります。

 REPAIR_ALLOW_DATA_LOSS  
 検出されたすべてのエラーの修復を試行します。 修復を実行すると、データが失われることがあります。 REPAIR_ALLOW_DATA_LOSS はアロケーション エラーを修復できる唯一のオプションです。

 REPAIR_FAST  
 構文は、旧バージョンとの互換性のためにのみ残されています。 修復操作は実行されません。

 REPAIR_REBUILD  
 該当なし。  
 REPAIR オプションは、最後の手段としてのみ使用してください。 エラーの修復では、バックアップから復元することをお勧めします。 修復操作では、テーブルまたはテーブル間に制約があっても考慮されません。 指定したテーブルに 1 つでも関連する制約がある場合は、修復操作の後に DBCC CHECKCONSTRAINTS を実行することをお勧めします。 REPAIR を使用する必要がある場合は、修復オプションを指定せずに DBCC CHECKDB を実行して、使用する修復レベルを確認してください。 REPAIR_ALLOW_DATA_LOSS レベルを使用する場合は、このオプションを指定して DBCC CHECKDB を実行する前に、データベースをバックアップすることをお勧めします。

 WITH  
 オプションを指定可能にします。

 ALL_ERRORMSGS  
 すべてのエラー メッセージを表示します。 既定では、すべてのエラー メッセージが表示されます。 このオプションを指定しても省略しても影響はありません。

 NO_INFOMSGS  
 すべての情報メッセージと使用領域に関するレポートを表示しないようにします。

 TABLOCK  
 DBCC コマンドでデータベースを排他的にロックします。

 ESTIMATEONLY  
 他のすべてのオプションを指定したときに、DBCC CHECKALLOC の実行に必要な tempdb 領域の予測サイズを表示します。
  
## <a name="remarks"></a>Remarks  
DBCC CHECKALLOC では、ページの種類やページが属するオブジェクトの種類に関係なく、データベースのすべてのページの割り当てがチェックされます。 また、ページとページ間の関係の追跡に使用されるさまざまな内部構造も検証されます。
NO_INFOMSGS を指定しない場合、DBCC CHECKALLOC ではデータベースのすべてのオブジェクトに関する領域の使用情報が収集されます。 この情報は、検出されたエラーと共に出力されます。
  
> [!NOTE]  
> DBCC CHECKALLOC 機能は、[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) と [DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md) に含まれています。 つまり、これらのステートメントと別に DBCC CHECKALLOC を実行する必要はありません。   DBCC CHECKALLOC では、FILESTREAM データはチェックされません。 FILESTREAM はバイナリ ラージ オブジェクト (BLOB) をファイル システムに格納します。  
  
## <a name="internal-database-snapshot"></a>内部データベース スナップショット  
DBCC CHECKALLOC では、内部データベースのスナップショットを使用して、これらのチェックを実行するために必要なトランザクションの一貫性を確保します。 スナップショットを作成できない場合や、TABLOCK が指定されている場合は、DBCC CHECKALLOC はデータベースの排他 (X) ロックを取得して、必要な一貫性を確保します。
  
> [!NOTE]  
> Tempdb に対して DBCC CHECKALLOC を実行してもチェックは実行されません。 これは、パフォーマンス上の理由から、データベースのスナップショットが tempdb では利用できないためです。 つまり、必要なトランザクションの一貫性を実現できないためです。 tempdb の割り当ての問題を解決するのには、MSSQLSERVER サービスを停止して開始します。 この操作では、tempdb データベースを削除して再作成します。  
  
## <a name="understanding-dbcc-error-messages"></a>DBCC エラー メッセージについて  
DBCC CHECKALLOC コマンドの終了後、メッセージが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに書き込まれます。 DBCC コマンドが正常に実行された場合、メッセージでは正常完了とコマンド実行時間が示されます。 エラーが発生して DBCC コマンドが完了前に停止した場合、メッセージではコマンドが終了したことと、状態の値、コマンド実行時間が示されます。 次の表は、メッセージに含まれる可能性がある状態値の一覧と説明です。
  
|状態|[説明]|  
|---|---|  
|0|エラー番号 8930 が発生しました。 メタデータの破損が原因で DBCC コマンドが終了しました。|  
|1|エラー番号 8967 が発生しました。 内部 DBCC エラーがあります。|  
|2|緊急モードのデータベース修復中にエラーが発生しました。|  
|3|メタデータの破損が原因で DBCC コマンドが終了しました。|  
|4|アサートまたはアクセス違反が検出されました。|  
|5|不明なエラーが発生し、DBCC コマンドが終了しました。|  
  
## <a name="error-reporting"></a>[エラー報告]  
DBCC CHECKALLOC で破損エラーが検出されるたびに、ミニ ダンプ ファイル (SQLDUMP*nnnn*.txt) が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の LOG ディレクトリに作成されます。 機能の使用状況データ収集とエラー報告機能が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して有効になっている場合、ダンプ ファイルは自動的に [!INCLUDE[msCoName](../../includes/msconame-md.md)] に転送されます。 収集されたデータは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能向上のために使用されます。
このダンプ ファイルには、DBCC CHECKALLOC コマンドの結果と追加の診断出力が含まれます。 また、制限付きの随意アクセス制御リスト (DACL) が割り当てられます。 アクセスが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントと sysadmin ロールのメンバーに制限されます。 既定では、sysadmin ロールには、Windows の builtin \administrators グループとローカルの管理者のグループのすべてのメンバーが含まれています。 データ収集プロセスが失敗しても、DBCC コマンドは失敗しません。
  
## <a name="resolving-errors"></a>エラーの解決  
DBCC CHECKALLOC でエラーがレポートされた場合は、修復を実行せずに、データベース バックアップからデータベースを復元することをお勧めします。 バックアップが存在しない場合は、修復を実行することでレポートされたエラーを修正できますが、エラーを修正するためにページとデータの削除が必要になることがあります。
修復はユーザー トランザクションで実行できます。 この場合、変更はロールバックできます。 変更をロールバックした場合、データベースにはエラーが残っているので、データベースをバックアップから復元する必要があります。 修復が完了したら、データベースをバックアップします。
  
## <a name="result-sets"></a>結果セット  
次の表は、DBCC CHECKALLOC によって返される情報です。
  
|アイテム|[説明]|  
|---|---|  
|FirstIAM|内部使用のみです。|  
|Root|内部使用のみです。|  
|Dpages|データ ページ数。|  
|Pages used|割り当てられているページ。|  
|Dedicated extents|オブジェクトに割り当てられているエクステント。<br /><br /> 混合アロケーション ページが使用されている場合は、エクステントなしで割り当てられているページが存在している可能性があります。|  
  
DBCC CHECKALLOC では、各ファイルのインデックスとパーティションの割り当ての概要もレポートされます。 この概要では、データの分布が示されます。
  
|アイテム|[説明]|  
|---|---|  
|Reserved pages|インデックスに割り当てられているページ、および割り当てられているエクステント内の未使用ページ。|  
|Used pages|インデックスによって割り当てられ、使用中のページ。|  
|Partition ID|内部使用のみです。|  
|Alloc Unit ID|内部使用のみです。|  
|In-row data|インデックスまたはヒープ データが含まれるページ。|  
|LOB データ|ページには、**varchar(max)** 、**nvarchar(max)** 、**varbinary(max)** 、**text**、**ntext**、**xml**、**image** データが含まれています。|  
|Row-overflow data|行外に移動した可変長の列のデータが含まれるページ。|  
  
DBCC CHECKALLOC では、ESTIMATEONLY または NO_INFOMSGS を指定した場合を除き、次の結果セットが返されます。値は変化することがあります。
  
```
DBCC results for 'master'.  
***************************************************************  
Table sysobjects                Object ID 1.  
Index ID 1         FirstIAM (1:11)   Root (1:12)    Dpages 22.  
    Index ID 1. 24 pages used in 5 dedicated extents.  
Index ID 2         FirstIAM (1:1368)   Root (1:1362)    Dpages 10.  
    Index ID 2. 12 pages used in 2 dedicated extents.  
Index ID 3         FirstIAM (1:1392)   Root (1:1408)    Dpages 4.  
    Index ID 3. 6 pages used in 0 dedicated extents.  
Total number of extents is 7.  
***************************************************************  
'...'  
***************************************************************  
Table spt_server_info                Object ID 1938105945.  
Index ID 1         FirstIAM (1:520)   Root (1:508)    Dpages 1.  
    Index ID 1. 3 pages used in 0 dedicated extents.  
Total number of extents is 0.  
***************************************************************  
Processed 52 entries in sysindexes for database ID 1.  
File 1. Number of extents = 210, used pages = 1126, reserved pages = 1280.  
           File 1 (number of mixed extents = 73, mixed pages = 184).  
    Object ID 1, Index ID 0, data extents 5, pages 24, mixed extent pages 9.  
'...'  
    Object ID 1938105945, Index ID 0, data extents 0, pages 3, mixed extent pages 3.  
Total number of extents = 210, used pages = 1126, reserved pages = 1280 in this database.  
       (number of mixed extents = 73, mixed pages = 184) in this database.  
CHECKALLOC found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC results for 'master'.  
***************************************************************  
Table sys.sysrowsetcolumns                Object ID 4.  
Index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data). FirstIAM (1:98). Root (1:94). Dpages 7.  
Index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data). 9 pages used in 1 dedicated extents.  
Index ID 1, partition ID 262144, alloc unit ID 262398 (type Row-overflow data). FirstIAM (0:0). Root (0:0). Dpages 0.  
Index ID 1, partition ID 262144, alloc unit ID 262398 (type Row-overflow data). 0 pages used in 0 dedicated extents.  
Total number of extents is 1.  
...  
***************************************************************  
Processed 201 entries in system catalog for database ID 1.  
File 1. Number of extents = 44, used pages = 300, reserved pages = 345.  
           File 1 (number of mixed extents = 29, mixed pages = 225).  
    Object ID 4, index ID 1, partition ID 262144, alloc unit ID 262144 (type In-row data), data extents 1, pages 9, mixed extent pages 8.  
    Object ID 5, index ID 1, partition ID 327680, alloc unit ID 327680 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 7, index ID 1, partition ID 458752, alloc unit ID 458752 (type In-row data), data extents 0, pages 5, mixed extent pages 5.  
    Object ID 8, index ID 0, partition ID 524288, alloc unit ID 524288 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 13, index ID 1, partition ID 851968, alloc unit ID 851968 (type In-row data), data extents 1, pages 9, mixed extent pages 8.  
    Object ID 15, index ID 1, partition ID 983040, alloc unit ID 983040 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
    Object ID 26, index ID 1, partition ID 281474978414592, alloc unit ID 1703937 (type In-row data), data extents 0, pages 3, mixed extent pages 3.  
    Object ID 27, index ID 1, partition ID 281474978480128, alloc unit ID 1769473 (type In-row data), data extents 0, pages 3, mixed extent pages 3.  
    Object ID 27, index ID 2, partition ID 562949955190784, alloc unit ID 1769474 (type In-row data), index extents 0, pages 3, mixed extent pages 3.  
...  
    Object ID 1179151246, index ID 1, partition ID 72057594038845440, alloc unit ID 13435136 (type In-row data), data extents 2, pages 18, mixed extent pages 8.  
    Object ID 1179151246, index ID 2, partition ID 72057594038910976, alloc unit ID 13566208 (type In-row data), index extents 1, pages 16, mixed extent pages 8.  
    Object ID 1911677858, index ID 0, partition ID 72057594039631872, alloc unit ID 15073536 (type In-row data), data extents 0, pages 2, mixed extent pages 2.  
Total number of extents = 41, used pages = 289, reserved pages = 323 in this database.  
       (number of mixed extents = 27, mixed pages = 211) in this database.  
CHECKALLOC found 0 allocation errors and 0 consistency errors in database 'master'.  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
ESTIMATEONLY を指定した場合、DBCC CHECKALLOC では次の結果セットが返されます。
  
```
Estimated TEMPDB space needed for CHECKALLOC (KB)   
-------------------------------------------------   
34  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>アクセス許可  
Sysadmin 固定サーバー ロールまたは db_owner 固定データベース ロールのメンバーシップが必要です。
  
## <a name="examples"></a>使用例  
次の例では、現在のデータベースと `AdventureWorks2012` データベースに対して `DBCC CHECKALLOC` を実行します。
  
```sql  
-- Check the current database.  
DBCC CHECKALLOC;  
GO  
-- Check the AdventureWorks2012 database.  
DBCC CHECKALLOC (AdventureWorks2012);  
GO  
```  
  
## <a name="see-also"></a>参照  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

