---
title: ALTER WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_WORKLOAD_GROUP_TSQL
- ALTER WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER WORKLOAD GROUP statement
ms.assetid: 957addce-feb0-4e54-893e-5faca3cd184c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 47b924754f221b93e8f9e661a1b12afb5f07fcd4
ms.sourcegitcommit: 8c1c6232a4f592f6bf81910a49375f7488f069c4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70026232"
---
# <a name="alter-workload-group-transact-sql"></a>ALTER WORKLOAD GROUP (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  既存の Resource Governor ワークロード グループの構成を変更します。必要に応じて、そのワークロード グループを Resource Governor リソース プールに割り当てることもできます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
## <a name="syntax"></a>構文  
  
```  
ALTER WORKLOAD GROUP { group_name | "default" }  
[ WITH  
    ([ IMPORTANCE = { LOW | MEDIUM | HIGH } ]  
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]  
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]  
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]   
      [ [ , ] MAX_DOP = value ]  
      [ [ , ] GROUP_MAX_REQUESTS = value ] )  
 ]  
[ USING { pool_name | "default" } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *group_name* | "**default**"       
 既存のユーザー定義のワークロード グループの名前か、リソース ガバナーの既定のワークロード グループを指定します。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール時に、リソース ガバナーにより "既定の" グループと内部のグループが作成されます。  
  
 オプションの "default" を ALTER WORKLOAD GROUP で使用する場合は、システム予約語の DEFAULT と競合しないように引用符 ("") または角かっこ ([]) で囲む必要があります。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
> [!NOTE]  
> 定義済みのワークロード グループおよびリソース プールはすべて、"default" などの小文字の名前を使用しています。 大文字と小文字を区別する照合順序を使用するサーバーでは、これを考慮する必要があります。 SQL_Latin1_General_CP1_CI_AS など、大文字と小文字を区別しない照合順序を使用するサーバーでは、"default" と "Default" が同じものと見なされます。  
  
 IMPORTANCE = { LOW | **MEDIUM** | HIGH }       
 ワークロード グループでの要求の相対的な重要度を指定します。 重要度は次のいずれかです。  
  
-   LOW  
-   MEDIUM (既定)  
-   HIGH  
  
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
  
 REQUEST_MEMORY_GRANT_TIMEOUT_SEC =*value*  
 メモリ許可 (作業バッファー メモリ) が使用可能になるのをクエリが待機できる最大時間を秒単位で指定します。  
  
> [!NOTE]  
> メモリ許可のタイムアウトに達しても、常にクエリが失敗するとは限りません。 クエリが失敗するのは、同時実行クエリ数が多すぎる場合だけです。 それ以外の場合、クエリは最小限のメモリ許可しか取得できないので、クエリのパフォーマンスが低下します。  
  
 *value* は正の整数である必要があります。 *value* の既定の設定である 0 の場合、クエリ コストに基づく内部の計算を使用して、最大時間が決定されます。  
  
 MAX_DOP =*value*       
 並列要求の最大 DOP (並列処理の次数) を指定します。 *value* は 0 または正の整数 (1 から 255) にする必要があります。 *value* が 0 の場合、サーバーは並列処理の最大限度を選択します。 これは既定の推奨設定です。  
  
> [!NOTE]  
> [!INCLUDE[ssDE](../../includes/ssde-md.md)]によって MAX_DOP に設定される実際の値は、指定された値よりも小さくなる場合があります。 最終的な値は、min(255, *number of CPUs)* という式で決定されます。  
  
> [!CAUTION]  
> MAX_DOP を変更すると、サーバーのパフォーマンスが低下することがあります。 MAX_DOP を変更する必要がある場合には、1 つの NUMA ノードで示されているハードウェア スケジューラの最大数以下の値に設定することをお勧めします。 MAX_DOP に 8 よりも大きな値を設定することはお勧めできません。  
  
 MAX_DOP は次のように処理されます。  
  
-   ワークロード グループの MAX_DOP を超えない限り、クエリ ヒントとしての MAX_DOP が有効になります。  
  
-   クエリ ヒントとしての MAX_DOP は、sp_configure の 'max degree of parallelism' を常にオーバーライドします。  
  
-   ワークロード グループの MAX_DOP は、sp_configure の 'max degree of parallelism' をオーバーライドします。  
  
-   コンパイル時にクエリが直列 (MAX_DOP = 1) としてマークされている場合は、ワークロード グループまたは sp_configure の設定にかかわらず、実行時に並列に変更することはできません。  
  
 DOP は、構成した後、許可メモリの不足時にのみ低くすることができます。 ワークロード グループの再構成は、許可メモリ キューで待機している間は認識されません。  
  
 GROUP_MAX_REQUESTS = *value*      
 ワークロード グループで実行を許可する同時要求の最大数を指定します。 *value* は、0 または正の整数にする必要があります。 *value* の既定の設定である 0 の場合、無制限の要求が許可されます。 同時要求の最大数に達した場合、そのグループのユーザーはログインできますが、同時要求数が指定した値を下回るまで待機状態になります。  
  
 USING { *pool_name* | "**default**" }      
 ワークロード グループを *pool_name* で識別されるユーザー定義のリソース プールに関連付けます。実質的には、これによってワークロード グループがリソース プールに配置されます。 *pool_name* を指定していない場合、または USING 引数を使用していない場合、ワークロード グループは事前に定義されたリソース ガバナーの既定のプールに配置されます。  
  
 オプションの "default" を ALTER WORKLOAD GROUP で使用する場合は、システム予約語の DEFAULT と競合しないように引用符 ("") または角かっこ ([]) で囲む必要があります。 詳細については、「[データベース識別子](../../relational-databases/databases/database-identifiers.md)」を参照してください。  
  
> [!NOTE]  
> オプションの "default" は、大文字と小文字が区別されます。  
  
## <a name="remarks"></a>Remarks  
 ALTER WORKLOAD GROUP は、既定のグループに対して使用できます。  
  
 ワークロード グループの構成の変更は、ALTER RESOURCE GOVERNOR RECONFIGURE を実行しないと有効になりません。 プランを変更し、設定に影響する場合、新しい設定は、DBCC FREEPROCCACHE (*pool_name*) の実行後にのみ、前にキャッシュされたプランに反映されます。この *pool_name* は、ワークロード グループが関連付けられているリソース ガバナー リソース プールの名前です。  
  
-   MAX_DOP を 1 に変更する場合、並列プランは直列モードで実行できるため、DBCC FREEPROCCACHE を実行する必要はありません。 ただし、直列プランとしてコンパイルされたプランほど効率的ではない可能性があります。  
  
-   MAX_DOP を 1 から 0、または 1 より大きい値に変更する場合、DBCC FREEPROCCACHE を実行する必要はありません。 ただし、直列プランは並列で実行できません。そのため、個々のキャッシュを消去すると、場合によっては、新しいプランを並列処理でコンパイルできます。  
  
> [!CAUTION]  
> 複数のワークロード グループに関連付けられているリソース プールからキャッシュされているプランを消去すると、ユーザー定義のリソース プールが *pool_name* で識別されているすべてのワークロード グループに影響します。  
  
 DDL ステートメントを実行する場合、Resource Governor の状態について詳しく理解しておくことをお勧めします。 詳細については、「[リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)」を参照してください。  
  
 REQUEST_MEMORY_GRANT_PERCENT:[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]インデックスの作成では、パフォーマンスの改善のために最初に付与されたのよりも多くのワークスペース メモリを使用することが許可されています。 この特別な処理は、今後のバージョンのリソース ガバナーでもサポートされますが、最初のメモリ許可も追加のメモリ許可もリソース プール設定とワークロード グループ設定によって制限されます。  
  
 **パーティション テーブルのインデックス作成**  
  
 非固定パーティション テーブルのインデックス作成によって消費されるメモリは、含まれるパーティションの数に比例します。  必要なメモリの合計が、リソース ガバナーのワークロード グループの設定によって課せられているクエリごとの制限 (REQUEST_MAX_MEMORY_GRANT_PERCENT) を超えると、インデックス作成の実行に失敗します。 "default" ワークロード グループでは、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] との互換性のために、クエリごとの制限を超えてもクエリの開始に必要な最低限のメモリを使用できるようになっているので、そのようなクエリを実行するのに十分な量のメモリが "default" リソース プールに対して構成されていれば、同じインデックス作成を "default" ワークロード グループで実行できる可能性があります。  
  
## <a name="permissions"></a>アクセス許可  
 `CONTROL SERVER` 権限が必要です。  
  
## <a name="examples"></a>使用例  
 次の例は、既定のグループの要求の重要度を `MEDIUM` から `LOW` に変更する方法を示しています。  
  
```sql  
ALTER WORKLOAD GROUP "default"  
WITH (IMPORTANCE = LOW);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
 次の例は、ワークロード グループを現在のプールから既定のプールに移動する方法を示しています。  
  
```sql  
ALTER WORKLOAD GROUP adHoc  
USING [default];  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
