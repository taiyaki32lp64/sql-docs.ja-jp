---
title: 分散型可用性グループとは
description: 分散型可用性グループは、2 つの異なる可用性グループにまたがるもので、特殊な種類の可用性グループです。 分散型可用性グループに参加する可用性グループは、同じ場所に存在している必要はありません。
ms.custom: seodec18
ms.date: 10/15/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], distributed
ms.assetid: ''
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ee844af9f851d1dab1d77c54dfdd04fadd4d3c06
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706223"
---
# <a name="distributed-availability-groups"></a>分散型可用性グループ
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
分散型可用性グループは、SQL Server 2016 で導入された新しい機能であり、既存の AlwaysOn 可用性グループ機能のバリエーションです。 この記事では、分散型可用性グループのいくつかの側面を明らかにし、既存の [SQL Server ドキュメント](https://docs.microsoft.com/sql/sql-server/)を補完します。

> [!NOTE]
> "DAG" は、Exchange のデータベース可用性グループ機能で既に使われているため、"*分散型可用性グループ*" の正式な省略形ではありません。 Exchange のこの機能は、SQL Server の可用性グループまたは分散型可用性グループとは関係がありません。

分散型可用性グループの構成方法については、「[分散型可用性グループを構成する](configure-distributed-availability-groups.md)」をご覧ください。

## <a name="understand-distributed-availability-groups"></a>分散型可用性グループについて理解する

分散型可用性グループは、2 つの異なる可用性グループにまたがるもので、特殊な種類の可用性グループです。 分散型可用性グループに参加する可用性グループは、同じ場所に存在している必要はありません。 物理、仮想、オンプレミス、パブリック クラウド、または可用性グループの配置をサポートする任意の場所のいずれでもかまいません。 これには、Linux と Windows でホストされている可用性グループの間などの、クロス ドメインおよびクロス プラットフォームが含まれます。 2 つの可用性グループが通信できる限り、それらで分散型可用性グループを構成できます。

従来の可用性グループには、WSFC クラスター内に構成されたリソースがあります。 分散型可用性グループでは、WSFC クラスター内には何も構成されません。 分散型可用性グループに関するすべてのものは、SQL Server 内に保持されます。 分散型可用性グループの情報を表示する方法については、「[Viewing distributed availability group information](#monitor-distributed-availability-group-health)」(分散可用性グループの情報を表示する) を参照してください。 

分散型可用性グループでは、基になる可用性グループにリスナーが存在する必要があります。 従来の可用性グループではスタンドアロン インスタンスに対して基になるサーバー名を指定しましたが (または、SQL Server フェールオーバー クラスター インスタンス (FCI) の場合は、ネットワーク名リソースに関連付けられた値)、分散型可用性グループでは、可用性グループを作成するときに ENDPOINT_URL パラメーターで分散型可用性グループに構成されているリスナーを指定します。 分散型可用性グループの基になる各可用性グループにはリスナーがありますが、分散型可用性グループにはリスナーはありません。

次の図では、それぞれが専用の WSFC クラスターに構成されている 2 つの可用性グループ (AG 1 および AG 2) にまたがる分散型可用性グループの概略を示します。 分散型可用性グループには、可用性グループごとに 2 つずつ、合計で 4 つのレプリカがあります。 可用性グループごとにレプリカの最大数までサポートできるため、分散型の可用性ではレプリカを最大合計 18 個まで所有することができます。


![分散型可用性グループの概要](./media/distributed-availability-group/dag-01-high-level-view-distributed-ag.png)

分散型可用性グループでのデータ移動は、同期または非同期として構成できます。 ただし、分散型可用性グループでのデータの移動は、従来の可用性グループと若干異なります。 各可用性グループにはプライマリ レプリカがありますが、挿入、更新、削除を受け付けることができるのは、分散型可用性グループに参加しているデータベースの 1 つのコピーだけです。 次の図に示すように、AG 1 はプライマリ可用性グループです。 AG 1 のプライマリ レプリカは、AG 1 のセカンダリ レプリカと AG 2 のプライマリ レプリカの両方にトランザクションを送信します。 AG 2 のプライマリ レプリカは、*フォワーダー*とも呼ばれます。 フォワーダーは、分散型可用性グループのセカンダリ可用性グループのプライマリ レプリカです。 フォワーダーは、プライマリ可用性グループ内のプライマリ レプリカからトランザクションを受信し、それを独自の可用性グループ内のセカンダリ レプリカに転送します。  そしてフォワーダーが、更新された AG 2 のセカンダリ レプリカを保持します。 

![分散型可用性グループとそのデータ移動](./media/distributed-availability-group/dag-02-distributed-ag-data-movement.png)

AG 2 のプライマリ レプリカが挿入、更新、削除を受け付けるようにする唯一の方法は、AG 1 から分散型可用性グループを手動でフェールオーバーすることです。 上の図で、AG 1 にはデータベースの書き込み可能なコピーが含まれるため、フェールオーバーを発行すると、AG 2 は挿入、更新、削除を処理できる可用性グループになります。 1 つの分散型可用性グループを別の分散型可用性グループにフェールオーバーする方法については、「[セカンダリ可用性グループにフェールオーバーする](configure-distributed-availability-groups.md#failover)」を参照してください。

> [!NOTE]
> SQL Server 2016 の分散型可用性グループは、FORCE_FAILOVER_ALLOW_DATA_LOSS オプションを使った可用性グループ間のフェールオーバーのみをサポートします。

> [!NOTE]
> 分散型可用性グループでトランザクション レプリケーションを使う場合、フォワーダー レプリカをパブリッシャーとして構成することはできません。

## <a name="sql-server-version-and-edition-requirements-for-distributed-availability-groups"></a>分散型可用性グループに関する SQL Server のバージョンとエディションの要件

SQL Server 2017 以降の分散型可用性グループでは、SQL Server の複数のメジャー バージョンを、同じ分散型可用性グループ内に混在させることができます。 読み取り/書き込みプライマリを含む AG は、同じバージョンでも、分散型 AG に参加している他の AR より低くてもかまいません。 他の AG は、同じバージョンか、それより高くてもかまいません。 このシナリオは、アップグレードおよび移行のシナリオを対象としたものです。 たとえば、読み取り/書き込みプライマリ レプリカを含む SQL Server 2016 の AG を、SQL Server 2017 以降にアップグレードまたは移行したい場合、分散型 AG に参加している他の AG を SQL Server 2017 で構成できます。

SQL Server 2012 または 2014 には分散型可用性グループ機能が存在しなかったため、これらのバージョンで作成された可用性グループは、分散型可用性グループに参加できません。 

> [!NOTE]
> 分散型可用性グループは、Standard Edition を使って構成したり、Standard Edition と Enterprise Edition を組み合わせて構成したりすることはできません。

2 つの異なる可用性グループが存在するため、分散型可用性グループに参加しているレプリカに Service Pack または累積更新プログラムをインストール プロセスは、従来の可用性グループと少し異なります。

1. 最初に、分散型可用性グループの第 2 の可用性グループのレプリカを更新します。

2. 分散型可用性グループのプライマリ可用性グループのレプリカに修正プログラムを適用します。

3. 標準的な可用性グループと同様に、プライマリ可用性グループを (第 2 の可用性グループのプライマリではなく) それ自体のレプリカの 1 つにフェールオーバーして、修正プログラムを適用します。 プライマリ以外のレプリカがない場合は、第 2 の可用性グループに手動でフェールオーバーする必要があります。

> [!NOTE]
> 将来のバージョンの SQL Server で以前のバージョンを同じ分散型可用性グループに参加させることができるようになるかどうかに関しては、何も発表されていません。 そのシナリオが有効になった場合は、分散型可用性グループを SQL Server のバージョン アップグレード計画に含めることができるようになります。

### <a name="windows-server-versions-and-distributed-availability-groups"></a>Windows Server のバージョンと分散型可用性グループ

分散型可用性グループには複数の可用性グループが含まれ、それぞれに独自の基になる WSFC クラスターがあり、分散型可用性グループは SQL Server 専用の構成です。  つまり、個々の可用性グループを含む WSFC クラスターは、Windows Server のメジャー バージョンが異なっていてもかまいません。 前のセクションで説明したように、SQL Server のメジャー バージョンは同じである必要があります。 次の図では AG 1 と AG 2 が分散型可用性グループに参加しており、最初の図とほとんど同じですが、各 WSFC クラスターの Windows Server のバージョンは異なっています。


![Windows Server のバージョンが異なる WSFC クラスターを含む分散型可用性グループ](./media/distributed-availability-group/dag-03-distributed-ags-wsfcs-different-versions-windows-server.png)

個々の WSFC クラスターとそれに対応する可用性グループは、従来の規則に従います。 つまり、ドメインに参加してもしなくてもかまいません (Windows Server 2016 以降)。 2 つの異なる可用性グループを 1 つの分散型可用性グループに結合するときは、4 つのシナリオがあります。

* 両方の WSFC クラスターが同じドメインに参加している。
* 各 WSFC クラスターが異なるドメインに参加している。
* 1 つの WSFC クラスターはドメインに参加しており、もう 1 つの WSFC クラスターはドメインに参加していない。
* どちらの WSFC クラスターもドメインに参加していない。

両方の WSFC クラスターが同じドメイン (信頼されていないドメイン) に参加している場合、分散型可用性グループを作成するときに特別なことを行う必要ありません。 可用性グループと WSFC クラスターが同じドメインに参加していない場合は、ドメインに依存しない可用性グループを作成する場合と同じように、証明書を使って分散型可用性グループを動作させる必要があります。 分散型可用性グループ用に証明書を構成する方法については、「[Create a domain-independent availability group](domain-independent-availability-groups.md)」(ドメインに依存しない可用性グループを作成する) のステップ 3 ～ 13 に従ってください。

分散型可用性グループでは、基になる各可用性グループのプライマリ レプリカが相互の証明書を持っている必要があります。 証明書を使わないエンドポイントが既にある場合は、[ALTER ENDPOINT](https://docs.microsoft.com/sql/t-sql/statements/alter-endpoint-transact-sql) を使って証明書を使うようにエンドポイントを再構成します。

## <a name="distributed-availability-group-usage-scenarios"></a>分散型可用性グループの使用シナリオ

分散型可用性グループには、次の 3 つの主な使用シナリオがあります。 

* [ディザスター リカバリーと簡単なマルチサイト構成](#disaster-recovery-and-multi-site-scenarios)
* [新しいハードウェアまたは構成への移行 (新しいハードウェアの使用、または基になるオペレーティング システムの変更が含まれる場合があります)](#migrate-by-using-a-distributed-availability-group)
* [複数の可用性グループを使うことによる、1 つの可用性グループの 8 個を超えた読み取り可能レプリカの数の拡張](#scale-out-readable-replicas-with-distributed-availability-groups)

### <a name="disaster-recovery-and-multi-site-scenarios"></a>ディザスター リカバリーとマルチサイトのシナリオ

従来の可用性グループではすべてのサーバーが同じ WSFC クラスターの一部である必要があり、複数のデータ センターを使うのが困難な場合があります。 次の図は、従来のマルチサイト可用性グループのアーキテクチャとデータ フローを示したものです。 1 つのプライマリ レプリカが、すべてのセカンダリ レプリカにトランザクションを送信しています。 この構成は、いくつかの点で分散型可用性グループよりも劣ります。 たとえば、Active Directory (該当する場合) や、WSFC クラスター内のクォーラムに対するミラーリング監視サーバーといったものを、実装する必要があります。 また、ノードの投票の変更など、WSFC クラスターの他の側面の考慮も必要になることがあります。

![従来のマルチサイト可用性グループ](./media/distributed-availability-group/dag-04-traditional-multi-site-ag.png)

分散型可用性グループでは、複数のデータ センターにまたがる可用性グループに対して、より柔軟な配置シナリオが提供されます。 [ログ配布]( https://docs.microsoft.com/sql/database-engine/log-shipping/about-log-shipping-sql-server)のような機能が、ディザスター リカバリーなどのシナリオで過去に使われていた場合でも、分散型可用性グループを使うことができます。 ただし、ログ配布とは異なり、分散型可用性グループではトランザクションの適用を遅延することはできません。 つまり、データが正しく更新または削除されないヒューマン エラーが発生した場合、可用性グループまたは分散型可用性グループでは役に立ちません。

分散型可用性グループは疎結合されていますが、この場合それは、分散型可用性グループは単一の WSFC クラスターを必要とせず、SQL Server によって保持されることを意味します。 WSFC クラスターは個別に保持され、同期は主に 2 つの可用性グループの間で非同期に行われるため、別のサイトにディザスター リカバリーを構成するのが簡単になります。 各可用性グループのプライマリ レプリカは、独自のセカンダリ レプリカを同期します。

* 分散型可用性グループに対しては、手動フェールオーバーのみがサポートされています。 データ センターを切り替えるディザスター リカバリーの場合、(まれなケースを除き) 自動フェールオーバーを構成することはできません。 
* 多くの場合は、マルチサイトまたはサブネットの WSFC クラスターでは従来の項目またはパラメーター (CrossSubnetThreshold など) の一部を設定する必要はありませんが、データ転送の異なるレイヤーでのネットワーク待機時間に注意する必要があります。 違いは、各 WSFC クラスターは独自の可用性を維持しており、クラスターは 4 ノードの 1 つの大きなエンティティではないということです。 前の図で示したように、2 つの独立した 2 ノード WSFC クラスターで構成されます。  
* ディザスター リカバリーを目的とするアプローチである非同期データ移動を使うことをお勧めします。
* プライマリ レプリカと第 2 の可用性グループの少なくとも 1 つのセカンダリ レプリカの間に同期データ移動を構成し、分散型可用性グループに同期移動を構成した場合、分散型可用性グループはすべての同期コピーでデータの存在が確認されるまで待機します。

### <a name="migrate-by-using-a-distributed-availability-group"></a>分散型可用性グループを使って移行する

分散型可用性グループは 2 つのまったく異なる可用性グループの構成をサポートするため、ディザスター リカバリーとマルチサイトのシナリオだけでなく、移行のシナリオも容易になります。 移行先が新しいハードウェアか仮想マシン (オンプレミスまたはパブリック クラウドの IaaS) かに関係なく、分散型可用性グループを構成すると、以前はバックアップ、コピー、復元またはログ配布を使っていたような状況で、移行を行うことができます。 

移行の機能は、SQL Server を同じバージョンにしたまま基になる OS を変更またはアップグレードするシナリオで特に便利です。 Windows Server 2016 では、同じハードウェア上で Windows Server 2012 R2 からローリング アップグレードできますが、ほとんどのユーザーは新しいハードウェアまたは仮想マシンの配置を選びます。 

新しい構成への移行を完了するには、プロセスの最後に、元の可用性グループへのすべてのデータ トラフィックを停止し、分散型可用性グループを同期データ移動に変更します。 これにより、第 2 の可用性グループのプライマリ レプリカが完全に同期され、データが失われないことが保証されます。 同期を確認した後、セカンダリ可用性グループに分散型可用性グループをフェールオーバーします。 詳細については、「[セカンダリ可用性グループにフェールオーバーする](configure-distributed-availability-groups.md#failover)」を参照してください。

移行後には、第 2 の可用性グループが新しいプライマリ可用性グループになり、次のいずれかを行うことが必要な場合があります。

* セカンダリ可用性グループのリスナーの名前を変更するか (および、場合によっては、元のプライマリ可用性グループの古いリスナーを削除または名前変更します)、または元のプライマリ可用性グループ のリスナーで再作成して、アプリケーションとユーザーが新しい構成にアクセスできるようにします。
* 名前の変更または再作成が不可能な場合は、アプリケーションおよびユーザーが第 2 の可用性グループのリスナーを参照するようにします。

### <a name="scale-out-readable-replicas-with-distributed-availability-groups"></a>分散型可用性グループで読み取り可能レプリカをスケールアウトする

必要に応じて、1 個の分散型可用性グループで最大 16 個のセカンダリ レプリカを持つことができます。 したがって、別の可用性グループの 2 個のプライマリ レプリカを含めて、最大 18 個のコピーを読み取りに使うことができます。 つまり、このアプローチでは、複数のサイトがレポートのためにさまざまなアプリケーションにほぼリアルタイムでアクセスできます。

分散型可用性グループは、読み取り専用ファームを複数の可用性グループにスケールアウトするのに役立ちます。 分散型可用性グループでは、2 つの方法で読み取り可能レプリカをスケールアウトできます。

* 分散型可用性グループの第 2 の可用性グループのプライマリ レプリカを使って、別の分散型可用性グループを作成できます (データベースが RECOVERY ではない場合でも)。
* また、1 番目の可用性グループのプライマリ レプリカを使って、別の分散型可用性グループを作成することもできます。

つまり、1 つのプライマリ レプリカが、2 つの異なる分散型可用性グループに参加できます。 次の図では、AG 1 と AG 2 はどちらも分散型 AG 1 に参加しており、AG 2 と AG 3 は分散型 AG 2 に参加しています。 AG 2 のプライマリ レプリカ (フォワーダー) は、分散型 AG 1 のセカンダリ レプリカであると同時に、分散型 AG 2 のプライマリ レプリカでもあります。

![分散型可用性グループでの読み取りのスケールアウト](./media/distributed-availability-group/dag-05-scaling-out-reads-with-distributed-ags.png)

次の図の AG 1 は、次の 2 つの異なる分散型可用性グループのプライマリ レプリカになっています:分散型 AG 1 (AG 1 と AG2 で構成) および分散型 AG 2 (AG 1 と AG 3 で構成)。


![分散型可用性グループを使った読み取りのスケールアウトのもう 1 つの例]( ./media/distributed-availability-group/dag-06-another-scaling-out-reads-using-distributed-ags-example.png)


上のどちらの例でも、3 つの可用性グループ全体で最大 27 個のレプリカを持つことができ、そのすべてを読み取り専用クエリに使うことができます。 

[読み取り専用ルーティング]( https://docs.microsoft.com/sql/database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server)は、分散型可用性グループでは正しく動作しません。 より詳細な情報:

1. 読み取り専用ルーティングを構成することができ、分散型可用性グループのプライマリ可用性グループに対して動作します。 
2. 読み取り専用ルーティングを構成できますが、分散型可用性グループのセカンダリ可用性グループには動作しません。 すべてのクエリがリスナーを使ってセカンダリ可用性グループに接続する場合は、セカンダリ可用性グループのプライマリ レプリカに移動します。 それ以外の場合は、各レプリカがすべての接続をセカンダリ レプリカとして許可し、それらに直接アクセスするように、構成する必要があります。 ただし、フェールオーバー後に、セカンダリ可用性グループがプライマリになっている場合は、読み取り専用ルーティングは動作します。 この動作は、SQL Server 2016 の更新プログラムまたは SQL Server の将来のバージョンで、変更される可能性があります。


## <a name="initialize-secondary-availability-groups-in-a-distributed-availability-group"></a>分散型可用性グループのセカンダリ可用性グループを初期化する

分散型可用性グループは、第 2 の可用性グループのプライマリ レプリカを初期化するための主要な方法として[自動シード処理](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group)を使うように設計されています。 第 2 の可用性グループのプライマリ レプリカでの完全なデータベース復元は、次のようにすることで可能です。

1. WITH NORECOVERY を指定してデータベース バックアップを復元します。
2. 必要な場合は、適切なトランザクション ログ バックアップを WITH NORECOVERY で復元します。
3. データベース名を指定せず、SEEDING_MODE を AUTOMATIC に設定して、第 2 の可用性グループを作成します。
4. 自動シード処理を使って、分散型可用性グループを作成します。

分散型可用性グループに第 2 の可用性グループのプライマリ レプリカを追加すると、レプリカは第 1 の可用性グループのプライマリ データベースと照合され、シード処理はソースに合わせてデータベースを更新します。 いくつかの注意事項があります。

* 第 2 の可用性グループのプライマリ レプリカの `sys.dm_hadr_automatic_seeding` で示される出力では、`current_state` が FAILED、理由が "Seeding Check Message Timeout" と表示されます。

* 第 2 の可用性グループのプライマリ レプリカの現在の SQL Server ログでは、シード処理が行われて、[LSN](https://docs.microsoft.com/sql/relational-databases/sql-server-transaction-log-architecture-and-management-guide) が同期されたと表示されます。

* 第 1 の可用性グループのプライマリ レプリカの `sys.dm_hadr_automatic_seeding` で示される出力では、current_state が COMPLETED と表示されます。 

* 分散型可用性グループではシード処理の動作も異なります。 第 2 のレプリカでシード処理が開始するためには、レプリカで `ALTER AVAILABILITY GROUP [AGName] GRANT CREATE ANY DATABASE` コマンドを実行する必要があります。 この条件は基になる可用性グループに参加しているすべてのセカンダリ レプリカにやはり当てはまりますが、第 2 の可用性グループのプライマリ レプリカは、分散型可用性グループに追加された後でシード処理が開始するために必要な適切なアクセス許可を既に持っています。 

## <a name="monitor-distributed-availability-group-health"></a>分散型可用性グループの正常性を監視する

分散型可用性グループは SQL Server のみの構成であり、基になる WSFC クラスターでは認識されません。 次の図の 2 つの異なる WSFC クラスター (CLUSTER_A と CLUSTER_B) は、それぞれが独自の可用性グループを持っています。 ここでは、CLUSTER_A の AG1 と CLUSTER_B の AG2 についてのみ説明します。 

[PowerShell Get-ClusterGroup コマンドを使用する可用性グループが複数ある 2 つの WSFC クラスター](./media/distributed-availability-group/dag-07-two-wsfcs-multiple-ags-through-get-clustergroup-command.png)


```
PS C:\> Get-ClusterGroup -Cluster CLUSTER_A

Name                            OwnerNode             State
----                            ---------             -----
AG1                             DENNIS                Online
Available Storage               GLEN                  Offline
Cluster Group                   JY                    Online
New_RoR                         DENNIS                Online
Old_RoR                         DENNIS                Online
SeedingAG                       DENNIS                Online


PS C:\> Get-ClusterGroup -Cluster CLUSTER_B

Name                            OwnerNode             State
----                            ---------             -----
AG2                             TOMMY                 Online
Available Storage               JC                    Offline
Cluster Group                   JC                    Online
```

分散型可用性グループの詳細情報は、SQL Server の特に可用性グループの動的管理ビューに表示されます。 現在のところ、分散型可用性グループについて SQL Server Management Studio に表示される情報は、可用性グループのプライマリ レプリカについてのみです。 以下の図のように、SQL Server Management Studio の [可用性グループ] フォルダーに分散型可用性グループが表示されます。 この図では、分散型可用性グループではなく、そのインスタンスでローカルの各可用性グループのプライマリ レプリカとして AG1 が表示されます。

![分散型可用性グループの最初の WSFC クラスター上のプライマリ レプリカが表示された SQL Server Management Studio のビュー](./media/distributed-availability-group/dag-08-view-smss-primary-replica-first-wsfc-distributed-ag.png)


ただし、分散型可用性グループを右クリックしても使用できるオプションが表示されません (次の図を参照)。また、[可用性データベース]、[可用性グループ リスナー]、[可用性レプリカ] の各フォルダーを展開してもすべて空です。 SQL Server Management Studio 16 ではこの結果が表示されますが、今後のバージョンの SQL Server Management Studio では変更される可能性があります。

![操作できるオプションがありません](./media/distributed-availability-group/dag-09-no-options-available-action.png)

次の図のように、セカンダリ レプリカの場合、分散型可用性グループに関連する情報が SQL Server Management Studio に表示されません。 これらの可用性グループ名は、前述の「CLUSTER_A WSFC クラスター」図に表示されるロールにマップされます。

![SQL Server Management Studio のセカンダリ レプリカのビュー](./media/distributed-availability-group/dag-10-view-ssms-secondary-replica.png)

### <a name="dmv-to-list-all-availability-replica-names"></a>すべての可用性レプリカ名を一覧表示する DMV

動的管理ビューを使用する場合にも同じ概念が適用されます。 次のクエリを使用すると、すべての可用性グループ (通常と分散型) とそれに参加しているノードが表示されます。 この結果は、分散型可用性グループに参加しているいずれかの WSFC クラスター内のプライマリ レプリカに対してクエリを実行した場合にのみ表示されます。 動的管理ビュー `sys.availability_groups` には、`is_distributed` という新しい列があります。可用性グループが分散型可用性グループの場合、これは 1 です。 この列を表示するには:

```sql
-- shows replicas associated with availability groups
SELECT 
   ag.[name] AS [AG Name], 
   ag.Is_Distributed, 
   ar.replica_server_name AS [Replica Name]
FROM sys.availability_groups AS ag 
INNER JOIN sys.availability_replicas AS ar       
   ON ag.group_id = ar.group_id
GO
```

次の図は、分散型可用性グループに参加している 2 つ目の WSFC クラスターの出力例です。 SPAG1 は、次の 2 つのレプリカで構成されています:DENNIS と JY。 一方、SPDistAG という分散型可用性グループには、従来の可用性グループのようにインスタンス名ではなく、2 つの参加している可用性グループ (SPAG1 と SPAG2) の名前が表示されます。 

![上記のクエリの出力例](./media/distributed-availability-group/dag-11-example-output-of-query-above.png)

### <a name="dmv-to-list-distributed-ag-health"></a>分散型 AG の正常性を一覧表示する DMV

SQL Server Management Studio で、ダッシュボードや他の領域に表示される状態は、その可用性グループ内のローカル同期についてのみです。 分散型可用性グループの正常性を表示するには、動的管理ビューに対してクエリを実行します。 次のクエリ例では、前のクエリを拡張して改善しています。

```sql
-- shows sync status of distributed AG
SELECT 
   ag.[name] AS [AG Name], 
   ag.is_distributed, 
   ar.replica_server_name AS [Underlying AG], 
   ars.role_desc AS [Role], 
   ars.synchronization_health_desc AS [Sync Status]
FROM  sys.availability_groups AS ag
INNER JOIN sys.availability_replicas AS ar 
   ON  ag.group_id = ar.group_id        
INNER JOIN sys.dm_hadr_availability_replica_states AS ars       
   ON  ar.replica_id = ars.replica_id
WHERE ag.is_distributed = 1
GO
```
       
       
![分散型可用性グループの状態](./media/distributed-availability-group/dag-12-distributed-ag-status.png)

### <a name="dmv-to-view-underlying-performance"></a>基になるパフォーマンスを表示する DMV

前のクエリをさらに拡張するために、`sys.dm_hadr_database_replicas_states` に追加して、動的管理ビューで基となるパフォーマンスを表示することもできます。 現在、動的管理ビューはセカンダリ可用性グループの情報のみを保存しています。 次のクエリ例は、プライマリ可用性グループ上で実行し、以下の出力例を生成します。

```sql
-- shows underlying performance of distributed AG
SELECT 
   ag.[name] AS [Distributed AG Name], 
   ar.replica_server_name AS [Underlying AG], 
   dbs.[name] AS [Database],
   ars.role_desc AS [Role],
   drs.synchronization_health_desc AS [Sync Status],
   drs.log_send_queue_size,
   drs.log_send_rate, 
   drs.redo_queue_size, 
   drs.redo_rate
FROM sys.databases AS dbs
INNER JOIN sys.dm_hadr_database_replica_states AS drs
   ON dbs.database_id = drs.database_id
INNER JOIN sys.availability_groups AS ag
   ON drs.group_id = ag.group_id
INNER JOIN sys.dm_hadr_availability_replica_states AS ars
   ON ars.replica_id = drs.replica_id
INNER JOIN sys.availability_replicas AS ar
   ON ar.replica_id = ars.replica_id
WHERE ag.is_distributed = 1
GO
```


![分散型可用性グループのパフォーマンス情報](./media/distributed-availability-group/dag-13-performance-information-distributed-ag.png)

### <a name="dmv-to-view-performance-counters-for-distributed-ag"></a>分散型 AG のパフォーマンス カウンターを表示する DMV
次のクエリでは、分散型可用性グループに特別に関連付けられているパフォーマンス カウンターが表示されます。 


 ```sql
 -- displays OS performance counters related to the distributed ag named 'distributedag'
 SELECT * FROM sys.dm_os_performance_counters WHERE instance_name LIKE '%distributed%'
 ```

 ![DAG の OS パフォーマンス カウンターを表示する DMV](./media/distributed-availability-group/dmv-os-performance-counters.png)


 >[!NOTE]
 >`LIKE` フィルターに分散型可用性グループの名前を指定する必要があります。 この例で、分散型可用性グループの名前は 'distributedag' です。 分散型可用性グループの名前を反映するように `LIKE` 修飾子を変更します。  

### <a name="dmv-to-display-health-of-both-ag-and-distributed-ag"></a>AG と分散型 AG の両方の正常性を表示する DMV
次のクエリでは、可用性グループと分散型可用性グループ両方の正常性に関するさまざまな情報が表示されます。 [Tracy Boggiano さん、ありがとうございます](https://tracyboggiano.com/archive/2017/11/distributed-availability-groups-setup-and-monitoring/)

 ```sql
 -- displays sync status, send rate, and redo rate of availability groups, including distributed AG
 SELECT 
        ag.name AS 'AG Name', 
        ag.is_distributed, 
        ar.replica_server_name AS 'AG', 
        dbs.name AS 'Database',
    ars.role_desc, 
    drs.synchronization_health_desc, 
    drs.log_send_queue_size, 
    drs.log_send_rate, 
    drs.redo_queue_size, 
    drs.redo_rate,
    drs.suspend_reason_desc,
    drs.last_sent_time,
    drs.last_received_time,
    drs.last_hardened_time,
    drs.last_redone_time,
    drs.last_commit_time,
    drs.secondary_lag_seconds
 FROM sys.databases dbs 
 INNER JOIN sys.dm_hadr_database_replica_states drs 
    ON dbs.database_id = drs.database_id
 INNER JOIN sys.availability_groups ag 
    ON drs.group_id = ag.group_id
 INNER JOIN sys.dm_hadr_availability_replica_states ars 
    ON ars.replica_id = drs.replica_id
 INNER JOIN sys.availability_replicas ar 
    ON ar.replica_id =  ars.replica_id
 --WHERE ag.is_distributed = 1
 GO
 ```

![AG と分散型 AG の正常性](./media/distributed-availability-group/dmv-sync-status-send-rate.png)

### <a name="dmvs-to-view-metadata-of-distributed-ag"></a>分散型 AG のメタデータを表示する DMV
次のクエリでは、分散型可用性グループを含め、可用性グループが使用しているエンドポイント URL に関する情報が表示されます。  [David Barbarin さん、ありがとうございます](https://blog.dbi-services.com/sql-server-2016-alwayson-distributed-availability-groups/)



 ```sql
 -- shows endpoint url and sync state for ag, and dag
 SELECT
    ag.name AS group_name,
    ag.is_distributed,
    ar.replica_server_name AS replica_name,
    ar.endpoint_url,
    ar.availability_mode_desc,
    ar.failover_mode_desc,
    ar.primary_role_allow_connections_desc AS allow_connections_primary,
    ar.secondary_role_allow_connections_desc AS allow_connections_secondary,
    ar.seeding_mode_desc AS seeding_mode
 FROM sys.availability_replicas AS ar
 JOIN sys.availability_groups AS ag
    ON ar.group_id = ag.group_id
 GO
 ```


![分散型 AG のメタデータ DMV](./media/distributed-availability-group/dmv-metadata-dag2.png)



### <a name="dmv-to-show-current-state-of-seeding"></a>シード処理の現在の状態を表示する DMV
次のクエリでは、シード処理の現在の状態に関する情報が表示されます。 このクエリは、レプリカ間の同期エラーを解決するために役立ちます。 [David Barbarin さんに改めて感謝](https://blog.dbi-services.com/sql-server-2016-alwayson-distributed-availability-groups/)

 ```sql
 -- shows current_state of seeding 
 SELECT
    ag.name AS aag_name,
    ar.replica_server_name,
    d.name AS database_name,
    has.current_state,
    has.failure_state_desc AS failure_state,
    has.error_code,
    has.performed_seeding,
    has.start_time,
    has.completion_time,
    has.number_of_attempts
 FROM sys.dm_hadr_automatic_seeding AS has
 JOIN sys.availability_groups AS ag
    ON ag.group_id = has.ag_id
 JOIN sys.availability_replicas AS ar
    ON ar.replica_id = has.ag_remote_replica_id
 JOIN sys.databases AS d
    ON d.group_database_id = has.ag_db_id
 GO
 ```


![シード処理の現在の状態](./media/distributed-availability-group/dmv-seeding.png)




### <a name="next-steps"></a>次の手順 

* [可用性グループ ウィザードの使用 (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

* [[新しい可用性グループ] ダイアログ ボックスの使用 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
* [Transact-SQL での可用性グループの作成](create-an-availability-group-transact-sql.md)
