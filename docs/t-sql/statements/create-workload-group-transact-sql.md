---
title: CREATE WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/18/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- WORKLOAD GROUP
- WORKLOAD_GROUP_TSQL
- CREATE WORKLOAD GROUP
- CREATE_WORKLOAD_GROUP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE WORKLOAD GROUP statement
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: bed396bf39b4b621c5b333a7b13218998264675a
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165895"
---
# <a name="create-workload-group-transact-sql"></a>CREATE WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>製品をクリックしてください

次の行から興味がある製品名をクリックしてみてください。 この Web ページでは、クリックした製品に合わせて、異なるコンテンツが表示されます。

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**_\* SQL Server \*_** &nbsp;|[SQL Database<br />マネージド インスタンス](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](create-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>SQL Server と SQL Database Managed Instance

リソース ガバナー ワークロード グループを作成し、そのワークロード グループをリソース ガバナー リソース プールに関連付けます。 リソース ガバナーは、[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

## <a name="syntax"></a>構文

```
CREATE WORKLOAD GROUP group_name
[ WITH
    ( [ IMPORTANCE = { LOW | MEDIUM | HIGH } ]
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]
      [ [ , ] MAX_DOP = value ]
      [ [ , ] GROUP_MAX_REQUESTS = value ] )
 ]
[ USING {
    [ pool_name | "default" ]
    [ [ , ] EXTERNAL external_pool_name | "default" ] ]
    } ]
[ ; ]
```

## <a name="arguments"></a>引数

*group_name*     
ワークロード グループのユーザー定義の名前を指定します。 *group_name* には、英数字を最大 128 文字まで使用できます。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス内で一意である必要があり、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。

IMPORTANCE = { LOW | **MEDIUM** | HIGH }     
ワークロード グループでの要求の相対的な重要度を指定します。 重要度は次のいずれかで、MEDIUM が既定値です。

- LOW
- MEDIUM (既定)
- HIGH

> [!NOTE]
> 各重要度の設定は、内部に計算用の数値として格納されます。

IMPORTANCE は、リソース プールに対してローカルです。同じリソース プール内の異なる重要度のワークロード グループは互いに影響しますが、別のリソース プールのワークロード グループには影響しません。

REQUEST_MAX_MEMORY_GRANT_PERCENT = *value*     
1 つの要求にプールから割り当てられる最大メモリ量を指定します。 *value* は、MAX_MEMORY_PERCENT で指定したリソース プールのサイズが基準になります。 

*value* は [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] までの整数と [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] で始まる float です。 既定値は 25 です。 *value* の許容範囲は 1 ～ 100 です。

> [!NOTE]  
> 指定した量のみがクエリの実行時に許可されるメモリとして割り当てられます。  
  
> [!IMPORTANT]
> *value* を 0 に設定すると、ユーザー定義のワークロード グループでは SORT と HASH JOIN 操作を含むクエリが実行されなくなります。     
>
> 同時に他のクエリが実行されているとサーバーが空きメモリを十分に確保できない可能性があるため、*value* を 70 より大きな値に設定することはお勧めしません。 これによってやがては、クエリの時間切れエラー 8645 が発生します。      
  
> [!NOTE]  
> クエリのメモリ要求がこのパラメーターによって指定されている制限を超えると、サーバーは次のように対応します。  
>   
> -  ユーザー定義のワークロード グループでは、メモリ要求が制限より低くなるか、並列処理の次数が 1 になるまで、サーバーはクエリの並列処理の次数を下げます。 それでもクエリのメモリ要求が制限を超える場合は、エラー 8657 が発生します。  
>   
> -  内部および既定のワークロード グループでは、そのクエリに必要なメモリの確保がサーバーによって許可されます。  
>   
> サーバーに十分な物理メモリがない場合は、どちらの場合も時間切れエラー 8645 が発生する可能性があります。  

REQUEST_MAX_CPU_TIME_SEC = *value*     
要求が使用できる最大 CPU 時間を秒単位で指定します。 *value* は、0 または正の整数にする必要があります。 *value* の既定の設定が 0 の場合は、無制限を示します。

> [!NOTE]
> 既定では、リソース ガバナーでは最大時間を超過しても、要求は継続されます。 ただし、イベントが生成されます。 詳細については、「[CPU Threshold Exceeded イベント クラス](../../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)」を参照してください。     

> [!IMPORTANT]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3 以降では、[トレース フラグ 2422](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) を使用すると、最大時間を超えたときにリソース ガバナーが要求を中止します。

REQUEST_MEMORY_GRANT_TIMEOUT_SEC = *value*     
メモリ許可 (作業バッファー メモリ) が使用可能になるのをクエリが待機できる最大時間を秒単位で指定します。 *value* は、0 または正の整数にする必要があります。 *value* の既定の設定である 0 の場合、クエリ コストに基づく内部の計算を使用して、最大時間が決定されます。

> [!NOTE]
> メモリ許可のタイムアウトに達しても、常にクエリが失敗するとは限りません。 クエリが失敗するのは、同時実行クエリ数が多すぎる場合だけです。 それ以外の場合、クエリは最小限のメモリ許可しか取得できないので、クエリのパフォーマンスが低下します。

MAX_DOP = *value*     
並列クエリ実行に対する**並列処理の最大限度 (MAXDOP)** を指定します。 *value* は、0 または正の整数にする必要があります。 *value* の許容範囲は 0 から 64 です。 *value* の既定の設定は 0 で、グローバル設定が使用されます。 MAX_DOP は次のように処理されます。

> [!NOTE]
> ワークロード グループの MAX_DOP では、[並列処理の最大限度に対するサーバー構成](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)と、**MAXDOP** [データベース スコープ構成](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)がオーバーライドされます。

> [!TIP]
> これをクエリ レベルで行うには、**MAXDOP** [クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md)を使用します。 ワークロード グループの MAX_DOP を超えない限り、クエリ ヒントとして並列処理の最大限度を設定することは有効です。 MAXDOP クエリ ヒントの値が Resource Governor を使用して構成されている値を超える場合、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ではリソース ガバナーの `MAX_DOP` の値が使用されます。 MAXDOP [クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md)では常に、[並列処理の最大限度のサーバー構成](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)がオーバーライドされます。      
>   
> データベース レベルでこれを行うには、**MAXDOP** [データベース スコープ構成](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)を使用します。      
>   
> これをサーバー レベルで行うには、**並列処理の最大限度 (MAXDOP)** [サーバー構成オプション](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)を使用します。     

GROUP_MAX_REQUESTS = *value*     
ワークロード グループで実行を許可する同時要求の最大数を指定します。 *value* には、0 または正の整数を指定する必要があります。 *value* の既定の設定は 0 であり、これでは無制限の要求が許可されます。 同時要求の最大数に達した場合、そのグループのユーザーはログインできますが、同時要求数が指定した値を下回るまで待機状態になります。

USING { *pool_name* |  **"default"** }     
ワークロード グループを *pool_name* で識別されるユーザー定義のリソース プールに関連付けます。 実質的には、これによってワークロード グループがグループ リソースに配置されます。 *pool_name* を指定していない場合、または USING 引数を使用していない場合、ワークロード グループは事前に定義されたリソース ガバナーの既定のプールに配置されます。

予約語の "default" を USING で使用する場合は、引用符 ("") または角かっこ ([]) で囲む必要があります。

> [!NOTE]
> 定義済みのワークロード グループおよびリソース プールではすべて、"default" などの小文字の名前が使用されています。 大文字と小文字を区別する照合順序を使用するサーバーでは、これを考慮する必要があります。 SQL_Latin1_General_CP1_CI_AS など、大文字と小文字を区別しない照合順序を使用するサーバーでは、"default" と "Default" が同じものと見なされます。

EXTERNAL external_pool_name | "default"     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)。

ワークロード グループには、外部リソース プールを指定できます。 ワークロード グループを定義し、2 つのプールに関連付けることができます。

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ワークロードおよびクエリのリソース プール
- 外部プロセス用の外部リソース プール 詳細については、「[sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)」を参照してください。

## <a name="remarks"></a>解説
`REQUEST_MEMORY_GRANT_PERCENT` が使用される場合、インデックスの作成では、パフォーマンスの改善のために最初に付与されたのよりも多くのワークスペース メモリを使用できます。 この特別な処理は、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のリソース ガバナーでサポートされています。 ただし、最初のメモリ許可も追加のメモリ許可も、リソース プール設定およびワークロード グループ設定によって制限されます。

`MAX_DOP` の制限は、[タスク](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)ごとに設定されます。 この設定は、[要求](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)ごとまたはクエリ制限ごとではありません。 つまり、並列クエリ実行中に、1 つの要求で、[スケジューラ](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)に割り当てられてた複数のタスクを生成することができます。 詳細については、「[スレッドおよびタスクのアーキテクチャ ガイド](../../relational-databases/thread-and-task-architecture-guide.md)」を参照してください。

`MAX_DOP` が使用されていて、コンパイル時にクエリが直列としてマークされている場合は、ワークロード グループまたはサーバー構成の設定にかかわらず、実行時に並列に変更することはできません。 構成後の `MAX_DOP` は、メモリの不足時にのみ低くすることができます。 ワークロード グループの再構成は、許可メモリ キューで待機している間は認識されません。

### <a name="index-creation-on-a-partitioned-table"></a>パーティション テーブルのインデックス作成

非固定パーティション テーブルのインデックス作成によって消費されるメモリは、含まれるパーティションの数に比例します。 必要なメモリの合計が、Resource Governor のワークロード グループの設定によって課せられているクエリごとの制限 `REQUEST_MAX_MEMORY_GRANT_PERCENT` を超えると、このインデックス作成の実行に失敗します。 *"default"* ワークロード グループでは、クエリごとの制限を超えてもクエリの開始に必要な最低限のメモリを使用できるようになっているので、そのようなクエリを実行するのに十分な量のメモリが *"default"* リソース プールに対して構成されていれば、同じインデックス作成を *"default"* ワークロード グループで実行できる可能性があります。

## <a name="permissions"></a>アクセス許可
`CONTROL SERVER` 権限が必要です。

## <a name="example"></a>例

Resource Governor の既定の設定を使用し、Resource Governor の既定のプールに配置される、`newReports` という名前のワークロード グループを作成します。 この例では `default` プールを指定していますが、必須ではありません。

```sql
CREATE WORKLOAD GROUP newReports
    USING "default" ;
GO
```

## <a name="see-also"></a>参照

- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)
- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](create-workload-group-transact-sql.md?view=sql-server-2017)||[SQL Database<br />マネージド インスタンス](create-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* SQL Data<br />Warehouse \*_** &nbsp;||||

&nbsp;

## <a name="sql-data-warehouse-preview"></a>SQL Data Warehouse (プレビュー)

ワークロード グループを作成します。  ワークロード グループは、一連の要求用のコンテナーであり、システムでワークロード管理を構成する方法の基礎となります。  ワークロード グループでは、ワークロードの分離のためのリソースの予約、リソースの格納、要求ごとのリソースの定義、実行ルールへの準拠を行う機能が提供されます。  ステートメントが完了すると、設定が有効になります。

 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。 

```
CREATE WORKLOAD GROUP group_name  
 WITH  
 (        MIN_PERCENTAGE_RESOURCE = value  
      ,   CAP_PERCENTAGE_RESOURCE = value 
      ,   REQUEST_MIN_RESOURCE_GRANT_PERCENT = value   
  [ [ , ] REQUEST_MAX_RESOURCE_GRANT_PERCENT = value ]  
  [ [ , ] IMPORTANCE = { LOW | BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }]
  [ [ , ] QUERY_EXECUTION_TIMEOUT_SEC = value ] )  
  [ ; ]
```

*group_name*</br>
ワークロード グループを識別する名前を指定します。  group_name は、sysname です。  これは長さを最大で 128 文字とすることができ、インスタンス内では一意である必要があります。

*MIN_PERCENTAGE_RESOURCE* = value</br>
他のワークロード グループと共有されない、このワークロード グループに対して保証される最小リソース割り当てを指定します。  value は 0 から 100 の範囲の整数です。  すべてのワークロード グループでの min_percentage_resource の合計は、100 を超えることはできません。  min_percentage_resource の値を cap_percentage_resource より大きくすることはできません。  サービス レベルごとに有効な最小値があります。  詳細については、「[有効な値](#effective-values)」を参照してください。

*CAP_PERCENTAGE_RESOURCE* = value</br>
ワークロード グループ内のすべての要求に対するリソースの最大使用率を指定します。  value に対して許可される整数の範囲は 1 から 100 です。  cap_percentage_resource の値は、min_percentage_resource よりも大きくする必要があります。  cap_percentage_resource の有効な値は、他のワークロード グループで min_percentage_resource が 0 より大きく構成されている場合に減らすことができます。

*REQUEST_MIN_RESOURCE_GRANT_PERCENT* = value</br>
要求ごとに割り当てられるリソースの最小量を設定します。  value は 0.75 から 100.00 の 10 進数の範囲の必須パラメーターです。  request_min_resource_grant_percent の値は、0.25 の倍数である必要があります。また、min_percentage_resource の係数であり、cap_percentage_resource よりも小さくする必要があります。  サービス レベルごとに有効な最小値があります。  詳細については、「[有効な値](#effective-values)」を参照してください。

次に例を示します。

```sql
CREATE WORKLOAD GROUP wgSample WITH  
( MIN_PERCENTAGE_RESOURCE = 26              -- integer value
 ,REQUEST_MIN_RESOURCE_GRANT_PERCENT = 3.25 -- factor of 26 (guaranteed a minimum of 8 concurrency)
 ,CAP_PERCENTAGE_RESOURCE = 100 )
```

request_min_resource_grant_percent のガイドラインとして、リソース クラスに使用される値を検討してください。  次の表には、Gen2 のリソース割り当てが含まれています。

|リソース クラス|リソースの割合|
|---|---|
|Smallrc|3%|
|Mediumrc|10%|
|Largerc|22%|
|Xlargerc|70%|
|||

*REQUEST_MAX_RESOURCE_GRANT_PERCENT* = value</br>
要求ごとに割り当てられるリソースの最大量を設定します。  value は省略可能な 10 進数のパラメーターで、既定値は request_min_resource_grant_percent と同じ値です。  value は request_min_resource_grant_percent 以上である必要があります。  request_max_resource_grant_percent の値が request_min_resource_grant_percent より大きく、システム リソースが使用可能な場合は、追加のリソースが要求に割り当てられます。

*IMPORTANCE* = { LOW |  BELOW_NORMAL | NORMAL | ABOVE_NORMAL | HIGH }</br>
ワークロード グループに対する要求の既定の重要度を指定します。  重要度は次のいずれかで、NORMAL が既定値です。
- LOW
- BELOW_NORMAL
- NORMAL (既定値)
- ABOVE_NORMAL
- HIGH  

ワークロード グループでの重要度セットは、ワークロード グループ内のすべての要求に対する既定の重要度です。  ユーザーは、分類子レベルで重要度を設定することもできます。これにより、ワークロード グループの重要度の設定をオーバーライドできます。  これにより、ワークロード グループ内の要求の重要度を区別して、予約されていないリソースにすばやくアクセスできるようになります。  ワークロード グループ全体で min_percentage_resource の合計が 100 未満の場合は、重要度に基づいて割り当てられた予約されていないリソースがあります。

*QUERY_EXECUTION_TIMEOUT_SEC* = value</br>
クエリが取り消されるまでに実行できる最大時間を秒単位で指定します。  value は、0 または正の整数にする必要があります。  value の既定の設定が 0 の場合は、クエリはタイムアウトしません。クエリが実行状態になると、QUERY_EXECUTION_TIMEOUT_SEC がカウントされます。クエリがキューに入れられたときではありません。

## <a name="remarks"></a>解説
リソース クラスに対応するワークロード グループは、旧バージョンとの互換性のために自動的に作成されます。  これらのシステム定義のワークロード グループは削除できません。  さらに 8 つのユーザー定義のワークロード グループを作成できます。

ワークロード グループが 0 より大きい min_percentage_resource で作成された場合、`CREATE WORKLOAD GROUP` ステートメントは、ワークロード グループを作成するのに十分なリソースが確保されるまでキューに格納されます。

## <a name="effective-values"></a>有効な値

min_percentage_resource、cap_percentage_resource、request_min_resource_grant_percent、request_max_resource_grant_percent パラメーターには、現在のサービス レベルのコンテキストで調整された有効な値と、その他のワークロード グループの構成が含まれます。

サービス レベルごとにサポートされるコンカレンシーは、リソース クラスを使用してクエリごとにリソースの許可を定義したときと同じになります。したがって、request_min_resource_grant_percent でサポートされる値は、インスタンスに設定されているサービス レベルによって異なります。  最も低いサービス レベル (DW100c) では、要求ごとに最小 25% のリソースが必要です。  DW100c では、構成されたワークロード グループの有効な request_min_resource_grant_percent は、25% 以上にすることができます。  有効値がどのように派生するかの詳細については、以下の表を参照してください。

|サービス レベル|REQUEST_MIN_RESOURCE_GRANT_PERCENT の有効な最小値|同時クエリの最大数|
|---|---|---|
|DW100c|25%|4|
|DW200c|12.5%|8|
|DW300c|8%|12|
|DW400c|6.25%|16|
|DW500c|5%|20|
|DW1000c|3%|32|
|DW1500c|3%|32|
|DW2000c|2%|48|
|DW2500c|2%|48|
|DW3000c|1.5%|64|
|DW5000c|1.5%|64|
|DW6000c|0.75%|128|
|DW7500c|0.75%|128|
|DW10000c|0.75%|128|
|DW15000c|0.75%|128|
|DW30000c|0.75%|128|
||||

同様に、request_min_resource_grant_percent、min_percentage_resource は、有効な request_min_resource_grant_percent 以上である必要があります。  有効な min_percentage_resource 未満に構成された min_percentage_resource のワークロード グループには、実行時にゼロに調整される値が含まれています。  この場合、min_percentage_resource 用に構成されたリソースは、すべてのワークロード グループとの間で共有できます。  たとえば、DW1000c で実行されている min_percentage_resource が 10% であるワークロード グループ wgAdHoc には、有効な 10% の min_percentage_resource が含まれます (DW1000c でサポートされている最小値は 3.25% です)。  DW100c の wgAdhoc には、有効な 0% の min_percentage_resource が含まれます。  WgAdhoc 用に構成された 10% は、すべてのワークロード グループとの間で共有されます。

cap_percentage_resource にも有効な値があります。  ワークロード グループ wgAdhoc が 100% の cap_percentage_resource で構成され、別のワークロード グループ wgDashboards が 25% の min_percentage_resource で作成されている場合、wgAdhoc の有効な cap_percentage_resource は 75% になります。

ワークロード グループの実行時の値を理解する最も簡単な方法は、システム ビュー [sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md) に対してクエリを実行することです。


## <a name="permissions"></a>アクセス許可

CONTROL DATABASE アクセス許可が必須です

## <a name="see-also"></a>参照
[DROP WORKLOAD GROUP (Transact-SQL)](drop-workload-group-transact-sql.md) <br>
[sys.workload_management_workload_groups](../../relational-databases/system-catalog-views/sys-workload-management-workload-groups-transact-sql.md) <br>
[sys.dm_workload_management_workload_groups_stats](../../relational-databases/system-dynamic-management-views/sys-dm-workload-management-workload-group-stats-transact-sql.md) <br>
[ワークロード グループを作成して使用する方法のクイック スタート](https://docs.microsoft.com/azure/sql-data-warehouse/quickstart-configure-workload-isolation-tsql)

::: moniker-end
