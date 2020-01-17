---
title: sys.fn_virtualfilestats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_virtualfilestats_TSQL
- fn_virtualfilestats
dev_langs:
- TSQL
helpviewer_keywords:
- I/O [SQL Server], statistics
- fn_virtualfilestats function
- sys.fn_virtualfilestats function
- statistical information [SQL Server], I/O
ms.assetid: 96b28abb-b059-48db-be2b-d60fe127f6aa
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: aade9e02515e0d18e4edae188d72e5edafebbd3f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059187"
---
# <a name="sysfnvirtualfilestats-transact-sql"></a>sys.fn_virtualfilestats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  ログ ファイルを含む、データベース ファイルの I/O 統計を返します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]からこの情報はまた、 [sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md)動的管理ビュー。  

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_virtualfilestats ( { database_id | NULL } , { file_id | NULL } )  
```  
  
## <a name="arguments"></a>引数  
 *database_id* | NULL  
 データベースの ID です。 *database_id* は **int**, 、既定値はありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのすべてのデータベースに関する情報を返すには NULL を指定します。  
  
 *file_id* | NULL  
 ファイルの ID を指定します。 *file_id*は**int**、既定値はありません。 データベースのすべてのファイルの情報を返す NULL を指定します。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データの種類|説明|  
|-----------------|---------------|-----------------|  
|**DbId**|**smallint**|データベース ID。|  
|**FileId**|**smallint**|ファイル ID。|  
|**TimeStamp**|**bigint**|データが取り出されたデータベース タイムスタンプです。 **int**より前に、のバージョンで[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]します。 |  
|**NumberReads**|**bigint**|ファイルで実行された読み取りの数。|  
|**BytesRead**|**bigint**|ファイルに対して実行された読み取りバイト数。|  
|**IoStallReadMS**|**bigint**|ユーザーが、読み取りの待機している、ミリ秒単位の時間の合計 I/o 数のファイルが完了します。|  
|**NumberWrites**|**bigint**|そのファイルで実行された書き込みの数です。|  
|**BytesWritten**|**bigint**|ファイルに書き込まれたバイト数。|  
|**IoStallWriteMS**|**bigint**|ユーザーが書き込み、ファイル、完了する I/o の待機している、ミリ秒単位の時間の合計。|  
|**IoStallMS**|**bigint**|合計**IoStallReadMS**と**IoStallWriteMS**します。|  
|**FileHandle**|**bigint**|ファイル ハンドルの値。|  
|**BytesOnDisk**|**bigint**|ディスク上の物理ファイル サイズ (バイト数)。<br /><br /> データベース ファイルの場合と同じ値は、この**サイズ**で**sys.database_files**ページではなくバイトで表現されますが、します。<br /><br /> データベース スナップショットのスパース ファイルでは、これは、ファイルのオペレーティング システムが使用している領域です。|  
  
## <a name="remarks"></a>コメント  
 **fn_virtualfilestats**ファイルで I/o の合計数などの統計情報を提供するテーブル値関数は実行システムです。 ユーザーは、読み取りまたはファイルへの書き込みを待機するのに必要がある時間の長さを追跡するのに役立つ、この関数を使用することができます。 関数は、多数の I/O アクティビティが発生するファイルの特定にも役立ちます。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-displaying-statistical-information-for-a-database"></a>A. データベースの統計情報を表示する  
 次の例の ID を使用してデータベース内のファイル ID 1 の統計情報を表示する`1`します。  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(1, 1);  
GO  
```  
  
### <a name="b-displaying-statistical-information-for-a-named-database-and-file"></a>B. 名前付きデータベースおよびファイルの統計情報を表示します。  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] サンプル データベースのログ ファイルの統計情報を表示します。 システム関数`DB_ID`を指定するために使用、 *database_id*パラメーター。  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(DB_ID(N'AdventureWorks2012'), 2);  
GO  
```  
  
### <a name="c-displaying-statistical-information-for-all-databases-and-files"></a>C. すべてのデータベースおよびファイルの統計情報を表示する  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内のすべてのデータベースにあるすべてのファイルの統計情報を表示します。  
  
```sql  
SELECT *  
FROM fn_virtualfilestats(NULL,NULL);  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [DB_ID &#40;TRANSACT-SQL&#41;](../../t-sql/functions/db-id-transact-sql.md)   
 [FILE_IDEX &#40;Transact-SQL&#41;](../../t-sql/functions/file-idex-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
