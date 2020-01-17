---
title: アプライアンスのインストールと構成
description: Analytics Platform System (APS) アプライアンス管理者に、新しいアプライアンスのセットアップと使用を開始するための最初の手順を説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9f96d953dbd427bfb6cf94470c0ee80ade3aed48
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401446"
---
# <a name="appliance-installation-and-configuration-for-analytics-platform-system"></a>Analytics Platform System のアプライアンスのインストールと構成
Analytics Platform System (APS) アプライアンス管理者に、新しいアプライアンスのセットアップと使用を開始するための最初の手順を説明します。  
  
<!-- MISSING LINKS ## <a name="BeforeYouBegin"></a>Before You Begin  
Before you begin to install, configure, and use your new appliance, we recommend reviewing information about the appliance components. Review the following to familiarize yourself with the appliance:  
  
-   Review [Understanding the Appliance Nodes and Hardware (SQL Server PDW)](assetId:///f60f419f-d1e1-403d-8cf9-07e7ef6d6627) to be sure you understand the components included in your new appliance.  
  
-   Review [Connecting to SQL Server PDW (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808) to understand how and when appliance administrators will connect to each appliance node.  
-->

## <a name="InstallHardware"></a>1. ハードウェアをインストールする  
新しいアプライアンスは、データセンターの dock に、パレットに配送されます。  
  
> [!IMPORTANT]  
> 場合によっては、IHV がデータセンターでアプライアンスを開梱し、ラックに接続し、接続することがあります。 その場合、これらの手順は必要ありません。 3. に進むことができ[ます。アプライアンスを構成する](#ConfigureAppliance)」セクションを参照してください。  
  
IHV がハードウェアのインストールを実行していない場合は、次の手順を使用してハードウェアをインストールします。  
  
|||  
|-|-|  
|**タスク**|**記述**|  
|ドキュメントの確認|独立系ハードウェアベンダー (IHV) から必要なすべてのドキュメントと情報を受信したことを確認します。 [IHV &#40;Analytics Platform System&#41;から入手するための情報を](information-to-obtain-from-your-ihv.md)参照してください。|  
|ハードウェアのインストール|データセンターがアプライアンスに対応できることを確認します。 アプライアンスコンポーネントをデータセンターに移動します。 ネットワークスイッチ、Pdu、ケーブル配線をラックに収納します。 「[ハードウェアのインストール &#40;Analytics Platform System&#41;](hardware-installation.md)」を参照してください。|  
  
## <a name="PowerOnAppliance"></a>2. アプライアンスの電源をオンにする  
  
|||  
|-|-|  
|**タスク**|**記述**|  
|アプライアンスの電源をオンにする|必要に応じて各アプライアンスコンポーネントノードの電源を入れ、エラーが発生していないことを確認します。|  
  
## <a name="ConfigureAppliance"></a>3. アプライアンスを構成する  
  
|||  
|-|-|  
|**タスク**|**記述**|  
|||  
|SQL Server PDW を使用してアプライアンスを構成し**Configuration Manager**|アプライアンスのパスワード、タイムゾーン、ネットワークとファイアウォールの設定、セキュリティ証明書、パフォーマンスなどの設定を設定するには、Configuration Manager を使用します。 「[アプライアンス構成 &#40;Analytics Platform System&#41;](appliance-configuration.md)」を参照してください。|  
  
> [!WARNING]  
> 構成の変更は、SQL Server PDW**Configuration Manager**を使用してのみ行う必要があります。 **Configuration Manager**によって公開されていない変更はサポートされていません。 たとえば、SQL Server PDW アプライアンスでは、米国英語の設定のみがサポートされています。  
  
## <a name="SoftwareServicing"></a>4. ソフトウェアサービスをセットアップする  
  
|||  
|-|-|  
|**タスク**|**記述**|  
|更新プログラムの適用 SQL Server PDW|OptionalSQL Server PDW ソフトウェアを最新バージョンに更新するには、1つまたは複数の SQL Server PDW 更新プログラムを適用することが必要になる場合があります。 「Analytics platform [system&#41;&#40;analytics ](apply-analytics-platform-system-hotfixes.md)platform System の修正プログラムを適用する」を参照してください。|  
|Windows Server Update Services の構成|ソフトウェアをサポートするために Windows Server Update Services から更新プログラムを受信するようにアプライアンスを構成します。 「 [Microsoft 更新プログラムのダウンロードと適用 &#40;Analytics Platform System&#41;」を](download-and-apply-microsoft-updates.md)参照してください。|  
  
## <a name="NextSteps"></a>次のステップ  
前の手順をすべて完了したら、アプライアンスを使用できるようになります。 お客様やその他の担当者は、次のタスクに進むことができます。  
  
|||  
|-|-|  
|**タスク**|**記述**|  
|SQL Server PDW ドライバーをインストールして接続を構成する|SQL Server Data Tools、sqlcmd、ビジネスインテリジェンスソフトウェアなどのツールを使用して SQL Server PDW に接続するようにローカルコンピューターを構成します。 <!-- MISSING LINKS See [Client Tools (SQL Server PDW)](assetId:///721851d5-e521-4d5b-ba6d-8e2e9d3c7808).-->|  
|ログオンとサーバーの役割を作成し、アクセス許可を割り当てる|ユーザーが適切なアクセス許可を使用して SQL Server PDW にログオンできるようにするログオンとサーバーの役割を計画し、作成します。 <!-- MISSING LINKS See [PDW Permissions &#40;SQL Server PDW&#41;](../sqlpdw/pdw-permissions-sql-server-pdw.md).-->|  
|Azure Data Management Gateway の構成|ゲートウェイを使用すると、Azure ユーザーは、セキュリティで保護された OData フィードとして APS データを公開することで、オンプレミスの APS データにアクセスできます。 ゲートウェイは、既にコントロールノードにインストールされています。 構成については、Microsoft にお問い合わせください。|  
|クエリとアプライアンスユーザーの監視|管理コンソールやその他のリソースを使用して、クエリおよびアプライアンスユーザーを監視します。 「[管理コンソールを使用したアプライアンスの監視 &#40;Analytics Platform System](monitor-the-appliance-by-using-the-admin-console.md) 」を参照してください&#41;<!-- MISSING LINKS and [User Sessions &#40;SQL Server PDW&#41;](../sqlpdw/user-sessions-sql-server-pdw.md)-->.|  
|SQL Server PDW にデータを読み込む|アプライアンスにデータを読み込みます。 <!-- MISSING LINKS See [Load &#40;SQL Server PDW&#41;](../sqlpdw/load-sql-server-pdw.md).-->|  
|ディザスターリカバリー計画を作成する|ハードウェアの障害やデータの上書きからデータを保護する方法を計画します。 データの破損または損失が発生した場合に備えて、定期的なバックアップと復元プランを使用して計画を作成します。 <!-- MISSING LINKS See [Create a Disaster Recovery Plan &#40;SQL Server PDW&#41;](../sqlpdw/create-a-disaster-recovery-plan-sql-server-pdw.md).-->|  
|アプライアンスを監視する|システムビュー、ログ、および管理コンソールを使用して、アプライアンスの状態、ヘルス、およびパフォーマンスを監視します。 問題を修正または報告します。 「 [Monitor Appliance Health State &#40;Analytics Platform System&#41;](../relational-databases/system-dynamic-management-views/sys-dm-pdw-component-health-status-transact-sql.md)」を参照してください。|  
