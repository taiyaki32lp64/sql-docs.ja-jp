---
title: cdc.ddl_history (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.ddl_history_TSQL
- cdc.ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.ddl_history
ms.assetid: cb97ea71-da2f-441a-bbd2-db1f5f48ab49
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1855120dde6e6f4e9037a6f14832cd24f310d77b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079225"
---
# <a name="cdcddlhistory-transact-sql"></a>cdc.ddl_history (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  変更データ キャプチャが有効になっているテーブルに対して行われたデータ定義言語 (DDL) の変更について、各変更に対応する 1 行を返します。 このテーブルでは、ソース テーブルに対して、いつ、どのような DDL の変更が行われたかを確認できます。 DDL の変更されていないソース テーブルでは、このテーブル内のエントリは必要はありません。  
  
 システム テーブルに対して直接クエリを実行することは、できるだけ避けてください。 代わりに、実行、 [sys.sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)ストアド プロシージャ。  
   
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**source_object_id**|**int**|DDL の変更が適用された元のテーブルの ID。|  
|**object_id**|**int**|ソース テーブルに対してキャプチャ インスタンスに関連付けられている変更テーブルの ID。|  
|**required_column_update**|**bit**|ソース テーブルのキャプチャ対象列のデータ型が変更されたことを示します。 この変更は、変更テーブル内の列を変更します。|  
|**ddl_command**|**nvarchar(max)**|DDL ステートメントは、ソース テーブルに適用します。|  
|**ddl_lsn**|**binary(10)**|ログ シーケンス番号 (LSN) の DDL 変更のコミットに関連付けられています。|  
|**ddl_time**|**datetime**|DDL の変更された日付と時刻は、ソース テーブルにしました。|  
  
## <a name="see-also"></a>関連項目  
 [sys.sp_cdc_help_change_data_capture &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
