---
title: sys.fn_cdc_map_time_to_lsn (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_map_time_to_lsn
- fn_cdc_map_time_to_lsn_TSQL
- sys.fn_cdc_map_time_to_lsn_TSQL
- fn_cdc_map_time_to_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_map_time_to_lsn
- sys.fn_cdc_map_time_to_lsn
ms.assetid: 6feb051d-77ae-4c93-818a-849fe518d1d4
author: rothja
ms.author: jroth
ms.openlocfilehash: 7f4f6820aeeca8b600631810ed35933d2519b495
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68046330"
---
# <a name="sysfncdcmaptimetolsn-transact-sql"></a>sys.fn_cdc_map_time_to_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ログ シーケンス番号 (LSN) の値を返します、 **start_lsn**内の列、 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)が指定した期間のシステム テーブル。 この関数を使用するには、変更データ キャプチャの列挙関数で必要な LSN ベースの範囲に日付時刻範囲を体系的にマップする[cdc.fn_cdc_get_all_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)と[cdc.fn_cdc_get_net_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)その範囲内のデータ変更を取得します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_cdc_map_time_to_lsn ( '<relational_operator>', tracking_time )  
  
<relational_operator> ::=  
{  largest less than  
 | largest less than or equal  
 | smallest greater than  
 | smallest greater than or equal  
}  
```  
  
## <a name="arguments"></a>引数  
 **'** < relational_operator > **'** {よりも少ない最大 | よりも少ない最も大きいまたは等しい | 最小値を超える | 最小値より大きいか等しい}  
 内の個別の LSN 値を識別するために使用、 **cdc.lsn_time_mapping**関連付けられているテーブル**tran_end_time**と比較するとの関係を満たす、 *tracking_time*値。  
  
 *relational_operator*は**nvarchar (30)** します。  
  
 *tracking_time*  
 照合する datetime 値です。 *tracking_time*は**datetime**します。  
  
## <a name="return-type"></a>戻り値の型  
 **binary(10)**  
  
## <a name="remarks"></a>コメント  
 理解する方法、 **sys.fn_cdc_map_time_lsn**日付時刻範囲を LSN 範囲にマップを次のシナリオをご検討ください使用できます。 変更データを毎日抽出するとします。 つまり、特定の日の午前 0 時までに発生した変更を取得する必要があります。 前の日の午前 0 時まで、時間の範囲の下限の境界となります。 指定した日の午前 0 時を含む、上限となります。 次の例はどのように関数**sys.fn_cdc_map_time_to_lsn**体系的にこの時間ベースの範囲をすべて取得する、変更データ キャプチャの列挙関数に必要な LSN ベースの範囲にマップするために使用できます範囲内の変更。  
  
 `DECLARE @begin_time datetime, @end_time datetime, @begin_lsn binary(10), @end_lsn binary(10);`  
  
 `SET @begin_time = '2007-01-01 12:00:00.000';`  
  
 `SET @end_time = '2007-01-02 12:00:00.000';`  
  
 `SELECT @begin_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than', @begin_time);`  
  
 `SELECT @end_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);`  
  
 `SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@begin_lsn, @end_lsn, 'all` `');`  
  
 関係演算子 '`smallest greater than`' 前日の午前 0 時後に発生したものに変更を制限するために使用します。 複数のエントリをさまざまな LSN 値を共有する場合、 **tran_end_time**内の下限として識別される値、 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)テーブル、関数はことを確認する最小の LSN を返しますすべてのエントリが含まれます。 関係演算子いる上限の '`largest less than or equal to`' 範囲に、1 日の午前 0 時を持つすべてのエントリが含まれていることを確認するために使用、 **tran_end_time**値。 複数のエントリをさまざまな LSN 値を共有する場合、 **tran_end_time**上限関数として識別される値はすべてのエントリが含まれる最大の LSN を返します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`sys.fn_cdc_map_time_lsn`内の行があるかどうかを判断する関数、 [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)を持つテーブルを**tran_end_time**値が午前 0 時以上です。 このクエリは、続行できるかどうか、キャプチャ プロセスが既に処理前の日の午前 0 時からコミットされた変更の抽出は、その日のデータを変更できるように、判断に使用できます。  
  
```  
DECLARE @extraction_time datetime, @lsn binary(10);  
SET @extraction_time = '2007-01-01 12:00:00.000';  
SELECT @lsn = sys.fn_cdc_map_time_to_lsn ('smallest greater than or equal', @extraction_time);  
IF @lsn IS NOT NULL  
BEGIN  
<some action>  
END  
```  
  
## <a name="see-also"></a>関連項目  
 [cdc.lsn_time_mapping &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [sys.fn_cdc_map_lsn_to_time &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
