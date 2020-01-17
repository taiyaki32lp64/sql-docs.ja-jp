---
title: CREATE EVENT SESSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE EVENT SESSION
- SESSION
- EVENT SESSION
- SESSION_TSQL
- EVENT_SESSION_TSQL
- CREATE_EVENT_SESSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- CREATE EVENT SESSION statement
ms.assetid: 67683027-2b0f-47aa-b223-604731af8b4d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5033bbb939c2c6237e82683fba4e32defef69281
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902801"
---
# <a name="create-event-session-transact-sql"></a>CREATE EVENT SESSION (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

イベントのソース、イベント セッション ターゲット、およびイベント セッション オプションを識別する拡張イベント セッションを作成します。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

## <a name="syntax"></a>構文

```
CREATE EVENT SESSION event_session_name
ON { SERVER | DATABASE }
{  
    <event_definition> [ ,...n]
    [ <event_target_definition> [ ,...n] ]
    [ WITH ( <event_session_options> [ ,...n] ) ]
}
;

<event_definition>::=
{
    ADD EVENT [event_module_guid].event_package_name.event_name
         [ ( {
                 [ SET { event_customizable_attribute = <value> [ ,...n] } ]
                 [ ACTION ( { [event_module_guid].event_package_name.action_name [ ,...n] } ) ]
                 [ WHERE <predicate_expression> ]
        } ) ]
}

<predicate_expression> ::=
{
    [ NOT ] <predicate_factor> | {( <predicate_expression> ) }
    [ { AND | OR } [ NOT ] { <predicate_factor> | ( <predicate_expression> ) } ]
    [ ,...n ]
}  
  
<predicate_factor>::=
{
    <predicate_leaf> | ( <predicate_expression> )
}

<predicate_leaf>::=
{
      <predicate_source_declaration> { = | < > | ! = | > | > = | < | < = } <value>
    | [event_module_guid].event_package_name.predicate_compare_name ( <predicate_source_declaration>, <value> )
}

<predicate_source_declaration>::=
{
    event_field_name | ( [event_module_guid].event_package_name.predicate_source_name )
}

<value>::=
{
    number | 'string'
}

<event_target_definition>::=
{
    ADD TARGET [event_module_guid].event_package_name.target_name
        [ ( SET { target_parameter_name = <value> [ ,...n] } ) ]
}

<event_session_options>::=
{  
    [    MAX_MEMORY = size [ KB | MB ] ]
    [ [,] EVENT_RETENTION_MODE = { ALLOW_SINGLE_EVENT_LOSS | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } ]
    [ [,] MAX_DISPATCH_LATENCY = { seconds SECONDS | INFINITE } ]
    [ [,] MAX_EVENT_SIZE = size [ KB | MB ] ]
    [ [,] MEMORY_PARTITION_MODE = { NONE | PER_NODE | PER_CPU } ]
    [ [,] TRACK_CAUSALITY = { ON | OFF } ]
    [ [,] STARTUP_STATE = { ON | OFF } ]
}
```

## <a name="arguments"></a>引数

*event_session_name* には、イベント セッションのユーザー定義の名前を指定します。 *event_session_name* には英数字を最大 128 文字まで使用できます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で一意である必要があり、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。

ADD EVENT [ *event_module_guid* ].*event_package_name*.*event_name* は、イベント セッションに関連付けるイベントです。各要素は次のとおりです。

- *event_module_guid* は、イベントを含むモジュールの GUID です。
- *event_package_name* は、アクション オブジェクトを含むパッケージです。
- *event_name* は、イベント オブジェクトです。

イベントは、object_type 'event' として sys.dm_xe_objects ビューに表示されます。

SET { *event_customizable_attribute*= \<value> [ ,...*n*] } によって、イベントのカスタマイズ可能な属性を設定できます。 カスタマイズ可能な属性は、column_type 'customizable' および object_name = *event_name* として sys.dm_xe_object_columns ビューに表示されます。

ACTION ( { [*event_module_guid*].*event_package_name*.*action_name* [ **,** ...*n*] }) は、イベント セッションに関連付けるアクションです。各要素は次のとおりです。

- *event_module_guid* は、イベントを含むモジュールの GUID です。
- *event_package_name* は、アクション オブジェクトを含むパッケージです。
- *action_name* は、アクション オブジェクトです。

アクションは、object_type 'action' として sys.dm_xe_objects ビューに表示されます。

WHERE \<predicate_expression> イベントを処理する必要があるかどうかを判定するために使用する述語式を指定します。 \<predicate_expression> が true の場合、イベントは、セッションのアクションおよびターゲットによって処理されます。 \<predicate_expression> が false の場合、イベントは、セッションのアクションおよびターゲットによって処理される前にセッションによって削除されます。 述語式は 3,000 文字に制限され、これにより文字列引数が制限されます。

*event_field_name* は、述語ソースを識別するイベント フィールドの名前です。

[*event_module_guid*].*event_package_name*.*predicate_source_name* は、グローバル述語ソースの名前です。各要素は次のとおりです。

- *event_module_guid* は、イベントを含むモジュールの GUID です。
- *event_package_name* は、述語オブジェクトを含むパッケージです。
- *predicate_source_name* は、object_type 'pred_source' として sys.dm_xe_objects ビューに定義されます。

[*event_module_guid*].*event_package_name*.*predicate_compare_name* は、イベントに関連付ける述語オブジェクトの名前です。各要素は次のとおりです。

- *event_module_guid* は、イベントを含むモジュールの GUID です。
- *event_package_name* は、述語オブジェクトを含むパッケージです。
- *predicate_compare_name* は、object_type 'pred_compare' として sys.dm_xe_objects ビューに定義されるグローバル ソースです。

*number* は、**decimal** を含む任意の数値型です。 制限として、使用可能な物理メモリの不足、または 64 ビット整数として表すのに大きすぎる数字が挙げられます。

'*string*' は、述語の比較に必要な ANSI または Unicode 文字列です。 述語比較関数に対しては、暗黙の文字列型変換は行われません。 無効な型を渡すとエラーになります。

ADD TARGET [*event_module_guid*].*event_package_name*.*target_name* は、イベント セッションに関連付けるターゲットです。各要素は次のとおりです。

- *event_module_guid* は、イベントを含むモジュールの GUID です。
- *event_package_name* は、アクション オブジェクトを含むパッケージです。
- *target_name* はターゲットです。 ターゲットは、object_type 'target' として sys.dm_xe_objects ビューに表示されます。

SET { *target_parameter_name*= \<value> [, ...*n*] } によって、ターゲット パラメーターを設定します。 ターゲット パラメーターは、column_type 'customizable' および object_name = *target_name* として sys.dm_xe_object_columns ビューに表示されます。

> [!IMPORTANT]
> リング バッファー ターゲットを使用している場合、max_memory ターゲット パラメーターを 2048 KB に設定し、XML 出力のデータの切り捨てを回避することをお勧めします。 さまざまなターゲットの種類の使用について詳しくは、「[SQL Server 拡張イベント ターゲット](https://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)」をご覧ください。

WITH ( \<event_session_options> [ ,...*n*] ) イベント セッションで使用するオプションを指定します。

MAX_MEMORY =*size* [ KB | **MB** ] によって、イベントのバッファーリング用にセッションに割り当てる最大メモリ容量を指定します。 既定値は 4 MB です。 *size* は、キロバイト (KB) またはメガバイト (MB) 数を示す整数値です。 最大容量は 2 GB を超える (2048 MB 未満にする) ことはできません。 しかし、GB 域のメモリの値を使用することはお勧めしません。

EVENT_RETENTION_MODE = { **ALLOW_SINGLE_EVENT_LOSS** | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } によって、イベントの削除を処理するために使用するイベント保有モードを指定します。

**ALLOW_SINGLE_EVENT_LOSS** を指定すると、セッションからイベントを削除できます。 単独のイベントは、すべてのイベント バッファーがいっぱいになった場合にのみ削除されます。 イベント バッファーがいっぱいのときに単独のイベントを削除することで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンス特性が許容可能な状態になり、処理後のイベント ストリームのデータ損失を最小限に抑えることができます。

ALLOW_MULTIPLE_EVENT_LOSS を指定すると、複数のイベントでいっぱいのイベント バッファーをセッションから削除できます。 削除されるイベントの数は、セッションに割り当てられているメモリ サイズ、メモリのパーティション分割、およびバッファー内のイベントのサイズによって異なります。 このオプションを使用すると、イベント バッファーがすぐにいっぱいになるときにサーバーのパフォーマンスに与える影響を最小限に抑えることができますが、多数のイベントがセッションから削除される可能性があります。

NO_EVENT_LOSS を指定した場合、イベントの削除は許可されません。 このオプションを指定した場合、発生したすべてのイベントが保持されます。 このオプションを使用した場合、イベントを開始するすべてのタスクは、イベント バッファーに空きができるまで待機します。 その結果、イベント セッションがアクティブになっている間、検知できる程度のパフォーマンスの問題が発生することがあります。 バッファーからイベントがフラッシュされるのを待機する間、ユーザーの接続に遅延が生じる可能性があります。

MAX_DISPATCH_LATENCY = { *seconds* SECONDS | **INFINITE** } によって、イベントをイベント セッション ターゲットにディスパッチする前に、メモリ内にバッファー処理する時間の長さを指定できます。 既定では、この値は 30 秒に設定されます。

*seconds* SECONDS によって、ターゲットへのバッファーのフラッシュを開始する前に待機する秒数を指定できます。 *seconds* は整数です。 最小待機値は 1 秒です。 ただし、0 を使用すると、INFINITE 待機を指定できます。

**INFINITE** を指定すると、バッファーがいっぱいになったか、イベント セッションが閉じられた場合にのみ、バッファーをターゲットにフラッシュします。

> [!NOTE]
> MAX_DISPATCH_LATENCY = 0 SECONDS と MAX_DISPATCH_LATENCY = INFINITE は同じです。

MAX_EVENT_SIZE =*size* [ KB | **MB** ] によって、イベントの最大許容サイズを指定します。 MAX_EVENT_SIZE は、MAX_MEMORY よりも大きな単独のイベントのみを許可するように設定する必要があります。MAX_MEMORY よりも小さな値を設定した場合はエラーが発生します。 *size* は、キロバイト (KB) またはメガバイト (MB) 数を示す整数値です。 *size* をキロバイト単位で指定する場合、最小許容サイズは 64 KB です。 MAX_EVENT_SIZE を設定すると、MAX_MEMORY に加えて、サイズが *size* のバッファーが 2 つ作成されます。 つまり、イベントのバッファリングに使用されるメモリの合計量は MAX_MEMORY + 2 * MAX_EVENT_SIZE となります。

MEMORY_PARTITION_MODE = { **NONE** | PER_NODE | PER_CPU } によって、イベント バッファーを作成する場所を指定します。

**NONE** を指定した場合、1 つのバッファー セットが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内に作成されます。

PER_NODE の場合、NUMA ノードごとに 1 つのバッファー セットが作成されます。

PER_CPU の場合、CPU ごとに 1 つのバッファー セットが作成されます。

TRACK_CAUSALITY = { ON | **OFF** } によって、因果関係を追跡するかどうかを指定します。 有効な場合、因果関係により、異なるサーバー接続上の関連イベントを一緒に関連付けることができます。

STARTUP_STATE = { ON | **OFF** } によって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時にこのイベント セッションを自動的に開始するかどうかを指定します。

> [!NOTE]
> `STARTUP_STATE = ON` の場合、イベント セッションは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が停止後に再起動されたときにだけ開始されます。

ON の場合、起動時にイベント セッションが開始されます。

**OFF** の場合、起動時にイベント セッションが開始されません。

## <a name="remarks"></a>Remarks

論理演算子の優先順位は、高い方から `NOT`、`AND`、`OR` です。

## <a name="permissions"></a>アクセス許可

SQL Server では、`ALTER ANY EVENT SESSION` アクセス許可が必要です。
SQL Database では、データベースにおける `ALTER ANY DATABASE EVENT SESSION` アクセス許可が必要です。

## <a name="examples"></a>使用例

### <a name="sql-server-example"></a>SQL Server の例

`test_session` という名前のイベント セッションを作成する方法を次の例に示します。 この例では、2 つのイベントを追加し、Event Tracing for Windows ターゲットを使用しています。

```sql
IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='test_session')
    DROP EVENT session test_session ON SERVER;
GO
CREATE EVENT SESSION test_session
ON SERVER
    ADD EVENT sqlos.async_io_requested,
    ADD EVENT sqlserver.lock_acquired
    ADD TARGET package0.etw_classic_sync_target
        (SET default_etw_session_logfile_path = N'C:\demo\traces\sqletw.etl' )
    WITH (MAX_MEMORY=4MB, MAX_EVENT_SIZE=4MB);
GO
```
### <a name="sql-database-example"></a>SQL Database の例

Azure SQL Database の例については、[SQL Database の拡張イベントのためのイベント ファイル ターゲット コード](https://docs.microsoft.com/azure/sql-database/sql-database-xevent-code-event-file#transact-sql-code)に関連する記事に記載されている例をご覧ください

### <a name="code-examples-can-differ-for-azure-sql-database"></a>Azure SQL Database では、コード例が異なる可能性があります。

[!INCLUDE[sql-on-premises-vs-azure-similar-sys-views-include.](../../includes/paragraph-content/sql-on-premises-vs-azure-similar-sys-views-include.md)]

## <a name="see-also"></a>参照

- [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)
- [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)
- [sys.server_event_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)
- [sys.dm_xe_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)
- [sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)
