---
title: DBCC SHRINKDATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_SHRINKDATABASE_TSQL
- DBCC SHRINKDATABASE
- SHRINKDATABASE_TSQL
- SHRINKDATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- shrinking files
- shrinking databases
- DBCC SHRINKDATABASE statement
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
ms.assetid: fc976afd-1edb-4341-bf41-c4a42a69772b
author: pmasl
ms.author: umajay
monikerRange: = azuresqldb-current ||>= sql-server-2016 ||>= sql-server-linux-2017||=azure-sqldw-latest||= sqlallproducts-allversions
ms.openlocfilehash: 1bda4ebd946bfd8adf31190c36125075d50dc28d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073162"
---
# <a name="dbcc-shrinkdatabase-transact-sql"></a>DBCC SHRINKDATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

指定したデータベース内のデータ ファイルとログ ファイルのサイズを圧縮します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
DBCC SHRINKDATABASE   
( database_name | database_id | 0   
     [ , target_percent ]   
     [ , { NOTRUNCATE | TRUNCATEONLY } ]   
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>引数  
_database\_name_ | _database\_id_ | 0  
圧縮するデータベースの名前または ID です。 0 は、現在のデータベースを使用するように指定します。  
  
_target\_percent_  
データベースを圧縮した後、データベース ファイル内に残す空き領域のパーセンテージを指定します。  
  
NOTRUNCATE  
ファイル末尾の割り当て済みページをファイル先頭の未割り当てページに移動します。 この操作により、ファイル内のデータが圧縮されます。 _target\_percent_ は省略可能です。 Azure SQL Data Warehouse では、このオプションはサポートされていません。 
  
ファイル末尾の空き領域はオペレーティング システムに返されず、ファイルの物理サイズは変わりません。 そのため、NOTRUNCATE を指定した場合、データベースが圧縮されていないように見えます。  
  
NOTRUNCATE はデータ ファイルにのみ適用され、 NOTRUNCATE はログ ファイルには影響しません。  
  
TRUNCATEONLY  
ファイル末尾のすべての空き領域をオペレーティング システムに解放します。 ファイル内でのページの移動は行いません。 データ ファイルは、最後に割り当てられたエクステントを限度として圧縮されます。 _target\_percent_ が TRUNCATEONLY と共に指定された場合は、無視します。 Azure SQL Data Warehouse では、このオプションはサポートされていません。
  
TRUNCATEONLY はログ ファイルに影響します。 データ ファイルのみを切り捨てるには、DBCC SHRINKFILE を使用します。  
  
WITH NO_INFOMSGS  
重大度レベル 0 から 10 のすべての情報メッセージを表示しないようにします。  
  
## <a name="result-sets"></a>結果セット  
次の表では、結果セットの列について説明します。
  
|列名|[説明]|  
|-----------------|-----------------|  
|**DbId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]で圧縮が試行されたファイルのデータベース識別番号。|  
|**FileId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]で圧縮が試行されたファイルのファイル識別番号。|  
|**CurrentSize**|ファイルが現在占有する 8 KB ページの数。|  
|**MinimumSize**|ファイルが占有できる 8 KB ページの最小数。 この値は、ファイルの最小サイズまたは最初に作成されたサイズと一致します。|  
|**UsedPages**|ファイルが現在使用している 8 KB ページの数。|  
|**EstimatedPages**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]で推定されるファイル圧縮後の 8 KB ページの数。|  
  
>[!NOTE]
> [!INCLUDE[ssDE](../../includes/ssde-md.md)]では圧縮されないファイルの行は表示されません。  
  
## <a name="remarks"></a>Remarks  

>[!NOTE]
> 現在、Azure SQL Data Warehouse では DBCC SHRINKDATABASE はサポートされません。 このコマンドを実行することはお勧めできません。これは大量の I/O が発生する操作であり、データ ウェアハウスがオフラインになる可能性があるためです。 また、このコマンドを実行すると、データ ウェアハウス スナップショットのコストに影響します。 

特定のデータベースに関するすべてのデータとログ ファイルを圧縮するには、DBCC SHRINKDATABASE コマンドを実行します。 特定のデータベースで一度に 1 つのデータまたはログ ファイルを圧縮するには、[DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) コマンドを実行します。
  
データベースの空き (未割り当て) 領域の現在の量を表示するには、[sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) を実行します。
  
DBCC SHRINKDATABASE 操作は、プロセスのどの時点でも中断でき、中断時に完了していた作業は保持されます。
  
データベースは、そのデータベースの構成された最小サイズより小さくすることはできません。 データベースの最初の作成時に、最小サイズを指定します。 または、ファイル サイズ変更操作を使用して最後に明示的に設定したサイズを最小サイズにすることができます。 ファイル サイズ変更操作の例として、DBCC SHRINKFILE や ALTER DATABASE のような操作があります。 

たとえば、データベースの最初の作成時にサイズを 10 MB に指定したとします。 その後、100 MB まで拡張したとします。 データベース内のすべてのデータを削除したとしても、データベースを縮小できる限界は 10 MB です。
  
DBCC SHRINKDATABASE を実行するときは、NOTRUNCATE オプションまたは TRUNCATEONLY オプションのいずれかを指定します。 そうしない場合、NOTRUNCATE を指定して DBCC SHRINKDATABASE 操作を実行した後に、TRUNCATEONLY を指定して DBCC SHRINKDATABASE 操作を実行した場合と同じ結果になります。
  
圧縮されるデータベースは、シングル ユーザー モードになっていなくてもかいません。 データベースを圧縮している最中でも、他のユーザーがそのデータベースで作業することができます。システム データベースの場合も同様です。
  
データベースのバックアップ中、データベースを圧縮することはできません。 逆に、データベースの圧縮操作の進行中、データベースをバックアップすることはできません。
  
## <a name="how-dbcc-shrinkdatabase-works"></a>DBCC SHRINKDATABASE の動作  
DBCC SHRINKDATABASE では、データ ファイルはファイルごとに圧縮されますが、ログ ファイルはすべてが 1 つの連続的なログ プールに存在するものとして圧縮されます。 ファイルは常に末尾から圧縮されます。
  
いくつかのログ ファイルと 1 つのデータ ファイルがあり、**mydb** というデータベースがあるとします。 各データ ファイルとログ ファイルのサイズは 10 MB で、データ ファイルに 6 MB のデータが含まれているとします。 それぞれのファイルについて、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって目標サイズが計算されます。 この値はファイルの圧縮後のサイズです。 DBCC SHRINKDATABASE を _target\_percent_ と共に指定すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では、圧縮後にファイル内の空き領域が _target\_percent_ の量になるように目標サイズが計算されます。 

たとえば、**mydb** を圧縮する場合に _target\_percent_ を 25 に指定すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)]ではデータ ファイルの目標サイズが 8 MB (6 MB のデータに 2 MB の空き領域を加えたもの) と計算されます。 したがって、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では、データ ファイルの末尾 2 MB にあるすべてのデータがデータ ファイルの先頭 8 MB にある空き領域に移動されてから、ファイルが圧縮されます。
  
次に、**mydb** のデータ ファイルに 7 MB のデータが含まれているとします。 _target\_percent_ を 30 に指定した場合、このデータ ファイルは空き領域のパーセンテージが 30 になるように圧縮されます。 ただし、_target\_percent_ を 40 に指定した場合、データ ファイルは圧縮されません。[!INCLUDE[ssDE](../../includes/ssde-md.md)]では、圧縮後のファイル サイズが現在のデータ占有領域よりも小さくなる場合、ファイルは圧縮されません。 

この問題について別の考え方もできます。目的の空き領域 40% にデータ ファイル最大容量の 70% (10 MB 中の 7 MB) を加算すると、100% を超えます。 30 を超える値を _target\_size_ に指定すると、データ ファイルは圧縮されません。 圧縮されない理由は、目的の空き領域のパーセンテージと、データ ファイルの現在の占有パーセンテージを加算した値が 100% を超えることです。
  
ログ ファイルの場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]では _target\_size_ を使用してログ全体の目標サイズを計算します。 _target\_percent_ は圧縮操作後のログ内の空き領域の量になります。 その後、ログ全体の目標サイズは各ログ ファイルの目標サイズに変換されます。
  
DBCC SHRINKDATABASE では、各物理ログ ファイルの目標サイズへの圧縮がすぐに試行されます。 論理ログのどの部分も、ログ ファイルの目標サイズを超える仮想ログ内にないとします。 するとファイルは正常に切り捨てられ、DBCC SHRINKDATABASE はメッセージなしで終了します。 ただし、論理ログの一部が、目標サイズを超える仮想ログ内に存在する場合は、[!INCLUDE[ssDE](../../includes/ssde-md.md)]により、できるだけ多くの領域が解放され、その後に情報メッセージが発行されます。 このメッセージには、ファイルの末尾で仮想ログから論理ログを移動するために行う必要のある操作が説明されています。 操作の実行後、DBCC SHRINKDATABASE を使って、残りの領域を解放できます。
  
ログ ファイルは、仮想ログ ファイルの境界を越えて圧縮することはできません。 そのため、ログ ファイルを仮想ログ ファイルのサイズより小さく圧縮することはできません。 これはログ ファイルが使用されていない場合でも同じです。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]では、ログ ファイルの作成時または拡張時に仮想ログ ファイルのサイズが動的に選択されます。
  
## <a name="best-practices"></a>ベスト プラクティス  
データベースを圧縮する場合は次のことを考慮してください。
-   圧縮操作は、何かの操作後に行うと最も効果的です。 この操作は、未使用領域を作成する、テーブルの切り捨てやテーブルの削除操作などです。  
-   ほとんどのデータベースでは、毎日の定期的操作で使用するための空き領域が必要です。 データベースを繰り返し圧縮し、サイズが再び大きくなったことに気付く場合があります。 この拡張は、通常の操作に圧縮領域が必要であることを示しています。 このような場合、繰り返しデータベースを圧縮することは無意味です。  
-   圧縮操作では、データベース内のインデックスの断片化状態は保持されず、一般に、断片化の程度が大きくなります。 この結果からも、データベースを繰り返し圧縮することはお勧めできません。  
-   特別な要件がない限り、AUTO_SHRINK データベース オプションを ON に設定しないでください。  
  
## <a name="troubleshooting"></a>トラブルシューティング  
[行のバージョン管理に基づく分離レベル](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)で実行されているトランザクションによって圧縮操作がブロックされる可能性があります。 たとえば、DBCC SHRINK DATABASE 操作を実行するときに、行のバージョン管理に基づく分離レベルでの大規模な削除操作が進行中であるとします。 このような状況の場合、圧縮操作はファイルを圧縮する前に、削除操作が完了するまで待機します。 圧縮操作が待機しているとき、DBCC SHRINKFILE および DBCC SHRINKDATABASE 操作によって、情報メッセージ (SHRINKDATABASE は 5202、SHRINKFILE は 5203) が出力されます。 このメッセージは、最初の 1 時間は 5 分おきに、それ以降は 1 時間おきに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに書き込まれます。 たとえば、エラー ログに次のエラー メッセージが含まれているとします。  
  
```sql
DBCC SHRINKDATABASE for database ID 9 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
このエラーは、109 より前のタイムスタンプが存在するスナップショット トランザクションによって、圧縮操作がブロックされることを意味します。 そのトランザクションは、圧縮操作によって完了した最後のトランザクションです。 また、[sys.dm_tran_active_snapshot_database_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) 動的管理ビューの **transaction_sequence_num** 列または **first_snapshot_sequence_num** 列に、値 15 が含まれることも示しています。 そのビューの **transaction_sequence_num** 列または **first_snapshot_sequence_num** 列に、圧縮操作により完了した最後のトランザクション (109) より低い番号が含まれている場合があります。 その場合は、それらのトランザクションが終了するまで圧縮操作は待機状態となります。
  
この問題を解決するために、次のいずれかの作業を実行できます。
-   圧縮操作をブロックしているトランザクションを終了します。  
-   圧縮操作を終了します。 完了済みの作業は保持されます。  
-   何もせず、ブロックしているトランザクションが完了するまで圧縮操作を待機状態にしておきます。  
  
## <a name="permissions"></a>アクセス許可  
**sysadmin** 固定サーバー ロールまたは **db_owner** 固定データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-shrinking-a-database-and-specifying-a-percentage-of-free-space"></a>A. データベースを圧縮し、空き領域のパーセンテージを指定する  
次の例では、`UserDB` ユーザー データベース内のデータ ファイルとログ ファイルのサイズを圧縮して、データベースの空き領域が 10% になるようにします。  
  
```sql  
DBCC SHRINKDATABASE (UserDB, 10);  
GO  
```  
  
### <a name="b-truncating-a-database"></a>B. データベースを切り捨てる  
次の例では、`AdventureWorks` サンプル データベース内のデータ ファイルとログ ファイルを、最後に割り当てられたエクステントまで圧縮します。  
  
```sql  
DBCC SHRINKDATABASE (AdventureWorks2012, TRUNCATEONLY);  
```  
  
## <a name="see-also"></a>参照  
[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKFILE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
[データベースの圧縮](../../relational-databases/databases/shrink-a-database.md)
  
  
