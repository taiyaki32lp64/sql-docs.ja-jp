---
title: sp_filestream_force_garbage_collection (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_filestream_force_garbage_collection
- sp_filestream_force_garbage_collection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILESTREAM [SQL Server]
- sp_filestream_force_garbage_collection
ms.assetid: 9d1efde6-8fa4-42ac-80e5-37456ffebd0b
author: stevestein
ms.author: sstein
ms.openlocfilehash: e836fb2bd64a4fb0be15288322aa8fee30dc763e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942283"
---
# <a name="spfilestreamforcegarbagecollection-transact-sql"></a>sp_filestream_force_garbage_collection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  不要な FILESTREAM ファイルの削除を実行するには、FILESTREAM ガベージ コレクターに強制します。  
  
 ガベージ コレクターによってクリーンアップされました内に削除されたすべてのファイルまで、FILESTREAM コンテナーを削除できません。 FILESTREAM ガベージ コレクターは自動的に実行されます。 ただし、ガベージ コレクターの前にコンテナーを削除するが実行する必要がある場合は、sp_filestream_force_garbage_collection を使用するには、ガベージ コレクターを手動で実行します。  
  
  
## <a name="syntax"></a>構文  
  
```  
sp_filestream_force_garbage_collection
    [ @dbname = ]  'database_name'
    [ , [ @filename = ] 'logical_file_name' ]
```  
  
## <a name="arguments"></a>引数  
 `[ @dbname = ]  'database_name'`  
 ガベージ コレクターを実行するデータベースの名前を示します。  
  
> [!NOTE]  
> `@dbname` **sysname**します。 指定しない場合、指定すると、現在のデータベースが想定されます。  
  
 `[ @filename = ] 'logical_file_name'`  
 ガベージ コレクターを実行する FILESTREAM コンテナーの論理名を指定します。 `@filename` 省略可能です。 論理ファイル名が指定されていない場合、ガベージ コレクターは、指定されたデータベース内のすべての FILESTREAM コンテナーをクリーンアップします。  
  
## <a name="return-code-values"></a>リターン コードの値  
  
|||  
|-|-|  
|値|説明|  
|0|操作に成功しました。|  
|1|操作に失敗しました|  
  
## <a name="result-sets"></a>結果セット  
  
|値|説明|  
|-----------|-----------------|  
|*file_name*|FILESTREAM コンテナー名を示します。|  
|*num_collected_items*|このコンテナー内の、ガベージ コレクションが実行 (削除) された FILESTREAM アイテム (ファイルまたはディレクトリ) の数を示します。|  
|*num_marked_for_collection_items*|このコンテナー内の、ガベージ コレクションの対象としてマークされた FILESTREAM アイテム (ファイルまたはディレクトリ) の数を示します。 これらの項目は、まだ削除されていないが、削除、ガベージ コレクション フェーズを次の対象となる場合があります。|  
|*num_unprocessed_items*|この FILESTREAM コンテナー内の、ガベージ コレクションで処理されなかった対象となる FILESTREAM アイテム (ファイルまたはディレクトリ) の数を示します。 アイテムは次のようなさまざまな理由で処理されないことがあります。<br /><br /> ログのバックアップまたはチェックポイントが作成されていないため、ピン留めする必要があるファイル。<br /><br /> 完全または一括ログ復旧モデル内のファイル。<br /><br /> 実行時間の長いアクティブなトランザクションが存在している。<br /><br /> レプリケーション ログ リーダー ジョブが実行されません。 ホワイト ペーパーを参照してください。 [SQL Server 2008 の FILESTREAM ストレージ](https://go.microsoft.com/fwlink/?LinkId=209156)詳細についてはします。|  
|*last_collected_xact_seqno*|指定した FILESTREAM コンテナー内の、ガベージ コレクションが実行されたファイルに対応する最後のログ シーケンス番号 (LSN) を返します。|  
  
## <a name="remarks"></a>コメント  
 明示的に FILESTREAM ガベージ コレクターのタスクを完了するまで要求されたデータベース (および FILESTREAM コンテナー) で実行されます。 不要になったファイルは、ガベージ コレクション プロセスによって削除されます。 この操作を完了するために必要な時間は、そのデータベースまたはコンテナーだけでなく、FILESTREAM データに対して最近実行された DML アクティビティの量での FILESTREAM データのサイズによって異なります。 この操作はデータベースがオンラインのときに実行できますが、ガベージ コレクション プロセスによってさまざまな I/O 操作が行われるため、実行中にデータベースのパフォーマンスに影響を与える可能性があります。  
  
> [!NOTE]  
>  必要な場合にのみ、通常の業務時間外にこの操作を実行することをお勧めします。  
  
このストアド プロシージャの複数の呼び出しは、個別のコンテナーまたは別のデータベースでのみ同時に実行できます。  

2 段階の操作のためには、基になる Filestream ファイルを実際に削除するには、2 回ストアド プロシージャを実行する必要があります。  

ガベージ コレクション (GC) は、ログの切り捨てに依存します。 そのため、ファイルは完全復旧モデルを使用してデータベースで最近削除された場合は GC ed、トランザクション ログの一部のログ バックアップが取得され、ログ部分が非アクティブとマークした後のみです。 単純復旧モデルを使用して、データベースに対するログの切り捨ての発生後に、`CHECKPOINT`がデータベースに対して発行されています。  


## <a name="permissions"></a>アクセス許可  
 Db_owner データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例で FILESTREAM コンテナーに対してガベージ コレクターの実行、`FSDB`データベース。  
  
### <a name="a-specifying-no-container"></a>A. コンテナーを指定しません。  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB';  
```  
  
### <a name="b-specifying-a-container"></a>B. コンテナーを指定する  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB',
    @filename = N'FSContainer';  
```  
  
## <a name="see-also"></a>関連項目  
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream および FileTable の動的管理ビュー (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream および FileTable のカタログ ビュー (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[sp_kill_filestream_non_transacted_handles (TRANSACT-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)
  
  
