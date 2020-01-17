---
title: sys.fn_cdc_has_column_changed (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_has_column_changed_TSQL
- sys.fn_cdc_has_column_changed
- fn_cdc_has_column_changed_TSQL
- fn_cdc_has_column_changed
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_cdc_has_column_changed
- fn_cdc_has_column_changed
ms.assetid: 2b9e6278-050d-4ffc-8d1a-09606180facc
author: rothja
ms.author: jroth
ms.openlocfilehash: 9c409581771055e2c6d85d2cdd01937e2f033ba9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046382"
---
# <a name="sysfncdchascolumnchanged-transact-sql"></a>sys.fn_cdc_has_column_changed (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新マスクは、関連する変更行で指定された列が更新されたことを示すかどうかを識別します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_cdc_has_column_changed ( 'capture_instance','column_name' , update_mask )  
```  
  
## <a name="arguments"></a>引数  
 **'** *capture_instance* **'**  
 キャプチャ インスタンスの名前を指定します。 *capture_instance*は**sysname**します。  
  
 **'** *column_name* **'**  
 指定したキャプチャ インスタンスのレポート対象となるキャプチャ対象列を指定します。 *column_name*は**sysname**します。  
  
 *update_mask*  
 関連する変更行の列を更新マスクを識別します。 *update_mask*は**varbinary (128)** します。  
  
## <a name="return-type"></a>戻り値の型  
 **bit**  
  
## <a name="remarks"></a>コメント  
 この関数を使用すると、変更データのクエリで返された更新マスクから情報を抽出します。 関連する変更行の特定の列が変更されているかどうかを把握する必要がある場合、更新マスクの後処理で便利です。 詳細については、「[変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)」を参照してください。  
  
 関数を使用することをお勧めこの情報は、変更データ クエリの一部として返されます、 [sys.fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md)と[sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md)この関数の代わりにします。 必要な列序数が 1 回しか計算されないようにするために、変更データを照会する前に fn_cdc_get_column_ordinal 関数を使用します。 クエリ内で fn_cdc_is_bit_set を使用して、返された各行の更新マスクから情報を抽出します。  
  
## <a name="permissions"></a>アクセス許可  
 固定サーバー ロール sysadmin または固定データベース ロール db_owner のメンバーシップが必要です。 それ以外のすべてのユーザーについては、ソース テーブルのすべてのキャプチャ対象列に対する SELECT 権限が必要です。さらに、キャプチャ インスタンスのゲーティング ロールが定義されている場合は、そのデータベース ロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>関連項目  
 [cdc です。&#60;capture_instance&#62;_CT &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)   
 [cdc.captured_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/cdc-captured-columns-transact-sql.md)  
  
  
