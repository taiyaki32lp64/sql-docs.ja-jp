---
title: cdc.fn_cdc_get_all_changes_&lt;capture_instance&gt; (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_all_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_all_changes_<capture_instance>
ms.assetid: c6bad147-1449-4e20-a42e-b51aed76963c
author: rothja
ms.author: jroth
ms.openlocfilehash: 0a4e0e62121d289f9eb897c79abb2991a57890a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043050"
---
# <a name="cdcfncdcgetallchangesltcaptureinstancegt--transact-sql"></a>cdc.fn_cdc_get_all_changes_&lt;capture_instance&gt; (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定されたログ シーケンス番号 (LSN) の範囲内で、ソース テーブルに適用された各変更につき 1 行を返します。 該当する期間中、1 つのソース行に複数の変更が加えられた場合、返される結果セットには、それぞれの変更が格納されます。 返された変更データおよび 4 つのメタデータ列によって、他のデータ ソースにその変更を適用するために必要な情報を得ることができます。 結果セットとして返される行およびメタデータ列の内容は、行のフィルター選択オプションによって制御されます。 行のフィルター選択オプションに 'all' を指定した場合、それぞれの変更について、対応する 1 行が返されます。 'all update old' オプションを指定した場合、更新操作は、更新前と更新後のキャプチャ対象列の値を格納する 2 つの行で表されます。  
  
 この列挙関数は、ソース テーブルに対して変更データ キャプチャを有効にした時点で作成されます。 関数の名前は派生し、形式を使用して**cdc.fn_cdc_get_all_changes_** _capture_instance_場所*capture_instance*キャプチャ用に指定された値は、ソース テーブルが変更データ キャプチャの有効な場合はインスタンス。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
cdc.fn_cdc_get_all_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all update old  
}  
```  
  
## <a name="arguments"></a>引数  
 *from_lsn*  
 結果セットに含める LSN 範囲の下端を表す LSN 値を指定します。 *from_lsn*は**binary (10)** します。  
  
 内の行のみ、 [cdc&#91; 。capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)で値を持つテーブルを変更する **_ _ $start_lsn**より大きいまたは等しい*from_lsn*結果セットに含まれます。  
  
 *to_lsn*  
 結果セットに含める LSN 範囲の上端を表す LSN 値を指定します。 *to_lsn*は**binary (10)** します。  
  
 内の行のみ、 [cdc&#91; 。capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md)で値を持つテーブルを変更する **_ _ $start_lsn**に等しいまたはそれよりも小さい*from_lsn*以上*to_lsn*が含まれています結果セット。  
  
 <row_filter_option> ::= { all | all update old }  
 結果セットで返される行と同様に、メタデータ列の内容を制御するオプション。  
  
 次のいずれかのオプションを指定できます。  
  
 all  
 指定された LSN 範囲内のすべての変更を返します。 更新操作で生じた変更の場合、更新適用後の新しい値を格納した行だけが返されます。  
  
 all update old  
 指定された LSN 範囲内のすべての変更を返します。 更新操作のための変更は、このオプションは、更新前に列の値を含む行と更新後の列の値を含む行の両方を返します。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|変更に関連付けられたコミット LSN。この LSN によって変更のコミット順が維持されます。 同じトランザクションでコミットされた変更は、同じコミット LSN 値を共有します。|  
|**__$seqval**|**binary(10)**|シーケンス値が、トランザクション内で行の順序変更するために使用します。|  
|**__$operation**|**int**|変更データの行をターゲット データ ソースに適用するために必要となった DML (データ操作言語) 操作を識別します。 次のいずれかになります。<br /><br /> 1 = 削除<br /><br /> 2 = 挿入<br /><br /> 3 = 更新 (キャプチャされる列値は更新操作前の値)。 この値が該当するのは、行フィルター オプションに 'all update old' を指定した場合だけです。<br /><br /> 4 = 更新 (キャプチャされる列値は更新操作後の値)|  
|**__$update_mask**|**varbinary (128)**|キャプチャ インスタンスに対して指定された各キャプチャ対象列に対応するビットを持ったビット マスク。 この値がすべて定義すると 1 に設定されたビット **_ _ $操作**= 1 または 2 です。 ときに **_ _ $操作**= 3 または 4、変更された列に対応するビットだけが 1 に設定されます。|  
|**\< キャプチャ対象のソース テーブルの列 >**|各種|この関数によって返されるその他の列は、キャプチャ インスタンスの作成時に指定されたキャプチャ対象列です。 キャプチャ対象列リストで列が指定されなかった場合、ソース テーブルのすべての列が返されます。|  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **sysadmin**固定サーバー ロールまたは**db_owner**固定データベース ロール。 それ以外のすべてのユーザーについては、ソース テーブルのすべてのキャプチャ対象列に対する SELECT 権限が必要です。さらに、キャプチャ インスタンスのゲーティング ロールが定義されている場合は、そのデータベース ロールのメンバーシップが必要です。 関数が、エラー 229 を返します、呼び出し元にソース データを表示するアクセス許可がないとき ("SELECT 権限が拒否されましたオブジェクト 'fn_cdc_get_all_changes_...'、データベース '\<DatabaseName >'、スキーマ 'cdc' です。")。  
  
## <a name="remarks"></a>コメント  
 指定した LSN 範囲が、キャプチャ インスタンスの変更追跡時間外に該当した場合、エラー 208 ("プロシージャまたは関数 cdc.fn_cdc_get_all_changes に指定された引数が不足しています。") が返されます。  
  
 データ型の列**イメージ**、**テキスト**、および**ntext**常に NULL が割り当てられている値と **_ _ $操作**= 1 または **_ _ $操作**= 3。 データ型の列**varbinary (max)** 、 **varchar (max)** 、または**nvarchar (max)** NULL が割り当てられている値と **_ _ $操作**3 を =しない限り、列が更新中に変更します。 ときに **_ _ $操作**= 1、これらの列には、削除時にその値が割り当てられます。 キャプチャ インスタンスに含まれる計算列の値は、常に NULL になります。  
  
## <a name="examples"></a>使用例  
 いくつか[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]テンプレートは、変更データ キャプチャ クエリ関数を使用する方法を示します。 これらのテンプレートでは、**ビュー**メニュー[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]します。 詳細については、次を参照してください。[テンプレート エクスプ ローラー](../../ssms/template/template-explorer.md)します。  
  
 この例は、`Enumerate All Changes for Valid Range Template` を示しています。 この例では、関数 `cdc.fn_cdc_get_all_changes_HR_Department` を使用して、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内の HumanResources.Department ソース テーブルに対して定義されているキャプチャ インスタンス `HR_Department` で現在使用できる変更をすべてレポートします。  
  
```  
-- ========  
-- Enumerate All Changes for Valid Range Template  
-- ========  
USE AdventureWorks2012;  
GO  
  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HR_Department');  
SET @to_lsn   = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HR_Department  
  (@from_lsn, @to_lsn, N'all');  
GO  
```  
  
## <a name="see-also"></a>参照  
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sys.sp_cdc_get_ddl_history &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)   
 [sys.sp_cdc_get_captured_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
