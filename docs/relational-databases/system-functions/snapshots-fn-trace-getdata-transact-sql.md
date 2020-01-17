---
title: snapshots.fn_trace_getdata (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- snapshots.fn_trace_getdata
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots.fn_trace_getdata function
ms.assetid: ac28ef48-f4f4-4bf2-ba22-d44e1be88172
author: rothja
ms.author: jroth
ms.openlocfilehash: a85a911d4c9f5cd4565e9839f3be44a4e2366079
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067753"
---
# <a name="snapshotsfntracegetdata-transact-sql"></a>snapshots.fn_trace_getdata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  この関数は、指定されたトレースにキャプチャされたすべてのイベントを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
snapshots.fn_trace_gettable ( trace_info_id, start_time, end_time )  
```  
  
## <a name="arguments"></a>引数  
 *trace_info_id*  
 ウェアハウス データベースの管理データに snapshots.trace_info テーブルの主キーの一意の識別子。 *trace_info_id*は**int**します。  
  
 *start_time*  
 トレースが開始された時刻。 *start_time*は**datetime**します。  
  
 *end_time*  
 トレースが終了した時刻。 *end_time*は**datetime**します。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|\<すべてのトレース列 >|\<異なる >|管理データ ウェアハウス データベースの snapshots.trace_data テーブルからのトレース データ。<br /><br /> 指定されたトレースの列の一覧は、次のクエリを使用して取得できます。<br /><br /> `SELECT * FROM sys.trace_columns`<br /><br /> **注:** Snapshots.fn_trace_gettable 関数から返される列は、sys.trace_columns システム ビュー内の name 列の値に対応します。 この関数から GroupID 列が返されない点のみが異なります。|  
  
## <a name="permissions"></a>アクセス許可  
 mdw_reader に対する SELECT 権限が必要です。  
  
## <a name="see-also"></a>関連項目  
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
