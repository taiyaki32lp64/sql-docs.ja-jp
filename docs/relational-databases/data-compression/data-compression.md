---
title: データ圧縮 | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- page compression [Database Engine]
- indexes [SQL Server], compressed
- compressed indexes [SQL Server]
- storage compression [Database Engine]
- tables [SQL Server], compressed
- storage [SQL Server], compressed
- compression [SQL Server]
- row compression [Database Engine]
- compression [SQL Server], about compressed tables and indexes
- data compression [Database Engine]
- compressed tables [SQL Server]
ms.assetid: 5f33e686-e115-4687-bd39-a00c48646513
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e31898c8252084a34ed645e5b3f5113f9893ee48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055452"
---
# <a name="data-compression"></a>Data Compression
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] および [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]では、行ストア インデックスおよびテーブルのための行およびページの圧縮がサポートされます。また、列ストアと、列ストアおよびインデックスのための列ストアの保存用圧縮もサポートされます。  
  
 行ストア テーブルおよびインデックスについては、データベースのサイズを小さくするためにデータ圧縮機能を使用してください。 領域を削減するだけでなく、データ圧縮を使用すると、データを格納するページ数が少なくなり、クエリがディスクから読み取る必要のあるページが少なくなるため、大量の I/O が発生する作業のパフォーマンスを向上できます。 ただし、アプリケーションとの間でデータが交換される間は、データの圧縮と圧縮解除のためデータベース サーバーで追加の CPU リソースが必要になります。 次のデータベース オブジェクトで行とページの圧縮を構成することができます。   
-   ヒープとして格納されているテーブル全体。  
-   クラスター化インデックスとして格納されているテーブル全体。  
-   非クラスター化インデックス全体。  
-   インデックス付きビュー全体。  
-   パーティション分割されているテーブルおよびインデックスの場合、パーティションごとに圧縮オプションを構成することができ、オブジェクトの各パーティションを同じ圧縮設定にする必要がありません。  
  
列ストア テーブルおよびインデックスの場合、すべての列ストア テーブルおよびインデックスで列ストア圧縮が使用されます。これはユーザーが構成できません。 データを格納および取得できる CPU リソースと時間に余裕がある場合にデータ サイズをさらに小さくするには、列ストアの保存用圧縮を使用します。  次のデータベース オブジェクトで列ストアの保存用圧縮を構成することができます。  
-   列ストア テーブル全体またはクラスター化列ストア インデックス全体。  列ストア テーブルはクラスター化列ストア インデックスとして格納されるため、どちらの方法を使っても同じ結果になります。  
-   非クラスター化列ストア インデックス全体。  
-   パーティション分割されている列ストア テーブルおよび列ストア インデックスの場合、パーティションごとに保存用圧縮オプションを構成することができ、オブジェクトの各パーティションを同じ保存用圧縮設定にする必要がありません。  
  
> [!NOTE]  
>  GZIP アルゴリズム形式を使用してデータを圧縮することもできます。 これは追加の手順であり、古いデータを長期保管するためにアーカイブする際にデータの一部を圧縮する場合に最も適しています。 COMPRESS 関数を使用して圧縮したデータにインデックスを付けることはできません。 詳細については、「[COMPRESS &#40;Transact-SQL&#41;](../../t-sql/functions/compress-transact-sql.md)」を参照してください。  
  
## <a name="considerations-for-when-you-use-row-and-page-compression"></a>行とページの圧縮の使用に関する注意点  
 行とページの圧縮を使用する際は、次の点に注意してください。  
-   データの圧縮に関する詳細情報は、Service Pack または今後のリリースで予告なしに変更されることがあります。
-   圧縮は、[!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]で使用できます。  
-   圧縮は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 詳細については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
-   圧縮は、システム テーブルには使用できません。  
-   圧縮を使用すると、ページに格納できる行数が増えますが、テーブルまたはインデックスの最大行サイズは変更されません。  
-   最大行サイズに圧縮のオーバーヘッドを加えると最大行サイズが 8,060 バイトを超える場合、テーブルで圧縮を有効にすることはできません。 例えば、列 c1**char(8000)** および c2**char(53)** を含むテーブルは、圧縮のオーバーヘッドが追加で発生するため、圧縮できません。 vardecimal ストレージ形式を使用する場合は、この形式が有効になると行サイズのチェックが実行されます。 行とページの圧縮の場合は、オブジェクトが最初に圧縮されるときに行サイズのチェックが実行され、各行が挿入または変更されるときにもチェックされます。 圧縮では、次の 2 つのルールが適用されます。  
    -   固定長の型に対する更新が常に成功する必要があります。  
    -   データ圧縮の無効化が常に成功する必要があります。 圧縮された行がページに収まる場合 (行のサイズが 8,060 バイト未満の場合) でも、圧縮されていないときの行に収まらない更新は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって回避されます。  
-   パーティションの一覧を指定する場合は、個々のパーティションの圧縮の種類を ROW、PAGE、または NONE に設定できます。 パーティションの一覧を指定しない場合は、すべてのパーティションがステートメントで指定されたデータ圧縮プロパティを使用して設定されます。 特に指定しない限り、データ圧縮はテーブルまたはインデックスの作成時に NONE に設定されます。 特に指定しない限り、既存の圧縮はテーブルの変更時にも保持されます。  
-   範囲外の一連のパーティションまたは単独のパーティションを指定すると、エラーが生成されます。  
-   テーブルの圧縮プロパティは非クラスター化インデックスに継承されません。 インデックスを圧縮するには、インデックスの圧縮プロパティを明示的に設定する必要があります。 既定では、インデックスの圧縮設定はインデックスの作成時に NONE に設定されます。  
-   ヒープにクラスター化インデックスを作成する場合、圧縮状態を特に指定しない限り、ヒープの圧縮状態がクラスター化インデックスに継承されます。  
-   ヒープがページ レベルの圧縮用に構成されている場合、ページでは、次の方法によるページ レベルの圧縮のみが受け入れられます。  
    -   データは一括最適化を有効にして一括インポートされます。  
    -   INSERT INTO ...WITH (TABLOCK) 構文とテーブルに非クラスター化インデックスはありません。  
    -   PAGE 圧縮オプションを指定して ALTER TABLE ...REBUILD ステートメントを実行し、テーブルを再構築する方法  
-   DML 操作の一部としてヒープに割り当てられた新しいページでは、ヒープが再構築されるまで PAGE 圧縮は使用されません。 圧縮を解除してから再適用するか、クラスター化インデックスを作成してから削除することで、ヒープを再構築します。  
-   ヒープの圧縮設定を変更するには、テーブルのすべての非クラスター化インデックスを再構築して、ヒープ内の新しい行位置へのポインターを持つようにする必要があります。  
-   ROW または PAGE 圧縮はオンラインまたはオフラインで有効または無効にすることができます。 オンライン操作の場合、ヒープに対する圧縮の有効化はシングル スレッドです。  
-   行またはページの圧縮を有効または無効にするために必要なディスク空き容量は、インデックスを作成または再構築するために必要なディスク空き容量と同じです。 パーティション データの場合は、一度に 1 つのパーティションの圧縮を有効または無効にすることによって必要な空き容量を削減できます。  
-   パーティション テーブルのパーティションの圧縮状態を調べるには、sys.partitions カタログ ビューの data_compression 列に対してクエリを実行します。  
-   インデックスを圧縮する場合、行とページの両方の圧縮を使用してリーフ レベルのページを圧縮できます。 リーフ レベル以外のページでは、ページの圧縮は受け入れられません。  
-   大きな値のデータ型は、そのサイズが原因で、通常の行データとは別に特殊な目的のページに格納される場合があります。 データ圧縮は、別個に格納されているデータには使用できません。  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] で vardecimal ストレージ形式を実装したテーブルは、アップグレード時にもその設定を保持します。 vardecimal ストレージ形式を使用するテーブルに行の圧縮を適用することができます。 ただし、行の圧縮は vardecimal ストレージ形式のスーパーセットなので、vardecimal ストレージ形式を保持する理由はありません。 vardecimal ストレージ形式と行の圧縮を組み合わせても、10 進値の圧縮は追加されません。 vardecimal ストレージ形式を使用するテーブルにページの圧縮を適用することができます。ただし、vardecimal ストレージ形式の列の圧縮が追加される可能性は低くなります。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] は vardecimal ストレージ形式をサポートしていますが、行レベルの圧縮で同じ目的が果たされるので、vardecimal ストレージ形式は非推奨とされます。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="using-columnstore-and-columnstore-archive-compression"></a>列ストアおよび列ストアの保存用圧縮の使用  
  
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)、[!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]。  
  
### <a name="basics"></a>の基本操作  
 列ストア テーブルおよび列ストア インデックスは常に列ストア圧縮を使用して格納されます。 保存用圧縮と呼ばれる追加の圧縮機能を構成するによって、列ストアのデータ サイズをさらに小さくすることができます。  保存用圧縮を使用するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でデータに対して Microsoft Xpress 圧縮アルゴリズムを実行します。 次の種類のデータ圧縮を使用して、保存用圧縮を追加または削除します。  
-   保存用圧縮で列ストア データを圧縮するには、 **COLUMNSTORE_ARCHIVE** データ圧縮を使用します。  
-   保存用圧縮を解凍するには、 **COLUMNSTORE** データ圧縮を使用します。 この結果として生成されるデータは、引き続き列データの圧縮を使用して圧縮できます。  
  
保存用圧縮を追加するには、REBUILD オプションと DATA COMPRESSION = COLUMNSTORE_ARCHIVE を指定して [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) または [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) を使用します。  
  
#### <a name="examples"></a>例 :  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE_ARCHIVE ON PARTITIONS (2,4)) ;  
```  
  
保存用圧縮を削除して、データを列ストア圧縮に復元するには、REBUILD オプションと DATA COMPRESSION = COLUMNSTORE を指定して [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) または [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md) を使用します。  
  
#### <a name="examples"></a>例 :  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE) ;  
  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (DATA_COMPRESSION =  COLUMNSTORE ON PARTITIONS (2,4) ) ;  
```  
  
次の例では、データ圧縮をあるパーティションの列ストアに設定し、列ストアの圧縮を別のパーティションに設定しています。  
  
```  
ALTER TABLE ColumnstoreTable1   
REBUILD PARTITION = ALL WITH (  
    DATA_COMPRESSION =  COLUMNSTORE ON PARTITIONS (4,5),  
    DATA COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (1,2,3)  
) ;  
```  
  
### <a name="performance"></a>パフォーマンス  
 保存用圧縮を使用して列ストア インデックスを圧縮すると、列ストア インデックスに保存用圧縮がない場合に比べて実行速度が遅くなります。 保存用圧縮は、データを圧縮および取得する時間と CPU リソースに余裕がある場合にのみ使用します。  
  
 記憶域を削減するデータ圧縮の利点は、頻繁にアクセスしないデータに便利です。 たとえば、各月のデータ用のパーティションがある場合、ほとんどアクティビティは最新の月のデータに対して実行されるため、古い月のデータをアーカイブして必要なストレージを削減できます。  
  
### <a name="metadata"></a>メタデータ  
次のシステム ビューには、クラスター化インデックスのデータ圧縮に関する情報が含まれています。  
-   [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) - **type** 列と **type_desc** 列には、CLUSTERED COLUMNSTORE と NONCLUSTERED COLUMNSTORE が含まれます。  
-   [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) - **data_compression** 列と **data_compression_desc** 列には、COLUMNSTORE と COLUMNSTORE_ARCHIVE が含まれます。  
  
プロシージャ [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) も列ストア インデックスに適用されます。  
  
## <a name="how-compression-affects-partitioned-tables-and-indexes"></a>パーティション テーブルとパーティション インデックスへの圧縮の影響  
 パーティション テーブルとパーティション インデックスでデータ圧縮を使用する場合は、次の点に注意してください。  
-   ALTER PARTITION ステートメントを使用してパーティションを分割すると、両方のパーティションに元のパーティションのデータ圧縮属性が継承されます。  
-   2 つのパーティションをマージすると、結果として得られるパーティションにマージ先パーティションのデータ圧縮属性が継承されます。  
-   パーティションを切り替えるには、パーティションのデータ圧縮プロパティがテーブルの圧縮プロパティと一致する必要があります。  
-   パーティション テーブルまたはパーティション インデックスの圧縮の変更に使用できる構文には、次の 2 種類があります。  
    -   次の構文では、参照されているパーティションのみが再構築されます。  
        ```  
        ALTER TABLE <table_name>   
        REBUILD PARTITION = 1 WITH (DATA_COMPRESSION =  <option>)  
        ```  
    -   次の構文では、参照されていないパーティションの既存の圧縮設定を使用して、テーブル全体が再構築されます。  
        ```  
        ALTER TABLE <table_name>   
        REBUILD PARTITION = ALL   
        WITH (DATA_COMPRESSION = PAGE ON PARTITIONS(<range>),  
        ... )  
        ```  
  
     パーティション インデックスの場合は、ALTER INDEX を使用して同じ原則に従います。  
  
-   クラスター化インデックスを削除する場合、パーティション構成を変更しない限り、対応するヒープ パーティションでデータ圧縮設定が維持されます。 パーティション構成を変更すると、すべてのパーティションが圧縮されていない状態に再構築されます。 クラスター化インデックスを削除し、パーティション構成を変更するには、次の手順を実行します。  
     1. クラスター化インデックスを削除します。  
     2. 圧縮オプションを指定する ALTER TABLE ...REBUILD ... オプションを使用して、テーブルを変更します。  
  
     OFFLINE でクラスター化インデックスを削除すると、クラスター化インデックスの上位レベルだけが削除されます。そのため、操作はとても高速です。 ONLINE でクラスター化インデックスを削除すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、ヒープが手順 1. で 1 回、手順 2. で 1 回の計 2 回再構築されます。  
  
## <a name="how-compression-affects-replication"></a>レプリケーションへの圧縮の影響 
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。   
レプリケーションでデータ圧縮を使用する場合は、次の点に注意してください。  
-   スナップショット エージェントで最初のスキーマ スクリプトが生成されるときに、新しいスキーマでは、テーブルとインデックスの両方に同じ圧縮設定が使用されます。 圧縮をテーブルのみで有効にし、インデックスで無効にすることはできません。  
-   トランザクション レプリケーションの場合、アーティクル スキーマ オプションによって、スクリプトを作成する必要がある依存オブジェクトおよびプロパティが特定されます。 詳細については、「 [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)」を参照してください。  
     ディストリビューション エージェントでは、スクリプトの適用時に下位のサブスクライバーのチェックが行われません。 圧縮のレプリケーションが選択されている場合、下位のサブスクライバーに対するテーブルの作成は失敗します。 混合トポロジの場合は、圧縮のレプリケーションを有効にしないでください。  
-   マージ レプリケーションの場合、パブリケーションの互換性レベルがスキーマ オプションをオーバーライドし、この互換性レベルによってスクリプトが作成されるスキーマ オブジェクトが特定されます。  
     混合トポロジの場合、新しい圧縮オプションをサポートする必要がないときは、パブリケーションの互換性レベルを下位のサブスクライバー バージョンに設定してください。 サポートする必要があるときは、テーブルをサブスクライバーに作成してから圧縮してください。  
  
次の表に、レプリケーション時に圧縮を制御するレプリケーション設定を示します。  
  
|ユーザーの目的|テーブルまたはインデックスのパーティション構成のレプリケート|圧縮設定のレプリケート|スクリプト作成の動作|  
|-----------------|-----------------------------------------------------|------------------------------------|------------------------|  
|パーティション構成をレプリケートしてパーティションのサブスクライバーで圧縮を有効にする。|True|True|パーティション構成と圧縮設定の両方のスクリプトを作成します。|  
|パーティション構成をレプリケートするがサブスクライバーでデータ圧縮は実行しない。|True|False|パーティション構成のスクリプトは作成しますが、パーティションの圧縮設定のスクリプトは作成しません。|  
|パーティション構成をレプリケートせず、サブスクライバーでデータ圧縮も実行しない。|False|False|パーティションと圧縮設定のスクリプトを作成しません。|  
|パブリッシャーですべてのパーティションが圧縮される場合はサブスクライバーでテーブルを圧縮するが、パーティション構成はレプリケートしない。|False|True|すべてのパーティションで圧縮が有効になっているかどうかを確認します。<br /><br /> テーブル レベルで圧縮のスクリプトを作成します。|  
  
## <a name="how-compression-affects-other-sql-server-components"></a>他の SQL Server コンポーネントへの圧縮の影響 
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] から[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658)まで)。  
   
 圧縮はストレージ エンジンで行われるので、他のほとんどの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントには、データは圧縮されていない状態で提供されます。 このため、他のコンポーネントに対する圧縮の影響は、次のように制限されます。  
-   一括インポート操作と一括エクスポート操作  
     データをエクスポートする場合、データはネイティブ形式であっても圧縮されていない行形式で出力されます。 この結果、エクスポートされたデータ ファイルのサイズがソース データより大幅に大きくなる可能性があります。  
     データをインポートする場合、インポート先のテーブルで圧縮が有効になっているときは、データはストレージ エンジンによって圧縮された行形式に変換されます。 この結果、圧縮されていないテーブルにデータをインポートする場合と比較して、CPU 使用率が上昇する可能性があります。  
     ページの圧縮を使用するヒープにデータを一括インポートする場合、一括インポート操作では、データの挿入時にページの圧縮を使用したデータ圧縮が試行されます。  
-   圧縮はバックアップと復元には影響しません。  
-   圧縮はログ配布には影響しません。  
-   データ圧縮は、スパース列と互換性がありません。 したがって、スパース列を含むテーブルを圧縮したり、スパース列を圧縮されたテーブルに追加したりすることはできません。  
-   圧縮を有効にすると、クエリ プランが変更される可能性があります。データの格納に使用されるページ数とページあたりの行数が異なるためです。  
  
## <a name="see-also"></a>参照  
 [行の圧縮の実装](../../relational-databases/data-compression/row-compression-implementation.md)   
 [ページの圧縮の実装](../../relational-databases/data-compression/page-compression-implementation.md)   
 [Unicode 圧縮の実装](../../relational-databases/data-compression/unicode-compression-implementation.md)   
 [CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)   
 [CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
  

