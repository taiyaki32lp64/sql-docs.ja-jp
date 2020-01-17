---
title: sys.dm_exec_cursors (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cursors_TSQL
- dm_exec_cursors
- dm_exec_cursors_TSQL
- sys.dm_exec_cursors
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cursors dynamic management function
ms.assetid: f520b63c-36af-40f1-bf71-6901d6331d3d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1ebffa740abe55a176c8577f754cf1a18db65022
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68097837"
---
# <a name="sysdmexeccursors-transact-sql"></a>sys.dm_exec_cursors (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  各種データベースで開いているカーソルに関する情報を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
dm_exec_cursors (session_id | 0 )  
```  
  
## <a name="arguments"></a>引数  
 *session_id* | 0  
 セッションの ID を指定します。 場合*session_id*を指定すると、この関数は、指定したセッションでカーソルに関する情報を返します。  
  
 0 を指定した場合、この関数ではすべてのセッションのすべてのカーソルに関する情報が返されます。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|このカーソルを保持しているセッションの ID。|  
|**cursor_id**|**int**|カーソル オブジェクトの ID。|  
|**name**|**nvarchar (256)**|ユーザーによって定義されたカーソルの名前。|  
|**properties**|**nvarchar (256)**|カーソルのプロパティ。 この列の値をフォームに次のプロパティの値が連結されます。<br />宣言インターフェイス<br />カーソルの種類 <br />カーソルの同時実行<br />カーソルのスコープ<br />カーソルの入れ子レベル<br /><br /> たとえば、この列に返される値があります"TSQL&#124;動的&#124;Optimistic &#124; Global (0)"。|  
|**sql_handle**|**varbinary(64)**|カーソルを宣言したバッチのテキストへのハンドルします。|  
|**statement_start_offset**|**int**|現在実行中に文字数のバッチまたはストアド プロシージャが現在実行中のステートメントの開始位置。 組み合わせて使用することができます、 **sql_handle**、 **statement_end_offset**、および[sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)動的管理関数を取得する、現在要求のステートメントを実行します。|  
|**statement_end_offset**|**int**|現在実行中に文字数のバッチまたはストアド プロシージャが現在実行中のステートメントが終了します。 組み合わせて使用することができます、 **sql_handle**、 **statement_start_offset**、および**sys.dm_exec_sql_text**動的管理関数を取得する、現在要求のステートメントを実行します。|  
|**plan_generation_num**|**bigint**|再コンパイル後、プランのインスタンス間で区別するために使用できるシーケンス番号。|  
|**creation_time**|**datetime**|カーソルが作成されたタイムスタンプ。|  
|**is_open**|**bit**|カーソルが開いているかどうかを示します。|  
|**is_async_population**|**bit**|KEYSET または STATIC カーソルが非同期にバック グラウンド スレッドが作成するかどうかを指定します。|  
|**is_close_on_commit**|**bit**|CURSOR_CLOSE_ON_COMMIT を使用して、カーソルが宣言されているかどうかを指定します。<br /><br /> 1 = カーソルはトランザクションが終了したときに閉じられます。|  
|**fetch_status**|**int**|返します。 は、最後、カーソルの状態を取得します。 これは、返された最終@FETCH_STATUS値。|  
|**fetch_buffer_size**|**int**|フェッチ バッファーのサイズに関する情報。<br /><br /> 1 = Transact-SQL カーソル。 これは、API カーソルに最高値に設定できます。|  
|**fetch_buffer_start**|**int**|FAST_FORWARD と DYNAMIC カーソルでは、最初の行の前に配置されている場合、カーソルが開いていない場合または 0 を返します。 それ以外のときは -1 が返されます。<br /><br /> STATIC と KEYSET カーソルでは、カーソルはオープン、および-1、カーソルが最後の行外に配置されている場合場合 0 を返します。<br /><br /> それが配置されている行番号を返します。|  
|**ansi_position**|**int**|カーソルのフェッチ バッファー内の位置。|  
|**worker_time**|**bigint**|時間 (マイクロ秒)、このカーソルを実行するワーカーによって費やさ。|  
|**reads**|**bigint**|カーソルで実行された読み取りの数。|  
|**書き込み**|**bigint**|カーソルで実行された書き込みの数。|  
|**dormant_duration**|**bigint**|前回のクエリ以降のミリ秒 (開くまたはフェッチ) が、このカーソル上で開始します。|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="remarks"></a>コメント  
 次の表は、カーソル宣言インターフェイスについて説明し、プロパティ列の値が含まれています。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|API|カーソルは、データ アクセス Api (ODBC、OLEDB) のいずれかを使用して宣言されています。|  
|TSQL|カーソルは、TRANSACT-SQL DECLARE CURSOR 構文を使用して宣言されています。|  
  
 次の表は、カーソルの種類に関する説明と、プロパティ列に返される値です。  
  
|種類|説明|  
|----------|-----------------|  
|Keyset|カーソルはキーセットとして宣言されています。|  
|動的|カーソルは Dynamic として宣言されました。|  
|スナップショット|カーソルは、スナップショットまたは Static として宣言されています。|  
|Fast_Forward|カーソルは高速順方向として宣言されています。|  
  
 次の表は、カーソルのコンカレンシーに関する説明と、プロパティ列に返される値です。  
  
|コンカレンシー|説明|  
|-----------------|-----------------|  
|[読み取り専用]|カーソルは、読み取り専用として宣言されています。|  
|スクロール ロック|カーソルはスクロール ロックを使用します。|  
|オプティミスティック|カーソルはオプティミスティック同時実行制御を使用します。|  
  
 次の表は、カーソルのスコープについて説明し、プロパティ列の値が含まれています。  
  
|スコープ|説明|  
|-----------|-----------------|  
|ローカル|カーソルのスコープは、カーソルが作成されたバッチ、ストアド プロシージャ、またはトリガーに対してローカルです。|  
|グローバル|カーソルのスコープは、接続に対してグローバルです。|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-detecting-old-cursors"></a>A. 古いカーソルを検出します。  
 この例では、36 時間の指定した時間より長く、サーバー上で開いているカーソルに関する情報を返します。  
  
```  
SELECT creation_time, cursor_id, name, c.session_id, login_name   
FROM sys.dm_exec_cursors(0) AS c   
JOIN sys.dm_exec_sessions AS s ON c.session_id = s.session_id   
WHERE DATEDIFF(hh, c.creation_time, GETDATE()) > 36;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数&#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
  

