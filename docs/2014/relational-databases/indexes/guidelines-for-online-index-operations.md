---
title: オンライン インデックス操作のガイドライン | Microsoft Docs
ms.custom: ''
ms.date: 11/11/2016
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: e2f7a25a4a6a4bb6b8f153a8b04b47aeb542265c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63162486"
---
# <a name="guidelines-for-online-index-operations"></a>オンライン インデックス操作のガイドライン
  インデックス操作をオンラインで実行するときは、次のガイドラインに従ってください。  
  
-   クラスター化インデックスを作成または削除は再構築、オフライン基になるテーブルには、次のラージ オブジェクト (LOB) データ型が含まれている場合: `image`、 **ntext**、および`text`します。  
  
-   ローカル一時テーブルのインデックスの作成、再構築、または削除は、オンラインでは実行できません。 この制限は、グローバル一時テーブルのインデックスには当てはまりません。  
  
> [!NOTE]  
>  オンラインでのインデックス操作は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
 次の表に、オンラインで実行可能なインデックス操作と、これらのオンライン操作対象から除外されるインデックスを示します。 また、その他の制限についても記載します。  
  
|オンラインのインデックス操作|操作対象外のインデックス|その他の制限事項|  
|----------------------------|----------------------|------------------------|  
|ALTER INDEX REBUILD|無効化されたクラスター化インデックスまたは無効化されたインデックス付きビュー<br /><br /> XML インデックス <br /><br />列ストア インデックス<br /><br /> ローカル一時テーブルのインデックス|テーブルに操作対象外のインデックスが含まれている場合、キーワード ALL を指定すると操作が失敗する可能性があります。<br /><br /> 無効化されたインデックスの再構築には、他にも制限があります。 詳細については、「 [インデックスと制約の無効化](disable-indexes-and-constraints.md)」を参照してください。|  
|CREATE INDEX|XML インデックス<br /><br /> ビューの最初の一意クラスター化インデックス<br /><br /> ローカル一時テーブルのインデックス||  
|CREATE INDEX WITH DROP_EXISTING|無効化されたクラスター化インデックスまたは無効化されたインデックス付きビュー<br /><br /> ローカル一時テーブルのインデックス<br /><br /> XML インデックス||  
|DROP INDEX|無効化されたインデックス<br /><br /> XML インデックス<br /><br /> 非クラスター化インデックス<br /><br /> ローカル一時テーブルのインデックス|1 つのステートメント内に複数のインデックスは指定できません。|  
|ALTER TABLE ADD CONSTRAINT (PRIMARY KEY または UNIQUE)|ローカル一時テーブルのインデックス<br /><br /> クラスター化インデックス|サブ句は、一度に 1 つしか使用できません。 たとえば、同じ ALTER TABLE ステートメント内で PRIMARY KEY 制約または UNIQUE 制約を追加して削除することはできません。|  
||||  
  
 オンラインのインデックス操作の実行中は、基になるテーブルを変更、切り捨て、または削除できません。  
  
 クラスター化インデックスの作成または削除時に指定したオンライン オプションの設定 (ON または OFF) は、再構築する必要のある非クラスター化インデックスに適用されます。 たとえば、クラスター化インデックスが CREATE INDEX WITH DROP_EXISTING, ONLINE=ON を使用してオンラインで構築される場合、関連するすべての非クラスター化インデックスも、オンラインで再作成されます。  
  
 UNIQUE インデックスをオンラインで作成または再構築するときに、インデックス ビルダーと同時実行ユーザー トランザクションが、同じキーの挿入を試み、一意性が損なわれる場合があります。 ソース テーブルの元の行が新しいインデックス (ターゲット) に移動される前に、ユーザーが入力した行が新しいインデックスに挿入されると、オンラインのインデックス操作が失敗します。  
  
 ユーザーやアプリケーションの作業によっては、オンラインのインデックス操作とデータベースの更新が連携して実行される場合、まれに、オンラインのインデックス操作によりデッドロックが発生する場合があります。 このようなまれなケースでは、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] により、ユーザーやアプリケーションの作業がデッドロックの対象として選択されます。  
  
 複数の新しい非クラスター化インデックスを作成しているとき、または非クラスター化インデックスを再構成しているときに限り、同じテーブルやビューに対してインデックス DDL 操作をオンラインで同時実行できます。 その他すべてのオンライン インデックス操作は、同時に実行しようとしても失敗します。 たとえば、既存のインデックスをオンラインで再構築している間に、同じテーブルの新しいインデックスをオンラインで作成することはできません。  
  
 インデックスにラージ オブジェクト型の列が含まれていて、同じトランザクション内でオンライン操作の前に更新操作がある場合は、このオンライン操作を実行できません。 この問題を回避するには、オンライン操作をトランザクションの外部に配置するか、トランザクション内で更新操作の前に配置してください。  
  
## <a name="disk-space-considerations"></a>ディスク領域に関する注意点  
 基本的に、オンラインとオフラインのインデックス操作間で、必要なディスク領域に違いはありません。 一時マッピング インデックスに追加のディスク領域が必要になる場合だけは例外です。 この一時インデックスは、クラスター化インデックスを作成、再構築、または削除する、オンライン インデックス操作で使用されます。 クラスター化インデックスをオンラインで削除する場合と、クラスター化インデックスをオンラインで作成する場合は同じ量の領域が必要になります。 詳細については、「 [Disk Space Requirements for Index DDL Operations](disk-space-requirements-for-index-ddl-operations.md)」をご参照ください。  
  
## <a name="performance-considerations"></a>パフォーマンスに関する考慮事項  
 オンラインのインデックス操作では、同時実行ユーザーによる更新操作は許可されていますが、その更新操作の負荷が非常に高いと、インデックス操作の処理時間が長くなります。 通常、オンラインのインデックス操作は、同時実行更新操作の負荷レベルに関係なく、同じインデックス操作をオフラインで行った場合よりも時間がかかります。  
  
 オンラインのインデックス操作中は、ソースの構造とターゲットの構造の両方が保持されるため、挿入、更新、削除のトランザクションによるリソースの使用量は、最大 2 倍にまで増加する場合があります。 このため、インデックス操作中のパフォーマンスが低下し、リソースの使用量 (特に CPU 使用時間) が増大する可能性があります。 オンラインでのインデックス操作は、完全にログに記録されます。  
  
 オンラインでの操作を推奨しますが、実際の環境と特定の要件を評価してください。 オフラインでインデックス操作を実行することが最適な場合もあります。 この場合、操作中にユーザーからのデータ アクセスは制限されますが、操作をより短時間で完了でき、使用するリソースも軽減できます。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]を実行するマルチプロセッサ コンピューターでは、他のクエリと同様に、インデックスのステートメントがこのステートメントに関連付けられているスキャン操作や並べ替え操作の実行に、より多くのプロセッサを使用する場合があります。 MAXDOP インデックス オプションを使用して、オンラインでのインデックス操作専用に使用するプロセッサ数を制御できます。 このようにすることで、インデックス操作が使用するリソースと他の同時実行ユーザーが使用するリソースのバランスをとることができます。 詳細については、「 [並列インデックス操作の構成](configure-parallel-index-operations.md)」を参照してください。 サポート並列インデックス操作をする SQL Server のエディションの詳細については、次を参照してください。[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。  
  
 S-Lock または Sch-M ロックはインデックス操作の最後のフェーズで保持されるので、BEGIN TRANSACTION...COMMIT ブロックなど、明示的なユーザー トランザクション内でのオンラインのインデックス操作を実行する場合は十分に注意してください。 この場合、ロックがトランザクションの最後まで保持され、その結果ユーザーのコンカレンシーが損なわれます。  
  
 インデックスをオンラインで再構築すると、 `MAX DOP > 1` オプションと `ALLOW_PAGE_LOCKS = OFF` オプションでの実行が許可されたときに断片化が増加する可能性があります。 詳細については、「[How It Works:Online Index Rebuild - Can Cause Increased Fragmentation (しくみ: オンラインでのインデックス再構築 - 断片化が増加する可能性)](https://blogs.msdn.com/b/psssql/archive/2012/09/05/how-it-works-online-index-rebuild-can-cause-increased-fragmentation.aspx)」をご覧ください。  
  
## <a name="transaction-log-considerations"></a>トランザクション ログに関する注意点  
 オフライン、オンラインを問わず、大規模なインデックス操作を行うと、大量のデータ読み込みが発生し、トランザクション ログがすぐにいっぱいになってしまうことがあります。 インデックス操作をロールバックできるようにするため、インデックス操作が完了するまでは、トランザクション ログを切り捨てることはできません。ただし、インデックス操作中にログをバックアップすることはできます。 したがって、トランザクション ログには、インデックス操作中にインデックス操作によるトランザクションと、同時実行ユーザーによるトランザクションの両方を格納できるだけの十分な領域が割り当てられている必要があります。 詳細については、「 [インデックス操作用のトランザクション ログのディスク領域](transaction-log-disk-space-for-index-operations.md)」を参照してください。  
  
## <a name="related-content"></a>関連コンテンツ  
 [オンライン インデックス操作の動作原理](how-online-index-operations-work.md)  
  
 [オンラインでのインデックス操作の実行](perform-index-operations-online.md)  
  
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)  
  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
  
