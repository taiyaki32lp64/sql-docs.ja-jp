---
title: 高可用性
description: Analytics Platform System (APS) が高可用性を実現するためにどのように設計されているかについて説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6246ed25909a2e366d8bbafcd912a4fd923cc84a
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401103"
---
# <a name="analytics-platform-system-high-availability"></a>Analytics Platform System の高可用性
Analytics Platform System (APS) が高可用性を実現するためにどのように設計されているかについて説明します。  
  
## <a name="high-availability-architecture"></a>高可用性アーキテクチャ  
![アプライアンスのアーキテクチャ](media/appliance-architecture.png "アプライアンスのアーキテクチャ")  
  
## <a name="network"></a>ネットワーク  
ネットワークの可用性を確保するために、APS アプライアンスには2つの InfiniBand ネットワークがあります。 InfiniBand ネットワークの1つがダウンしても、もう一方は使用できます。 また、Active Directory は、正しい InfiniBand ネットワークへの受信要求を解決するためにドメインコントローラーをレプリケートしました。  
  
詳細については、「 [Configure InfiniBand network adapters](configure-infiniband-network-adapters.md)」を参照してください。  
  
## <a name="storage"></a>Storage  
データを安全に保つために、APS は RAID 1 ミラーリングを使用して、すべてのユーザーデータのコピーを2つ保持します。 ディスクに障害が発生すると、ハードウェアシステムはデータを予備ディスクに再構築し、ディスク障害が発生したことを示すアラートを設定します。  
  
データをオンラインで保持するために、APS は Windows 記憶域スペースとクラスター化共有ボリュームを使用して、直接接続された記憶域のユーザーデータディスクを管理します。 クラスター共有ボリュームに構成されているデータスケールユニットごとに1つの記憶域プールがあります。これは、マウントポイントを介してコンピューティングノードホストが使用できます。  
  
記憶域プールがオンラインのままになるように、データスケールユニット内の各ホストには、フェールオーバーされない ISCSI 仮想マシンがあります。 ホストで障害が発生した場合でも、データスケールユニット内の他のホストからデータにアクセスできるので、このアーキテクチャは重要です。  
  
## <a name="hosts"></a>ホスト  
ホストの可用性を確保するために、すべてのホストが Windows フェールオーバークラスターに構成されています。 すべてのラックにパッシブホストがあります。 必要に応じて、並列データウェアハウス (PDW) とアプライアンスファブリックを制御する最初のラックは、2つ目のパッシブホストを持つことができ SQL Server ます。 ホストで障害が発生した場合、フェールオーバー用に構成されているバーチャルマシンは、使用可能なパッシブホストにフェールオーバーします。  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>PDW ノードとアプライアンスファブリック  
PDW ノードとアプライアンスファブリックの高可用性を実現するために、APS は仮想化を使用します。 各 PDW およびアプライアンスファブリックコンポーネントは、仮想マシンで実行されます。  
  
各仮想マシンは、Windows フェールオーバークラスターの役割として定義されています。 仮想マシンで障害が発生すると、クラスターは使用可能なパッシブホスト上で再起動します。 仮想マシンは System Center Virtual Machine Manager を使用して展開されます。 フェールオーバーが発生すると、パッシブホストで実行されている仮想マシンは、InfiniBand ネットワークを介してユーザーデータにアクセスできます。  
  
制御ノードとコンピューティングノードの仮想マシンはそれぞれ、単一ノードクラスターとして構成されます。 単一ノードクラスターは、クラスターが常にアクティブな InfiniBand IP を使用していることを確認するために、InfiniBand ネットワークをクラスターリソースとして管理します。 単一ノードクラスターは、仮想マシン内で実行される PDW プロセスを管理します。 たとえば、単一ノードクラスターは、適切な順序で開始できるように、リソースとして SQL Server およびデータ移動サービス (DMS) を持っています。 Control node VM は、オーケストレーションホスト上で実行される他の Vm の開始順序も制御します。  
  
