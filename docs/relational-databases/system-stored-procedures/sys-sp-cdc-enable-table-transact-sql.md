---
title: sys.sp_cdc_enable_table (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_enable_table_TSQL
- sp_cdc_enable_table_TSQL
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], enabling tables
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
ms.assetid: 26150c09-2dca-46ad-bb01-3cb3165bcc5d
author: rothja
ms.author: jroth
ms.openlocfilehash: b846ff31d4acbc9d87f66a76a19f688384c88982
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106459"
---
# <a name="syssp_cdc_enable_table-transact-sql"></a>sys.sp_cdc_enable_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  現在のデータベース内の指定したソース テーブルを対象に変更データ キャプチャを有効にします。 テーブルに対して変更データ キャプチャが有効の場合は、テーブルに適用される各データ操作言語 (DML) 操作の記録がトランザクション ログに書き込まれます。 変更データ キャプチャのプロセスはログからこの情報を取得し、一連の関数を使用してアクセスできる変更テーブルに書き込みます。  
  
 変更データ キャプチャは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_enable_table   
  [ @source_schema = ] 'source_schema',   
  [ @source_name = ] 'source_name' ,  [,[ @capture_instance = ] 'capture_instance' ]  
  [,[ @supports_net_changes = ] supports_net_changes ]  
  , [ @role_name = ] 'role_name'  
  [,[ @index_name = ] 'index_name' ]  
  [,[ @captured_column_list = ] 'captured_column_list' ]  
  [,[ @filegroup_name = ] 'filegroup_name' ]  
  [,[ @allow_partition_switch = ] 'allow_partition_switch' ]  
  [;]  
```  
  
## <a name="arguments"></a>引数  
`[ @source_schema = ] 'source_schema'` ソース テーブルが所属するスキーマの名前です。 *source_schema*は**sysname**、既定値はありません、NULL にすることはできません。  
  
`[ @source_name = ] 'source_name'` 変更データ キャプチャを有効にするソース テーブルの名前です。 *source_name*は**sysname**、既定値はありません、NULL にすることはできません。  
  
 *source_name*現在のデータベースに存在する必要があります。 内のテーブル、 **cdc**スキーマは変更データ キャプチャを有効にすることはできません。  
  
`[ @role_name = ] 'role_name'` 変更データへのアクセスに使用するデータベース ロールの名前です。 *role_name*は**sysname**と指定する必要があります。 明示的に NULL に設定した場合、変更データへのアクセスを制限する際にゲーティング ロールは使用されません。  
  
 役割が現在存在する場合に使用されます。 指定されたロールが存在しない場合は、その名前でデータベース ロールの作成が試行されます。 ロール名は文字列の右側にある空白のロールを作成する前に切り捨てられます。 呼び出し元がデータベース内でロールを作成する権限がない場合、ストアド プロシージャの操作は失敗します。  
  
`[ @capture_instance = ] 'capture_instance'` 名前のインスタンスに固有の変更データ キャプチャ オブジェクトに使用されるキャプチャ インスタンスの名前です。 *capture_instance*は**sysname** NULL にすることはできません。  
  
 名前が、ソース スキーマ名の形式でソース テーブル名から派生した指定しない場合、 *schemaname_sourcename*します。 *capture_instance* 100 文字を超えることはできませんし、データベース内で一意である必要があります。 指定されたか、派生*capture_instance*文字列の右側にある空白は切り捨てられます。  
  
 ソース テーブルには、2 つのキャプチャ インスタンスの最大数を持つことができます。 詳細については、「 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)します。  
  
`[ @supports_net_changes = ] supports_net_changes` 示すかどうかをこのキャプチャ インスタンスに対して有効にするには差分変更クエリをサポートします。 *supports_net_changes*は**bit**、既定値は、テーブルに主キーまたはテーブルに一意のインデックスを使用して識別されている場合は 1、@index_nameパラメーター。 それ以外の場合、既定値は 0 になります。  
  
 0 の場合は、すべての変更を照会するサポート関数のみが生成されます。  
  
 1 の場合、差分変更のクエリに必要な関数も生成されます。  
  
 場合*supports_net_changes*を 1 に設定されている*index_name*指定する必要がありますか、ソース テーブルは主キーが定義されている必要があります。  
  
`[ @index_name = ] 'index_name_'` 使用して、ソース テーブル内の行を一意に識別する一意のインデックスの名前。 *index_name*は**sysname** NULL にすることができます。 指定した場合*index_name*ソース テーブルに一意のインデックスを有効にする必要があります。 場合*index_name*インデックス列よりも優先、定義された主キー列、テーブルの一意の行識別子として指定します。  
  
`[ @captured_column_list = ] 'captured_column_list'` 変更テーブルに含まれるソース テーブルの列を識別します。 *captured_column_list*は**nvarchar (max)** NULL にすることができます。 NULL の場合、すべての列が変更テーブルに追加されます。  
  
 列名は、ソース テーブルの有効な列である必要があります。 主キー インデックスで定義された列または列によって参照されるインデックスで定義されている*index_name*含める必要があります。  
  
 *captured_column_list*は列名のコンマ区切りのリスト。 二重引用符を使用して、リスト内の個々 の列名できます必要に応じて引用符で囲む ("") または角かっこ ()。 列名には、埋め込みのコンマが含まれている、列名が引用符で囲まれたする必要があります。  
  
 *captured_column_list*次の予約済みの列名を含めることはできません: **_ _ $start_lsn**、 **_ _ $end_lsn**、 **_ _ $$seqval**、 **_ _ $操作**、および **_ _ $update_mask**します。  
  
`[ @filegroup_name = ] 'filegroup_name'` キャプチャ インスタンスの作成、変更テーブルに使用するファイル グループです。 *filegroup_name*は**sysname** NULL にすることができます。 指定した場合*filegroup_name*現在のデータベースを定義する必要があります。 NULL の場合、既定のファイル グループが使用されます。  
  
 変更データ キャプチャの変更テーブル用に、別個のファイル グループを作成することをお勧めします。  
  
`[ @allow_partition_switch = ] 'allow_partition_switch'` 変更データ キャプチャが有効になっているテーブルに対して ALTER TABLE の SWITCH PARTITION コマンドを実行できるかどうかを示します。 *allow_partition_switch*は**bit**、既定値は 1 です。  
  
 テーブルのパーティション分割されていない場合、切り替え設定は常に 1、および実際の設定は無視されます。 非パーティション テーブルで切り替え設定を明示的に 0 に設定すると、切り替え設定が無視されたことを示す警告 22857 が生成されます。 パーティション テーブルで切り替え設定を明示的に 0 に設定すると、ソース テーブルに対するパーティションの切り替え操作が許可されなくなることを示す警告 22356 が生成されます。 最後に、パーティションの切り替えをブロックしないことを示す場合は、切り替え設定は 1 または 1 の既定値を明示的に設定するか、有効になっているテーブルがパーティション分割、警告 22855 が発行されます。 すべてのパーティションの切り替えが発生した場合、変更データ キャプチャには、スイッチによって生じた変更は記録されません。 変更データが使用されるときに、データの不整合になります。  
  
> [!IMPORTANT]  
>  SWITCH PARTITION はメタデータの操作ですが、データ変更を伴います。 変更データには、この操作に関連付けられている変更は保存されていないデータは、変更テーブルをキャプチャします。 3 つのパーティションを持つテーブルを検討し、このテーブルに変更します。 キャプチャ プロセスでは、このテーブルに対して実行されるユーザーの挿入操作、更新操作、および削除操作を追跡します。 ただし、パーティションが別のテーブルに切り替えられた場合 (一括削除の実行など)、この操作の一部として移動された行は、変更テーブルには削除された行としてキャプチャされません。 同様に、既に行が作成されている新しいパーティションがテーブルに追加された場合、これらの行は変更テーブルには反映されません。 このため、変更がアプリケーションで使用され、変更先に適用されると、データの不整合が生じる可能性があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または**1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>コメント  
 変更データ キャプチャのテーブルで有効にする前に、データベースを有効にする必要があります。 データベースで変更データ キャプチャが有効かどうかを確認するのには、クエリ、 **is_cdc_enabled**内の列、 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)カタログ ビューです。 データベースを有効にするには使用、 [sys.sp_cdc_enable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md)ストアド プロシージャ。  
  
 テーブルに対して変更データ キャプチャを有効にすると、変更テーブルと 1 つまたは 2 つのクエリ関数が生成されます。 変更テーブルは、キャプチャ プロセスによってトランザクション ログから抽出されたソース テーブルの変更に関するリポジトリとして機能します。 クエリ関数は、変更テーブルからデータを抽出に使用されます。 これらの関数の名前がから派生した、 *capture_instance*次の方法でパラメーター。  
  
-   すべての変更関数: **cdc.fn_cdc_get_all_changes_ < capture_instance >**  
  
-   差分変更関数: **cdc.fn_cdc_get_net_changes_ < capture_instance >**  
  
 **sys.sp_cdc_enable_table**ソース テーブルが変更データ キャプチャを有効にするデータベース内の最初のテーブルおよびデータベースのトランザクション パブリケーションが存在しない場合も、データベースのキャプチャとクリーンアップ ジョブを作成します。 設定、 **is_tracked_by_cdc**内の列、 [sys.tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)カタログ ビューを 1 にします。  
  
> [!NOTE]  
>  テーブルで変更データ キャプチャが有効になっている場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されている必要はありません。 ただし、キャプチャ プロセスがトランザクション ログの処理されず、しない限り、変更テーブルにエントリを書き込む[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェントが実行されています。  
  
## <a name="permissions"></a>アクセス許可  
 メンバーシップが必要です、 **db_owner**固定データベース ロール。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-enabling-change-data-capture-by-specifying-only-required-parameters"></a>A. 必要なパラメーターのみを指定することで変更データ キャプチャを有効にします。  
 次の例では変更データ キャプチャを`HumanResources.Employee`テーブル。 必要なパラメーターのみが指定されます。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Employee'  
  , @role_name = N'cdc_Admin';  
GO  
```  
  
### <a name="b-enabling-change-data-capture-by-specifying-additional-optional-parameters"></a>B. 追加のオプション パラメーターを指定することで変更データ キャプチャを有効にします。  
 次の例では変更データ キャプチャを`HumanResources.Department`テーブル。 除くすべてのパラメーター`@allow_partition_switch`が指定されています。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Department'  
  , @role_name = N'cdc_admin'  
  , @capture_instance = N'HR_Department'   
  , @supports_net_changes = 1  
  , @index_name = N'AK_Department_Name'   
  , @captured_column_list = N'DepartmentID, Name, GroupName'   
  , @filegroup_name = N'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [sys.sp_cdc_disable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sys.sp_cdc_help_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)  
  
  
