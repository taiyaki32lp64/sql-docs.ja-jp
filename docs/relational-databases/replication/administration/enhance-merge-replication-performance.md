---
title: マージ レプリケーション パフォーマンスの向上 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- designing databases [SQL Server], replication performance
- Merge Agent, performance
- snapshots [SQL Server replication], performance considerations
- merge replication performance [SQL Server replication]
- subscriptions [SQL Server replication], performance considerations
- performance [SQL Server replication], merge replication
- agents [SQL Server replication], performance
ms.assetid: f929226f-b83d-4900-a07c-a62f64527c7f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 261f22847c8b397d57ff5f732ea4d97091895daa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939202"
---
# <a name="enhance-merge-replication-performance"></a>マージ レプリケーション パフォーマンスの向上
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  「 [レプリケーションの全般的パフォーマンスの向上](../../../relational-databases/replication/administration/enhance-general-replication-performance.md)」で説明した全般的なパフォーマンスのヒントを検討した後、マージ レプリケーションに固有なこれらの項目を併せて検討してください。  
  
## <a name="database-design"></a>データベースの設計  
  
-   行フィルターおよび結合フィルター内で使用される列にインデックスを作成する。  
  
     パブリッシュされたアーティクルに行フィルターを使用する際には、フィルターの WHERE 句で使用する各列にインデックスを作成します。 インデックスがない場合、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、行をパーティション内に含めるかどうかを決定するためにテーブル内の各行を読み取る必要があります。 インデックスがあると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] は、含める行をすばやく見つけられます。 レプリケーションがインデックスのみを基にフィルターの WHERE 句を完全に解決できる場合、最高の処理速度になります。  
  
     また、結合フィルターで使用するすべての列に対してもインデックスを作成することが重要です。 マージ エージェントは、実行時にベース テーブルを検索して、パーティションに含める親テーブルの行と関連テーブルの行を判断します。 結合された列のインデックスを作成すれば、マージ エージェントを実行するたびに [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] がテーブルの各行を読み取る必要はなくなります。  
  
     フィルター選択の詳細については、「[マージ レプリケーション用にパブリッシュされたデータのフィルター選択](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)」を参照してください。  
  
-   Large Object (LOB) データ型を含むテーブルで、正規化を十分に行うことを検討する。  
  
     同期が発生するとき、マージ エージェントはパブリッシャーまたはサブスクライバーからすべての行を読み取って転送する必要があります。 行に LOB を使用する列が含まれている場合、この処理には追加のメモリ割り当てが必要となることがあり、これらの列が更新されていない場合でもパフォーマンスを低下させる可能性があります。 このようなパフォーマンス低下が発生する可能性を減らすには、LOB 列を別のテーブルに置き、残りの行データとの一対一リレーションシップを使用することを検討してください。 **text**、 **ntext**、および **image** の各データ型は非推奨とされます。 LOB が必要な場合は、 **varchar(max)** 、 **nvarchar(max)** 、および **varbinary(max)** の各データ型を使用することをお勧めします。  
  
## <a name="publication-design"></a>パブリケーションの設計  
  
-   90RTM ([!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョン) のパブリケーション互換性レベルを使用する。  
  
     1 つ以上のサブスクライバーが異なるバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を使用している場合を除き、パブリケーションが [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンのみをサポートする必要があるように指定します。 これによって、パブリケーションは、新しい機能とパフォーマンスの最適化を利用できるようになります。  
  
-   適切なパブリケーション保有期間設定を使用する。  
  
     パブリケーションの保有期間は、サブスクリプションが同期されるまでの最長期間を示し、この期間によって追跡メタデータを保存する期間が決定されます。 この値を大きくすると、ストレージと処理のパフォーマンスが影響を受ける可能性があります。 パブリケーションの保有期間の設定の詳細については、「 [Subscription Expiration and Deactivation](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)」を参照してください。  
  
-   パブリッシャーでのみ変更されるテーブルについては、ダウンロード専用アーティクルを使用する。 詳細については、「[ダウンロード専用アーティクルを使用したマージ レプリケーションのパフォーマンス最適化](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)」を参照してください。  
  
### <a name="filter-design-and-use"></a>フィルターの設計および使用方法  
  
-   複雑な行フィルター句を制限する。  
  
     フィルター条件の複雑さを制限することにより、サブスクライバーに送信する行の変更をマージ エージェントが評価するときのパフォーマンスが向上することになります。 マージ行フィルター句では、副選択の使用は避けてください。 代わりに、結合フィルターの使用を検討してください。一般に結合フィルターは、他のテーブルの行フィルター句を基に、テーブルのデータをパーティション分割するために使用すると、より効率的です。 フィルター選択の詳細については、「[マージ レプリケーション用にパブリッシュされたデータのフィルター選択](../../../relational-databases/replication/merge/filter-published-data-for-merge-replication.md)」を参照してください。  
  
-   パラメーター化されたフィルターによる事前計算済みパーティションを使用する (これは既定で使用される機能です)。 詳細については、「[事前計算済みパーティションによるパラメーター化されたフィルターのパフォーマンス最適化](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md)」を参照してください。  
  
     事前計算済みパーティションでは、フィルターの動作にさまざまな制限が課せられます。 アプリケーションがこれらの制限に従うことができない場合は、 **keep_partition_changes** オプションを **True**に設定すると、パフォーマンスが向上します。 詳しくは、「 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」をご覧ください。  
  
-   フィルター選択されたデータがユーザー間で共有されていない場合は、重複しないパーティションを使用する。  
  
     レプリケーションは、複数のパーティションまたはサブスクリプションによって共有されていないデータのパフォーマンスを最適化できます。 詳しくは、「 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」をご覧ください。  
  
-   複雑な結合フィルター階層を作成しない。  
  
     5 個以上のテーブルを使用した結合フィルターは、マージ処理中のパフォーマンスに大きく影響を与える可能性があります。 5 個以上のテーブルに結合フィルターを生成するような場合には、他の方法を検討することをお勧めします。  
  
    -   テーブルのフィルター選択で、プライマリ参照テーブル、より小さなテーブル、および変更されないテーブルは回避する。 これらのテーブルは、全体をパブリケーションの一部にしてください。 結合フィルターは、複数のサブスクライバーの間でパーティション分割する必要があるテーブル間のみで使用することをお勧めします。 詳しくは、「 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)」をご覧ください。  
  
    -   結合内に多数のテーブルが存在する場合は、データベース設計の正規化の低減、またはマッピング テーブルの使用を検討する。 たとえば、営業担当者が自分の担当する顧客のデータのみ必要なのに、1 人の顧客を 1 人の営業担当者に関連付けるために 6 個の結合が必要な場合は、顧客テーブルに営業担当者を識別する列を 1 つ追加することを検討してください。 この営業担当者データは冗長ですが、レプリケーションのパーティション分割のパフォーマンス向上は、テーブルの正規化が低減されたコストを何らかの形で上回る可能性があります。  
  
    -   バッチにデータ変更が多数含まれている場合に事前計算済みパーティションのパフォーマンスを向上させるには、アプリケーションを慎重に設計してください。 結合フィルターに含まれる親テーブル内のデータへの変更は、子テーブル内で対応する変更が生じる前に行う必要があります。  
  
-   ロジックで許容される場合は、 **join_unique_key** オプションに「 **1** 」を設定する。  
  
     このパラメーターを「 **1** 」に設定することによって、結合フィルター内の親テーブルと子テーブルのリレーションシップが一対一または一対多であることが指定されます。 一意性を保証する子テーブル内の列の結合についての制約がある場合にのみ、このパラメーターを「 **1** 」に設定します。 このパラメーターを誤って「 **1** 」に設定した場合は、データの未集約が発生する可能性があります。 詳しくは、「 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)」をご覧ください。  
  
-   事前計算済みパーティションを使用する場合は、多数の変更を含むバッチの実行を回避します。  
  
     多数のデータ変更を含むバッチを実行した後でマージ エージェントを実行すると、エージェントは大きいバッチを複数の小さいバッチに分割しようとします。 この処理の間に、他のマージ エージェントのプロセスがブロックされる可能性があります。 バッチ内の変更の数を減らしてから、バッチとバッチの間でマージ エージェントを実行することを検討してください。 この処理を実行できない場合は、パブリケーションの **generation_leveling_threshold** の値を大きくします。  
  
## <a name="subscription-considerations"></a>サブスクリプションに関する注意点  
  
-   サブスクリプションの同期スケジュールをずらす。  
  
     多数のサブスクライバーが 1 つのパブリッシャーと同期される場合、マージ エージェントが異なるタイミングで実行されるように、スケジュールをずらすことを検討してください。 詳細については、「 [Specify Synchronization Schedules](../../../relational-databases/replication/specify-synchronization-schedules.md)」を参照してください。  
  
## <a name="merge-agent-parameters"></a>マージ エージェントのパラメーター  
 マージ エージェントおよびそのパラメーターの詳細については、「 [Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)」を参照してください。  
  
-   プル サブスクリプションを行うすべてのサブスクライバーを [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンにアップグレードする。  
  
     サブスクライバーを [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンにアップグレードすることにより、そのサブスクライバーのサブスクリプションによって使用されるマージ エージェントが更新されます。 新しい機能の多くとパフォーマンスの最適化を利用するには、 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降のバージョンのマージ エージェントが必要です。  
  
-   サブスクリプションが高速接続を介して同期され、パブリッシャーおよびサブスクライバーから変更が送信される場合は、マージ エージェントに対して **-ParallelUploadDownload** パラメーターを使用する。  
  
     [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] で、新しいマージ エージェント パラメーターである **–ParallelUploadDownload**が導入されました。 このパラメーターを設定することによって、マージ エージェントはパブリッシャーにアップロードされた複数の変更およびサブスクライバーにダウンロードされた複数の変更を並列処理できるようになります。 これは、帯域幅が広いネットワークを使用している大容量環境において役立ちます。 エージェント パラメーターは、エージェント プロファイルおよびコマンド ラインで指定できます。 詳細については、以下をご覧ください。  
  
    -   [レプリケーション エージェント プロファイルの操作](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [レプリケーション エージェント コマンド プロンプト パラメーターを表示および変更する &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
-   特に同期でサブスクライバーにダウンロードするよりもサブスクライバーからダウンロードすることが多い場合は、 **-MakeGenerationInterval** パラメーターの値を大きくすることを検討する。  
  
-   LOB 列を含む行など、大量のデータを含むデータ行を同期すると、Web 同期から追加メモリの割り当てが要求され、パフォーマンスが低下する場合があります。 この動作は、マージ エージェントから生成された XML メッセージに、大量のデータを含むデータ行が過剰に含まれている場合に発生します。 マージ エージェントが Web 同期中に使用するリソースが多すぎる場合は、次のいずれかの方法を使用して、1 つのメッセージで送信される行の数を減らします。  
  
    -   マージ エージェントで低速リンク エージェント プロファイルを使用する。 詳しくは、「 [Replication Agent Profiles](../../../relational-databases/replication/agents/replication-agent-profiles.md)」をご覧ください。  
  
    -   マージ エージェントの **-DownloadGenerationsPerBatch** パラメーターと **-UploadGenerationsPerBatch** パラメーターの値を 10 未満に減らす。 これらのパラメーターの既定値は 50 です。  
  
## <a name="snapshot-considerations"></a>スナップショットに関する注意点  
  
-   初期スナップショットを生成する前に大きなテーブルに ROWGUIDCOL 列を作成する。  
  
     マージ レプリケーションでは、パブリッシュされた各テーブルに ROWGUIDCOL 列が必要です。 スナップショット エージェントが初期スナップショット ファイルを作成する際に ROWGUIDCOL 列があらかじめテーブルに作成されていない場合、エージェントはまず ROWGUIDCOL 列を作成し、追加しなくてはなりません。 マージ レプリケーションでスナップショットを生成および適用するときのパフォーマンスを向上させるには、テーブルをパブリッシュする前に各テーブルで ROWGUIDCOL 列を作成します。 列の名前は任意ですが (スナップショット エージェントは既定で**rowguid** を使用します)、以下のデータ型の特性を持つ必要があります。  
  
    -   UNIQUEIDENTIFIER のデータ型。  
  
    -   NEWSEQUENTIALID() または NEWID() の既定値。 変更および変更の追跡の際にパフォーマンスを向上させることができるため、NEWSEQUENTIALID() の使用をお勧めします。  
  
    -   ROWGUIDCOL プロパティ セット。  
  
    -   列の一意なインデックス。  
  
-   スナップショットを事前に生成するか、最初の同期時にサブスクライバーからスナップショットの生成および適用を要求できるようにする。  
  
     これらのオプションの両方またはどちらかを使用して、パラメーター化されたフィルターを使用するパブリケーションに対するスナップショットを提供します。 これらのオプションのどちらかを指定しないと、 **bcp** ユーティリティを使用するのではなく、一連の SELECT ステートメントおよび INSERT ステートメントを使用してサブスクリプションが初期化されます。この処理は、かなり低速で実行されます。 詳しくは、「 [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。  
  
## <a name="maintenance-and-monitoring-considerations"></a>メンテナンスおよび監視に関する注意点  
  
-   必要な場合、マージ レプリケーションのシステム テーブルのインデックスを再度作成する。  
  
     マージ レプリケーションのメンテナンスの一環として、マージ レプリケーションと関連するシステム テーブルが拡大しているかを時々確認してください(**MSmerge_contents**、**MSmerge_genhistory**、**MSmerge_tombstone**、**MSmerge_current_partition_mappings**、および **MSmerge_past_partition_mappings**)。 定期的にこれらのテーブルのインデックスを再設定します。 詳細については、「 [インデックスの再編成と再構築](../../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)」を参照してください。  
  
-   レプリケーション モニターの **[同期の履歴]** タブを使用して、同期のパフォーマンスを監視する。  
  
     マージ レプリケーションの場合、レプリケーション モニターの **[同期の履歴]** タブには、同期中に処理される各アーティクルの詳細な統計情報が表示されます。この統計には、各処理フェーズ (変更のアップロードやダウンロードなど) にかかる時間などが含まれます。 この情報によって、速度低下の原因となっているテーブルを特定することができます。マージ サブスクリプションのパフォーマンスに関するトラブルシューティングを、この情報から開始することをお勧めします。 詳細な統計情報を表示する方法について詳しくは、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。  
  
  
