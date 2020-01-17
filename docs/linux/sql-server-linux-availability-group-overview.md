---
title: SQL Server on Linux の可用性グループ
description: SQL Server on Linux の Always On 可用性グループの特徴について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 04/17/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.openlocfilehash: e4979fbb4e2dbbccf7ed11b744051373b0750d1f
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558638"
---
# <a name="always-on-availability-groups-on-linux"></a>Linux 上の AlwaysOn 可用性グループ

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux ベースの [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] インストールでの、Always On 可用性グループ (AG) の特性について説明します。 また、Linux ベースの AG と、Windows Server フェールオーバー クラスター (WSFC) ベースの AG の違いについても説明します。 AG の基本については、[Windows ベースのドキュメント](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)を参照してください (WSFC を除き、AG は Windows 上でも Linux 上でも同様に機能します)。

全体的に見ると、Linux 上の [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] の可用性グループは、WSFC ベースの実装で使用する場合と同様に機能します。 つまり、制限事項や機能は基本的に同じですが、いくつかの例外があります。 主な違いは次のとおりです。

-   SQL Server 2017 CU16 以降では、Linux で Microsoft 分散トランザクション コーディネーター (DTC) がサポートされています。 ただし、Linux 上の可用性グループでは DTC はまだサポートされていません。 アプリケーションで分散トランザクションを使用する必要があり、AG が必要な場合は、Windows 上で [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] をデプロイしてください。
-   高可用性を必要とする Linux ベースのデプロイでは、クラスタリングに WSFC ではなく Pacemaker が使われます。
-   Windows 上の AG のほとんどの構成 (ワークグループクラスターのシナリオを除く) とは異なり、Pacemaker では Active Directory Domain Services (AD DS) が必要とされることはありません。
-   1 つのノードから別のノードに AG をフェールオーバーする方法は、Linux と Windows で異なります。
-   特定の設定 (`required_synchronized_secondaries_to_commit` など) は、Linux 上の Pacemaker を使用してのみ変更できます。一方、WSFC ベースのインストールでは Transact-SQL を使用します。

## <a name="number-of-replicas-and-cluster-nodes"></a>レプリカとクラスター ノードの数

[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] 内の AG には、2 つのレプリカを含めることができます。1 つはプライマリ、もう 1 つは可用性の目的にのみ使用できます。 他の目的 (読み取り可能なクエリなど) には使用できません。 [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] 内の AG は、最大 9 個のレプリカを持つことができます。1 つのプライマリと最大 8 つのセカンダリで構成し、最大 3 つ (プライマリを含む) を同期できます。 基になるクラスターを使用している場合で、Corosync が使用されている場合には、最大で 16 個のノードを使用できます。 可用性グループでは、[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] なら 16 ノードのうち最大 9 ノードを使用でき、[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] なら 2 ノードまで使用できます。

レプリカ 2 個の構成で、別のレプリカに自動的にフェールオーバーする機能が必要な場合は、構成専用レプリカを使用する必要があります (「[構成専用レプリカとクォーラム](#configuration-only-replica-and-quorum)」で説明されています)。 構成専用レプリカは [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] Cumulative Update 1 (CU1) で導入されたので、このバージョンが、この構成用にデプロイできる最低のバージョンになります。

Pacemaker が使用されている場合は、その実行を維持できるように適切に構成する必要があります。 つまり、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] の要件 (構成専用レプリカなど) に加えて、Pacemaker の観点からクォーラムと STONITH を適切に実装する必要があります。

読み取り可能なセカンダ リレプリカは、[!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] でのみサポートされます。

## <a name="cluster-type-and-failover-mode"></a>クラスターの種類とフェールオーバー モード

[!INCLUDE[sssql17-md](../includes/sssql17-md.md)] では、AG のクラスターの種類が新たに導入されました。 Linux の場合、有効な値は次の 2 つです。External と None。 "External" というクラスターの種類は、AG の下で Pacemaker が使用されることを意味します。 クラスターの種類として External を使用するには、フェールオーバー モードも External に設定する必要があります (これも [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] の新機能です)。 自動フェールオーバーはサポートされていますが、WSFC とは異なり、Pacemaker が使用されている場合はフェールオーバー モードが (自動ではなく) External に設定されます。 WSFC とは異なり、AG の Pacemaker 部分は AG の構成後に作成されます。

クラスターの種類が None の場合は、Pacemaker に対する要件がない (AG でも使用されない) ことを意味します。 Pacemaker が構成されているサーバー上でも、クラスターの種類を None にして AG が構成されている場合、Pacemaker ではその AG は表示されず、管理もされません。 クラスターの種類が None の場合は、プライマリからセカンダリ レプリカへの手動フェールオーバーのみがサポートされます。 None で作成された AG は、主に読み取りスケールアウトのシナリオやアップグレードに使用されます。 ディザスター リカバリーやローカルの可用性など、自動フェールオーバーを必要としないシナリオでも機能しますが、推奨はされません。 リスナーの取り扱いも、Pacemaker を使わない場合より複雑になります。

クラスターの種類は、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 動的管理ビュー (DMV) `sys.availability_groups`の `cluster_type` と `cluster_type_desc` の列に格納されます。

## <a name="required_synchronized_secondaries_to_commit"></a>required\_synchronized\_secondaries\_to\_commit

[!INCLUDE[sssql17-md](../includes/sssql17-md.md)] では、AG によって使用される、`required_synchronized_secondaries_to_commit` という設定が新たに導入されました。 これは、プライマリと同期する必要があるセカンダリ レプリカの数を AG に伝えるためのものです。 これにより、自動フェールオーバー などの処理が可能になります (クラスターの種類を External にして Pacemaker と統合されている場合のみ)。また、適切な数のセカンダリ レプリカがオンラインまたはオフラインの場合に、プライマリの可用性などに関する動作を制御できるようになります。 このしくみの詳細については、「[可用性グループの構成の高可用性とデータの保護](sql-server-linux-availability-group-ha.md)」を参照してください。 `required_synchronized_secondaries_to_commit` の値は既定で設定され、Pacemaker/ [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] によって管理されます。 この値は手動でオーバーライドできます。

`required_synchronized_secondaries_to_commit` と新しいシーケンス番号 (`sys.availability_groups` に格納されます) の組み合わせにより、たとえば、自動フェールオーバーを実行できることが Pacemaker と [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] に通知されます。 その場合、セカンダリ レプリカはプライマリと同じシーケンス番号を持っていることになります。つまり、最新の構成情報がすべて含まれた状態であるということです。

`required_synchronized_secondaries_to_commit` に設定できる値は、次の 3 つです。0、1、2 のいずれか。 これらの値によって、レプリカが使用できなくなったときの動作が制御されます。 これらの数は、プライマリと同期する必要があるセカンダリ レプリカの数に対応しています。 Linux では、動作は次のようになります。

-   0 - セカンダ リレプリカがプライマリと同期された状態である必要はありません。 ただし、セカンダリが同期されていない場合、自動フェールオーバーは行われません。 
-   1 - 1 つのセカンダリ レプリカがプライマリと同期された状態である必要があります。自動フェールオーバーが可能です。 プライマリ データベースは、セカンダリの同期レプリカが使用可能になるまで使用できません。
-   2 - 3 ノード以上の AG 構成内にある両方のセカンダリ レプリカが、プライマリと同期されている必要があります。自動フェールオーバーが可能です。

`required_synchronized_secondaries_to_commit` は、同期レプリカを使用したフェールオーバーの動作だけでなく、データ損失も制御します。 値が 1 または 2 の場合、セカンダリ レプリカは常に同期されていることを要求されるため、常にデータの冗長性が確保されます。 つまり、データ損失は発生しません。

`required_synchronized_secondaries_to_commit` の値を変更するには、次の構文を使用します。

>[!NOTE]
>値を変更すると、リソースが再起動されます。つまり、短時間停止します。 これを回避する唯一の方法は、リソースが一時的にクラスターによって管理されないように設定することです。

**Red Hat Enterprise Linux (RHEL) と Ubuntu**

```bash
sudo pcs resource update <AGResourceName> required_synchronized_secondaries_to_commit=<Value>
```

**SUSE Linux Enterprise Server (SLES)**

```bash
sudo crm resource param ms-<AGResourceName> set required_synchronized_secondaries_to_commit <value>
```

ここで、*AGResourceName* は AG 用に構成されているリソースの名前で、*Value* は 0、1、または 2 です。 パラメーターを管理する Pacemaker の既定の設定に戻すには、値を指定せずに同じステートメントを実行します。

次の条件が満たされている場合は、AG の自動フェールオーバーが可能です。

-   プライマリ レプリカとセカンダリ レプリカが、同期データ移動に設定されている。
-   セカンダリが (同期中ではなく) 同期済みの状態である。つまり、2 つが同じデータ ポイントにある。
-   クラスターの種類が External に設定されている。 クラスターの種類が None の場合、自動フェールオーバーは実行できません。
-   プライマリになるセカンダリ レプリカの `sequence_number` が、最大のシーケンス番号になっている。つまり、セカンダリ レプリカの `sequence_number` が、元のプライマリ レプリカの番号と一致している。

これらの条件が満たされている場合、プライマリ レプリカをホストしているサーバーで障害が発生すると、AG は所有者を同期レプリカに変更します。 同期レプリカ (1 つのプライマリ レプリカと 2 つのセカンダリ レプリカで合計 3 つ) の動作は、`required_synchronized_secondaries_to_commit` によってさらに制御することができます。 この設定は、Windows と Linux の両方で AG と連携しますが、構成の方法はまったく異なります。 Linux の場合、この値は AG リソース自体のクラスターによって自動的に構成されます。

## <a name="configuration-only-replica-and-quorum"></a>構成専用レプリカとクォーラム

[!INCLUDE[sssql17-md](../includes/sssql17-md.md)] CU1 では、構成専用レプリカも新しく導入されました。 Pacemaker は WSFC とは異なり、特にクォーラムと STONITH の使用に関しては大きく異なるため、2 ノードのみの構成では AG との連携が機能しません。 FCI については、Pacemaker で提供されるクォーラム メカニズムで問題ありません。これは、 FCI のフェールオーバーのアービトレーションがすべてクラスター レイヤーで行われるためです。 AG の場合、Linux でのアービトレーションは、すべてのメタデータが格納されている [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 内で発生します。 そこで必要となるのが、構成専用レプリカです。

3 つ目のノードと、少なくとも 1 つの同期されたレプリカがどうしても必要となります。 構成専用レプリカは、AG 構成内の他のレプリカと同じように、AG 構成を master データベースに格納します。 構成専用レプリカでは、AG に参加しているユーザー データベースは保持されません。 構成データは、プライマリから同期的に送信されます。 この構成データは、自動か手動かにかかわらず、フェールオーバー中に使用されます。

AG でクォーラムを維持し、External のクラスターについて自動フェールオーバーを有効にするには、次のいずれかの条件を満たす必要があります。

-   3 つの同期レプリカがある ([!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] のみ)。または
-   2 つのレプリカ (プライマリとセカンダリ) と、構成専用レプリカがある。

手動フェールオーバーは、AG 構成に使用しているクラスターの種類が External か None かにかかわらず実行できます。 構成専用レプリカは、クラスターの種類が None の AG でも構成できますが、デプロイが複雑になるため推奨されません。 そのように構成する場合は、値が少なくとも 1 になるように `required_synchronized_secondaries_to_commit` を手動で変更して、同期されたレプリカが少なくとも 1 つ存在するようにしてください。

構成専用レプリカは、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] の任意のエディション ([!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)] を含む) でホストできます。 そのため、ライセンス コストを最小限に抑えつつ、[!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] の AG で動作させることができます。 つまり、3 つ目の必須サーバーでは、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] の最小の仕様を満たすだけで済みます (AG のユーザー トランザクション トラフィックを受信しないため)。

構成専用レプリカを使用する場合、その動作は次のようになります。

-   既定では、`required_synchronized_secondaries_to_commit` は 0 に設定されています。 これは、必要に応じて手動で 1 に変更できます。
-   プライマリで障害が発生し、`required_synchronized_secondaries_to_commit` が 0 の場合は、セカンダリ レプリカが新しいプライマリになり、読み取りと書き込みの両方に使用できるようになります。 値が 1 の場合は、自動フェールオーバーが実行されますが、他のレプリカがオンラインになるまで新しいトランザクションは受け入れられません。
-   セカンダリ レプリカで障害が発生し、`required_synchronized_secondaries_to_commit` が 0 の場合、プライマリ レプリカは引き続きトランザクションを受け入れますが、その時点でプライマリ レプリカに障害が発生した場合は、セカンダリ レプリカが使用できないため、データ保護もフェールオーバーも (手動と自動のいずれを問わず) 提供されません。
-   構成専用レプリカで障害が発生した場合、AG は正常に機能しますが、自動フェールオーバーは実行できません。
-   同期セカンダリ レプリカと構成専用レプリカの両方で障害が発生した場合、プライマリはトランザクションを受け付けることができず、プライマリからのフェイルオーバー先もなくなります。

CU1 では、`mssql-server-ha` によって生成される corosync.log ファイルのログに既知のバグがあります。 使用可能なレプリカの数が原因でセカンダリ レプリカがプライマリになることができない場合、現在のメッセージは "1 つのシーケンス番号を受け取る必要がありましたが、2 つしか受信されませんでした。 ローカル レプリカを安全に昇格させるための十分なレプリカがオンラインになっていません。" これらの数は逆にする必要があります。正しいメッセージは次のとおりです: "2 つのシーケンス番号を受け取る必要がありましたが、1 つしか受信されませんでした。 ローカル レプリカを安全に昇格させるための十分なレプリカがオンラインになっていません。" 

## <a name="multiple-availability-groups"></a>複数の可用性グループ 

AG は、Pacemaker クラスターまたは一連のサーバーごとに複数作成できます。 唯一の制限は、システム リソースです。 AG の所有権はマスターによって示されます。 複数の AG を異なるノードで所有することもできます。それらがすべて同じノードで実行されている必要はありません。

## <a name="drive-and-folder-location-for-databases"></a>データベースのドライブとフォルダーの場所

Windows ベースの AG の場合と同様に、AG に参加しているユーザー データベースのドライブとフォルダーの構造は同じである必要があります。 たとえば、ユーザー データベースがサーバー A 上の `/var/opt/mssql/userdata` にある場合は、それと同じフォルダーがサーバー B にも存在する必要があります。これに関する唯一の例外については、「[Windows ベースの可用性グループとレプリカとの相互運用性](#interoperability-with-windows-based-availability-groups-and-replicas)」に記載されています。

## <a name="the-listener-under-linux"></a>Linux 下のリスナー

リスナーは、AG のオプション機能です。 これは、すべての接続 (プライマリ レプリカへの読み取り/書き込み接続や、セカンダリ レプリカへの読み取り専用接続) に対する単一のエントリ ポイントを提供するものです。これにより、アプリケーションとエンド ユーザーは、どのサーバーがデータをホストしているのかを認識しなくて済むようになります。 WSFC では、これはネットワーク名リソースと IP リソースの組み合わせであり、AD DS (必要な場合) と DNS に登録されます。 この抽象化は、AG リソース自体との組み合わせによって提供されます。 リスナーの詳細については、「[リスナー、クライアント接続、およびアプリケーションのフェールオーバー](../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)」を参照してください。

Linux ではリスナーの構成方法が異なりますが、その機能は同じです。 Pacemaker にはネットワーク名リソースの概念がなく、AD DS で作成されたオブジェクトもありません。Pacemaker で作成された IP アドレス リソースしかなく、それらを任意のノードで実行できます。 "フレンドリ名" を使用して、DNS 内のリスナーの IP リソースに関連付けられたエントリを作成する必要があります。 リスナーの IP リソースは、その可用性グループのプライマリ レプリカをホストしているサーバー上でのみアクティブになります。

Pacemaker が使用されていて、リスナーに関連付けられた IP アドレス リソースが作成されている場合は、1 つのサーバーで IP アドレスが停止し、もう 1 つのサーバーで起動する際に、システムがしばらく停止します (フェールオーバーが自動か手動かにかかわらず)。 これにより、単一の名前と IP アドレスの組み合わせによる抽象化が提供されますが、システム停止はマスクされません。 アプリケーションでは、この問題を検出して再接続するための何らかの機能を設けて、切断に対応できるようにする必要があります。

ただし、DNS 名と IP アドレスを組み合わせても、WSFC のリスナーで提供されるすべての機能 (セカンダリ レプリカのための読み取り専用ルーティングなど) を提供するのに十分ではありません。 AG を構成する際、やはり [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] で "リスナー" を構成する必要があります。 これはウィザードだけでなく、Transact-SQL 構文でも確認できます。 これを Windows と同様に機能するように 構成するには、次の 2 つの方法があります。

-   クラスターの種類が External の AG の場合、[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] で作成された "リスナー" に関連付けられた IP アドレスは、Pacemaker で作成されたリソースの IP アドレスである必要があります。
-   クラスターの種類を None にして作成された AG の場合は、プライマリ レプリカに関連付けられた IP アドレスを使用します。

指定された IP アドレスに関連付けられたインスタンスは、アプリケーションからの読み取り専用ルーティング要求などに対するコーディネーターになります。

## <a name="interoperability-with-windows-based-availability-groups-and-replicas"></a>Windows ベースの可用性グループとレプリカとの相互運用性 

クラスターの種類が External または WSFC である AG では、そのレプリカをクロスプラットフォームにすることはできません。 このことは、AG が [!INCLUDE[ssstandard-md](../includes/ssstandard-md.md)] と [!INCLUDE[ssenterprise-md](../includes/ssenterprise-md.md)] のどちらであっても同様です。 つまり、基になるクラスターを持つ従来の AG 構成では、一方のレプリカを WSFC に配置し、もう一方のレプリカを、Pacemaker を使用して Linux 上に配置することはできません。

クラスターの種類が NONE の AG では、OS の境界をまたいでレプリカを配置することができます。そのため、同じ AG 内に Linux ベースと Windows ベースの両方のレプリカを配置することができます。 次に示すのは、プライマリ レプリカが Windows ベースで、セカンダリが Linux ディストリビューション上にある場合の例です。

![ハイブリッド None](./media/sql-server-linux-availability-group-overview/image1.png)

分散型 AG も、OS 境界をまたぐことができます。 基になる AG は、構成方法に関する規則によって制約を受けます (External で構成されたものは Linux のみだが、それが参加している AG は WSFC を使用して構成できるなど)。 次の例を確認してください。

![ハイブリッド分散型 AG](./media/sql-server-linux-availability-group-overview/image2.png)

<!-- Distributed AGs are also supported for upgrades from [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] to [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. For more information on how to achieve this, see [the article "x"].

If using automatic seeding with a distributed availability group that crosses OSes, it can handle the differences in folder structure. How this works is described in [the documentation for automatic seeding].
-->
 
## <a name="next-steps"></a>次のステップ
[SQL Server on Linux の可用性グループを構成する](sql-server-linux-availability-group-configure-ha.md)

[SQL Server on Linux の読み取りスケール可用性グループを構成する](sql-server-linux-availability-group-configure-rs.md)

[RHEL 上で可用性グループのクラスター リソースを追加する](sql-server-linux-availability-group-cluster-rhel.md)

[SLES 上で可用性グループのクラスター リソースを追加する](sql-server-linux-availability-group-cluster-sles.md)

[Ubuntu 上で可用性グループのクラスター リソースを追加する](sql-server-linux-availability-group-cluster-ubuntu.md)

[クロスプラットフォームの可用性グループを構成する](sql-server-linux-availability-group-cross-platform.md)

