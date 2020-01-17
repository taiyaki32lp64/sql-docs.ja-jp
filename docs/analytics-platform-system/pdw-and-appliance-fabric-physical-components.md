---
title: アプライアンスの物理コンポーネント
description: PDW およびアプライアンスファブリック物理コンポーネントの名前と説明。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5cbed66f53189668518e04848002ae69adb8c614
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400908"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>アプライアンスの物理コンポーネント-分析プラットフォームシステム
PDW およびアプライアンスファブリック物理コンポーネントの名前と説明。 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>コンポーネント図  
物理コンポーネントの名前と、6コンピューティングノードアプライアンスの最初のラックに配置されている場所が表示されます。  
  
![PDW リージョン コンポーネント名 - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames-HP")  
  
PDW コンポーネントの実際の名前は、PDW のリージョン名、ダッシュ、コンポーネント名の順に続きます。 たとえば、PDW のリージョン名が PDW123 の場合、実際の名前は**PDW123-CTL01**、 **PDW123 pqth4a-cmp01**などになります。  
  
同様に、アプライアンスファブリックコンポーネントの実際の名前はアプライアンスドメイン、ダッシュ、コンポーネント名の順になります。 たとえば、アプライアンスドメインが FSW123 の場合、アプライアンスファブリック Vm は**FSW123**、 **FSW123**、 **FSW123**のようになります。  
  
次に示すのは、6つのコンピューティングノードを持つ PDW リージョンの統合ビューです。  
  
![PDW コンポーネント名](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>PDW コンポーネント  
PDW の仮想マシンは、PDW のリージョンに含まれています。  
  
*PDW_region*-CTL01  
コントロールノードを実行する仮想マシン。 これは HST01 で実行され、HST02 にフェールオーバーできます。  
  
> [!WARNING]  
> SQL Server PDW では、Hyper-v マネージャーを使用した CTL01 仮想マシンのスナップショットの作成はサポートされていません。 スナップショットはローカルストレージに依存します。これにより、仮想マシンがバックアップにフェールオーバーしようとした場合にエラーが発生します。 スナップショットを作成すると、パッシブサーバーにフェールオーバーする他の VM の信頼性の問題が発生する可能性もあります。  
  
*PDW_region*- *PDW_Region*から pqth4a-cmp01-CMP06  
コンピューティングノードを実行する仮想マシン。 この6コンピューティングノードの図では、HSA06 を介して HSA01 を介してホストがコンピューティングノード Vm をそれぞれ PQTH4A-CMP01 から CMP06 に実行します。  
  
## <a name="fabric"></a>アプライアンスファブリックコンポーネント  
これらのコンポーネントは、アプライアンスファブリックの一部です。  
  
### <a name="virtual-machines"></a>Virtual Machines  
*appliance_domain*-WDS  
この仮想マシンは Windows 展開サービス (WDS) をホストします。これは、分析プラットフォームシステムが、アプライアンスネットワーク経由で Windows オペレーティングシステムを展開します。 また、DHCP サービスもホストします。これにより、アプライアンスホストは、事前に構成された IP アドレスを使用せずにアプライアンスネットワークに参加できます。  
  
*Appliance_domain*WDS 仮想マシンは HST01 上で実行され、HST02 にフェールオーバーできます。 WDS 仮想マシンと VMM 仮想マシンで、アプライアンスのインストール中に、物理ホスト上に Windows を展開します。 アプライアンスのライフサイクル中、WDS と VMM はホストの交換などの操作を実行します。  
  
*appliance_domain*-VMM  
Virtual Machine Manager (VMM) は仮想マシンで実行され、HST02 にフェールオーバーできます。 VMM は System Center をホストして、物理ホストにオペレーティングシステムを展開します。 VMM では、すべてのホストとバーチャルマシンで Windows 更新プログラムを適用または削除するための Windows Server Update Services (WSUS) も用意されています。  
  
*appliance_domain*-AD01、 *appliance_domain*-AD02  
ドメインネームシステム (DNS) を含む Active Directory Domain Services は、HST01 と HST02 の両方の仮想マシンで実行されます。 アプライアンスの高可用性を確保するために、AD01 と AD02 はレプリケートされたドメインコントローラーであり、フェールオーバーは行われません。 失敗した場合は、もう1つは正しいデータで既に利用できます。  
  
*appliance_domain*-ISCSI01  
記憶域が接続されている各ホストで1つの ISCSI 仮想マシンが実行されます (HSA01-HSA06)。 この VM はフェールオーバーしません。  
  
### <a name="hosts"></a>ホスト  
*appliance_domain*- *appliance_domain*から HST01-HST06  
PDW コントロールノードおよびアプライアンスファブリック仮想マシンのホスト。 HST03 はオプションのパッシブホストです。  
  
*appliance_domain*- *appliance_domain*から HSA01-HSA08  
ストレージが接続されているホスト (HSA)。 各ホストには、1つのコンピューティングノード VM と1つの ISCSI VM が実行されます。  
  
### <a name="cluster-for-pdw"></a>PDW のクラスター  
*appliance_domain*-WFOHST01  
PDW クラスターには WFOHST01 という名前が付けられています。 PDW に属するすべての物理ホストと仮想マシンを管理します。  
  
### <a name="direct-attached-storage"></a>直接接続ストレージ  
*appliance_domain*- *appliance_domain*から DAS01-DAS03  
これは、コンピューティングノードに接続されている直接接続ストレージです。 HP では、2つのコンピューティングノードごとに1つの DAS を使用します。 Dell とクォンタムは、3つのコンピューティングノードごとに1つの DAS を備えています。  
  
## <a name="see-also"></a>参照  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[アプライアンス構成 &#40;Analytics Platform System&#41;](appliance-configuration.md)  
[アプライアンス管理タスク &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
