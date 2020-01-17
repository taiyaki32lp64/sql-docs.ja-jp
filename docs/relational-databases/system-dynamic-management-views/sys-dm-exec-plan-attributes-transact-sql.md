---
title: sys.dm_exec_plan_attributes (Transact-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_plan_attributes_TSQL
- dm_exec_plan_attributes_TSQL
- dm_exec_plan_attributes
- sys.dm_exec_plan_attributes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_plan_attributes dynamic management function
ms.assetid: dacf3ab3-f214-482e-aab5-0dab9f0a3648
author: stevestein
ms.author: sstein
ms.openlocfilehash: 4b6e5b28612efccafa9e2de0606eef821e341081
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68255600"
---
# <a name="sysdm_exec_plan_attributes-transact-sql"></a>sys.dm_exec_plan_attributes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  プラン ハンドルで指定したプランのプラン属性ごとに 1 行のデータを返します。 このテーブル値関数を使用すると、キャッシュ キーの値やプランの同時実行数など、特定のプランに関する詳細情報を取得できます。  
  
> [!NOTE]  
>  によって返される情報の一部をこの関数は、マップ、 [sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md)旧バージョンとの互換性ビューです。

## <a name="syntax"></a>構文  
```  
sys.dm_exec_plan_attributes ( plan_handle )  
```  
  
## <a name="arguments"></a>引数  
 *plan_handle*  
 既に実行されていて、そのプランがプラン キャッシュに格納されているバッチのクエリ プランを一意に識別します。 *plan_handle*は**varbinary (64)** します。 プラン ハンドルを取得できます、 [sys.dm_exec_cached_plans](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)動的管理ビュー。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|attribute|**varchar(128)**|このプランに関連付けられている属性の名前。 この 1 つのすぐ下の表は、使用可能な属性、そのデータ型とその説明を一覧表示します。|  
|value|**sql_variant**|プランに関連付けられている属性の値。|  
|is_cache_key|**bit**|属性が、プランに対するキャッシュ参照キーの一部として使用されているかどうかを示します。|  

上記の表から**属性**次の値を持つことができます。

|属性|データ型|説明|  
|---------------|---------------|-----------------|  
|set_options|**int**|プランをコンパイルしたオプションの値を示します。|  
|objectid|**int**|キャッシュ内のオブジェクトを検索するために使用される主キーの 1 つです。 これは、オブジェクトに格納されている ID [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)のデータベース オブジェクト (プロシージャ、ビュー、トリガー、およびなど)。 "アドホック プラン" または "準備されたプラン" では、バッチ テキストの内部ハッシュです。|  
|dbid|**int**|プランによって参照されるエンティティを含むデータベースの ID を指定します。<br /><br /> アドホック プランまたは準備されたプランでは、バッチの実行元となるデータベース ID です。|  
|dbid_execute|**int**|格納されているシステム オブジェクトに対して、**リソース**データベース、キャッシュされたプランを実行するためのデータベース ID。 その他の場合は 0 になります。|  
|user_id|**int**|値 -2 は、送られたバッチが暗黙的な名前解決に依存せず、複数ユーザー間での共有が可能であることを示します。 これは推奨される方法です。 他の値は、データベースのクエリを送っているユーザーのユーザー ID を示します。| 
|language_id|**smallint**|キャッシュ オブジェクトを作成した接続の言語の ID です。 詳細については、次を参照してください。 [sys.syslanguages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)します。|  
|date_format|**smallint**|キャッシュ オブジェクトを作成した接続の日付形式です。 詳しくは、「[SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md)」をご覧ください。|  
|date_first|**tinyint**|日付の最初の値です。 詳しくは、「[SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md)」をご覧ください。|  
|status|**int**|キャッシュ参照キーの一部である内部ステータス ビットです。|  
|required_cursor_options|**int**|カーソルの種類など、ユーザーによって指定されたカーソル オプションです。|  
|acceptable_cursor_options|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がステートメントの実行をサポートするために暗黙的に変換できるカーソル オプションです。 たとえば、ユーザーは動的カーソルを指定することがありますが、クエリ オプティマイザーでは、このカーソルの種類を静的カーソルに変換することが許可されています。|  
|inuse_exec_context|**int**|クエリ プランを使用している現在実行中のバッチの数です。|  
|free_exec_context|**int**|クエリ プランのキャッシュされた実行コンテキストのうち、現在使用されていない実行コンテキストの数です。|  
|hits_exec_context|**int**|実行コンテキストがプラン キャッシュから取得され再利用された回数です。これにより、SQL ステートメントを再コンパイルする際のオーバーヘッドが少なくなります。 この値は、これまでのすべてのバッチ実行の集計です。|  
|misses_exec_context|**int**|実行コンテンツがプラン キャッシュに見つからなかった回数です。これにより、バッチ実行に対して新しい実行コンテンツが作成されます。|  
|removed_exec_context|**int**|キャッシュされたプランのメモリの負荷により削除された実行コンテンツの数です。|  
|inuse_cursors|**int**|キャッシュされたプランを使用しているカーソルを 1 つ以上含む、現在実行中のバッチの数です。|  
|free_cursors|**int**|キャッシュされたプランのアイドル状態または解放されたカーソルの数です。|  
|hits_cursors|**int**|キャッシュされたプランから非アクティブなカーソルが取得され、再利用された回数です。 この値は、これまでのすべてのバッチ実行の集計です。|  
|misses_cursors|**int**|非アクティブなカーソルがキャッシュに見つからなかった回数です。|  
|removed_cursors|**int**|キャッシュされたプランのメモリの負荷により削除されたカーソルの数です。|  
|sql_handle|**varbinary**(64)|バッチの SQL ハンドルです。|  
|merge_action_type|**smallint**|MERGE ステートメントの結果として使用するトリガーの実行プランの種類。<br /><br /> 0 は、非トリガー プラン (MERGE ステートメントの結果として実行されないトリガー プラン)、または DELETE アクションのみを指定する MERGE ステートメントの結果として実行されるトリガー プランを示します。<br /><br /> 1 は、MERGE ステートメントの結果として実行される INSERT トリガー プランを示します。<br /><br /> 2 は、MERGE ステートメントの結果として実行される UPDATE トリガー プランを示します。<br /><br /> 3 は、対応する INSERT アクションまたは UPDATE アクションを含む MERGE ステートメントの結果として実行される DELETE トリガー プランを示します。<br /><br /> 連鎖操作によって実行される入れ子のトリガーの場合、この値は、連鎖操作の原因となった MERGE ステートメントのアクションです。|  
  
## <a name="permissions"></a>アクセス許可  

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]、必要があります`VIEW SERVER STATE`権限。   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium レベルでは、必要があります、`VIEW DATABASE STATE`データベースの権限。 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard および Basic 階層は、必要があります、**サーバー管理者**または**Azure Active Directory 管理者**アカウント。   

## <a name="remarks"></a>コメント  
  
## <a name="set-options"></a>SET オプション  
 値のみで、同じコンパイル済みプランのコピーが異なる場合があります、 **set_options**列。 これは、異なる接続では、同じクエリに対して異なる SET オプション セットが使用されていることを示します。 通常、異なるオプション セットを使用することは望ましくありません。異なるオプション セットを使用すると、余分なコンパイルが発生し、プランの再利用が減少して、キャッシュ内にプランの複数のコピーが存在することが原因でプラン キャッシュが増加します。  
  
### <a name="evaluating-set-options"></a>SET オプションの評価  
 戻り値を変換する**set_options** 、プランをコンパイルしたオプションから値を減算、 **set_options**するまで、最大有効値で始まる値0 に到達します。 減算する各値は、クエリ プランに使用されたオプションに対応しています。 たとえば場合の値**set_options** 251 では、プランをコンパイルしたオプションは ANSI_NULL_DFLT_ON (128)、QUOTED_IDENTIFIER (64)、ansi_nulls (32)、ANSI_WARNINGS (16)、CONCAT_NULL_YIELDS_NULL (8)、並列 Plan(2)ANSI_PADDING (1)。  
  
|オプション|値|  
|------------|-----------|  
|ANSI_PADDING|1|  
|Parallel Plan|2|  
|FORCEPLAN|4|  
|CONCAT_NULL_YIELDS_NULL|8|  
|ANSI_WARNINGS|16|  
|ANSI_NULLS|32|  
|QUOTED_IDENTIFIER|64|  
|ANSI_NULL_DFLT_ON|128|  
|ANSI_NULL_DFLT_OFF|256|  
|NoBrowseTable<br /><br /> プランが FOR BROWSE 操作の実装に作業テーブルを使用しないことを示します。|512|  
|TriggerOneRow<br /><br /> AFTER トリガー デルタ テーブルに対する 1 行の最適化がプランに含まれていることを示します。|1024|  
|ResyncQuery<br /><br /> クエリが内部システム ストアド プロシージャによって送信されたことを示します。|2048|  
|ARITH_ABORT|4096|  
|NUMERIC_ROUNDABORT|8192|  
|DATEFIRST|16384|  
|DATEFORMAT|32768|  
|LanguageID|65536|  
|UPON<br /><br /> プランがコンパイルされたとき、データベース オプション PARAMETERIZATION が FORCED に設定されたことを示します。|131072|  
|ROWCOUNT|**適用対象:** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]に [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]<br /><br /> 262144|  
  
## <a name="cursors"></a>カーソル  
 非アクティブなカーソルは、カーソルの格納に使用されたメモリをカーソルの同時ユーザーが再利用できるように、コンパイル済みプランにキャッシュされます。 たとえば、カーソルの割り当てを解除せずに、バッチでそのカーソルを宣言して使用するとします。 2 人のユーザーが同じバッチを実行している場合、アクティブなカーソルが 2 つになります。 (場合によっては別のバッチで) カーソルの割り当てが解除されると、カーソルの格納に使用されたメモリはキャッシュされ、解放されません。 この非アクティブなカーソルの一覧は、コンパイル済みプランに保持されます。 次にユーザーがバッチを実行するときに、キャッシュされたカーソルのメモリが再利用され、アクティブなカーソルとして適切に初期化されます。  
  
### <a name="evaluating-cursor-options"></a>カーソル オプションの評価  
 戻り値を変換する**required_cursor_options**と**acceptable_cursor_options**プランをコンパイルしたオプションにするには、以降では、列の値から値を減算最大有効値を 0 に到達するまでです。 減算する各値は、クエリ プランに使用されたカーソル オプションに対応しています。  
  
|オプション|値|  
|------------|-----------|  
|なし|0|  
|INSENSITIVE|1|  
|SCROLL|2|  
|READ ONLY|4|  
|FOR UPDATE|8|  
|LOCAL|16|  
|GLOBAL|32|  
|FORWARD_ONLY|64|  
|KEYSET|128|  
|DYNAMIC|256|  
|SCROLL_LOCKS|512|  
|OPTIMISTIC|1024|  
|STATIC|2048|  
|FAST_FORWARD|4096|  
|IN PLACE|8192|  
|FOR *select_statement*|16384|  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-the-attributes-for-a-specific-plan"></a>A. 特定のプランの属性を返す  
 次の例では、指定したプランのすべてのプラン属性を返します。 `sys.dm_exec_cached_plans`動的管理ビューが最初に指定したプランのプラン ハンドルを取得するクエリが実行されます。 2 番目のクエリで置き換えます`<plan_handle>`計画を立てるには、最初のクエリから値を処理します。  
  
```sql  
SELECT plan_handle, refcounts, usecounts, size_in_bytes, cacheobjtype, objtype   
FROM sys.dm_exec_cached_plans;  
GO  
SELECT attribute, value, is_cache_key  
FROM sys.dm_exec_plan_attributes(<plan_handle>);  
GO  
```  
  
### <a name="b-returning-the-set-options-for-compiled-plans-and-the-sql-handle-for-cached-plans"></a>B. コンパイル済みプランの SET オプションとキャッシュされたプランの SQL ハンドルを返す  
 次の例では、各プランをコンパイルしたオプションを示す値を返します。 さらに、キャッシュされたすべてのプランの SQL ハンドルが返されます。  
  
```sql  
SELECT plan_handle, pvt.set_options, pvt.sql_handle  
FROM (  
    SELECT plan_handle, epa.attribute, epa.value   
    FROM sys.dm_exec_cached_plans   
        OUTER APPLY sys.dm_exec_plan_attributes(plan_handle) AS epa  
    WHERE cacheobjtype = 'Compiled Plan') AS ecpa   
PIVOT (MAX(ecpa.value) FOR ecpa.attribute IN ("set_options", "sql_handle")) AS pvt;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [実行関連の動的管理ビューおよび関数&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  

