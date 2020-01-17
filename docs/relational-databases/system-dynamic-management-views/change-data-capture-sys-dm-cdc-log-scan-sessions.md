---
title: sys.dm_cdc_log_scan_sessions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cdc_log_scan_sessions
- dm_cdc_log_scan_sessions_TSQL
- sys.dm_cdc_log_scan_sessions_TSQL
- sys.dm_cdc_log_scan_sessions
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], log scan reporting
- sys.dm_cdc_log_scan_sessions dynamic management view
ms.assetid: d337e9d0-78b1-4a07-8820-2027d0b9f87c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 52abdd077d892982c7fb63a34cec8bbdbd973379
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017995"
---
# <a name="change-data-capture---sysdmcdclogscansessions"></a>変更データ キャプチャ - sys.dm_cdc_log_scan_sessions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベース内のログ スキャン セッションごとに 1 行のデータを返します。 返された行の最後は、現在のセッションを表します。 このビューを使用すると、現在のログ スキャン セッションのステータス情報を取得できます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが開始されてからのすべてのセッションの集計情報を取得することもできます。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|セッションの ID を指定します。<br /><br /> 0 = で返されるデータは、この行は以降のインスタンスのすべてのセッションの集計[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が最後に起動します。|  
|**start_time**|**datetime**|セッションの開始時刻です。<br /><br /> ときに**session_id**集計されたデータの収集が開始された時間、0 を = です。|  
|**end_time**|**datetime**|セッションの時間が終了しました。<br /><br /> NULL は、セッションがアクティブであることを表します。<br /><br /> ときに**session_id** 0、最後のセッションが終了した時刻を = です。|  
|**duration**|**bigint**|セッションの実行時間 (秒単位) です。<br /><br /> 変更データ キャプチャ トランザクションがセッションに存在しない場合は 0 になります。<br /><br /> ときに**session_id** = 0、変更データ キャプチャ トランザクションですべてのセッションの期間を秒単位での合計。|  
|**scan_phase**|**nvarchar(200)**|セッションの現在のフェーズです。 使用可能な値とその説明を次に示します。<br /><br /> 1:構成の読み取り<br />2:最初のスキャン、ハッシュ テーブルの作成<br />3:1 番目のスキャン<br />4:1 番目のスキャン<br />5:1 番目のスキャン<br />6:スキーマのバージョン管理<br />7:最後のスキャン<br />8:完成です<br /><br /> ときに**session_id** = 0 の場合、この値は"Aggregate"は常にします。|  
|**error_count**|**int**|発生したエラーの数です。<br /><br /> ときに**session_id** = 0、すべてのセッションのエラーの合計数。|  
|**start_lsn**|**nvarchar(23)**|セッションの開始 LSN です。<br /><br /> ときに**session_id** = 0 の場合、最後のセッションの開始の LSN。|  
|**current_lsn**|**nvarchar(23)**|現在スキャン中の LSN です。<br /><br /> ときに**session_id** = 0 の場合、現在の LSN は 0。|  
|**end_lsn**|**nvarchar(23)**|セッションの最終 LSN です。<br /><br /> NULL は、セッションがアクティブであることを表します。<br /><br /> ときに**session_id** = 0 の場合は、最後のセッションの LSN を終了します。|  
|**tran_count**|**bigint**|処理された変更データ キャプチャ トランザクションの数です。 このカウンターはフェーズ 2 で設定されます。<br /><br /> ときに**session_id** = 0、すべてのセッションで処理されたトランザクションの数。|  
|**last_commit_lsn**|**nvarchar(23)**|処理された最終コミット ログ レコードの LSN です。<br /><br /> ときに**session_id** = 0、任意のセッションの最終コミット ログ レコードの LSN。|  
|**last_commit_time**|**datetime**|最終コミット ログ レコードが処理された時刻です。<br /><br /> ときに**session_id** 0、任意のセッションの最終コミット ログ レコードの時間を = です。|  
|**log_record_count**|**bigint**|スキャンされたログ レコードの数です。<br /><br /> ときに**session_id** = 0、すべてのセッションのスキャン レコードの数。|  
|**schema_change_count**|**int**|検出されたデータ定義言語 (DDL) 操作の数です。 このカウンターはフェーズ 6 で設定されます。<br /><br /> ときに**session_id** = 0、すべてのセッションの処理済み DDL 操作の数。|  
|**command_count**|**bigint**|処理されたコマンドの数です。<br /><br /> ときに**session_id** = 0、すべてのセッションで処理されたコマンドの数。|  
|**first_begin_cdc_lsn**|**nvarchar(23)**|変更データ キャプチャ トランザクションを含んでいた最初の LSN です。<br /><br /> ときに**session_id** = 0、変更データ キャプチャ トランザクションに含まれる最初の LSN。|  
|**last_commit_cdc_lsn**|**nvarchar(23)**|変更データ キャプチャ トランザクションを含んでいた最終コミット ログ レコードの LSN です。<br /><br /> ときに**session_id**任意のセッションに含まれる変更データ キャプチャ トランザクションの 0、最後のコミット ログ レコードの LSN を =|  
|**last_commit_cdc_time**|**datetime**|変更データ キャプチャ トランザクションを含んでいた最終コミット ログ レコードが処理された時刻です。<br /><br /> ときに**session_id** 0、最後のコミット ログ レコードのセッションに含まれる変更データ キャプチャ トランザクションが時間を = です。|  
|**latency**|**int**|差を秒単位で間**end_time**と**last_commit_cdc_time**セッションでします。 このカウンターはフェーズ 7 の最後に設定されます。<br /><br /> ときに**session_id** = 0、セッションによって記録された最後の待機時間が 0 以外の値。|  
|**empty_scan_count**|**int**|変更データ キャプチャ トランザクションが含まれていなかった、連続するセッションの数です。|  
|**failed_sessions_count**|**int**|失敗したセッションの数です。|  
  
## <a name="remarks"></a>コメント  
 この動的管理ビューでは値がリセットされるたびに、インスタンスの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が開始します。  
  
## <a name="permissions"></a>アクセス許可  
 クエリに対する VIEW DATABASE STATE 権限が必要です、 **sys.dm_cdc_log_scan_sessions**動的管理ビュー。 動的管理ビューに対する権限の詳細については、次を参照してください。[動的管理ビューおよび関数&#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)します。  
  
## <a name="examples"></a>使用例  
 次の例では、最新のセッションの情報を返します。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT session_id, start_time, end_time, duration, scan_phase  
    error_count, start_lsn, current_lsn, end_lsn, tran_count  
    last_commit_lsn, last_commit_time, log_record_count, schema_change_count  
    command_count, first_begin_cdc_lsn, last_commit_cdc_lsn,   
    last_commit_cdc_time, latency, empty_scan_count, failed_sessions_count  
FROM sys.dm_cdc_log_scan_sessions  
WHERE session_id = (SELECT MAX(b.session_id) FROM sys.dm_cdc_log_scan_sessions AS b);  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sys.dm_cdc_errors &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-errors.md)  
  
  

