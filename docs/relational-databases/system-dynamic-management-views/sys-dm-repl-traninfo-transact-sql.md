---
title: sys.dm_repl_traninfo (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_traninfo
- dm_repl_traninfo
- sys.dm_repl_traninfo_TSQL
- dm_repl_traninfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_traninfo dynamic management view
ms.assetid: 5abe2605-0506-46ec-82b5-6ec08428ba13
author: stevestein
ms.author: sstein
ms.openlocfilehash: fc4f107ef1c26aa51f3f1d58f910be9721f2a51a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067832"
---
# <a name="sysdmrepltraninfo-transact-sql"></a>sys.dm_repl_traninfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  レプリケートされたトランザクションまたは変更データ キャプチャ トランザクションごとの情報を返します。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**fp2p_pub_exists**|**tinyint**|ピア ツー ピア トランザクション レプリケーションを使用してパブリッシュされたデータベースでトランザクションの場合。 True の場合、値は 1 になります。それ以外の場合は 0 です。|  
|**db_ver**|**int**|データベースのバージョン。|  
|**comp_range_address**|**varbinary(8)**|スキップする必要があります、部分ロールバックの範囲を定義します。|  
|**textinfo_address**|**varbinary(8)**|キャッシュされたテキスト情報構造体のメモリ内アドレス。|  
|**fsinfo_address**|**varbinary(8)**|キャッシュされたファイル ストリーム情報構造のメモリ内アドレス。|  
|**begin_lsn**|**nvarchar(64)**|トランザクションの先頭ログ レコードのシーケンス番号 (LSN) を記録します。|  
|**commit_lsn**|**nvarchar(64)**|トランザクションのコミット ログ レコードの LSN。|  
|**dbid**|**smallint**|データベース ID。|  
|**rows**|**int**|トランザクション内でレプリケートされたコマンドの ID。|  
|**xdesid**|**nvarchar(64)**|トランザクション id。|  
|**artcache_table_address**|**varbinary(8)**|このトランザクションで最後に使用するキャッシュされたアーティクル テーブル構造のメモリ内アドレス。|  
|**server**|**nvarchar(514)**|サーバー名。|  
|**server_len_in_bytes**|**smallint**|文字長 (バイト単位)、サーバー名。|  
|**データベース (database)**|**nvarchar(514)**|データベース名。|  
|**db_len_in_bytes**|**smallint**|データベース名の文字長 (バイト単位)。|  
|**originator**|**nvarchar(514)**|トランザクションが発生したサーバーの名前。|  
|**originator_len_in_bytes**|**smallint**|文字長 (バイト単位)、サーバーのトランザクションが発生します。|  
|**orig_db**|**nvarchar(514)**|トランザクションが発生したデータベースの名前。|  
|**orig_db_len_in_bytes**|**smallint**|文字長 (バイト単位)、データベースのトランザクションが発生しますを。|  
|**cmds_in_tran**|**int**|論理トランザクションのコミットされた時期を決定するために使用、現在のトランザクションでレプリケートされたコマンド数です。|  
|**is_boundedupdate_singleton**|**tinyint**|一意の列の更新が 1 行だけに影響するかどうかを指定します。|  
|**begin_update_lsn**|**nvarchar(64)**|一意の列更新で使用される LSN。|  
|**delete_lsn**|**nvarchar(64)**|更新プログラムの一部として削除する LSN。|  
|**last_end_lsn**|**nvarchar(64)**|論理トランザクションの最後の LSN。|  
|**fcomplete**|**tinyint**|コマンドは部分的な更新であるかどうかを指定します。|  
|**fcompensated**|**tinyint**|トランザクションが部分ロールバックに含まれるかどうかを示します。|  
|**fprocessingtext**|**tinyint**|トランザクションにバイナリ ラージ データ型列が含まれるかどうかを示します。|  
|**max_cmds_in_tran**|**int**|ログ リーダー エージェントで指定したとおりの論理トランザクション内のコマンドの最大数。|  
|**begin_time**|**datetime**|トランザクションの開始時刻。|  
|**commit_time**|**datetime**|トランザクションがコミットされた時刻。|  
|**session_id**|**int**|変更データ キャプチャのログ スキャン セッションの ID。 この列にマップ、 **session_id**列[sys.dm_cdc_logscan_sessions](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)します。|  
|**session_phase**|**int**|フェーズのセッション時に、エラーを示す数値が発生しました。 この列にマップ、 **phase_number**列[sys.dm_cdc_errors](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md)します。|  
|**is_known_cdc_tran**|**bit**|トランザクションが変更データ キャプチャによって追跡されることを示します。<br /><br /> 0 = トランザクション レプリケーション トランザクション。<br /><br /> 1 = 変更データ キャプチャ トランザクション。|  
|**error_count**|**int**|発生したエラーの数です。|  
  
## <a name="permissions"></a>アクセス許可  
 パブリケーション データベースまたは変更データ キャプチャが有効にされたデータベースに対する VIEW DATABASE STATE 権限が必要です。  
  
## <a name="remarks"></a>コメント  
 情報は、レプリケートされたデータベース オブジェクトに対してのみ返されます。 または、有効にするテーブルがアーティクル キャッシュに現在読み込まれているデータのキャプチャを変更します。  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [レプリケーション関連の動的管理ビュー &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)   
 [変更データ キャプチャに関連した動的管理ビュー &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/2a771d7d-693a-4f56-9227-02cd00e0e200)  
  
  

