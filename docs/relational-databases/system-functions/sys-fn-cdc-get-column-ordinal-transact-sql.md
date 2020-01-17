---
title: sys.fn_cdc_get_column_ordinal (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_get_column_ordinal
- fn_cdc_get_column_ordinal_TSQL
- fn_cdc_get_column_ordinal
- sys.fn_cdc_get_column_ordinal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_column_ordinal
- sys.fn_cdc_get_column_ordinal
ms.assetid: 4bb21a57-2b94-4208-8bdf-6a3e2681d881
author: rothja
ms.author: jroth
ms.openlocfilehash: 893c7b0a4c7c88c0fdc7bf89b01b61bfaae6f2f4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046500"
---
# <a name="sysfncdcgetcolumnordinal-transact-sql"></a>sys.fn_cdc_get_column_ordinal (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  表示されます、として指定された列の列の序数を返します、[変更テーブル](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)指定したキャプチャ インスタンスに関連付けられています。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_cdc_get_column_ordinal ( 'capture_instance','column_name')  
```  
  
## <a name="arguments"></a>引数  
 **'** *capture_instance* **'**  
 指定された列がキャプチャ対象列として識別されるキャプチャ インスタンスの名前です。 *capture_instance*は**sysname**します。  
  
 **'** *column_name* **'**  
 レポートに列です。 *column_name*は**sysname**します。  
  
## <a name="return-type"></a>戻り値の型  
 **int**  
  
## <a name="remarks"></a>コメント  
 この関数は、変更データ キャプチャの更新マスク内のキャプチャ対象列の序数位置を識別するために使用されます。 これは、関数と組み合わせてで使用して主[sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md)変更データのクエリを実行するときに、更新マスクから情報を抽出します。  
  
## <a name="permissions"></a>アクセス許可  
 ソース テーブルのすべてのキャプチャ対象列に対する SELECT 権限が必要です。 場合は、データベース ロールの変更データ キャプチャ コンポーネントには、キャプチャ インスタンスが指定されて、そのロールのメンバーシップも必要にです。  
  
## <a name="examples"></a>使用例  
 次の例では、`VacationHours` キャプチャ インスタンスの更新マスク内の、`HumanResources_Employee` 列の序数位置を取得します。 さらに、この値を `sys.fn_cdc_is_bit_set` 関数の中で使用し、返された更新マスクから情報を抽出します。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10),  @VacationHoursOrdinal int;  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SET @VacationHoursOrdinal = sys.fn_cdc_get_column_ordinal   
    ( 'HumanResources_Employee','VacationHours');  
SELECT *, sys.fn_cdc_is_bit_set(@VacationHoursOrdinal,  
    __$update_mask) as 'VacationHours'  
FROM cdc.fn_cdc_get_net_changes_HumanResources_Employee  
    ( @from_lsn, @to_lsn, 'all with mask');  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [変更データ キャプチャの関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [sys.sp_cdc_help_change_data_capture &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [sys.sp_cdc_get_captured_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [sys.fn_cdc_is_bit_set &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md)  
  
  
