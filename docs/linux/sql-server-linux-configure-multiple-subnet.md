---
title: 複数サブネットの可用性グループと FCI の構成 (Linux)
description: 複数サブネットの Always On 可用性グループとフェールオーバー クラスター インスタンス (FCI) を SQL Server on Linux に構成する方法について説明します。
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/01/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: f35f1916107e8ede0e7bf7cc3df483a0c33f3355
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558612"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>複数サブネットの Always On 可用性グループとフェールオーバー クラスター インスタンスを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Always On 可用性グループ (AG) またはフェールオーバー クラスター インスタンス (FCI) が複数のサイトにまたがっている場合、通常、各サイトには独自のネットワークがあります。 つまり、多くの場合、各サイトに独自の IP アドレス指定があります。 たとえば、サイト A のアドレスが 192.168.1.*x* から開始し、サイト B のアドレスが 192.168.2.*x* から開始します (*x* はサーバー固有の IP アドレスの一部)。 ネットワーク層で何らかのルーティングが行われていない場合、これらのサーバーは相互に通信できません。 このシナリオに対処する方法は 2 つあります。2 つの異なるサブネットをブリッジするネットワーク (VLAN) をセットアップするか、サブネット間のルーティングを構成します。

## <a name="vlan-based-solution"></a>VLAN ベースのソリューション
 
**前提条件**:VLAN ベースのソリューションの場合、適切な可用性を確保するには、AG または FCI に参加する各サーバーに 2 枚のネットワーク カード (NIC) が必要です (デュアル ポート NIC は物理サーバー上の単一障害点になります)。これにより、IP アドレスをネイティブ サブネットだけでなく、VLAN 上のサブネットにも割り当てられるようになります。 これに加えて、他のネットワーク ニーズもあります (同じく独自のネットワークを必要とする iSCSI など)。

AG または FCI 用の IP アドレスの作成は、VLAN で実行されます。 次の例では、VLAN のサブネットは 192.168.3.*x* であるため、AG または FCI に作成される IP アドレスは 192.168.3.104 です。 1 つの IP アドレスが AG または FCI に割り当てられているため、その他の構成は必要ありません。

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Pacemaker を使用した構成

Windows の世界では、Windows Server フェールオーバー クラスター (WSFC) が複数のサブネットをネイティブでサポートし、IP アドレスに対して OR 依存関係を使用して複数の IP アドレスを処理します。 Linux には OR 依存関係はありませんが、次に示すように、適切な複数のサブネットを Pacemaker でネイティブに実現する方法があります。 通常の Pacemaker コマンドラインを使用してリソースを変更しただけでは、これを行うことはできません。 クラスター情報ベース (CIB) を変更する必要があります。 CIB は、Pacemaker 構成の XML ファイルです。

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>CIB を更新する

1.  CIB をエクスポートします。

    **Red Hat Enterprise Linux (RHEL) と Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    ここで、*filename* は CIB に付ける名前です。

2.  生成されたファイルを編集します。 `<resources>` セクションを探します。 AG または FCI に対して作成されたさまざまなリソースが表示されます。 IP アドレスに関連付けられたものを探します。 2 番目の IP アドレスの情報を含む `<instance attributes>` セクションを、既存のセクションの前後いずれか、ただし `<operations>` の前に追加します。 構文は次のようになります。

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    ここで、*NameForAttribute* はこの属性の一意名、*Score* は属性に割り当てられる数 (プライマリ サブネットの数よりも大きくする必要がある)、*RuleName* はルールの名前、*ExpressionName* は式の名前、*NodeNameInSubnet2* は他のサブネットのノードの名前、*NameForSecondIP* は 2 番目の IP アドレスに関連付けられる名前、*IPAddress* は 2 番目のサブネットの IP アドレス、*NameForSecondIPNetmask* はネットマスクに関連付けられた名前、*Netmask* は 2 番目のサブネットのネットマスクです。
    
    次に例を示します。
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  変更した CIB をインポートし、Pacemaker を再構成します。

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    ここで、*filename* は 変更した IP アドレス情報を含む CIB ファイルの名前です。

### <a name="check-and-verify-failover"></a>フェールオーバーを確認して検証する

1.  CIB が更新済みの構成に正常に適用されたら、Pacemaker で IP アドレス リソースに関連付けられている DNS 名に対して ping を実行します。 これは、現在 AG または FCI をホストしているサブネットに関連付けられた IP アドレスを反映する必要があります。
2.  AG または FCI を他のサブネットにフェールオーバーします。
3.  AG または FCI が完全にオンラインになったら、IP アドレスに関連付けられている DNS 名に対して ping を実行します。 これは、2 番目のサブネットの IP アドレスを反映する必要があります。
4.  必要であれば、AG または FCI を元のサブネットにフェールオーバーします。
