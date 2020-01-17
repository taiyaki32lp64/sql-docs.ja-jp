---
title: オンライン インデックス操作のガイドライン | Microsoft Docs
ms.custom: ''
ms.date: 11/12/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- clustered indexes, online operations
- online index operations
- indexes [SQL Server], online operations
- disk space [SQL Server], indexes
- nonclustered indexes [SQL Server], online operations
- transaction logs [SQL Server], indexes
ms.assetid: d82942e0-4a86-4b34-a65f-9f143ebe85ce
author: MikeRayMSFT
ms.author: mikeray
ms.prod_service: table-view-index, sql-database
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 32f1363901d06e8e3551c8f161c38d48fc190921
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73981797"
---
# <a name="guidelines-for-online-index-operations"></a>オンライン インデックス操作のガイドライン

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

インデックス操作をオンラインで実行するときは、次のガイドラインに従ってください。  

- 基になるテーブルに **image**、 **ntext**、 **text**などの LOB (ラージ オブジェクト) データ型が含まれている場合、クラスター化インデックスの作成、再構築、または削除は、オフラインで行う必要があります。  
- テーブルに LOB データ型が含まれていても、そのデータ型の列がキー列または非キー (付加) 列としてインデックス定義で使用されていない場合は、一意ではない非クラスター化インデックスをオンラインで作成できます。  
- ローカル一時テーブルのインデックスの作成、再構築、または削除は、オンラインでは実行できません。 この制限は、グローバル一時テーブルのインデックスには当てはまりません。
- インデックスは、予期しないエラー、データベースのフェールオーバー、または **PAUSE** コマンドの後で、停止したところから再開できます。 「[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)」および「[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)」を参照してください。

> [!NOTE]  
> オンラインでのインデックス操作は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各エディションでサポートされる機能の一覧については、[各エディションがサポートする機能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)に関するページを参照してください。  

次の表に、オンラインで実行可能なインデックス操作、これらのオンライン操作対象から除外されるインデックス、再開可能なインデックスの制限を示します。 また、その他の制限についても記載します。  

| オンラインのインデックス操作 | 操作対象外のインデックス | その他の制限事項 |  
|----------------------------|----------------------|------------------------|  
|ALTER INDEX REBUILD|無効化されたクラスター化インデックスまたは無効化されたインデックス付きビュー<br /><br /> XML インデックス<br /><br />列ストア インデックス <br /><br /> ローカル一時テーブルのインデックス|テーブルに操作対象外のインデックスが含まれている場合、キーワード ALL を指定すると操作が失敗する可能性があります。<br /><br /> 無効化されたインデックスの再構築には、他にも制限があります。 詳細については、「 [インデックスと制約の無効化](../../relational-databases/indexes/disable-indexes-and-constraints.md)」を参照してください。|  
|CREATE INDEX|XML インデックス<br /><br /> ビューの最初の一意クラスター化インデックス<br /><br /> ローカル一時テーブルのインデックス||  
|CREATE INDEX WITH DROP_EXISTING|無効化されたクラスター化インデックスまたは無効化されたインデックス付きビュー<br /><br /> ローカル一時テーブルのインデックス<br /><br /> XML インデックス||  
|DROP INDEX|無効化されたインデックス<br /><br /> XML インデックス<br /><br /> 非クラスター化インデックス<br /><br /> ローカル一時テーブルのインデックス|1 つのステートメント内に複数のインデックスは指定できません。|  
|ALTER TABLE ADD CONSTRAINT (PRIMARY KEY または UNIQUE)|ローカル一時テーブルのインデックス<br /><br /> クラスター化インデックス|サブ句は、一度に 1 つしか使用できません。 たとえば、同じ ALTER TABLE ステートメント内で PRIMARY KEY 制約または UNIQUE 制約を追加して削除することはできません。|  
|ALTER TABLE DROP CONSTRAINT (PRIMARY KEY または UNIQUE)|クラスター化インデックス||  
  
 オンラインのインデックス操作の実行中は、基になるテーブルを変更、切り捨て、または削除できません。  
  
 クラスター化インデックスの作成または削除時に指定したオンライン オプションの設定 (ON または OFF) は、再構築する必要のある非クラスター化インデックスに適用されます。 たとえば、クラスター化インデックスが CREATE INDEX WITH DROP_EXISTING, ONLINE=ON を使用してオンラインで構築される場合、関連するすべての非クラスター化インデックスも、オンラインで再作成されます。  
  
 UNIQUE インデックスをオンラインで作成または再構築するときに、インデックス ビルダーと同時実行ユーザー トランザクションが、同じキーの挿入を試み、一意性が損なわれる場合があります。 ソース テーブルの元の行が新しいインデックス (ターゲット) に移動される前に、ユーザーが入力した行が新しいインデックスに挿入されると、オンラインのインデックス操作が失敗します。  
  
 ユーザーやアプリケーションの作業によっては、オンラインのインデックス操作とデータベースの更新が連携して実行される場合、まれに、オンラインのインデックス操作によりデッドロックが発生する場合があります。 このようなまれなケースでは、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] により、ユーザーやアプリケーションの作業がデッドロックの対象として選択されます。  
  
 複数の新しい非クラスター化インデックスを作成しているとき、または非クラスター化インデックスを再構成しているときに限り、同じテーブルやビューに対してインデックス DDL 操作をオンラインで同時実行できます。 その他すべてのオンライン インデックス操作は、同時に実行しようとしても失敗します。 たとえば、既存のインデックスをオンラインで再構築している間に、同じテーブルの新しいインデックスをオンラインで作成することはできません。  
  
 インデックスにラージ オブジェクト型の列が含まれていて、同じトランザクション内でオンライン操作の前に更新操作がある場合は、このオンライン操作を実行できません。 この問題を回避するには、オンライン操作をトランザクションの外部に配置するか、トランザクション内で更新操作の前に配置してください。  
  
## <a name="disk-space-considerations"></a>ディスク領域に関する注意点

オンライン インデックス操作には、オフライン インデックス操作より多くのディスク容量が必要になります。

- インデックス作成操作やインデックス再構築操作の間、作成または再構築されるインデックスのために追加の領域が必要になります。
- また、仮のマッピング インデックス操作にもディスク容量が必要になります。 この一時インデックスは、クラスター化インデックスを作成、再構築、または削除する、オンライン インデックス操作で使用されます。
- クラスター化インデックスをオンラインで削除する場合と、クラスター化インデックスをオンラインで作成または再構築する場合は同じ量の領域が必要になります。

詳細については、「 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)」をご参照ください。  
  
## <a name="performance-considerations"></a>パフォーマンスに関する考慮事項

オンラインのインデックス操作では、同時実行ユーザーによる更新操作は許可されていますが、その更新操作の負荷が非常に高いと、インデックス操作の処理時間が長くなります。 通常、オンラインのインデックス操作は、同時実行更新操作の負荷レベルに関係なく、同じインデックス操作をオフラインで行った場合よりも時間がかかります。  
  
オンラインのインデックス操作中は、ソースの構造とターゲットの構造の両方が保持されるため、挿入、更新、削除のトランザクションによるリソースの使用量は、最大 2 倍にまで増加する場合があります。 このため、インデックス操作中のパフォーマンスが低下し、リソースの使用量 (特に CPU 使用時間) が増大する可能性があります。 オンラインでのインデックス操作は、完全にログに記録されます。  
  
オンラインでの操作を推奨しますが、実際の環境と特定の要件を評価してください。 オフラインでインデックス操作を実行することが最適な場合もあります。 この場合、操作中にユーザーからのデータ アクセスは制限されますが、操作をより短時間で完了でき、使用するリソースも軽減できます。  
  
SQL Server 2016 を実行するマルチプロセッサ コンピューターでは、他のクエリと同様に、インデックスのステートメントがこのステートメントに関連付けられているスキャン操作や並べ替え操作の実行に、より多くのプロセッサを使用する場合があります。 MAXDOP インデックス オプションを使用して、オンラインでのインデックス操作専用に使用するプロセッサ数を制御できます。 このようにすることで、インデックス操作が使用するリソースと他の同時実行ユーザーが使用するリソースのバランスをとることができます。 詳細については、「 [並列インデックス操作の構成](../../relational-databases/indexes/configure-parallel-index-operations.md)」を参照してください。 並列インデックス操作をサポートする SQL Server のエディションの詳細については、[各エディションがサポートする機能](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)に関するページを参照してください。  
  
S-Lock または Sch-M ロックはインデックス操作の最後のフェーズで保持されるので、BEGIN TRANSACTION...COMMIT ブロックなど、明示的なユーザー トランザクション内でのオンラインのインデックス操作を実行する場合は十分に注意してください。 この場合、ロックがトランザクションの最後まで保持され、その結果ユーザーのコンカレンシーが損なわれます。  
  
インデックスをオンラインで再構築すると、 `MAX DOP > 1` オプションと `ALLOW_PAGE_LOCKS = OFF` オプションでの実行が許可されたときに断片化が増加する可能性があります。 詳細については、「[How It Works:Online Index Rebuild - Can Cause Increased Fragmentation (しくみ: オンラインでのインデックス再構築 - 断片化が増加する可能性)](https://blogs.msdn.com/b/psssql/archive/2012/09/05/how-it-works-online-index-rebuild-can-cause-increased-fragmentation.aspx)」をご覧ください。  
  
## <a name="transaction-log-considerations"></a>トランザクション ログに関する注意点

オフライン、オンラインを問わず、大規模なインデックス操作を行うと、大量のデータ読み込みが発生し、トランザクション ログがすぐにいっぱいになってしまうことがあります。 インデックス操作をロールバックできるようにするため、インデックス操作が完了するまでは、トランザクション ログを切り捨てることはできません。ただし、インデックス操作中にログをバックアップすることはできます。 したがって、トランザクション ログには、インデックス操作中にインデックス操作によるトランザクションと、同時実行ユーザーによるトランザクションの両方を格納できるだけの十分な領域が割り当てられている必要があります。 詳細については、「 [インデックス操作用のトランザクション ログのディスク領域](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)」を参照してください。  

## <a name="resumable-index-considerations"></a>再開可能なインデックスに関する考慮事項

> [!NOTE]
> インデックス作成とインデックス再構築の再開可能インデックス オプションは SQL Server と SQL Database で利用できます (インデックス再構築は SQL Server 2017 以降。インデックス作成は SQL Server 2019 でもサポートされています)。 「[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)」および「[ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)」を参照してください。

再開可能なオンライン インデックスの作成または再構築を実行するときは、次のガイドラインが適用されます。

- インデックス メンテナンス期間の管理、計画、延長。 インデックスの作成または再構築操作を何回でも一時停止して再開し、メンテナンス期間に合わせることができます。
- インデックスの作成または再構築の障害からの回復 (データベースのフェールオーバーやディスク領域の不足など)。
- インデックス操作を一時停止すると、元のインデックスと新しく作成されたインデックスの両方にディスク領域が必要であり、DML 操作中に更新する必要があります。
- インデックスの作成または再構築操作の間はトランザクション ログの切り捨てを有効にします。
- SORT_IN_TEMPDB=ON オプションはサポートされていません。

> [!IMPORTANT]
> 再開可能なインデックスの作成または再構築では実行時間の長いトランザクションを開いたままにする必要はなく、この操作の間のログの切り捨てと、より優れたログ領域管理が可能です。 新しい設計では、必要なデータを、再開可能な操作を再開するために必要なすべての参照と共に、データベースに保持しています。

一般に、再開可能なオンライン インデックス再構築と再開不可能なオンライン インデックス再構築の間に、パフォーマンスの違いはありません。 再開可能なインデックス作成については、再開可能なインデックス作成と再開不可能なインデックス作成の間のわずかなパフォーマンスの違いを引き起こす一定のオーバーヘッドが存在します。 ほとんどの場合、この違いは小さいテーブルでのみ顕著です。

インデックス操作を一時停止している間に再開可能なインデックスを更新すると、次のようになります。

- 通常は読み取り専用のワークロードの場合、パフォーマンスに与える影響は大きくありません。
- 更新の多いワークロードの場合、スループットが低下する可能性があります (弊社テストで 10% 未満の低下)。

一般に、再開可能なオンライン インデックスの作成または再構築と再開不可能なオンライン インデックスの作成または再構築の間に、最適化の品質の違いはありません。

## <a name="online-default-options"></a>オンラインの既定のオプション

> [!IMPORTANT]
> これらのオプションは、[!INCLUDE[ssNoVersion](../../includes/sssqlv15-md.md)] でパブリック プレビュー状態です。

ELEVATE_ONLINE または ELEVATE_RESUMABLE データベース スコープ構成オプションを設定することで、データベース レベルでオンラインまたは再開可能の既定のオプションを設定できます。 これらの既定のオプションを設定すると、データベース テーブルをオフラインにする操作を誤って実行してしまう事態を回避できます。 いずれのオプションでも、エンジンは特定の操作をオンラインまたは再開可能実行に自動昇格します。  
[ALTER DATABASE SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) コマンドを使用して、オプションを FAIL_UNSUPPORTED、WHEN_SUPPORTED、または OFF のいずれかに設定できます。 オンラインと再開可能に異なる値を設定できます。

ELEVATE_ONLINE と ELEVATE_RESUMABLE はいずれも、オンラインと再開可能の構文をそれぞれサポートする DDL ステートメントにのみ適用されます。 たとえば、ELEVATE_ONLINE=FAIL_UNSUPORTED で XML インデックスを作成すると、XML インデックスで ONLINE= 構文がサポートされていないため、操作がオフラインで実行されます。 これらのオプションは、ONLINE または RESUMABLE オプションを指定せずに送信される DDL ステートメントでのみ有効になります。 たとえば、ONLINE=OFF または RESUMABLE=OFF でステートメントを送信することで、ユーザーは FAIL_UNSUPPORTED 設定をオーバーライドし、オフラインか再開不可能でステートメントを実行できます。

> [!NOTE]
> ELEVATE_ONLINE と ELEVATE_RESUMABLE は XML インデックス操作に適用されません。

## <a name="related-content"></a>関連コンテンツ

- [オンライン インデックス操作の動作原理](../../relational-databases/indexes/how-online-index-operations-work.md)  
- [オンラインでのインデックス操作の実行](../../relational-databases/indexes/perform-index-operations-online.md)  
- [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)  
- [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)  
