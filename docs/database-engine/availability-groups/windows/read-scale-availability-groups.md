---
title: 可用性グループで読み取りスケールを使用する
description: 'Always On 可用性グループの使用時、読み取りスケールを達成する方法の説明。 '
ms.custom: seodec18
ms.date: 10/24/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: ''
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2decc7e78b599ebcd0c16e3373a0b62401d09428
ms.sourcegitcommit: 0d5b0aeee2a2b34fd448aec2e72c0fa8be473ebe
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/07/2020
ms.locfileid: "75720845"
---
# <a name="use-read-scale-with-always-on-availability-groups"></a>Always On 可用性グループで読み取りスケールを使用する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

可用性グループは、SQL Server で高可用性機能を実現するだけではなく、統合されたスケーリング ソリューションも提供する、包括的なソリューションです。 一般的なデータベース アプリケーションでは、複数のクライアントがさまざまな種類のワークロードを実行します。 リソースの制約のために、ボトルネックが発生することもあります。 

可用性グループにおいては、読み取りスケールによって読み取りワークロードがセカンダリ レプリカに移されます。 リソースを解放すると、OLTP ワークロードのために、より高いスループットを達成することができます。 また、読み取り専用ワークロードで、より優れたパフォーマンスとスケールを実現することもできます。 SQL Server の高速レプリケーション技術を活用し、複製されたデータベースのグループを作成し、レポートと分析のワークロードを読み取り専用レプリカに移します。

可用性グループによって、セカンダリ データベースに読み取り専用アクセスができるように 1 つまたは複数のセカンダリ レプリカを構成できます。

分析やレポートのワークロードを実行するクライアント アプリケーションは、セカンダリ データベースに直接接続できます。 また、読み取り専用のルーティング リストを設定し、プライマリ データベースに接続できます。 その後、プライマリ データベースはルーティング リストに基づき、ラウンド ロビン方式で各セカンダリ レプリカに接続要求を転送します。

## <a name="read-scale-availability-groups-without-cluster"></a>読み取りスケール可用性グループ (クラスターなし)

[!INCLUDE[sssql15-md](../../../includes/sssql15-md.md)] 以前は、すべての可用性グループにクラスターが必要でした。 そのクラスターにより、事業継続性、つまり、高可用性とディザスター リカバリー (HADR) が実現していました。 また、セカンダリ レプリカを読み取り操作のために構成できました。 高可用性が最終目標ではない場合は、クラスターの構成と運用に、相当量の運用経費がかかっていました。 SQL Server 2017 では、クラスターのない、読み取りスケール可用性グループが導入されました。 

プライマリ レプリカで実行されるミッションクリティカルなワークロードのためにリソースを確保しておく必要がある場合、読み取り専用のルーティングを利用するか、読み取り可能セカンダリ レプリカに直接接続できます。 何らかのクラスタリング技術との統合に頼る必要はありません。 この新しい技術は、Windows プラットフォームと Linux プラットフォームの両方を実行している SQL Server 2017 で利用できます。

>[!IMPORTANT]
>これは高可用性設定ではありません。 障害検出と自動フェールオーバーを監視し、調整するためのインフラストラクチャはありません。 クラスターがない場合、SQL Server は自動化された 高可用性ソリューションで提供される、短い目標回復時間 (RTO) を提供することはできません。 高可用性機能が必要な場合は、クラスター マネージャー (Windows の Windows Server フェールオーバー クラスター、または Linux の Pacemaker) をご利用ください。
>
>読み取りスケール可用性グループは、ディザスター リカバリー機能を提供できます。 読み取り専用レプリカが同期コミット モードになっている場合、回復ポイントの目標 (RPO) がゼロになります。 読み取りスケール可用性グループのフェールオーバーについては、[読み取りスケール可用性グループのプライマリ レプリカのフェールオーバー](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md#ReadScaleOutOnly)に関するページをご覧ください。

## <a name="use-distributed-availability-groups-for-geographic-read-scale"></a>地理的読み取りスケールに分散型可用性グループを使用する

地理的に離れたソリューションでは、読み取りスケール ソリューションと分散型可用性グループを実装できます。 それらを使用して、プライマリ レプリカから読み取り可能セカンダリ レプリカに読み取り負荷を移し、読み取りワークロードの発生源に近いサイトに負荷を移すことができます。 分散型可用性グループは、プライマリ レプリカ上のリソースの使用率を低減させます。 また、ネットワーク待機時間を減らし、専用リソースを活用することで、読み取りスループットの向上にも役立ちます。

1 個の分散型可用性グループで最大 17 個のセカンダリ レプリカを持つことができます。 スケーリング容量が増えた場合、複数の可用性グループをデイジー チェーン接続し、読み取り可能レプリカの数をさらに増やすことができます。 同じ可用性グループから 2 つの分散型可用性グループを展開すれば、地理的に分散した環境で読み取りの待機時間を減らすこともできます。




## <a name="next-steps"></a>次のステップ

[Linux で読み取りスケール可用性グループを構成する](../../../linux/sql-server-linux-availability-group-configure-rs.md)

[Windows で読み取りスケール可用性グループを構成する](../../../database-engine/availability-groups/windows/configure-read-scale-availability-groups.md)

## <a name="see-also"></a>参照

 [AlwaysOn 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
