---
title: テーブル ヒント (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TABLE_HINT_TSQL
- Table Hint
dev_langs:
- TSQL
helpviewer_keywords:
- SERIALIZABLE table hint
- UPDLOCK table hint
- HOLDLOCK table hint
- TABLOCKX table hint
- READUNCOMMITTED table hint
- hints [SQL Server], tables
- READCOMMITTEDLOCK table hint
- FORCESCAN table hint
- ROWLOCK table hint
- XLOCK table hint
- NOLOCK table hint
- READPAST table hint
- NOWAIT table hint
- FORCESEEK table hint
- table hints [SQL Server]
- TABLOCK table hint
- REPEATABLEREAD table hint
- READ COMMITTED table hint
- NOEXPAND table hint
- PAGLOCK table hint
ms.assetid: 8bf1316f-c0ef-49d0-90a7-3946bc8e7a89
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: d5675f7c62ce43a9e41770075cd4a97253ea051e
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981761"
---
# <a name="hints-transact-sql---table"></a>ヒント (Transact-SQL) - Table
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  テーブル ヒントでは、ロック手法、1 つ以上のインデックス、クエリ処理操作 (テーブル スキャンやインデックスのシークなど)、またはその他のオプションを指定することによって、データ操作言語 (DML) ステートメントが存続する間だけ、クエリ オプティマイザーの既定の動作をオーバーライドします。 テーブル ヒントは、DML ステートメントの FROM 句で指定され、その句で参照されるテーブルまたはビューのみに影響します。  
  
> [!CAUTION]  
>  通常、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーでは、クエリにとって最適な実行プランが選択されるため、ヒントは、経験を積んだ開発者やデータベース管理者が最後の手段としてのみ使用することをお勧めします。  
  
 **適用対象:**  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [INSERT](../../t-sql/statements/insert-transact-sql.md)  
  
 [SELECT](../../t-sql/queries/select-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [MERGE](../../t-sql/statements/merge-transact-sql.md)  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
WITH  ( <table_hint> [ [, ]...n ] )  
  
<table_hint> ::=   
[ NOEXPAND ] {   
    INDEX  ( index_value [ ,...n ] )   
  | INDEX =  ( index_value )      
  | FORCESEEK [( index_value ( index_column_name  [ ,... ] ) ) ]  
  | FORCESCAN  
  | FORCESEEK  
  | HOLDLOCK   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | READUNCOMMITTED   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT   
  | SPATIAL_WINDOW_MAX_CELLS = integer  
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK   
}   
  
<table_hint_limited> ::=  
{  
    KEEPIDENTITY   
  | KEEPDEFAULTS   
  | HOLDLOCK   
  | IGNORE_CONSTRAINTS   
  | IGNORE_TRIGGERS   
  | NOLOCK   
  | NOWAIT  
  | PAGLOCK   
  | READCOMMITTED   
  | READCOMMITTEDLOCK   
  | READPAST   
  | REPEATABLEREAD   
  | ROWLOCK   
  | SERIALIZABLE   
  | SNAPSHOT   
  | TABLOCK   
  | TABLOCKX   
  | UPDLOCK   
  | XLOCK   
}   
```  
  
## <a name="arguments"></a>引数  
WITH **(** \<table_hint> **)** [ **[,]** ...*n* ]  
いくつかの例外を除き、テーブル ヒントは、FROM 句で WITH キーワードを使用して指定した場合にのみサポートされます。 また、テーブル ヒントはかっこを使用して指定する必要があります。  
  
> [!IMPORTANT]  
> WITH キーワードを省略することは非推奨とされます。[!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
次のテーブル ヒントは、WITH キーワードの有無に関係なく使用できます。NOLOCK、READUNCOMMITTED、UPDLOCK、REPEATABLEREAD、SERIALIZABLE、READCOMMITTED、TABLOCK、TABLOCKX、PAGLOCK、ROWLOCK、NOWAIT、READPAST、XLOCK、SNAPSHOT、NOEXPAND。 これらのテーブル ヒントを WITH キーワードを使用せずに指定するときは、単独で指定してください。 例:  
  
```sql  
FROM t (TABLOCK)  
```  
  
ヒントを他のオプションと一緒に指定する場合は、次のように WITH キーワードを使用して指定する必要があります。  
  
```sql  
FROM t WITH (TABLOCK, INDEX(myindex))  
```  
  
複数のテーブル ヒント間にはコンマを使用することをお勧めします。  
  
> [!IMPORTANT]  
>  ヒントの分割にコンマの代わりにスペースを用いる方法は非推奨とされます。[!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
NOEXPAND  
クエリ オプティマイザーがクエリを処理する場合に、インデックス付きビューが展開されず、基になるテーブルがアクセスされないことを指定します。 クエリ オプティマイザーは、ビューをクラスター化インデックスを持つテーブルのように取り扱います。 NOEXPAND はインデックス付きビューにのみ適用できます。 詳細については、「[NOEXPAND の使用](#using-noexpand)」を参照してください。  
  
INDEX  **(** _index\_value_ [ **,** ... _n_ ] ) | INDEX =  ( _index\_value_ **)**  
INDEX() 構文では、ステートメントを処理するときにクエリ オプティマイザーが使用する 1 つ以上のインデックスの名前または ID を指定します。 一方、INDEX = 構文では、単一のインデックス値を指定します。 各テーブルに対して指定できるのは 1 つのインデックス ヒントだけです。  
  
クラスター化インデックスがある場合、INDEX(0) はクラスター化インデックスのスキャンを実行し、INDEX(1) はクラスター化インデックスのスキャンまたはシークを実行します。 クラスター化インデックスがない場合、INDEX(0) はテーブル スキャンを実行し、INDEX(1) はエラーと見なされます。  
  
 1 つのヒント リストの中で複数のインデックスが使用されている場合、重複するものは無視され、リスト内の残りのインデックスを使用してテーブルの行が取得されます。 インデックス ヒント内のインデックスの順番は重要です。 複数のインデックス ヒントはインデックスの AND 処理も設定し、クエリ オプティマイザーはアクセスされる各インデックスに可能な限り多くの条件を適用します。 ヒント インデックスの集合に、クエリで参照される列のすべてが含まれているわけではない場合、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]がすべてのインデックス列を取得した後で、残りの列を取得するフェッチが実行されます。  
  
> [!NOTE]  
> 複数のインデックスを参照するインデックス ヒントが、スター結合のファクト テーブルで使用されている場合、オプティマイザーはそのインデックス ヒントを無視し、警告メッセージを返します。 また、インデックス論理和は、インデックス ヒントが指定されたテーブルでは許可されません。  
  
 テーブル ヒント内のインデックスの最大個数は、非クラスター化インデックスが 250 個です。  
  
KEEPIDENTITY  
INSERT ステートメントで、BULK オプションが [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) と一緒に使用されているときにのみ適用できます。  
  
 インポートしたデータ ファイルの ID 値 (複数可) を ID 列に使用することを指定します。 KEEPIDENTITY を指定しない場合、この列の ID 値は確認されるのみでインポートされません。クエリ オプティマイザーは、テーブルの作成時に指定された seed および increment の値を基に一意な値を自動的に割り当てます。  
  
> [!IMPORTANT]  
> テーブルやビューの ID 列の値がデータ ファイルに含まれておらず、ID 列がテーブルの最終列でもない場合は、その ID 列をスキップする必要があります。 詳細については、「[フォーマット ファイルを使用したデータ フィールドのスキップ &#40;SQL Server&#41;](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)」を参照してください。 ID 列のスキップに成功すると、クエリ オプティマイザーは、その ID 列の一意な値を、インポートされたテーブル行に自動的に割り当てます。  
  
このヒントを `INSERT ... SELECT * FROM OPENROWSET(BULK...)` ステートメントに使用する例については、「[データの一括インポート時の ID 値の保持 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)」を参照してください。  
  
テーブルの ID 値の確認については、「[DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)」を参照してください。  
  
KEEPDEFAULTS  
INSERT ステートメントで、BULK オプションが [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) と一緒に使用されているときにのみ適用できます。  
  
データ レコードにテーブルの列値が含まれていない場合に、NULL の代わりにテーブル列の既定値を挿入することを指定します。  
  
このヒントを INSERT ...SELECT * FROM OPENROWSET(BULK...) ステートメントに使用する例については、「[一括インポート中の NULL の保持または既定値の使用 &#40;SQL Server&#41;](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)」を参照してください。  
  
FORCESEEK [ **(** _index\_value_ **(** _index\_column\_name_ [ **,** ... _n_ ] **))** ]  
クエリ オプティマイザーに対し、テーブルやビューのデータへのアクセス パスとしてインデックスのシーク操作のみを使用することを指定します。 

> [!NOTE]
> [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] SP1 以降では、インデックス パラメーターも指定できます。 その場合、一度でも指定されたインデックス列が使用されると、クエリ オプティマイザーでは指定されたインデックスを介したインデックスのシーク操作のみが検討されます。  
  
 *index_value*  
 インデックスの名前またはインデックスの ID 値です。 インデックス ID 0 (ヒープ) は指定できません。 インデックスの名前または ID を返すには、**sys.indexes** カタログ ビューにクエリを実行します。  
  
 *index_column_name*  
 シーク操作に含めるインデックス列の名前です。 インデックス パラメーターを使用して FORCESEEK を指定することは、INDEX ヒントを使用して FORCESEEK を使用することと同じです。 ただし、シーク対象のインデックスとシーク操作で考慮するインデックス列の両方を指定することで、クエリ オプティマイザーで使用されるアクセス パスをより詳細に制御できるようになります。 オプティマイザーでは、必要に応じて、追加の列が検討される場合もあります。 たとえば、非クラスター化インデックスが指定されている場合、オプティマイザーでは、指定された列に加え、クラスター化インデックスのキー列を使用することもできます。  
  
FORCESEEK ヒントは以下の方法で指定できます。  
  
|構文|例|[説明]|  
|------------|-------------|-----------------|  
|インデックスまたは INDEX ヒントを使用しない場合|`FROM dbo.MyTable WITH (FORCESEEK)`|クエリ オプティマイザーでは、関連するインデックスを介してテーブルやビューにアクセスするためのインデックスのシーク操作のみが検討されます。|  
|INDEX ヒントと組み合わせた場合|`FROM dbo.MyTable WITH (FORCESEEK, INDEX (MyIndex))`|クエリ オプティマイザーでは、指定されたインデックスを介してテーブルやビューにアクセスするためのインデックスのシーク操作のみが検討されます。|  
|インデックスとインデックス列を指定してパラメーター化する場合|`FROM dbo.MyTable WITH (FORCESEEK (MyIndex (col1, col2, col3)))`|少なくとも指定されたインデックス列を使用した場合、クエリ オプティマイザーでは、指定されたインデックスを介してテーブルやビューにアクセスするためのインデックスのシーク操作のみが検討されます。|  
  
(インデックス パラメーターを使用するかどうかにかかわらず) FORCESEEK ヒントを使用する際は、次のガイドラインを考慮してください。  
-   ヒントは、テーブル ヒントまたはクエリ ヒントとして指定できます。 クエリ ヒントの詳細については、「[クエリ ヒント &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)」を参照してください。  
-   インデックス付きビューに FORCESEEK を適用するには、NOEXPAND ヒントも指定する必要があります。  
-   ヒントは、テーブルまたはビューごとに 1 回だけ適用できます。  
-   ヒントは、リモート データ ソースに指定できません。 インデックス ヒントを使用して FORCESEEK を指定すると、エラー 7377 が返されます。また、インデックス ヒントなしで FORCESEEK を使用すると、エラー 8180 が返されます。  
-   FORCESEEK が原因でプランが見つからない場合、エラー 8622 が返されます。  
  
インデックス パラメーターを使用して FORCESEEK を指定する際は、次のガイドラインと制限が適用されます。  
-   ヒントは、INSERT、UPDATE、または DELETE ステートメントの対象であるテーブルには指定できません。  
-   ヒントは、INDEX ヒントまたは別の FORCESEEK ヒントと組み合わせて指定することができません。  
-   少なくとも 1 列を指定する必要があり、先頭のキー列にする必要があります。  
-   追加のインデックス列を指定できますが、キー列は省略できません。 たとえば、指定されたインデックスに `a`、`b`、および `c` というキー列が含まれている場合、有効な構文には `FORCESEEK (MyIndex (a))` および `FORCESEEK (MyIndex (a, b)` が含まれます。 無効な構文には、`FORCESEEK (MyIndex (c))` と `FORCESEEK (MyIndex (a, c)` が含まれます。  
-   ヒントで指定された列名の順序は、参照先のインデックスでの列の順序と一致させる必要があります。  
-   インデックス キーの定義にない列は、指定できません。 たとえば、非クラスター化インデックスでは、定義されたインデックス キー列のみを指定できます。 自動的にインデックスに含まれるクラスター化キー列は指定できませんが、オプティマイザーでは使用できます。  
-   xVelocity メモリ最適化列ストア インデックスは、インデックス パラメーターとして指定できません。 エラー 366 が返されます。  
-   インデックス定義を変更すると (列の追加や削除など)、そのインデックスを参照するクエリに対する変更も必要になる場合があります。  
-   ヒントを使用すると、オプティマイザーでは、テーブル上の空間インデックスまたは XML インデックスが検討されなくなります。  
-   ヒントは、FORCESCAN ヒントと組み合わせて指定することはできません。  
-   パーティション インデックスでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって暗黙的に追加されたパーティション分割列を FORCESEEK ヒントで指定できません。  
  
> [!CAUTION]  
> パラメーターを使用して FORCESEEK を指定すると、オプティマイザーで考慮できるプラン数の制限は、パラメーターなしで FORCESEEK を指定した場合よりも多くなります。 これにより、`Plan cannot be generated` というエラーが生じる回数が増加する可能性があります。 将来のリリースでは、クエリ オプティマイザーに対して内部変更を行うため、より多くのプランを考慮できるようになります。  
  
FORCESCAN **適用対象**:[!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] SP1 以降。
クエリ オプティマイザーに対し、参照されているテーブルやビューへのアクセス パスとして、インデックスのスキャン操作のみを使うことを指定します。 FORCESCAN ヒントは、オプティマイザーが影響を受ける行数を過小評価し、スキャン操作ではなくシーク操作を選択するクエリに役立つ場合があります。 この場合、操作に許可されるメモリの量は少なすぎて、クエリのパフォーマンスに影響します。  
  
FORCESCAN を指定する際には、INDEX ヒントを使用してもしなくてもかまいません。 インデックス ヒントと組み合わせると (`INDEX = index_name, FORCESCAN`)、クエリ オプティマイザーでは、参照されるテーブルにアクセスする際に、指定されたインデックスを介したアクセス パスのみが検討されます。 インデックス ヒント INDEX(0) ベース テーブルのテーブル スキャン操作を強制するには、FORCESCAN を指定できます。  
  
パーティション テーブルやパーティション インデックスの場合、FORCESCAN が適用されるのは、クエリの述語評価によってパーティションが削除された後です。 つまり、スキャンは、テーブル全体ではなく、残りのパーティションのみに適用されます。  
  
FORCESCAN ヒントには次の制限があります。  
-   ヒントは、INSERT、UPDATE、または DELETE ステートメントの対象であるテーブルには指定できません。  
-   ヒントは、複数のインデックス ヒントと併用できません。  
-   ヒントを使用すると、オプティマイザーでは、テーブル上の空間インデックスまたは XML インデックスが検討されなくなります。  
-   ヒントは、リモート データ ソースに指定できません。  
-   ヒントは、FORCESEEK ヒントと組み合わせて指定することはできません。  
  
HOLDLOCK  
SERIALIZABLE に相当します。 詳細については、後の「SERIALIZABLE」を参照してください。 HOLDLOCK は、指定されたテーブルやビューに対してのみ、また、使用されているステートメントによって定義されたトランザクションの間のみ適用されます。 HOLDLOCK は、FOR BROWSE オプションを含む SELECT ステートメントでは使用できません。  
  
IGNORE_CONSTRAINTS  
INSERT ステートメントで、BULK オプションが [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) と一緒に使用されているときにのみ適用できます。  
  
テーブルに対する制約を一括インポート操作時に無視することを指定します。 既定では、INSERT は [Unique 制約と CHECK 制約](../../relational-databases/tables/unique-constraints-and-check-constraints.md)および[主キー制約と外部キー制約](../../relational-databases/tables/primary-and-foreign-key-constraints.md)をチェックします。 一括インポート操作の際に IGNORE_CONSTRAINTS を指定している場合、インポート対象のテーブルに対する制約が無視されます。 UNIQUE、PRIMARY KEY、または NOT NULL の各制約を無効にすることはできません。  
  
制約に違反する行が入力データに含まれている場合に、CHECK 制約および FOREIGN KEY 制約を無効化することができます。 CHECK 制約および FOREIGN KEY 制約を無効化することによって、データをインポートしてから、[!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用してデータをクリーンアップできます。  
  
ただし、CHECK 制約および FOREIGN KEY 制約を無視すると、操作の後、テーブルに設定されている制約のうち、無視された制約は [sys.check_constraints](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md) カタログ ビューまたは [sys.foreign_keys](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md) カタログ ビューで **is_not_trusted** とマークされます。 テーブル全体の制約は、任意の時点で必ず検証してください。 一括インポート操作の前にテーブルが空白になっていない場合、制約の再検証にかかるコストは、CHECK 制約および FOREIGN KEY 制約を増分データに適用することによるコストを上回る可能性があります。  
  
IGNORE_TRIGGERS  
INSERT ステートメントで、BULK オプションが [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) と一緒に使用されているときにのみ適用できます。  
  
テーブルに対して定義されたトリガーを、一括インポート操作時に無視することを指定します。 既定では、INSERT はトリガーを適用します。  
  
アプリケーションがいずれのトリガーにも依存しておらず、パフォーマンスの最大化が重要な場合にのみ、IGNORE_TRIGGERS を使用してください。  
  
NOLOCK  
READUNCOMMITTED に相当します。 詳細については、後の「READUNCOMMITTED」を参照してください。  
  
> [!NOTE]  
> UPDATE ステートメントまたは DELETE ステートメントの場合: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
NOWAIT  
テーブルでロックがかかったらすぐにメッセージを返すように[!INCLUDE[ssDE](../../includes/ssde-md.md)]を設定します。 NOWAIT は、特定のテーブルに SET LOCK_TIMEOUT 0 を指定することに相当します。 NOWAIT ヒントは、TABLOCK ヒントも指定されている場合は機能しません。 TABLOCK ヒントを使用している場合に待機しないでクエリを終了するには、代わりにクエリの前に `SETLOCK_TIMEOUT 0;` を指定します。  
  
PAGLOCK  
通常使用される行やキーに対する個々のロックまたは単一のテーブル ロックの代わりに、ページ ロックを使用します。 既定では、操作に適したロック モードを使用します。 SNAPSHOT 分離レベルで実行中のトランザクションにおいてこのオプションを指定しても、UPDLOCK や HOLDLOCK など、ロックが必要な他のテーブル ヒントと組み合わせて指定しない限り、ページ ロックは取得されません。  
  
READCOMMITTED  
読み取り操作が、ロックまたは行のバージョン管理を使用して、READ COMMITTED 分離レベルのルールに従うことを指定します。 データベース オプション READ_COMMITTED_SNAPSHOT が OFF の場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]はデータの読み取り時に共有ロックを取得し、読み取り操作が完了するとロックを解除します。 データベース オプション READ_COMMITTED_SNAPSHOT が ON の場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)]はロックを取得せずに行のバージョン管理を使用します。 分離レベルについての詳細については、「[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
> UPDATE ステートメントまたは DELETE ステートメントの場合: [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
READCOMMITTEDLOCK  
読み取り操作が、ロックを使用して、READ COMMITTED 分離レベルのルールに従うことを指定します。 READ_COMMITTED_SNAPSHOT データベース オプションの設定にかかわらず、[!INCLUDE[ssDE](../../includes/ssde-md.md)] はデータの読み取り時に共有ロックを取得し、読み取り操作が完了するとロックを解除します。 分離レベルについての詳細については、「[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)」を参照してください。 このヒントは、INSERT ステートメントの対象のテーブルには指定できません。指定すると、エラー 4140 が返されます。  
  
READPAST  
他のトランザクションによってロックされている行を、[!INCLUDE[ssDE](../../includes/ssde-md.md)] が読み取らないことを指定します。 READPAST を指定すると、行レベルのロックはスキップされますが、ページレベルのロックはスキップされません。 つまり、[!INCLUDE[ssDE](../../includes/ssde-md.md)]は、ロックが解除されるまで現在のトランザクションをブロックする代わりに、行をスキップします。 たとえば、テーブル `T1` に整数型の列が 1 つあり、値 1、2、3、4、5 が格納されているとします。 このテーブルに対してトランザクション A で値 3 を 8 に変更し、この変更をまだコミットしていない間に SELECT * FROM T1 (READPAST) を実行すると、取得される値は 1、2、4、5 となります。 READPAST は主に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルを使用する作業キューの実装時に、ロックの競合を減らすために使用します。 READPAST を使用するキュー リーダーは、他のトランザクションによってロックされたキュー エントリを、ロックが解除されるまで待たずにスキップして、次に使用可能なキュー エントリへ進みます。  
  
READPAST は、UPDATE ステートメントまたは DELETE ステートメントで参照されるテーブル、および FROM 句で参照されるテーブルで指定できます。 UPDATE ステートメントで READPAST を指定した場合、ステートメント内での指定場所にかかわらず、更新対象レコード特定のためのデータ読み取り時にだけ適用されます。 INSERT ステートメントの INTO 句では、テーブルに READPAST を指定することができません。 READPAST を使用する更新操作や削除操作は、外部キーやインデックス付きビューの読み取り時、またはセカンダリ インデックスの変更時にブロックを行う場合があります。  
  
READPAST は、READ COMMITTED 分離レベルまたは REPEATABLE READ 分離レベルで実行中のトランザクションでのみ指定できます。 SNAPSHOT 分離レベルで実行中のトランザクションにおいてこのオプションを指定する場合、UPDLOCK や HOLDLOCK など、ロックが必要な他のテーブル ヒントと組み合わせて指定する必要があります。  
  
READ_COMMITTED_SNAPSHOT データベース オプションが ON に設定され、次のいずれかの条件に該当する場合、READPAST テーブル ヒントは指定できません。  
-   セッションのトランザクション分離レベルが READ COMMITTED の場合  
-   READCOMMITTED テーブル ヒントもクエリで指定されている場合  
  
このような場合に READPAST ヒントを指定するには、READCOMMITTED テーブル ヒントがある場合は削除し、クエリに READCOMMITTEDLOCK テーブル ヒントを含めます。  
  
READUNCOMMITTED  
ダーティ リードを許可することを指定します。 現在のトランザクションによるデータ読み取りが他のトランザクションによって変更されないようにするため共有ロックを実行しません。また、他のトランザクションによって排他ロックが設定されていても、ロックされたデータの現在のトランザクションによる読み取りはブロックされません。 ダーティ リードを許可するとコンカレンシーが高まりますが、他のトランザクションによってロールバックされているデータ変更を読み取る可能性があります。 この結果、トランザクションでエラーが発生したり、コミットされていないデータがユーザーに提示されたり、レコードが重複表示されたりまったく表示されなかったりする場合があります。  
  
READUNCOMMITTED ヒントと NOLOCK ヒントはデータのロックにのみ適用されます。 READUNCOMMITTED ヒントおよび NOLOCK ヒントを含むクエリを含め、すべてのクエリは、コンパイル中と実行中にスキーマ安定度 (Sch-S) ロックを取得します。 このため、同時実行トランザクションがテーブルの Sch-M (スキーマ修正) ロックを保持している場合、クエリはブロックされます。 たとえば、データ定義言語 (DDL) 操作では、テーブルのスキーマ情報を変更する前にスキーマ修正 (Sch-M) ロックを取得します。 READUNCOMMITTED ヒントまたは NOLOCK ヒントを指定して実行しているクエリを含め、すべての同時実行クエリは、スキーマ安定度 (Sch-S) ロックを取得しようとするとブロックされます。 一方、スキーマ安定度 (Sch-S) ロックを保持するクエリによって、スキーマ修正 (Sch-M) ロックを取得しようとする同時実行トランザクションはブロックされます。  
  
READUNCOMMITTED および NOLOCK は、挿入、更新、削除の各操作によって変更されるテーブルに対しては指定できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーは、UPDATE ステートメントまたは DELETE ステートメントの対象テーブルに適用する FROM 句内の READUNCOMMITTED ヒントおよび NOLOCK ヒントを無視します。  
  
> [!NOTE]  
> FROM 句を UPDATE または DELETE ステートメントの対象テーブルに適用する場合、この句での READUNCOMMITTED ヒントと NOLOCK ヒントの使用は、将来のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされなくなる予定です。 新しい開発作業ではこのコンテキストでのヒントの使用を避け、現在このヒントを使用しているアプリケーションは変更を検討してください。  
  
次のいずれかを使用することによって、ロックの競合を最小限に抑えながら、コミットされていないデータ変更のダーティ リードからトランザクションを保護することができます。  
-   READ COMMITTED 分離レベル。READ_COMMITTED_SNAPSHOT データベース オプションを ON に設定します。  
-   SNAPSHOT 分離レベル。  
  
分離レベルについての詳細については、「[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
> READUNCOMMITTED が指定されているときにエラー メッセージ 601 が表示された場合は、デッドロック エラー (1205) を解決するときと同じように解決し、ステートメントを再実行してください。  
  
REPEATABLEREAD  
REPEATABLE READ 分離レベルで実行しているトランザクションと同じロック セマンティクスでスキャンを実行することを指定します。 分離レベルについての詳細については、「[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)」を参照してください。  
  
ROWLOCK  
通常取得されるページ ロックまたはテーブル ロックの代わりに、行ロックを取得することを指定します。 SNAPSHOT 分離レベルで実行中のトランザクションにおいてこのオプションを指定しても、UPDLOCK や HOLDLOCK など、ロックが必要な他のテーブル ヒントと組み合わせて指定しない限り、行ロックは取得されません。  
  
SERIALIZABLE  
HOLDLOCK に相当します。 共有ロックがより制限的になります。テーブルまたはデータ ページが不要になったときに、トランザクションが完了しているかどうかにかかわらず共有ロックが解除されるのではなく、共有ロックはトランザクションが完了するまで保持されます。 SERIALIZABLE 分離レベルで実行しているトランザクションと同じセマンティクスで、スキャンが実行されます。 分離レベルについての詳細については、「[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)」を参照してください。  
  
SNAPSHOT  
**適用対象**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降。 
  
メモリ最適化されたテーブルは、SNAPSHOT 分離でアクセスされます。 SNAPSHOT は、メモリ最適化されたテーブルだけで使用できまます (ディスク ベースのテーブルでは使用できません)。 詳細については、「[メモリ最適化テーブルの概要](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md)」を参照してください。  
  
```sql 
SELECT * FROM dbo.Customers AS c   
WITH (SNAPSHOT)   
LEFT JOIN dbo.[Order History] AS oh   
    ON c.customer_id=oh.customer_id;  
```  
  
SPATIAL_WINDOW_MAX_CELLS = *integer*  
**適用対象**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降。  
geometry オブジェクトや geography オブジェクトのテセレーションに使用するセルの最大数を指定します。 *数*は、1 から 8192 の範囲の値です。  
  
このオプションを使用すると、プライマリとセカンダリのフィルターの実行時間の間のトレードオフを調整することによって、クエリの実行時間を微調整できます。 値を大きくすると、セカンダリ フィルターの実行時間が短縮されますが、プライマリ フィルターの実行時間が増加します。値を小さくすると、プライマリ フィルターの実行時間が短縮されますが、セカンダリ フィルターの実行時間が増加します。 密度の高い空間データの場合は、大きい値を指定して、プライマリ フィルターでより適切な近似値を提供し、セカンダリ フィルターの実行時間を減少させることで、実行時間を短縮させます。 密度の低いデータでは、小さい値を指定して、プライマリ フィルターの実行時間を短縮させます。  
  
 このオプションは、手動と自動の両方のグリッド テセレーションに使用できます。  
  
TABLOCK  
取得したロックがテーブル レベルで適用されることを指定します。 取得されるロックの種類は、実行されるステートメントによって異なります。 たとえば、SELECT ステートメントを実行すると、共有ロックが取得されます。 TABLOCK を指定することで、行レベルまたはページ レベルではなくテーブル全体に共有ロックが適用されます。 HOLDLOCK も指定してある場合は、テーブル ロックがトランザクション終了まで保持されます。  
  
INSERT INTO \<target_table> SELECT \<columns> FROM \<source_table> ステートメントを使用してデータをヒープにインポートするときに、対象テーブルに対して TABLOCK ヒントを指定すると、そのステートメントに対してログ記録とロックの最適化を有効にすることができます。 データベース復旧モデルが単純復旧モデルまたは一括ログ復旧モデルに設定されている必要もあります。 詳細については、「[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)」を参照してください。  
  
テーブルにデータをインポートするため、[OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) 一括行セット プロバイダーで TABLOCK を使用すると、対象テーブルへのデータ読み込みを、ログ記録とロックを最適化して、複数のクライアントで同時に行うことができます。 詳細については、「[一括インポートで最小ログ記録を行うための前提条件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)」次を参照してください。  
  
TABLOCKX  
テーブルに排他ロックを使用することを指定します。  
  
UPDLOCK  
更新ロックを使用することと、これをトランザクション終了まで保持することを指定します。 UPDLOCK を使用すると、行レベルまたはページ レベルの読み取り操作のみに更新ロックが適用されます。 UPDLOCK を TABLOCK と組み合わせたり、なんらかの理由でテーブル レベルのロックが使用されたりすると、代わりに排他 (X) ロックが取得されます。  
  
UPDLOCK を指定すると、READCOMMITTED および READCOMMITTEDLOCK 分離レベル ヒントが無視されます。 たとえば、セッションの分離レベルを SERIALIZABLE に設定し、クエリで (UPDLOCK, READCOMMITTED) を指定すると、READCOMMITTED ヒントは無視され、トランザクションは SERIALIZABLE 分離レベルを使用して実行されます。  
  
XLOCK  
排他ロックを使用することと、これをトランザクション終了まで保持することを指定します。 ROWLOCK、PAGLOCK、または TABLOCK と組み合わせて指定すると、排他ロックは適切な粒度レベルに適用されます。  
  
## <a name="remarks"></a>Remarks  
テーブルがクエリ プランによってアクセスされているのではない場合、テーブル ヒントは無視されます。 これは、オプティマイザーがテーブルにまったくアクセスしないことを選択した結果であるか、またはインデックス付きビューが代わりにアクセスされるためである可能性があります。 後者の場合、OPTION (EXPAND VIEWS) クエリ ヒントを使用することで、インデックス付きビューへのアクセスを防ぐことができます。  
  
すべてのロック ヒントが、クエリ プランによってアクセスされているすべてのテーブルおよびビュー (ビューで参照されているテーブルおよびビューを含む) に反映されます。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、対応するロックの一貫性チェックを実行します。  
  
行レベルのロックを取得するロック ヒント ROWLOCK、UPDLOCK、および XLOCK では、実際のデータ行ではなくインデックス キーに対してロックが実行される場合があります。 たとえば、テーブルに非クラスター化インデックスがあり、ロック ヒントを使用する SELECT ステートメントがカバーするインデックスによって処理される場合、ベース テーブルのデータ行ではなく、カバーするインデックスのインデックス キーに対してロックが取得されます。  
  
テーブルに計算列があり、その計算列が、別のテーブル内の列にアクセスする式や関数によって計算される場合、テーブル ヒントがそのテーブル上で使用されることや、反映されることはありません。 たとえば、クエリ内のテーブルに NOLOCK テーブル ヒントが指定されているものとします。 このテーブルには、別のテーブル内の列にアクセスする式と関数の組み合わせで計算される、計算列があります。 式と関数で参照されるテーブルが、アクセスされるときに NOLOCK テーブル ヒントを使用することはありません。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、FROM 句内の各テーブルに対して、次の各グループの複数のテーブル ヒントが許可されません。  
-   粒度ヒント: PAGLOCK、NOLOCK、READCOMMITTEDLOCK、ROWLOCK、TABLOCK、または TABLOCKX。  
-   分離レベル ヒント: HOLDLOCK、NOLOCK、READCOMMITTED、REPEATABLEREAD、SERIALIZABLE。  
  
## <a name="filtered-index-hints"></a>フィルター選択されたインデックス ヒント  
 フィルター選択されたインデックスをテーブル ヒントとして使用できますが、クエリで選択する行のすべてがカバーされているわけではない場合、クエリ オプティマイザーからエラー 8622 が返されます。 フィルター選択されたインデックス ヒントが無効になる例を次に示します。 この例では、フィルター選択されたインデックス `FIBillOfMaterialsWithComponentID` を作成し、SELECT ステートメントのインデックス ヒントとして使用します。 フィルター選択されたインデックスの述語には、ComponentID が 533、324、および 753 のデータ行が含まれています。 クエリ述語にも ComponentID が 533、324、および 753 のデータ行が含まれていますが、フィルター選択されたインデックスには存在しない ComponentID 855 および 924 も結果セットに含めるよう拡張されています。 したがって、クエリ オプティマイザーはフィルター選択されたインデックス ヒントを使用できず、エラー 8622 が生成されます。 詳細については、「 [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md)」を参照してください。  
  
```sql  
IF EXISTS (SELECT name FROM sys.indexes  
    WHERE name = N'FIBillOfMaterialsWithComponentID'   
    AND object_id = OBJECT_ID(N'Production.BillOfMaterials'))  
DROP INDEX FIBillOfMaterialsWithComponentID  
    ON Production.BillOfMaterials;  
GO  
CREATE NONCLUSTERED INDEX "FIBillOfMaterialsWithComponentID"  
    ON Production.BillOfMaterials (ComponentID, StartDate, EndDate)  
    WHERE ComponentID IN (533, 324, 753);  
GO  
SELECT StartDate, ComponentID FROM Production.BillOfMaterials  
    WITH( INDEX (FIBillOfMaterialsWithComponentID) )  
    WHERE ComponentID in (533, 324, 753, 855, 924);  
GO  
```  
  
フィルター選択されたインデックスに必要な値が SET オプションにない場合、クエリ オプティマイザーはインデックス ヒントを無視します。 詳細については、「[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)」を参照してください。  
  
## <a name="using-noexpand"></a>NOEXPAND の使用  
NOEXPAND は*インデックス付きビュー*にのみ適用できます。 インデックス付きビューとは、一意なクラスター化インデックスが作成されているビューを示します。 インデックス付きビューおよびベース テーブルの両方に存在する列への参照がクエリに含まれていて、クエリ オプティマイザーがクエリの実行にインデックス付きビューを使用する方が最適であると判断した場合、クエリ オプティマイザーはビューのインデックスを利用します。 この機能は、*インデックス付きビューのマッチング*と呼ばれます。 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1 より前のバージョンでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特定のエディションでのみ、クエリ オプティマイザーではインデックス付きビューが自動的に使用されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
ただし、オプティマイザーで、インデックス付きビューのマッチングを検討したり、NOEXPAND ヒントで参照されるインデックス付きビューを使用したりするには、以下の SET オプションを ON に設定する必要があります。  
 
> [!NOTE]  
> [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、NOEXPAND ヒントを指定しなくても、自動的なインデックス付きビューの使用がサポートされます。
  
||||  
|-|-|-|  
|ANSI_NULLS|ANSI_WARNINGS|CONCAT_NULL_YIELDS_NULL|  
|ANSI_PADDING|ARITHABORT<sup>1</sup>|QUOTED_IDENTIFIER|  
  
 <sup>1</sup> ARITHABORT は、ANSI_WARNINGS が ON に設定されている場合は、暗黙的に ON に設定されます。 したがって、この設定を手動で調整する必要はありません。  
  
 また、NUMERIC_ROUNDABORT オプションは OFF に設定する必要があります。  
  
 オプティマイザーがインデックス付きビューのインデックスを使用するように強制するには、NOEXPAND オプションを指定します。 このヒントは、ビューがクエリ内でも指定されている場合にのみ使用できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、FROM 句で直接ビューを指定していないクエリで、特定のインデックス付きビューが使用されるようにするヒントは用意されていません。しかし、クエリ オプティマイザーでは、インデックス付きビューがクエリで直接参照されていなくても、その使用が検討されます。 NOEXPAND テーブル ヒントを使用すると、SQL Server はインデックス付きビューに対してのみ自動的に統計を作成します。 このヒントを省略すると、統計を手動で作成することでは解決できない、統計がないことに関する実行プランの警告につながる場合があります。 クエリの最適化中、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、クエリがビューを直接参照し、NOEXPAND ヒントが使用されるときに、自動的または手動で作成された統計情報の表示を使用します。    
  
## <a name="using-a-table-hint-as-a-query-hint"></a>クエリ ヒントとしてのテーブル ヒントの使用  
 OPTION (TABLE HINT) 句を使用すると、*テーブル ヒント*をクエリ ヒントとして指定することもできます。 [プラン ガイド](../../relational-databases/performance/plan-guides.md)のコンテキスト内でのみ、テーブル ヒントをクエリ ヒントとして使用することをお勧めします。 アドホック クエリに対しては、これらのヒントをテーブル ヒントとしてのみ指定します。 詳細については、「[クエリ ヒント &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 KEEPIDENTITY、IGNORE_CONSTRAINTS、IGNORE_TRIGGERS の各ヒントには、テーブルに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-using-the-tablock-hint-to-specify-a-locking-method"></a>A. TABLOCK ヒントを使用してロック手法を指定する  
 次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベース内の `Production.Product` テーブルに対して共有ロックを使用することと、このロックを UPDATE ステートメントの終了まで保持することを指定します。  
  
```sql  
UPDATE Production.Product  
WITH (TABLOCK)  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE 'BK-%';  
GO  
```  
  
### <a name="b-using-the-forceseek-hint-to-specify-an-index-seek-operation"></a>B. FORCESEEK ヒントを使用したインデックスのシーク操作の指定  
 次の例では、インデックスを指定せずに FORCESEEK ヒントを使用して、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベース内の `Sales.SalesOrderDetail` テーブルに対するインデックスのシーク操作を実行するようにクエリ オプティマイザーを設定します。  
  
```sql
SELECT *  
FROM Sales.SalesOrderHeader AS h  
INNER JOIN Sales.SalesOrderDetail AS d WITH (FORCESEEK)  
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);  
GO  
  
```  
  
 次の例では、インデックスを指定して FORCESEEK ヒントを使用して、指定したインデックスおよびインデックス列に対してインデックスのシーク操作を実行するようにクエリ オプティマイザーを設定します。  
  
```sql  
SELECT h.SalesOrderID, h.TotalDue, d.OrderQty  
FROM Sales.SalesOrderHeader AS h  
    INNER JOIN Sales.SalesOrderDetail AS d   
    WITH (FORCESEEK (PK_SalesOrderDetail_SalesOrderID_SalesOrderDetailID (SalesOrderID)))   
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);   
GO  
  
```  
  
### <a name="c-using-the-forcescan-hint-to-specify-an-index-scan-operation"></a>C. FORCESCAN ヒントを使用してインデックスのスキャン操作を指定する  
 次の例では、FORCESCAN ヒントを使用して、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベース内の `Sales.SalesOrderDetail` テーブルに対するスキャン操作を実行するようにクエリ オプティマイザーを設定します。  
  
```sql  
SELECT h.SalesOrderID, h.TotalDue, d.OrderQty  
FROM Sales.SalesOrderHeader AS h  
    INNER JOIN Sales.SalesOrderDetail AS d   
    WITH (FORCESCAN)   
    ON h.SalesOrderID = d.SalesOrderID   
WHERE h.TotalDue > 100  
AND (d.OrderQty > 5 OR d.LineTotal < 1000.00);  
```  
  
## <a name="see-also"></a>参照  
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Hints &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql.md)   
 [クエリ ヒント &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)  
  
  
