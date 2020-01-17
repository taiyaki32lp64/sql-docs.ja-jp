---
title: cdc.&lt;capture_instance&gt;_CT (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc
- cdc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.<capture_instance>_CT
ms.assetid: 979c8110-3c54-4e76-953c-777194bc9751
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6595fa2a2462463b9ecc64778af1d72e588477d8
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908396"
---
# <a name="cdcltcapture_instancegt_ct-transact-sql"></a>cdc.&lt;capture_instance&gt;_CT (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  ソース テーブルに対して変更データ キャプチャを有効にすると作成される変更テーブルです。 ソース テーブルに対して実行された操作が挿入や削除の場合は、各操作について 1 行を返します。ソース テーブルに対して実行された操作が更新の場合は、各操作について 2 行を返します。 ソース テーブルで変更データ キャプチャを有効にしたときに変更テーブルの名前を指定しなかった場合は、名前が自動的に生成されます。 名前の形式は cdc です。*capture_instance*_CT。 *capture_instance*は、ソーステーブルのスキーマ名と*schema_table*形式のソーステーブル名です。 たとえば、 **AdventureWorks**サンプルデータベースのテーブルの**ユーザー**が変更データキャプチャを有効にした場合、派生した変更テーブル名は cdc になり**ます。Person_Address_CT**。  
  
 **システムテーブルに対して直接クエリを実行しない**ことをお勧めします。 代わりに、 [fn_cdc_get_all_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)および[cdc. fn_cdc_get_net_changes_](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) < capture_instance 関数を実行します。  
  

  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|変更のコミット トランザクションに関連付けられたログ シーケンス番号 (LSN)。<br /><br /> 同じトランザクションでコミットされたすべての変更は、同じコミット LSN を共有します。 たとえば、ソーステーブルに対する削除操作によって2つの行が削除された場合、変更テーブルには、同じ **__ $ start_lsn**値を持つ2つの行が含まれます。|  
|**__$end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] では、この列は常に NULL です。|  
|**__$seqval**|**binary(10)**|特定のトランザクションに含まれる行の変更を並べ替えるためのシーケンス値。|  
|**__$operation**|**int**|変更に関連付けられているデータ操作言語 (DML) 操作を識別します。 次のいずれかになります。<br /><br /> 1 = 削除<br /><br /> 2 = 挿入<br /><br /> 3 = 更新 (古い値)<br /><br /> 列データには、更新ステートメントを実行する前の行の値が割り当てられます。<br /><br /> 4 = 更新 (新しい値)<br /><br /> 列データには、更新ステートメントを実行した後の行の値が割り当てられます。|  
|**__$update_mask**|**varbinary (128)**|変更された列を識別する、変更テーブルの列序数に基づくビット マスク。|  
|*\< キャプチャ対象のソース テーブルの列 >*|各種|変更テーブル内のその他の列は、ソース テーブルの列のうち、キャプチャ インスタンスの作成時にキャプチャ対象として指定された列です。 キャプチャ対象列リストで列が指定されなかった場合、ソース テーブルのすべての列がこのテーブルに格納されます。|  
|**__ $ command_id** |**int** |トランザクション内の操作の順序を追跡します。 |  
  
## <a name="remarks"></a>Remarks  

`__$command_id` 列の列は、バージョン2012から2016の累積的な更新プログラムで導入されました。 バージョンおよびダウンロードの情報については、 [Microsoft SQL Server データベースに対して変更データキャプチャを有効にした後に、更新された行の変更テーブルの順序が正しく設定さ](https://support.microsoft.com/help/3030352/fix-the-change-table-is-ordered-incorrectly-for-updated-rows-after-you)れ3030352ていないことを確認してください。  詳細については、 [SQL Server 2012、2014、2016の最新の CU にアップグレードした後に、CDC の機能が停止する場合があり](https://blogs.msdn.microsoft.com/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016/)ます。

## <a name="captured-column-data-types"></a>キャプチャ対象列のデータ型  
 このテーブルに含まれるキャプチャ対象列は、ソースの対応する列と同じデータ型および値を持ちます。ただし、次の例外があります。  
  
-   **Timestamp**列は**binary (8)** として定義されます。  
  
-   **Id**列は、 **int**または**bigint**として定義されます。  
  
 ただし、これらの列の値は、ソース列の値と同じです。  
  
### <a name="large-object-data-types"></a>ラージ オブジェクト データ型  
 __ $ Operation = 1 または \_\_$operation = 3 の場合、データ型**image**、 **text**、および**ntext**の列には常に**NULL**値が割り当てられます。 データ型**varbinary (max)** 、 **varchar (max)** 、または**nvarchar (max)** の列には、更新中に列が変更されていない限り、\_\_$operation = 3 を指定すると**NULL**値が割り当てられます。 \_\_$operation = 1 の場合、これらの列には削除時に値が割り当てられます。 キャプチャインスタンスに含まれる計算列の値は、常に**NULL**になります。  
  
 既定では、INSERT、UPDATE、WRITETEXT、または UPDATETEXT の 1 回のステートメントでキャプチャ対象列に追加できる最大サイズは、65,536 バイト (64 KB) です。 大きな LOB データをサポートするためにこのサイズを大きくするには、 [max text repl Size サーバー構成オプション](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md)を使用して、より大きな最大サイズを指定します。 詳細については、「 [max text repl size サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md)」を参照してください。  
  
## <a name="data-definition-language-modifications"></a>データ定義言語の修正  
 列の追加や削除など、ソーステーブルに対する DDL の変更は、 [ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)テーブルに記録されます。 これらの変更は変更テーブルに適用されません。 つまり、変更テーブルの定義は以前のままとなります。 ソース テーブルには、キャプチャ対象列リストが関連付けられていますが、キャプチャ プロセスで変更テーブルに行を挿入する際、そのリストに存在しない列は無視されます。 キャプチャ対象列リストに指定されていた列が、ソース テーブルから既に削除されていた場合、その列には NULL 値が割り当てられます。  
  
 ソーステーブル内の列のデータ型を変更することは、 [ddl_history](../../relational-databases/system-tables/cdc-ddl-history-transact-sql.md)テーブルにも記録されます。 ただし、この変更によって、変更テーブルの定義が修正されることはありません。 ソース テーブルに対する DDL 変更のログ レコードがキャプチャ プロセスで見つかった場合は、変更テーブルにおけるキャプチャ対象列のデータ型が変更されます。  
  
 ソース テーブルにおけるキャプチャ対象列のデータ型を、より小さなデータ型に変更する必要がある場合は、次の手順に従って、変更テーブル内の対応する列が正しく変更されるように配慮してください。  
  
1.  ソース テーブルで、変更する列の値を、変更後のデータ型に収まるように更新します。 たとえば、データ型を**int**から**smallint**に変更する場合は、値を**smallint**の範囲に収まる-32768 から32767に更新します。  
  
2.  変更テーブル側の対応する列にも、同じ更新操作を実行します。  
  
3.  ソース テーブル側で新しいデータ型を指定します。 データ型の変更が正しく変更テーブルに反映されます。  

## <a name="data-manipulation-language-modifications"></a>データ操作言語の変更  
 変更データ キャプチャが有効になっているソース テーブルに対して挿入、更新、削除の各操作を実行すると、それらの DML 操作のレコードがデータベース トランザクション ログに表示されます。 変更データキャプチャプロセスでは、これらの変更に関する情報をトランザクションログから取得し、変更を記録するために1つまたは2つの行を変更テーブルに追加します。 エントリは、ソース テーブルでコミットされたときと同じ順序で変更テーブルに追加されますが、変更テーブルのエントリのコミットは通常 1 つのエントリではなく変更のグループに対して実行される必要があります。  
  
 変更テーブルエントリ内では、 **__ $ start_lsn**列を使用して、ソーステーブルへの変更に関連付けられているコミット lsn を記録し、 **__ $ seqval 列**を使用してそのトランザクション内の変更を順序付けします。 これらのメタデータ列を使用して、ソース変更のコミット順を維持することができます。 キャプチャ プロセスではトランザクション ログから変更情報を取得するため、変更テーブルのエントリが、対応するソース テーブルの変更と同期して表示されていないか確認することが重要です。 代わりに、キャプチャ プロセスがトランザクション ログから関連の変更エントリを処理した後、対応する変更が非同期で表示されます。  
  
 挿入操作と削除操作については、更新マスクのすべてのビットが設定されます。 更新操作の場合、更新操作中に変更された列を反映するため、update old 行と update new 行の両方の更新マスクが変更されます。  
  
## <a name="see-also"></a>参照  
 [sp_cdc_enable_table &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sp_cdc_get_ddl_history &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)  
  
  
