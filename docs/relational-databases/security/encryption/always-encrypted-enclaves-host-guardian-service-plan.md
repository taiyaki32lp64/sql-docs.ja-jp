---
title: ホスト ガーディアン サービスの構成証明の計画
description: セキュリティで保護されたエンクレーブが設定された SQL Server Always Encrypted のホスト ガーディアン サービスの構成証明を計画します。
ms.custom: ''
ms.date: 10/12/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: rpsqrd
ms.author: ryanpu
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d774df3329c6c9e49e9e1bd9a86dbeaf30ac5765
ms.sourcegitcommit: 9e026cfd9f2300f106af929d88a9b43301f5edc2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74317955"
---
# <a name="plan-for-host-guardian-service-attestation"></a>ホスト ガーディアン サービスの構成証明の計画

[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

[セキュリティで保護されたエンクレーブが設定された Always Encrypted](always-encrypted-enclaves.md) を使用する場合は、クライアント アプリケーションが [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] プロセス内の信頼できるエンクレーブと通信していることを確認します。 仮想化ベースのセキュリティ (VBS) エンクレーブの場合、この要件には、エンクレーブ内のコードが有効であることと、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] をホストしているコンピューターが信頼できることの確認も含まれます。 リモート構成証明では、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターの ID (および必要に応じて構成) を検証できるサード パーティを導入することによって、この目標が達成されます。 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] でエンクレーブを使用してクエリを実行するには、事前に、その動作環境に関する情報を構成証明サービスに提供して正常性証明書を取得しておく必要があります。 その後、この正常性証明書はクライアントに送信され、クライアントでは構成証明サービスを使用してその信頼性を個別に確認できるようになります。 クライアントでは、正常性証明書を信頼したら、信頼できる VBS エンクレーブと通信しているものと認識し、そのエンクレーブを使用するクエリを発行します。

Windows Server 2019 のホスト ガーディアン サービス (HGS) ロールには、VBS エンクレーブが設定された Always Encrypted 向けのリモート構成証明機能が用意されています。
この記事では、VBS エンクレーブが設定された Always Encrypted と HGS 構成証明を使用するための、展開前の決定事項および要件について説明します。

## <a name="architecture-overview"></a>アーキテクチャの概要

ホスト ガーディアン サービス (HGS) は、Windows Server 2019 上で実行されるクラスター化された Web サービスです。
一般的な展開では、HGS サーバーが 1 台から 3 台、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行するコンピューターが少なくとも 1 台、および SQL Server Management Studio などのクライアント アプリケーションまたはツールを実行するコンピューターが必要になります。
HGS は、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行しているコンピューターが信頼できるかどうかを判断する役割を担っているため、保護対象の [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] インスタンスとは物理的にも論理的にも分離している必要があります。
HGS と [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターの両方にアクセスできる管理者は、悪意のあるコンピューターが [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行できるように構成証明サービスを構成することが可能であり、これにより VBS エンクレーブを侵害できるようになります。

### <a name="hgs-domain"></a>HGS ドメイン

HGS の設定では、HGS サーバー、フェールオーバー クラスター リソース、および管理者アカウント用に新しい Active Directory ドメインが自動的に作成されます。

[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行しているコンピューターはドメイン内に存在する必要はありませんが、その場合は、HGS サーバーで使用されているものとは別のドメインである必要があります。

### <a name="high-availability"></a>高可用性

HGS 機能では、フェールオーバー クラスターが自動的にインストールおよび構成されます。
運用環境では、高可用性を実現するために HGS サーバーを 3 台使用することをお勧めします。 クラスター クォーラムの決定方法と、外部監視付きの 2 つのノード クラスターを含む代替の構成の詳細については、[フェールオーバー クラスターのドキュメント](https://docs.microsoft.com/windows-server/failover-clustering/manage-cluster-quorum)を参照してください。

HGS ノード間に共有記憶域は必要ありません。 構成証明データベースのコピーは各 HGS サーバーに格納され、クラスター サービスによってネットワーク経由で自動的にレプリケートされます。

### <a name="network-connectivity"></a>ネットワーク接続

SQL クライアントと [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] は両方とも、HTTP 経由で HGS と通信できる必要があります。
SQL クライアントと HGS の間、および SQL Server と HGS の間のすべての通信を暗号化するため、TLS 証明書を使用して HGS を構成します。
この構成は中間者攻撃から保護するのに役立ち、正しい HGS サーバーと通信していることを保証します。

HGS サーバーでは、構成証明サービス データベースが確実に同期された状態で維持されるようにするために、クラスター内の各ノード間の接続が必要とされます。フェールオーバー クラスターのベスト プラクティスとして、クラスター通信の場合は 1 つのネットワーク上で HGS ノードを接続し、他のクライアントと HGS との通信の場合は別個のネットワークを使用します。

### <a name="attestation-modes"></a>構成証明モード

[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行しているコンピューターが HGS を使用して証明を試みる場合、そのコンピューターはまず必要な証明方法を HGS に問い合わせます。
HGS では、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] で使用する構成証明モードとして次の 2 つがサポートされています。

| 構成証明モード | 説明 |
| ---------------- | ------- |
| TPM | トラステッド プラットフォーム モジュール (TPM) 構成証明では、HGS で証明するコンピューターの ID と整合性について、最も強力な保証が提供されます。 この場合、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行するコンピューターには、TPM バージョン 2.0 がインストールされている必要があります。 各 TPM チップには、特定のコンピューターを識別するのに使用できる一意で不変の ID (保証キー) が含まれています。 また、TPM では、コンピューターの起動プロセスが測定され、セキュリティに影響する測定値のハッシュがプラットフォーム制御レジスタ (PCR) に格納されます。この情報は、オペレーティング システムによって読み取ることはできても変更することはできません。 これらの測定値は、コンピューターのセキュリティ構成が自らが主張する状態にあることを暗号で証明する構成証明時に使用されます。 |
| ホスト キー | ホスト キーの構成証明の形式はよりシンプルであり、非対称キー ペアを使用してコンピューターの ID を検証するだけです。 秘密キーは [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行しているコンピューターに格納され、公開キーは HGS に提供されます。 コンピューターのセキュリティ構成は測定されず、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行しているコンピューター上で TPM 2.0 チップは必要ありません。 [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターにインストールされている秘密キーを保護することが重要です。このキーを取得した者はだれでも、正当な [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューター、および [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] 内で実行されている VBS エンクレーブを偽装できるからです。 |

一般に、次の推奨事項があります。

- **物理的な運用サーバー**の場合は、提供される追加の保証に TPM 構成証明を使用することをお勧めします。
- **仮想運用サーバー**の場合は、ほとんどの仮想マシンに仮想 TPM とセキュア ブートがないため、ホスト キー構成証明をお勧めします。 [オンプレミスのシールドされた VM](https://aka.ms/shieldedvms) のようなセキュリティが強化された VM を使用している場合は、TPM モードの使用を選択できます。 すべての仮想化されたデプロイでは、構成証明プロセスで、VM 環境のみが分析され、VM の下の仮想化プラットフォームは分析されません。
- **開発/テスト シナリオ**の場合は、設定が簡単なため、ホスト キー構成証明をお勧めします。

### <a name="trust-model"></a>信頼モデル

VBS エンクレーブ信頼モデルでは、ホスト OS から保護されるように、暗号化されたクエリとデータはソフトウェアベースのエンクレーブで評価されます。
このエンクレーブへのアクセスはハイパーバイザーによって保護されていて、同じコンピューター上で稼働している 2 つの仮想マシンが互いのメモリにアクセスできないのと同じ方法が使用されます。
自身が VBS の正当なインスタンスと通信していることをクライアントが信頼できるようにするには、TPM ベースの構成証明を使用して、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューター上に信頼のハードウェア ルートを確立する必要があります。
起動プロセス中にキャプチャされた TPM 測定値には、VBS インスタンスの一意の ID キーが含まれているため、正常性証明書はそのコンピューター上でのみ有効になります。
さらに、VBS を実行しているコンピューター上で TPM を使用できる場合、VBS ID キーのプライベート部分は TPM によって保護されるため、だれもその VBS インスタンスを偽装することはできません。

TPM 構成証明の場合は、セキュア ブートが必要になります。これは、Microsoft が署名した正当なブートローダーが UEFI によって確実に読み込まれ、ルートキットによってハイパーバイザー起動プロセスがインターセプトされないようにするためです。
さらに、既定では IOMMU デバイスが必要です。これは、メモリに直接アクセスできるハードウェア デバイスを使用してもエンクレーブ メモリを検査または変更できないようにするためです。

これらの保護はいずれも、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行しているコンピューターが物理マシンであることを前提としています。
[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行しているコンピューターを仮想化すると、ハイパーバイザーまたはハイパーバイザー管理者による検査から VM のメモリが安全に守られる保証はなくなります。たとえば、ハイパーバイザー管理者が、VM のメモリをダンプして、エンクレーブ内のクエリとデータのプレーンテキスト バージョンへのアクセス権を取得する可能性があります。
同様に、VM に仮想 TPM が用意されている場合でも、VM のオペレーティング システムおよび起動環境の状態と整合性を測定できるだけです。
VM を制御しているハイパーバイザーの状態を測定することはできません。

ただし、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] が仮想化されている場合でも、エンクレーブは VM オペレーティング システム内からの攻撃から引き続き保護されます。
ご利用のハイパーバイザーまたはクラウド プロバイダーを信頼し、主にデータベース管理者および OS 管理者による機密データへの攻撃を心配している場合は、仮想化された [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] がその要件を満たす可能性があります。

同様に、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行しているコンピューターに TPM 2.0 モジュールがインストールされていないシナリオ、またはセキュリティが最重要ではない開発/テスト シナリオでは、ホスト キーの構成証明が依然として有用です。
これまでに説明した多くのセキュリティ機能 (セキュリティで保護された起動や TPM 1.2 モジュールなど) を使用して、VBS とオペレーティング システム全体をより適切に保護することもできます。
ただし、コンピューターのこれらの設定がホスト キー構成証明で実際に有効にされていることを HGS で確認する方法はないため、クライアントでは、使用可能なすべての保護がホストで実際に使用されているかどうかを確認できません。

## <a name="prerequisites"></a>前提条件

### <a name="hgs-server-prerequisites"></a>HGS サーバーの前提条件

ホスト ガーディアン サービス ロールを実行しているコンピューターは、次の要件を満たしている必要があります。

| コンポーネント | 要件 |
| --------- | ----------- |
| オペレーティング システム | Windows Server 2019 Standard または Datacenter Edition |
| CPU | 2 コア (最小)、4 コア (推奨) |
| RAM | 8 GB (最小) |
| NIC | 静的 IP が設定された 2 枚の NIC を推奨 (1 枚はクラスター トラフィック用、もう 1 枚は HGS サービス用) |

HGS は、暗号化と暗号化の解除を必要とするアクション数が多いため、CPU にバインドされたロールとなります。
暗号化アクセラレータ機能を備えた最新のプロセッサを使用すると、HGS のパフォーマンスが向上します。
構成証明データの記憶域の要件は、一意のコンピューター証明ごとに最小で 10 KB から 1 MB の範囲です。

開始する前に、HGS コンピューターをドメインに参加させないでください。

### <a name="include-ssnoversion-mdincludesssnoversion-mdmd-computer-prerequisites"></a>[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] コンピューターの前提条件

[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行しているコンピューターは、[SQL Server のインストール要件](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)と [Hyper-V ハードウェア要件](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/hyper-v-requirements#hardware-requirements)の両方を満たしている必要があります。

これらの要件の内容は次のとおりです。

- [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] 以降
- Windows 10 Enterprise バージョン 1809 以降、または Windows Server 2019 Datacenter エディション。 Windows 10 および Windows Server の他のエディションでは、HGS を使用した構成証明はサポートされていません。
- 仮想化テクノロジの CPU サポート:
  - Extended Page Tables を備えた Intel VT-x。
  - Rapid Virtualization Indexing を備えた AMD-V。
  - VM で [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行する場合、ハイパーバイザーおよび物理 CPU には入れ子になった仮想化機能が用意されている必要があります。 VM で VBS エンクレーブを実行する場合の保証については、「[信頼モデル](#trust-model)」セクションを参照してください。
    - Hyper-V 2016 以降では、VM プロセッサ上で[入れ子にされた仮想化拡張機能](https://docs.microsoft.com/virtualization/hyper-v-on-windows/user-guide/nested-virtualization#configure-nested-virtualization)を有効にします。
    - Azure では、入れ子になった仮想化をサポートする VM サイズを選択します。 すべての v3 シリーズ VM は、Dv3 や Ev3 などの入れ子になった仮想化をサポートしています。 [入れ子対応の Azure VM の作成](/azure/virtual-machines/windows/nested-virtualization#create-a-nesting-capable-azure-vm)に関するページを参照してください。
    - VMWare vSphere 6.7 以降では、[VMware のドキュメント](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.vm_admin.doc/GUID-C2E78F3E-9DE2-44DB-9B0A-11440800AADD.html)の説明に従って、仮想化ベースのセキュリティによる VM のサポートを有効にします。
    - 他のハイパーバイザーおよびパブリック クラウドでは、VBS エンクレーブが設定された Always Encrypted を有効にする入れ子になった仮想化機能がサポートされている場合もあります。 互換性と構成手順については、仮想化ソリューションのドキュメントを確認してください。
- TPM 構成証明を使用する予定がある場合は、サーバーで使用できる TPM 2.0 rev 1.16 チップが必要です。 現時点で、TPM 2.0 rev 1.38 チップでは HGS 構成証明は機能しません。 さらに、TPM には有効な保証キー証明書が必要です。

## <a name="devtest-environment-considerations"></a>開発/テスト環境に関する考慮事項

開発環境またはテスト環境で、VBS エンクレーブが設定された Always Encrypted を使用している場合に、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を実行しているコンピューターの高可用性または強力な保護を必要としないときは、次に示すいずれかまたはすべての譲歩を行って展開の簡略化を図ることができます。

- HGS のノードを 1 つだけ展開します。 HGS によってフェールオーバー クラスターがインストールされても、高可用性が問題にならない場合、ノードを追加する必要はありません。
- 設定エクスペリエンスをよりシンプルにするために、TPM モードではなくホスト キー モードを使用します。
- HGS や [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] を仮想化して物理リソースを節約します。
- セキュリティで保護されたエンクレーブが設定された Always Encrypted を、[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] と同じコンピューター上で構成する場合は、SSMS またはその他のツールを実行します。 この場合、列マスター キーは [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] と同じコンピューター上に残されるので、運用環境ではこれを実行しないでください。

## <a name="next-steps"></a>次のステップ

- [[!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] のホスト ガーディアン サービスを展開する](./always-encrypted-enclaves-host-guardian-service-deploy.md)
