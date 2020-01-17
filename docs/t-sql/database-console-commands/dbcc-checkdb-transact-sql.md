---
title: DBCC CHECKDB (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKDB_TSQL
- DBCC_CHECKDB_TSQL
- DBCC CHECKDB
- CHECKDB
dev_langs:
- TSQL
helpviewer_keywords:
- CHECKDB [DBCC statement]
- database objects [SQL Server], checking
- counting pages
- per-index row counts
- per-table row counts
- DBCC CHECKDB statement
- per-table page counts
- allocation checks
- integrity [SQL Server], database objects
- per-index page counts
- counting rows
- table integrity checks [SQL Server]
- row count accuracy [SQL Server]
- negative counts
- checking database objects
- page count accuracy [SQL Server]
ms.assetid: 2c506167-0b69-49f7-9282-241e411910df
author: pmasl
ms.author: umajay
ms.openlocfilehash: 54b6353b789f837f45759c34b0dbbbd591cf5dbf
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982422"
---
# <a name="dbcc-checkdb-transact-sql"></a>DBCC CHECKDB (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

次の操作を実行し、指定したデータベース内のすべてのオブジェクトの論理的および物理的な整合性をチェックします。    
    
-   データベースに対して [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md) を実行。    
-   データベース内にあるすべてのテーブルとビューに対して [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md) を実行。    
-   データベースに対して [DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md) を実行。    
-   データベース内にあるすべてのインデックス付きビューの内容を検証。    
-   FILESTREAM を使用して **varbinary(max)** データをファイル システムに格納する場合のテーブルのメタデータとファイル システムのディレクトリおよびファイルの間のリンクレベルの一貫性を検証。    
-   データベースの [!INCLUDE[ssSB](../../includes/sssb-md.md)] データを検証。    
    
DBCC CHECKALLOC、DBCC CHECKTABLE、または DBCC CHECKCATALOG コマンドは、DBCC CHECKDB と別に実行する必要はありません。 これらのコマンドで実行されるチェックに関する詳細については、各コマンドの説明を参照してください。    
 
> [!NOTE]
> DBCC CHECKDB は、メモリ最適化テーブルを含むデータベースでサポートされていますが、検証はディスク ベース テーブルでのみ行われます。 ただし、データベースのバックアップおよび復旧の一環として、メモリ最適化ファイル グループ内のファイルに対して CHECKSUM 検証が実行されます。    
>     
> DBCC 修復オプションはメモリ最適化テーブルに使用できないため、データベースを定期的にバックアップし、バックアップをテストする必要があります。 メモリ最適化テーブルでデータ整合性の問題が発生した場合は、最新の既知の良好なバックアップから復元する必要があります。    

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>構文    
    
```    
DBCC CHECKDB     
    [ ( database_name | database_id | 0    
        [ , NOINDEX     
        | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]    
    ) ]    
    [ WITH     
        {    
            [ ALL_ERRORMSGS ]    
            [ , EXTENDED_LOGICAL_CHECKS ]     
            [ , NO_INFOMSGS ]    
            [ , TABLOCK ]    
            [ , ESTIMATEONLY ]    
            [ , { PHYSICAL_ONLY | DATA_PURITY } ]    
            [ , MAXDOP  = number_of_processors ]    
        }    
    ]    
]    
```    
    
## <a name="arguments"></a>引数    
 *database_name* | *database_id* | 0  
 整合性チェックを実行するデータベースの名前または ID です。 値を指定しないか 0 を指定した場合は、現在のデータベースが使用されます。 データベース名は、[識別子](../../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。  
    
NOINDEX  
 ユーザー テーブルの非クラスター化インデックスの集中チェックを実行しないように指定します。 これにより、全体の実行時間が短縮されます。 整合性チェックは、常にシステム テーブルのインデックスに対して実行されるため、NOINDEX はシステム テーブルに対しては無効です。  
    
REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD  
 検出されたエラーを DBCC CHECKDB が修復するように指定します。 REPAIR オプションは、最後の手段としてのみ使用してください。 修復オプションを使用するには、指定するデータベースがシングル ユーザー モードになっている必要があります。以下の修復オプションを使用できます。  
    
REPAIR_ALLOW_DATA_LOSS  
 報告されたすべてのエラーの修復を試みます。 修復を実行すると、データが失われることがあります。  
    
> [!WARNING]
> REPAIR_ALLOW_DATA_LOSS オプションは、サポートされている機能ですが、データベースを物理的に一貫性のある状態にするためには、必ずしも最適なオプションではない場合があります。 成功した場合、REPAIR_ALLOW_DATA_LOSS オプションによりいくつかデータが失われることがあります。 実際には、ユーザーが最後の既知の良好なバックアップからデータベースを復元する場合よりも、失われるデータが多い場合があります。 
>
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、DBCC CHECKDB によって報告されたエラーから回復する主要な方法として、ユーザーが最後の既知の良好なバックアップから復元することが常に推奨されています。 REPAIR_ALLOW_DATA_LOSS オプションは、既知の適切なバックアップから復元する代替手段ではありません。 これは、緊急時の "最後の手段" のオプションであり、バックアップからの復元ができない場合にのみ使用することをお勧めします。    
>     
> REPAIR_ALLOW_DATA_LOSS オプションを使用してのみ修復できる特定のエラーには、エラーを消去するための行、ページ、または一連のページの割り当ての解除が含まれます。 割り当てが解除されたデータは、ユーザーによるアクセスまたは復旧が不可能になり、割り当てが解除されたデータの内容は正確に特定できません。 このため、任意の行またはページの割り当てが解除されると、この修復操作の一部として外部キー制約がチェックまたは保守されないため、参照整合性が正確でない可能性があります。 ユーザーは、REPAIR_ALLOW_DATA_LOSS オプションを使用した後で、(DBCC CHECKCONSTRAINTS を使用して)、データベースの参照整合性を調べる必要があります。    
>     
> 修復を実行する前に、このデータベースに属しているファイルの物理コピーを作成します。 これには、プライマリ データ ファイル (.mdf)、すべてのセカンダリ データ ファイル (.ndf)、すべてのトランザクション ログ ファイル (.ldf)、およびフルテキスト カタログ、ファイル ストリームのフォルダー、メモリ最適化データなどを含むデータベースを形成する他のコンテナーが含まれます。    
>     
> 修復を実行する前に、データベースの状態を EMERGENCY モードに変更し、クリティカルなテーブルから可能な限り多くの情報を抽出してデータを保存することを検討してください。    
    
REPAIR_FAST  
 旧バージョンとの互換性のためにのみ、構文が用意されています。 修復操作は実行されません。  
    
REPAIR_REBUILD  
 データ損失の可能性がない修復を実行します。 これには、非クラスター化インデックスの存在しない行の修復など時間のかからない修復操作と、インデックスの再構築など時間のかかる修復操作が含まれます。  
 この引数では、FILESTREAM データに関係するエラーは修復されません。  
    
> [!IMPORTANT] 
> 任意の REPAIR オプションが指定された DBCC CHECKDB は、完全にログに記録されて回復可能なため、[!INCLUDE[msCoName](../../includes/msconame-md.md)] は常にユーザーがトランザクション内で REPAIR オプションを使用して CHECKDB を使用することをお勧めします (コマンドを実行する前に、BEGIN TRANSACTION を実行します)。これにより、ユーザーが操作の結果を受け入れるか確認することができます。 ユーザーは、COMMIT TRANSACTION を実行して、修復操作によってなされたすべての作業をコミットできます。 ユーザーが操作の結果を受け入れない場合は、ROLLBACK TRANSACTION を実行して、修復操作の結果を元に戻すことができます。    
>     
> エラーの修復では、バックアップから復元することをお勧めします。 修復操作では、テーブルまたはテーブル間に制約があっても考慮されません。 指定したテーブルに 1 つでも関連する制約がある場合は、修復操作の後に DBCC CHECKCONSTRAINTS を実行することをお勧めします。 REPAIR を使用する必要がある場合は、修復オプションを指定せずに DBCC CHECKDB を実行して、使用する修復レベルを確認してください。 REPAIR_ALLOW_DATA_LOSS レベルを使用する場合は、このオプションを指定して DBCC CHECKDB を実行する前に、データベースをバックアップすることをお勧めします。    
    
ALL_ERRORMSGS  
 オブジェクトごとに、報告されているすべてのエラーを表示します。 既定では、すべてのエラー メッセージが表示されます。 このオプションを指定しても省略しても影響はありません。 [tempdb データベース](../../relational-databases/databases/tempdb-database.md)から生成されるメッセージを除き、エラー メッセージは、オブジェクト ID を基準として並べ替えられます。     

EXTENDED_LOGICAL_CHECKS  
 互換性レベルが 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) 以上の場合、インデックス付きビュー、XML インデックス、空間インデックス (存在する場合) について、論理的な一貫性をチェックします。  
 詳細については、このトピックの「[解説](#remarks)」の「*インデックスに対する論理的な一貫性チェックの実行*」を参照してください。  
    
NO_INFOMSGS  
 すべての情報メッセージを表示しないようにします。  
    
TABLOCK  
 DBCC CHECKDB が、内部データベースのスナップショットを使用せずに、ロックを取得します。 これにはデータベースの短期の排他 (X) ロックも含まれます。 TABLOCK の作用によって負荷の高いデータベースでも DBCC CHECKDB の実行速度が速くなりますが、DBCC CHECKDB の実行中はデータベースでのコンカレンシーが低下します。  
    
> [!IMPORTANT] 
> TABLOCK では実行されるチェックが制限されます。DBCC CHECKCATALOG はデータベースに対して実行されず、[!INCLUDE[ssSB](../../includes/sssb-md.md)] データは検証されません。
    
ESTIMATEONLY  
 必要な他のオプションをすべて指定した状態で、DBCC CHECKDB の実行時に必要となる tempdb 領域の予測サイズを表示します。 実際のデータベースのチェックは行われません。  
    
PHYSICAL_ONLY  
 チェック内容を、ページとレコード ヘッダーの物理構造の整合性、およびデータベースの割り当ての一貫性に限定します。 このチェックは、データベースの物理的一貫性に関する低オーバーヘッド チェックを提供するように設計されていますが、ユーザーのデータが損傷する可能性のある破損ページ、チェックサム エラー、一般的なハードウェア障害も検出できます。  
 完全な DBCC CHECKDB を実行すると、完了するまでに以前のバージョンよりはるかに時間がかかることがあります。 この動作が発生する原因は、次のとおりです。  
 -   論理チェックの対象範囲が広がった。  
 -   チェック対象の、基になる構造の一部が複雑になった。  
 -   新機能を含めるために多数の新しいチェックが導入された。  
 したがって、大規模なデータベースでは、PHYSICAL_ONLY オプションを使用すると DBCC CHECKDB の実行時間が大幅に短縮されることがあるため、実稼働システムで頻繁に使用する場合はこのオプションを使用することをお勧めします。 ただし、完全な DBCC CHECKDB を定期的に実行することもお勧めします。 実行する頻度は、それぞれの業務環境や運用環境に固有の要因によって異なります。    
この引数を指定した場合は常に NO_INFOMSGS も暗黙的に指定されるため、修復オプションを同時指定することはできません。  
    
> [!WARNING] 
> PHYSICAL_ONLY を指定すると、DBCC CHECKDB で FILESTREAM データのチェックがすべてスキップされるようになります。
    
DATA_PURITY  
 DBCC CHECKDB が、データベース内の、値が無効または範囲外の列をチェックします。 たとえば、DBCC CHECKDB は、**datetime** 型の許容範囲外となる日時の値を含む列や、小数点以下桁数または有効桁数の値が有効ではない **decimal** 型や概数型の列を検出します。  
 列の値の整合性チェックは既定で有効になっているため、DATA_PURITY オプションを指定する必要はありません。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からアップグレードしたデータベースの場合は、列の値のチェックは既定では有効になっていないため、データベースで DBCC CHECKDB WITH DATA_PURITY を実行します。 エラーなく実行されると、その後、DBCC CHECKDB は既定で列の値の整合性をチェックします。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からのデータベースのアップグレードによる CHECKDB への影響の詳細については、後の「解説」を参照してください。  
    
> [!WARNING]
> PHYSICAL_ONLY を指定した場合は、列の整合性チェックは行われません。
    
 DBCC 修復オプションを使用して、このオプションによって報告された検証エラーを修正することはできません。 これらのエラーを手動で修正する方法の詳細については、次のサポート技術情報の資料 923247 を参照してください。[SQL Server 2005 以降のバージョンでの DBCC エラー 2570 のトラブルシューティング](https://support.microsoft.com/kb/923247)。  
    
 MAXDOP  
 **適用対象**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 以降)。  
    
 ステートメントの **sp_configure** の **max degree of parallelism** 構成オプションをオーバーライドします。 MAXDOP では、sp_configure で構成されている値を超えることができます。 MAXDOP の値がリソース ガバナーで構成されている値を超える場合は、「[ALTER WORKLOAD GROUP](../../t-sql/statements/alter-workload-group-transact-sql.md)」で説明されているように、[!INCLUDE[ssDEnoversion](../../includes/ssDEnoversion_md.md)]でリソース ガバナーの MAXDOP 値が使用されます。 MAXDOP クエリ ヒントを使用している場合は、max degree of parallelism 構成オプションで使用されるすべての意味ルールを適用できます。 詳細については、「 [max degree of parallelism サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)」を参照してください。  
 
> [!WARNING] 
> MAXDOP が 0 に設定されている場合、SQL Server では使用する最大限の並列処理が選択されます。    

## <a name="remarks"></a>Remarks    
DBCC CHECKDB は、無効なインデックスについては検査しません。 無効なインデックスの詳細については、「[インデックスと制約の無効化](../../relational-databases/indexes/disable-indexes-and-constraints.md)」を参照してください。    

ユーザー定義型がバイト順としてマークされている場合、シリアル化されたユーザー定義型は 1 つだけ存在する必要があります。 シリアル化されたバイト順のユーザー定義型が一貫して存在していない場合、DBCC CHECKDB の実行中にエラー 2537 が発生します。 詳細については、「[ユーザー定義型の要件](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-requirements.md)」を参照してください。    

[Resource データベース](../../relational-databases/databases/resource-database.md)はシングル ユーザー モードでしか修正できないため、このデータベースに対して DBCC CHECKDB コマンドを直接実行することはできません。 ただし、DBCC CHECKDB を [master データベース](../../relational-databases/databases/master-database.md)に対して実行すると、内部的に次の CHECKDB が Resource データベースに対して実行されます。 このため、DBCC CHECKDB が追加の結果を返す場合があります。 このコマンドでは、オプションが設定されていないか、`PHYSICAL_ONLY` または `ESTIMATEONLY` オプションが設定されている場合に、追加の結果セットが返されます。    

[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2 以降では、DBCC CHECKDB を実行しても、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスのプラン キャッシュは消去**されません**。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2 より前のバージョンでは、DBCC CHECKDB を実行すると、プラン キャッシュが消去されます。 プラン キャッシュが消去されると、後続のすべての実行プランが再コンパイルされ、場合によっては、クエリ パフォーマンスが一時的に急激に低下する場合があります。 
    
## <a name="performing-logical-consistency-checks-on-indexes"></a>インデックスに対する論理的な一貫性チェックの実行    
インデックスに対する論理的な一貫性チェックは、データベースの互換性レベルによって次のように異なります。
-   互換性レベルが 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) 以上の場合:    
-   `NOINDEX` が指定されていない場合、DBCC CHECKDB は、1 つのテーブルとそのすべての非クラスター化インデックスについて、物理的な整合性チェックと論理的な整合性チェックの両方を実行します。 ただし、XML インデックス、空間インデックス、およびインデックス付きビューでは、既定で物理的な一貫性のみがチェックされます。
-   `WITH EXTENDED_LOGICAL_CHECKS` が指定されている場合、インデックス付きビュー、XML インデックス、および空間インデックス (存在する場合) に対して論理チェックが実行されます。 既定では、論理的な一貫性のチェック前に物理的な一貫性がチェックされます。 `NOINDEX` も指定されている場合は、論理チェックのみが実行されます。
    
この論理的な一貫性のチェックでは、インデックス オブジェクトの内部インデックス テーブルが参照先のユーザー テーブルと照合されます。 行の不整合を検出するために、内部テーブルとユーザー テーブルの完全な積集合を実行する内部クエリが作成されます。 このクエリを実行するとパフォーマンスに多大な影響を及ぼす可能性があり、その進行状況は追跡できません。 したがって、物理的な破損とは無関係のインデックスの問題があると考えられる場合、またはページ レベルのチェックサムがオフになっており、列レベルのハードウェアの破損が考えられる場合にのみ、`WITH EXTENDED_LOGICAL_CHECKS` を指定することをお勧めします。
-   インデックスがフィルター選択されたインデックスである場合、DBCC CHECKDB は一貫性チェックを実行して、インデックス エントリがフィルター述語に適合していることを確認します。
-   互換性レベルが 90 以下で `NOINDEX` が指定されていない場合、DBCC CHECKDB は、1 つのテーブルまたはインデックス付きビューと、そのすべての非クラスター化インデックスおよび XML インデックスについて、物理的な整合性チェックと論理的な整合性チェックの両方を実行します。 空間インデックスはサポートされません。  
- SQL Server 2016 以降では、コストの高い式の評価を避けるため、既定では、保存される計算列、UDT 列、およびフィルター選択されたインデックスへの追加のチェックは実行されません。 この変更により、これらのオブジェクトを含むデータベースに対する CHECKDB の時間が大幅に短縮されます。 ただし、これらのオブジェクトの物理的な整合性チェックは常に実行されます。 `EXTENDED_LOGICAL_CHECKS` オプションが指定されている場合にのみ、既存の論理チェック (インデックス付きビュー、XML インデックス、および空間インデックス) に加え、`EXTENDED_LOGICAL_CHECKS` オプションの一部として式の評価が行われます。   
    
**データベースの互換性レベルを調べるには**
-   [データベースの互換性レベルの表示または変更](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)    
    
## <a name="internal-database-snapshot"></a>内部データベース スナップショット    
DBCC CHECKDB では、チェックの実行に必要なトランザクションの一貫性を得るため、内部データベース スナップショットを使用します。 これにより、コマンド実行時のブロックやコンカレンシーの問題を回避できます。 詳細については、「[データベース スナップショットのスパース ファイルのサイズを表示する方法 &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)」および「[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)」の「DBCC 内部データベース スナップショットの使用」セクションを参照してください。 スナップショットを作成できない場合や TABLOCK が指定されていない場合、DBCC CHECKDB はロックを取得して必要な一貫性を実現します。 この場合、割り当てのチェックを行うための排他データベース ロックと、テーブルのチェックを行うための共有テーブル ロックが必要です。
内部データベース スナップショットを作成できない場合、master に対して DBCC CHECKDB を実行すると失敗します。
tempdb に対して DBCC CHECKDB を実行すると、割り当てまたはカタログのチェックは実行されず、テーブルのチェックを実行するには共有テーブル ロックを取得する必要があります。 これは、パフォーマンス上の理由から、データベースのスナップショットが tempdb では利用できないためです。 つまり、必要なトランザクションの一貫性を実現できないためです。
Microsoft SQL Server 2012 または SQL Server の以前のバージョンでは、ReFS でフォーマットされたボリュームにファイルがあるデータベースに対して DBCC CHECKDB コマンドを実行すると、エラー メッセージが表示される場合があります。 詳細については、サポート技術情報の資料 2974455「[DBCC CHECKDB behavior when the SQL Server database is located on an ReFS volume](https://support.microsoft.com/kb/2974455)」 (SQL Server データベースが ReFS ボリュームに配置されている場合の DBCC CHECKDB の動作) を参照してください。    
    
## <a name="checking-and-repairing-filestream-data"></a>FILESTREAM データのチェックと修復    
データベースとテーブルに対して FILESTREAM が有効になっている場合、**varbinary(max)** バイナリ ラージ オブジェクト (BLOB) をファイル システムに格納することもできます。 BLOB をファイル システムに格納するデータベースに対して DBCC CHECKDB を使用する場合は、DBCC によって、ファイル システムとデータベースの間のリンクレベルの一貫性がチェックされます。
たとえば、テーブルに FILESTREAM 属性を使用する **varbinary(max)** 列が含まれている場合、DBCC CHECKDB は、ファイル システムのディレクトリおよびファイルと、テーブルの行、列、および列の値とが一対一でマップされていることをチェックします。 REPAIR_ALLOW_DATA_LOSS オプションを指定すると、DBCC CHECKDB で破損を修復できます。 FILESTREAM の破損を修復するために、DBCC はファイル システム データが欠落しているテーブル行を削除します。
    
## <a name="best-practices"></a>ベスト プラクティス    
運用システムで頻繁に使用する場合は、`PHYSICAL_ONLY` オプションを使用することをお勧めします。 PHYSICAL_ONLY を使用すると、大規模なデータベースでの DBCC CHECKDB の実行時間を大幅に短縮できます。 また、定期的に、オプションを指定せずに DBCC CHECKDB を実行することもお勧めします。 実行する頻度は、個々の業務とその運用環境によって変わります。
    
## <a name="checking-objects-in-parallel"></a>オブジェクトの並列チェック    
既定では、DBCC CHECKDB はオブジェクトの並列チェックを実行します。 並列処理の次数は、クエリ プロセッサによって自動的に決定されます。 並列処理の次数の最大値は、並列クエリと同様に構成します。 DBCC チェックに利用できるプロセッサの最大数を制限するには、[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を使用します。 詳細については、「 [max degree of parallelism サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)」を参照してください。 並列チェックはトレース フラグ 2528 を使用して無効にできます。 詳細については、「[トレース フラグ &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)」を参照してください。
    
> [!NOTE]
> この機能は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 詳細については、「[SQL Server 2016 の各エディションでサポートされる機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」の「RDBMS の管理の容易性」で並列整合性チェックを確認してください。    
    
## <a name="understanding-dbcc-error-messages"></a>DBCC エラー メッセージについて    
DBCC CHECKDB コマンドの終了後、メッセージが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに書き込まれます。 DBCC コマンドが正常に実行された場合、メッセージでは正常に処理されたこととコマンドの実行時間が示されます。 エラーが発生して DBCC コマンドが完了前に停止した場合、メッセージではコマンドが終了したことと、状態の値、およびコマンド実行時間が示されます。 次の表は、メッセージに含まれる可能性がある状態値の一覧と説明です。
    
|状態|[説明]|    
|-----------|-----------------|    
|0|エラー番号 8930 が発生しました。 このエラーは、メタデータの破損により DBCC コマンドが終了したことを示します。|    
|1|エラー番号 8967 が発生しました。 内部 DBCC エラーがあります。|    
|2|緊急モードのデータベース修復中にエラーが発生しました。|    
|3|このエラーは、メタデータの破損により DBCC コマンドが終了したことを示します。|    
|4|アサートまたはアクセス違反が検出されました。|    
|5|不明なエラーが発生し、DBCC コマンドが終了しました。|    
    
## <a name="error-reporting"></a>[エラー報告]    
DBCC CHECKDB により破損エラーが検出されるたびに、ダンプ ファイル (`SQLDUMP*nnnn*.txt`) が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の LOG ディレクトリに生成されます。 *機能の使用状況*データ収集と*エラー報告*機能が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対して有効になっている場合、ダンプ ファイルは自動的に [!INCLUDE[msCoName](../../includes/msconame-md.md)] に転送されます。 収集されたデータは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能向上のために使用されます。
このダンプ ファイルには、DBCC CHECKDB コマンドの結果と追加の診断出力が含まれます。 アクセスが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントと sysadmin ロールのメンバーに制限されます。 既定では、sysadmin ロールには、Windows の `BUILTIN\Administrators` グループとローカルの管理者のグループのすべてのメンバーが含まれています。 データ収集プロセスが失敗しても、DBCC コマンドは失敗しません。
    
## <a name="resolving-errors"></a>エラーの解決    
DBCC CHECKDB でエラーが報告された場合は、REPAIR を REPAIR オプションのいずれかを指定して実行するのではなく、データベースのバックアップからデータベースを復元することをお勧めします。 バックアップが存在しない場合は、修復を実行することによって報告されたエラーを修正します。 使用する修復オプションは、報告されたエラーの一覧の最後に指定されています。 ただし、REPAIR_ALLOW_DATA_LOSS オプションを使用してエラーを修正する場合は、一部のページ (データ) が削除されることがあります。    

状況によっては、データベースに、列のデータ型に対して有効ではない値や範囲外の値が入力されていることがあります。 DBCC CHECKDB は、すべての列のデータ型について有効ではない列の値を検出します。 したがって、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からアップグレードしたデータベースに対して DATA_PURITY オプションを指定して DBCC CHECKDB を実行すると、以前から存在していた列の値のエラーが検出される場合があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ではこれらのエラーを自動的に修復することはできないため、列の値を手動で更新する必要があります。 CHECKDB でこのようなエラーが検出されると、CHECKDB は警告 (エラー番号 2570) を返し、影響を受ける行を特定してエラーを手動で修正するための情報を示します。    

ユーザー トランザクションを利用して修復を実行できるので、後からユーザーが変更をロールバックすることができます。 修復をロールバックしたときは、データベースにエラーが残っているので、データベースをバックアップから復元する必要があります。 修復が完了したら、データベースをバックアップします。
    
## <a name="resolving-errors-in-database-emergency-mode"></a>データベース緊急モードでのエラーの解決    
[ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) ステートメントによってデータベースが緊急モードに設定されている場合、REPAIR_ALLOW_DATA_LOSS オプションを指定して DBCC CHECKDB を実行すると、データベースに対していくつかの特別な修復を実行できます。 このような修復により、通常は復旧不可能なデータベースを、物理的な一貫性のある状態でオンラインに戻すことができる場合があります。 このような修復は、バックアップからデータベースを復元できない場合にのみ、最終的な手段として使用してください。 データベースを緊急モードに設定すると、データベースは READ_ONLY に設定され、ログ記録は無効になり、アクセスは sysadmin 固定サーバー ロールのメンバーに制限されます。
    
> [!NOTE]
> ユーザー トランザクション内で DBCC CHECKDB コマンドを緊急モードで実行したり、実行後にトランザクションをロールバックすることはできません。    
    
データベースが緊急モードのときに、REPAIR_ALLOW_DATA_LOSS 句を指定して DBCC CHECKDB を実行した場合は、次の処理が行われます。
-   DBCC CHECKDB では、I/O エラーまたはチェックサム エラーが原因でアクセス不可とマークされたページが、エラーが発生しなかった場合と同様に使用されます。 これにより、データベースからのデータ復旧の可能性が高くなります。    
-   DBCC CHECKDB では、標準的なログ ベースの復旧方法により、データベースの復旧が試行されます。    
-   トランザクション ログが壊れているためにデータベース復旧が失敗した場合、トランザクション ログは再構築されます。 ただし、トランザクション ログの再構築の結果、トランザクションの一貫性が失われる場合があります。    
    
> [!WARNING]
> REPAIR_ALLOW_DATA_LOSS オプションは、サポートされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の機能です。 ただし、データベースを物理的に一貫性のある状態にすることが、常に最適なオプションというわけではありません。 成功した場合、REPAIR_ALLOW_DATA_LOSS オプションによりいくつかデータが失われることがあります。 実際には、ユーザーが最後の既知の良好なバックアップからデータベースを復元する場合よりも、失われるデータが多い場合があります。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、DBCC CHECKDB によって報告されたエラーから回復する主要な方法として、ユーザーが最後の既知の良好なバックアップから復元することが常に推奨されています。 REPAIR_ALLOW_DATA_LOSS オプションは、既知の適切なバックアップから復元する代替手段では**ありません**。 これは、緊急時の "最後の手段" のオプションであり、バックアップからの復元ができない場合にのみ使用することをお勧めします。    
>     
>  ログの再構築後、完全な ACID の保証はありません。    
>     
>  ログの再構築後、DBCC CHECKDB が自動的に実行され、物理的な一貫性の問題を報告して修正します。    
>     
>  論理データの一貫性とビジネス ロジックに適用される制約を手動で検証する必要があります。    
>     
>  トランザクション ログのサイズは、既定のサイズのままなので、最近のサイズに手動で調整する必要があります。    
    
DBCC CHECKDB コマンドが正常に終了した場合、データベースでは物理的な一貫性が保たれ、データベースの状態は ONLINE に設定されます。 ただし、データベースにはトランザクション上一貫しない部分が 1 つ以上含まれる可能性があります。 [DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md) コマンドを実行してビジネス ロジックの不備を確認し、直ちにデータベースをバックアップすることをお勧めします。
DBCC CHECKDB コマンドが失敗した場合、データベースを修復することはできません。
    
## <a name="running-dbcc-checkdb-with-repair_allow_data_loss-in-replicated-databases"></a>レプリケートされたデータベースでの、REPAIR_ALLOW_DATA_LOSS を指定した DBCC CHECKDB の実行    
REPAIR_ALLOW_DATA_LOSS オプションを指定して DBCC CHECKDB コマンドを実行すると、レプリケーションで使用されるユーザー データベース (パブリケーション データベースおよびサブスクリプション データベース) とディストリビューション データベースに影響が生じる場合があります。 パブリケーション データベースとサブスクリプション データベースには、パブリッシュされたテーブルとレプリケーション メタデータ テーブルが含まれます。 これらのデータベースでは、次の問題が発生する可能性があります。
-   パブリッシュされたテーブル。 破損したユーザー データを修復するため CHECKDB 処理によって実行されるアクションが、レプリケートされない場合があります。    
-   マージ レプリケーションでは、パブリッシュされたテーブルに対する変更を追跡するために、トリガーを使用します。 CHECKDB 処理で行が挿入、更新、または削除された場合、トリガーは起動しません。このため、変更はレプリケートされません。
-   トランザクション レプリケーションではトランザクション ログを使用して、パブリッシュされたテーブルに対する変更を追跡します。 その後、ログ リーダー エージェントは変更をディストリビューション データベースに移動します。 DBCC 修復の一部は、ログには記録されますが、ログ リーダー エージェントでレプリケートできません。 たとえば、CHECKDB 処理によってデータ ページの割り当てが解除された場合、ログ リーダー エージェントではこの処理が DELETE ステートメントに変換されません。このため、変更はレプリケートされません。
-   レプリケーション メタデータ テーブル。 破損したレプリケーション メタデータ テーブルを修復するため CHECKDB 処理で実行されるアクションでは、レプリケーションの削除と再構成が必要になります。    
    
ユーザー データベースまたはディストリビューション データベースで、REPAIR_ALLOW_DATA_LOSS オプションを指定して DBCC CHECKDB コマンドを実行する必要がある場合は、次の手順に従います。
1.  システムを停止します。データベースの操作と、レプリケーション トポロジの他のすべてのデータベースの利用を停止した後、すべてのノードの同期を試行します。 詳細については、「[レプリケーション トポロジの停止 &#40;レプリケーション Transact-SQL プログラミング&#41;](../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)」を参照してください。    
1.  DBCC CHECKDB を実行します。    
1.  DBCC CHECKDB レポートで、ディストリビューション データベースの任意のテーブルまたはユーザー データベースのレプリケーション メタデータ テーブルの修復が示されている場合は、レプリケーションを削除して再構成します。 詳細については、「[パブリッシングの無効化と配布](../../relational-databases/replication/disable-publishing-and-distribution.md)」を参照してください。    
1.  DBCC CHECKDB レポートで、レプリケートされたテーブルの修復が示されている場合は、データ検証を実行して、パブリケーション データベースとサブスクリプション データベースのデータ間に違いがあるかどうかを確認します。    
    
## <a name="result-sets"></a>結果セット    
DBCC CHECKDB は以下の結果セットを返します。 ESTIMATEONLY オプション、PHYSICAL_ONLY オプション、または NO_INFOMSGS オプションを指定した場合以外は、値が異なることがあります。
    
```
 DBCC results for 'model'.    
    
 Service Broker Msg 9675, Level 10, State 1: Message Types analyzed: 13.    
    
 Service Broker Msg 9676, Level 10, State 1: Service Contracts analyzed: 5.    
    
 Service Broker Msg 9667, Level 10, State 1: Services analyzed: 3.    
    
 Service Broker Msg 9668, Level 10, State 1: Service Queues analyzed: 3.    
    
 Service Broker Msg 9669, Level 10, State 1: Conversation Endpoints analyzed: 0.    
    
 Service Broker Msg 9674, Level 10, State 1: Conversation Groups analyzed: 0.    
    
 Service Broker Msg 9670, Level 10, State 1: Remote Service Bindings analyzed: 0.    
    
 DBCC results for 'sys.sysrowsetcolumns'.    
    
 There are 630 rows in 7 pages for object 'sys.sysrowsetcolumns'.    
    
 DBCC results for 'sys.sysrowsets'.    
    
 There are 97 rows in 1 pages for object 'sys.sysrowsets'.    
    
 DBCC results for 'sysallocunits'.    
    
 There are 195 rows in 3 pages for object 'sysallocunits'.    
    
 There are 0 rows in 0 pages for object "sys.sysasymkeys".    
    
 DBCC results for 'sys.syssqlguides'.    
    
 There are 0 rows in 0 pages for object "sys.syssqlguides".    
    
 DBCC results for 'sys.queue_messages_1977058079'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_1977058079".    
    
 DBCC results for 'sys.queue_messages_2009058193'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2009058193".    
    
 DBCC results for 'sys.queue_messages_2041058307'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2041058307".    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'model'.    
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```

NO_INFOMSGS を指定した場合、DBCC CHECKDB は以下の結果セット (メッセージ) を返します。
    
```
 The command(s) completed successfully.
 ```
 
PHYSICAL_ONLY を指定した場合、DBCC CHECKDB は以下の結果セットを返します。
    
```
 DBCC results for 'model'.    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'master'.  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
 ```
 
ESTIMATEONLY を指定した場合、DBCC CHECKDB は以下の結果セットを返します。
    
```
 Estimated TEMPDB space needed for CHECKALLOC (KB)    
    
 -------------------------------------------------  
    
 13   
    
 (1 row(s) affected)   
    
 Estimated TEMPDB space needed for CHECKTABLES (KB)    
    
 --------------------------------------------------    
    
 57 
    
 (1 row(s) affected)  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```
    
## <a name="permissions"></a>アクセス許可    
Sysadmin 固定サーバー ロールまたは db_owner 固定データベース ロールのメンバーシップが必要です。
    
## <a name="examples"></a>使用例    
    
### <a name="a-checking-both-the-current-and-another-database"></a>A. 現在のデータベースと別のデータベースの両方をチェックする    
次の例では、現在のデータベースと [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに対して `DBCC CHECKDB` を実行します。
    
```sql    
-- Check the current database.    
DBCC CHECKDB;    
GO    
-- Check the AdventureWorks2012 database without nonclustered indexes.    
DBCC CHECKDB (AdventureWorks2012, NOINDEX);    
GO    
```    
    
### <a name="b-checking-the-current-database-suppressing-informational-messages"></a>B. 情報メッセージを表示せずに現在のデータベースをチェックする    
次の例では、現在のデータベースをチェックし、すべての情報メッセージを表示しないようにします。
    
```sql    
DBCC CHECKDB WITH NO_INFOMSGS;    
GO    
```    
    
## <a name="see-also"></a>参照    
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[データベース スナップショットのスパース ファイルのサイズを表示する方法 &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)  
[sp_helpdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)  
[システム テーブル &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  

