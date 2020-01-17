---
title: sys.fn_cdc_increment_lsn (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_cdc_increment_lsn_TSQL
- sys.fn_cdc_increment_lsn_TSQL
- sys.fn_cdc_increment_lsn
- fn_cdc_increment_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_increment_lsn
- sys.fn_cdc_increment_lsn
ms.assetid: e53b6703-358b-4c9a-912a-8f7c7331069b
author: rothja
ms.author: jroth
ms.openlocfilehash: a482acb22ad535e44d6ceb06a20474945a477e58
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046369"
---
# <a name="sysfncdcincrementlsn-transact-sql"></a>sys.fn_cdc_increment_lsn (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定された LSN の直後のログ シーケンス番号 (LSN) を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_cdc_increment_lsn ( lsn_value )  
```  
  
## <a name="arguments"></a>引数  
 *lsn_value*  
 LSN 値を指定します。 *lsn_value*は**binary (10)** します。  
  
## <a name="return-type"></a>戻り値の型  
 **binary(10)**  
  
## <a name="remarks"></a>コメント  
 関数によって返される LSN 値は常に指定した値より大きくして、2 つの値の間に LSN 値が存在しません。  
  
 時間の経過と共に変更データのストリームを体系的にクエリするには、クエリ関数の呼び出しを繰り返すことができますたびに、変更をバインドする新しいクエリ間隔を指定することが、クエリで返される、定期的にします。 データが失われないことを保証するうえには、後続のクエリの下限の境界を生成する前のクエリの上限の境界がよく使用されます。 クエリ間隔は、閉区間であるため、新しい下限の境界は以前の上限より大きくする必要がありますが、この値は、以前の上限値の間に LSN 値を変更しないようにするために十分小さいがあります。 sys.fn_cdc_increment_lsn 関数は、このような値を取得するために使用します。  
  
## <a name="permissions"></a>アクセス許可  
 public データベース ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、前回のクエリ時に保存した上限を `sys.fn_cdc_increment_lsn` 変数に格納し、それを `@save_to_lsn` 関数に渡すことによって、変更データ キャプチャ クエリに使用する新しい下限値を取得しています。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10), @save_to_lsn binary(10);  
SET @save_to_lsn = <previous_upper_bound_value>;  
SET @from_lsn = sys.fn_cdc_increment_lsn(@save_to_lsn);  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SELECT * from cdc.fn_cdc_get_all_changes_HumanResources_Employee( @from_lsn, @to_lsn, 'all' );  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sys.fn_cdc_decrement_lsn &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [トランザクション ログ &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
