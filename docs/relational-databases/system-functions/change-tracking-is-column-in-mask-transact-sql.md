---
title: CHANGE_TRACKING_IS_COLUMN_IN_MASK (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_IS_COLUMN_IN_MASK_TSQL
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_IS_COLUMN_IN_MASK
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
ms.assetid: 649b370b-da54-4915-919d-1b597a39d505
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a6f7e9d8d9ab99ebe4a7c5749033eacf85b8feb5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042990"
---
# <a name="changetrackingiscolumninmask-transact-sql"></a>CHANGE_TRACKING_IS_COLUMN_IN_MASK (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  CHANGETABLE(CHANGES...) 関数によって返される SYS_CHANGE_COLUMNS 値を解釈します。 これにより、指定した列が SYS_CHANGE_COLUMNS に返された値に含まれているかどうかを、アプリケーションで判断することができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CHANGE_TRACKING_IS_COLUMN_IN_MASK ( column_id , change_columns )  
```  
  
## <a name="arguments"></a>引数  
 *column_id*  
 チェックする列の ID です。 列の ID を使用して取得できます、 [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md)関数。  
  
 *change_columns*  
 バイナリ データの SYS_CHANGE_COLUMNS 列から、 [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md)データ。  
  
## <a name="return-type"></a>戻り値の型  
 **bit**  
  
## <a name="return-values"></a>戻り値  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK は次の値を返します。  
  
|戻り値|説明|  
|------------------|-----------------|  
|0|指定した列がない、 *change_columns*一覧。|  
|1|指定した列は、 *change_columns*一覧。|  
  
## <a name="remarks"></a>コメント  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK を検証するには、どのチェックは行われず、 *column_id*値、すなわち、 *change_columns*パラメーターは、元のテーブルから取得された、 *column_id*取得されました。  
  
## <a name="examples"></a>使用例  
 次の例を決定するかどうか、`Salary`の列、`Employees`テーブルが更新されました。 `COLUMNPROPERTY`関数の列の ID を返します、`Salary`列。 `@change_columns` CHANGETABLE をデータ ソースとして使用して、クエリの結果をローカル変数を設定する必要があります。  
  
```sql  
SET @SalaryChanged = CHANGE_TRACKING_IS_COLUMN_IN_MASK  
    (COLUMNPROPERTY(OBJECT_ID('Employees'), 'Salary', 'ColumnId')  
    ,@change_columns);  
```  
  
## <a name="see-also"></a>関連項目  
 [変更追跡関数 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [データ変更の追跡 &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
