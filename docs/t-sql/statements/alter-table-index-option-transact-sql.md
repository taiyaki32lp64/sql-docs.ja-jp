---
title: " | Microsoft Docs"
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- index_option
ms.assetid: 8a14f12d-2fbf-4036-b8b2-8db3354e0eb7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e70998bed1ed0f2681009622cfb086baa79dcf02
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982013"
---
# <a name="alter-table-index_option-transact-sql"></a>ALTER TABLE index_option (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) で作成される制約定義の一部であるインデックスに適用できる一連のオプションを指定します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
{   
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF } 
  | OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | OFF } 
  | SORT_IN_TEMPDB = { ON | OFF }   
  | ONLINE = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = { NONE |ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
      [ , ...n ] ) ]  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
  
<single_partition_rebuild__option> ::=  
{  
    SORT_IN_TEMPDB = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = {NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE } }  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                           ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )   
}  
```  
  
## <a name="arguments"></a>引数  
 PAD_INDEX **=** { ON | **OFF** }  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 インデックスの埋め込みを指定します。 既定値は OFF です。  
  
 ON  
 FILLFACTOR で指定される空き領域のパーセンテージが、インデックスの中間レベルのページに適用されます。  
  
 OFF または *fillfactor* の指定なし  
 中間レベル ページは、中間ページの一連のキーを考慮しつつ、インデックスが持つことのできる最大サイズの行が少なくとも 1 つ格納できる領域を残して、ほぼ容量いっぱいに使用されます。  
  
 FILLFACTOR **=** _fillfactor_  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 インデックスの作成時または変更時に、[!INCLUDE[ssDE](../../includes/ssde-md.md)] が各インデックス ページのリーフ レベルをどの程度まで埋めるかを、パーセント値で指定します。 1 ～ 100 の整数値を指定する必要があります。 既定値は 0 です。  
  
> [!NOTE]  
>  FILL FACTOR 値 0 と 100 は、すべての面でまったく同じ結果になります。  
  
 IGNORE_DUP_KEY **=** { ON | **OFF** }  
 挿入操作で、一意のインデックスに重複するキー値を挿入しようとした場合の応答の種類を指定します。 IGNORE_DUP_KEY オプションは、インデックスが作成または再構築された後の挿入操作のみに適用されます。 [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)、[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)、または [UPDATE](../../t-sql/queries/update-transact-sql.md) を実行した場合、このオプションは無効です。 既定値は OFF です。  
  
 ON  
 重複したキー値が一意のインデックスに挿入されると、警告メッセージが表示されます。 一意性制約に違反する行のみが失敗します。  
  
 OFF  
 重複したキー値が一意のインデックスに挿入されると、エラー メッセージが表示されます。 INSERT 操作全体がロールバックされます。  
  
 ビューに作成されたインデックス、一意でないインデックス、XML インデックス、空間インデックス、およびフィルター処理されたインデックスについては、IGNORE_DUP_KEY を ON に設定することはできません。  
  
 IGNORE_DUP_KEY を表示するには、[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) を使用します。  
  
 旧バージョンと互換性のある構文では、WITH IGNORE_DUP_KEY は WITH IGNORE_DUP_KEY = ON と同じです。  
  
 STATISTICS_NORECOMPUTE **=** { ON | **OFF** }  
 統計を再計算するかどうかを指定します。 既定値は OFF です。  
  
 ON  
 古い統計情報は、自動的には再計算されません。  
  
 OFF  
 自動統計更新が有効です。  
  
 ALLOW_ROW_LOCKS **=** { **ON** | OFF }  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 行ロックを許可するかどうかを指定します。 既定値は ON です。  
  
 ON  
 インデックスにアクセスするとき、行ロックが許可されます。 いつ行ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって決定されます。  
  
 OFF  
 行ロックは使用されません。  
  
 ALLOW_PAGE_LOCKS **=** { **ON** | OFF }  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 ページ ロックを許可するかどうかを指定します。 既定値は ON です。  
  
 ON  
 ページにアクセスするとき、行ロックが許可されます。 いつページ ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] によって決定されます。  
  
 OFF  
 ページ ロックは使用されません。  

 OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | **OFF** }

**適用対象**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 以降。

最終ページ挿入競合に対して最適化するかどうかを指定します。 既定値は OFF です。 詳細については、CREATE INDEX のページの「[シーケンシャル キー](./create-index-transact-sql.md#sequential-keys)」セクションを参照してください。
 
 SORT_IN_TEMPDB **=** { ON | **OFF** }  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 並べ替えの結果を **tempdb** に格納するかどうかを指定します。 既定値は OFF です。  
  
 ON  
 インデックス構築に使用される中間の並べ替え結果が **tempdb** に格納されます。 **tempdb** がユーザー データベースとは異なるディスク セットにある場合は、インデックスの作成に要する時間が削減されます。 インデックスの構築中に使用されるディスク領域のサイズは増加します。  
  
 OFF  
 中間の並べ替え結果はインデックスと同じデータベースに格納されます。  
  
 ONLINE **=** { ON | **OFF** }  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 インデックス操作時に、基になるテーブルや関連するインデックスをクエリやデータ変更で使用できるかどうかを指定します。 既定値は OFF です。 REBUILD は ONLINE 操作として実行できます。  
  
> [!NOTE]  
>  一意な非クラスター化インデックスはオンラインで作成できません。 これには、UNIQUE 制約または PRIMARY KEY 制約によって作成されるインデックスが含まれます。  
  
 ON  
 長期のテーブル ロックは、インデックス操作の間は保持されません。 インデックス操作の主なフェーズの間は、基になるテーブル上に、インテント共有 (IS) ロックのみが保持されます。 これにより、基になるテーブルやインデックスに対するクエリや更新を続行できます。 操作の開始時、非常に短い時間ですが、ソース オブジェクトの共有 (S) ロックが保持されます。 操作の終了時、短い時間ですが、非クラスタ化インデックスが作成される場合は、ソース オブジェクト上で共有 (S) ロックの取得が行われます。また、クラスター化インデックスがオンラインで作成または削除され、クラスター化または非クラスター化インデックスが再構築される場合は、SCH-M (スキーマ修正) ロックが取得されます。 オンライン インデックス ロックは短いメタデータ ロックですが、特に Sch-M ロックは、このテーブルに対するすべてのブロックしているトランザクションの完了を待機する必要があります。 待機中、Sch-M ロックは、同じテーブルにアクセスするためにこのロックの後に待機している他のすべてのトランザクションをブロックします。 インデックスがローカルの一時テーブルに作成される場合、ONLINE は ON にできません。  
  
> [!NOTE]  
>  オンライン インデックス再構築では、このセクションの後の方で説明されている *low_priority_lock_wait* オプションを設定できます。 *low_priority_lock_wait* は、オンライン インデックス再構築中の S および Sch-M ロックの優先度を管理します。  
  
 OFF  
 テーブル ロックは、インデックス操作の間適用されます。 このため、操作中は、すべてのユーザーは基になるテーブルにアクセスできません。 クラスター化インデックスを作成、再構築、または削除するオフライン インデックス操作や、非クラスター化インデックスを再構築または削除するオフライン インデックス操作では、テーブル上のスキーマ修正 (Sch-M) ロックが取得されます。 このため、操作中は、すべてのユーザーは基になるテーブルにアクセスできません。 非クラスター化インデックスを作成するオフライン インデックス操作では、テーブルの共有 (S) ロックが取得されます。 この場合は、基になるテーブルに対して更新は許可されませんが、SELECT ステートメントなどの読み取り操作は許可されます。  
  
 詳細については、「[オンライン インデックス操作の動作原理](../../relational-databases/indexes/how-online-index-operations-work.md)」を参照してください。  
  
> [!NOTE]
>  オンラインでのインデックス操作は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
 MAXDOP **=** _max_degree_of_parallelism_  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 インデックス操作の間、**max degree of parallelism** 構成オプションをオーバーライドします。 詳細については、「 [max degree of parallelism サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)」を参照してください。 並列プランの実行で使用されるプロセッサ数を制限するには、MAXDOP を使用します。 最大数は 64 プロセッサです。  
  
 *max_degree_of_parallelism* は次のように指定できます。  
  
 - 1 - 並列プラン生成を抑制します。  
 - \>1 - 並列インデックス操作で使用される最大プロセッサ数を、指定した数に制限します。  
 - 0 (既定値) - 実際のプロセッサの数を使用または現在のシステム ワークロードに基づいて少なくします。  
  
 詳細については、「 [並列インデックス操作の構成](../../relational-databases/indexes/configure-parallel-index-operations.md)」を参照してください。  
  
> [!NOTE]
>  並列インデックス操作は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
 DATA_COMPRESSION  
 **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 指定したテーブル、パーティション番号、またはパーティション範囲に、データ圧縮オプションを指定します。 次のオプションがあります。  
  
 NONE  
 テーブルまたは指定したパーティションが圧縮されません。 行ストア テーブルにのみ適用され、列ストア テーブルには適用されません。  
  
 ROW  
 行の圧縮を使用して、テーブルまたは指定したパーティションが圧縮されます。 行ストア テーブルにのみ適用され、列ストア テーブルには適用されません。  
  
 PAGE  
 ページの圧縮を使用して、テーブルまたは指定したパーティションが圧縮されます。 行ストア テーブルにのみ適用され、列ストア テーブルには適用されません。  
  
 COLUMNSTORE  
 **適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。  
  
 列ストア テーブルにのみ適用されます。 COLUMNSTORE は、COLUMNSTORE_ARCHIVE オプションで圧縮されたパーティションを解凍するように指定します。 データが復元されると、COLUMNSTORE インデックスはすべての列ストア テーブルに使用された列ストア圧縮を使用して引き続き圧縮されます。  
  
 COLUMNSTORE_ARCHIVE  
 **適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。  
  
 クラスター化列ストア インデックスを使用して格納されているテーブルである、列ストア テーブルのみに適用されます。 COLUMNSTORE_ARCHIVE は、指定したパーティションをより小さなサイズにさらに圧縮します。 これは、保存用や、ストレージの使用量を減らす必要があり、しかも保存と取得に時間をかける余裕があるその他の状況で使用できます。  
  
 圧縮の詳細については、「[データ圧縮](../../relational-databases/data-compression/data-compression.md)」を参照してください。  
  
ON PARTITIONS **(** { \<partition_number_expression> | \<range> } [ **,** ...*n* ] **)** **適用対象**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降。  
  
 DATA_COMPRESSION 設定を適用するパーティションを指定します。 テーブルがパーティション分割されていない場合に ON PARTITIONS 引数を使用すると、エラーが発生します。 ON PARTITIONS 句を指定しないと、パーティション テーブルのすべてのパーティションに対して DATA_COMPRESSION オプションが適用されます。  
  
\<partition_number_expression> は以下の方法で指定できます。  
  
-   たとえば次のようにパーティション番号を指定します。ON PARTITIONS (2)。  
-   コンマで区切った複数の個別のパーティションのパーティション番号を指定します。たとえば次のとおりです。ON PARTITIONS (1, 5)。  
-   範囲と個別のパーティションの両方を指定します。たとえば次のとおりです。ON PARTITIONS (2, 4, 6 TO 8)。  
  
\<範囲> はパーティション番号として、TO で区切って指定できます。たとえば次のとおりです。ON PARTITIONS (6 TO 8)。  
  
 さまざまなパーティションにさまざまな種類のデータ圧縮を設定するには、DATA_COMPRESSION オプションを複数回指定します。例:  
  
```sql  
--For rowstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
)  
  
--For columnstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = COLUMNSTORE ON PARTITIONS (1, 3, 5),   
DATA_COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (2, 4, 6 TO 8)  
)  
```  
  
**\<single_partition_rebuild__option>**  
 ほとんどの場合、インデックスの再構築では、パーティション インデックスのすべてのパーティションを再構築します。 次のオプションを 1 つのパーティションに適用した場合は、すべてのパーティションの再構築は行われません。  
  
-   SORT_IN_TEMPDB  
-   MAXDOP  
-   DATA_COMPRESSION  
  
**low_priority_lock_wait**  
 **適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。  
  
 このテーブルに対するブロック操作がなくなるとすぐに、**SWITCH** またはオンライン インデックス再構築が完了します。 *WAIT_AT_LOW_PRIORITY* は、**SWITCH** またはオンライン インデックス再構築の操作が直ちに完了できない場合は待機することを示します。 この操作は優先度の低いロックを保持し、DDL ステートメントと競合するロックを保持する他の操作が続行できるようにします。 **WAIT AT LOW PRIORITY** オプションを省略すると、`WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)` と同等になります。  
  
MAX_DURATION = *time* **[MINUTES]**  
 取得する必要がある、**SWITCH** またはオンライン インデックス再構築のロックが、DDL コマンドの実行時に待機する時間 (分単位で指定される整数値) です。 SWITCH またはオンライン インデックス再構築の操作は、直ちに完了しようとします。 操作が **MAX_DURATION** の期間ブロックされると、**ABORT_AFTER_WAIT** アクションのいずれかが実行されます。 **MAX_DURATION** の期間は常に分単位なので、**MINUTES** という単語は省略できます。  
  
ABORT_AFTER_WAIT = [**NONE** | **SELF** | **BLOCKERS** } ]  
 NONE  
 ロックの優先順位を変更せずに (通常の優先順位を使用して)、**SWITCH** またはオンライン インデックス再構築の操作を続行します。  
  
SELF  
 いずれのアクションも行わずに、現在実行中の **SWITCH** またはオンライン インデックス再構築の DDL 操作を終了します。  
  
BLOCKERS  
 現在 **SWITCH** またはオンライン インデックス再構築の DDL 操作をブロックしているすべてのユーザー トランザクションを強制終了して、操作を続行できるようにします。  
 BLOCKERS には **ALTER ANY CONNECTION** 権限が必要です。  
  
## <a name="remarks"></a>Remarks  
 インデックスのオプションについて詳しくは、「[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md)   
 [computed_column_definition &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-computed-column-definition-transact-sql.md)   
 [table_constraint &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)  
  
 
