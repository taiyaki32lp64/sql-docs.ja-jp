---
title: cdc.fn_cdc_get_net_changes_&lt;capture_instance&gt; (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_net_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_net_changes_<capture_instance>
ms.assetid: 43ab0d1b-ead4-471c-85f3-f6c4b9372aab
author: rothja
ms.author: jroth
ms.openlocfilehash: 77fb03c71bd0773cc8f004a89c28c1925284876b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043045"
---
# <a name="cdcfncdcgetnetchangesltcaptureinstancegt-transact-sql"></a>cdc.fn_cdc_get_net_changes_&lt;capture_instance&gt; (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  指定したログ シーケンス番号 (LSN) 範囲内で変更されたソース行ごとに 1 つの差分変更行を返します。  
  
 **待ってください、LSN とは何ですか。** すべてのレコード、 [SQL Server トランザクション ログ](../logs/the-transaction-log-sql-server.md)はログ シーケンス番号 (LSN) によって一意に識別します。 Lsn は、LSN2 が LSN1 より大きい場合は、LSN2 によって参照されるログ レコードで説明した変更が発生するように順序付けられている**後**でログ レコードの LSN。  
  
 重大なイベントが発生したログ レコードの LSN は、適切な復元シーケンスを構築するために役立ちます。 等号または不等号の比較は Lsn は順序付けられているため (つまり、 \<、>、=、 \<=、> =)。 このような比較は、復元シーケンスを構築するときに役立ちます。  
  
 ソース行は、複数の変更を LSN 範囲の中には、以下で説明する列挙関数によって、行の最終的な内容を反映する 1 つの行が返されます。 たとえば、トランザクションは、ソース テーブルに行を挿入すると、LSN 範囲内の後続のトランザクションがその行の 1 つまたは複数の列を更新、関数のみを返します**1 つ**行で、更新された列の値が含まれています。  
  
 この列挙関数は、ソース テーブルに対して変更データ キャプチャを有効にし、かつ、差分追跡を指定した場合に作成されます。 差分追跡を有効にするには、ソース テーブルに主キーまたは一意のインデックスが必要です。 関数の名前は派生し、形式 cdc.fn_cdc_get_net_changes_*capture_instance*ここで、 *capture_instance*が値をソース テーブルが、キャプチャ インスタンスの指定変更データ キャプチャを有効にします。 詳細については、次を参照してください。 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
cdc.fn_cdc_get_net_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all with mask  
 | all with merge  
}  
```  
  
## <a name="arguments"></a>引数  
 *from_lsn*  
 結果セットに含める LSN 範囲の下端を表す LSN を指定します。 *from_lsn*は**binary (10)** します。  
  
 内の行のみ、 [cdc&#91; 。capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) _ _ $start_lsn より大きいまたは等しい値を持つテーブルを変更する*from_lsn*結果セットに含まれます。  
  
 *to_lsn*  
 結果セットに含める LSN 範囲の上端を表す LSN を指定します。 *to_lsn*は**binary (10)** します。  
  
 内の行のみ、 [cdc&#91; 。capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) _ _ $start_lsn に以下の値を持つテーブルを変更する*from_lsn*以上*to_lsn*結果セットに含まれます。  
  
 *< row_filter_option >* :: = {すべて | マスク | すべてのマージで}  
 結果セットで返される行と同様に、メタデータ列の内容を制御するオプション。 次のいずれかのオプションを指定できます。  
  
 all  
 行およびメタデータ列 _ _ $start_lsn の行に適用するために必要な操作に最終的な変更の LSN を返しますと\_ \_$operation します。 列\_ \_$update_mask は常に NULL です。  
  
 all with mask  
 行およびメタデータ列 _ _ $start_lsn の行に適用するために必要な操作に最終的な変更の LSN を返しますと\_ \_$operation します。 さらに、更新操作を返す場合 (\_\_$operation = 4) で返される値で更新プログラムで変更されたキャプチャ対象列がマークされている\_ \_$update_mask します。  
  
 all with merge  
 行に対する最終的な変更の LSN が、メタデータ列 __$start_lsn に返されます。 列\_ \_$operation には、2 つの値のいずれかになります。削除と変更を適用するために必要な操作が挿入または更新プログラムのいずれかであることを示す 5 の場合は 1 です。 列\_ \_$update_mask は常に NULL です。  
  
 特定の変更に必要な操作を厳密に特定するロジックではクエリが複雑になってしまいます。そのため、このオプションでは、変更データの適用に必要な操作が、挿入と更新のいずれかであることがわかればよく、両者を明確に区別する必要がない場合に、より高いパフォーマンスでクエリを実行できるように設計されています。 このオプションは、マージ操作が、直接などに使用できるターゲット環境で最も魅力的な[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]環境。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|__$start_lsn|**binary(10)**|変更のコミット トランザクションに関連付けられた LSN。<br /><br /> 同じトランザクションでコミットされたすべての変更は、同じコミット LSN を共有します。 たとえば、ソース テーブルに対する update 操作では、2 つの行に 2 つの列を変更、変更テーブルには 4 つの行がすべて同じ _ _ $start_lsnvalue が含まれます。|  
|__$operation|**int**|変更データの行をターゲット データ ソースに適用するために必要となった DML (データ操作言語) 操作を識別します。<br /><br /> row_filter_option パラメーターの値が all または all with mask である場合、この列の値には、次のいずれかの値を指定できます。<br /><br /> 1 = 削除<br /><br /> 2 = 挿入<br /><br /> 4 = 更新<br /><br /> row_filter_option パラメーターの値が all with merge である場合、この列の値には、次のいずれかの値を指定できます。<br /><br /> 1 = 削除|  
|__$update_mask|**varbinary (128)**|キャプチャ インスタンスに対して指定された各キャプチャ対象列に対応するビットを持ったビット マスク。 __$operation が 1 または 2 の場合、定義されているすべてのビットが 1 に設定されます。 ときに\_ \_$operation = 3 または 4、変更された列に対応するビットだけが 1 に設定されます。|  
|*\< キャプチャ対象のソース テーブルの列 >*|各種|この関数によって返されるその他の列は、ソース テーブルの列のうち、キャプチャ インスタンスの作成時にキャプチャ対象として指定された列です。 キャプチャ対象列リストで列が指定されなかった場合、ソース テーブルのすべての列が返されます。|  
  
## <a name="permissions"></a>アクセス許可  
 固定サーバー ロール sysadmin または固定データベース ロール db_owner のメンバーシップが必要です。 それ以外のすべてのユーザーについては、ソース テーブルのすべてのキャプチャ対象列に対する SELECT 権限が必要です。さらに、キャプチャ インスタンスのゲーティング ロールが定義されている場合は、そのデータベース ロールのメンバーシップが必要です。 呼び出し元にソース データを表示する権限がなかった場合、エラー 208 (無効なオブジェクト名) が返されます。  
  
## <a name="remarks"></a>コメント  
 指定した LSN 範囲が、キャプチャ インスタンスの変更追跡時間外に該当した場合、エラー 208 (無効なオブジェクト名) が返されます。

 行の一意識別子で変更には、削除による初期の UPDATE コマンドを表示し、コマンドの代わりに挿入し、fn_cdc_get_net_changes が発生します。  この動作は前に、と変更後の両方にキーを追跡する必要があります。
  
## <a name="examples"></a>使用例  
 次の例では、関数を使用して`cdc.fn_cdc_get_net_changes_HR_Department`net に、ソース テーブルに加えられた変更をレポートする`HumanResources.Department`特定の時間間隔中にします。  
  
 まず、`GETDATE`関数を使用して、時間間隔の開始をマークします。 ソース テーブルに対して複数の DML ステートメントを適用した後、再び `GETDATE` 関数を呼び出して期間の終わりを指定します。 関数は、 [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)しに LSN 値で範囲指定された変更データ キャプチャのクエリ範囲を時間間隔をマップするために使用します。 最後に、`cdc.fn_cdc_get_net_changes_HR_Department` 関数を呼び出して、該当期間中に行われたソース テーブルへの差分変更を取得します。 挿入後に削除された行については、関数から返される結果セットに含まれません。 たとえ行を追加しても、同じ期間内に削除されれば、その期間におけるソース テーブルへの差分変更とはならないためです。 この例を実行する前に、例 B を初めて実行する必要があります[sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)します。  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @begin_time datetime, @end_time datetime, @from_lsn binary(10), @to_lsn binary(10);  
-- Obtain the beginning of the time interval.  
SET @begin_time = GETDATE() -1;  
-- DML statements to produce changes in the HumanResources.Department table.  
INSERT INTO HumanResources.Department (Name, GroupName)  
VALUES (N'MyDept', N'MyNewGroup');  
  
UPDATE HumanResources.Department  
SET GroupName = N'Resource Control'  
WHERE GroupName = N'Inventory Management';  
  
DELETE FROM HumanResources.Department  
WHERE Name = N'MyDept';  
  
-- Obtain the end of the time interval.  
SET @end_time = GETDATE();  
-- Map the time interval to a change data capture query range.  
SET @from_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than or equal', @begin_time);  
SET @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);  
  
-- Return the net changes occurring within the query window.  
SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@from_lsn, @to_lsn, 'all');  
```  
  
## <a name="see-also"></a>参照  
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [変更データ キャプチャについて &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
