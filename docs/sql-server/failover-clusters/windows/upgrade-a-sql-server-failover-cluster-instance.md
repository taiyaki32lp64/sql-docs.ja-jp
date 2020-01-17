---
title: SQL Server フェールオーバー クラスター インスタンスのアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 681e944da0a49c6a1b485606e5ed1ed0bd8ffd0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904984"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance"></a>SQL Server フェールオーバー クラスター インスタンスのアップグレード
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターを、新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]バージョン、新しい [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]サービス パック、または累積更新プログラムにアップグレードするか、新しい Windows サービス パックや累積更新プログラムを、すべてのフェールオーバー クラスター ノードに個別にインストールして、ダウンタイムを、単一の手動フェールオーバー (元のプライマリにフェールバックする場合は、2 回の手動フェールオーバー) に制限できます。  
  
 フェールオーバー クラスターの Windows オペレーティング システムのアップグレードは、[!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] より前のオペレーティング システムではサポートされません。 [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] 以降で実行されているクラスター ノードのアップグレードについては、「[ローリング アップグレードまたは更新の実行](#perform-a-rolling-upgrade-or-update)」を参照してください。  
  
 サポートの詳細は、次のとおりです。  
  
-   ユーザー インターフェイスとコマンド プロンプトの両方からの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アップグレードがサポートされています。 各フェールオーバー クラスター ノードでコマンド プロンプトからアップグレードを実行するか、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ UI を使用して各クラスター ノードをアップグレードできます。  詳細については、「[SQL Server フェールオーバー クラスター インスタンスのアップグレード &#40;セットアップ&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)」および「[コマンド プロンプトからの SQL Server のインストール](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)」を参照してください。  
  
-   次のシナリオは、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] アップグレードではサポートされていません。  
  
    -   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のスタンドアロン インスタンスからフェールオーバー クラスターにはアップグレードできません。  
  
    -   フェールオーバー クラスターに機能を追加することはできません。 たとえば、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)] のみの既存のフェールオーバー クラスターに [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]を追加することはできません。  
  
    -   フェールオーバー クラスター ノードからスタンドアロン インスタンスへのダウングレード。  
  
    -   フェールオーバー クラスターのエディションの変更は、特定のシナリオに制限されています。 詳細については、「 [サポートされているバージョンとエディションのアップグレード](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)」をご覧ください。  
  
-   フェールオーバー クラスターのアップグレードにおけるダウンタイムは、フェールオーバー時間およびアップグレード スクリプトの実行に必要な時間のみです。 次のフェールオーバー クラスターのローリング アップグレード プロセスに従い、さらに、すべてのノードですべての前提条件を満たしてから、アップグレード プロセスを開始することで、ダウンタイムを最小限に抑えることができます。 メモリ最適化テーブルを使用している場合、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] をアップグレードすると、余分な時間がかかることがあります。 詳細については、「 [データベース エンジンのアップグレード計画の策定およびテスト](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md)」を参照してください。  
  
## <a name="prerequisites"></a>Prerequisites  
 作業を開始する前に、次の重要な情報を確認してください。  
  
-   [サポートされているバージョンとエディションのアップグレード](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md):使用している Windows オペレーティング システムのバージョンと [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のバージョンから [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] にアップグレードできることを確認します。 たとえば、SQL Server 2005 フェールオーバー クラスタリング インスタンスから [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] には直接アップグレードできません。また、[!INCLUDE[winxpsvr-md](../../../includes/winxpsvr-md.md)] で実行されているフェールオーバー クラスターをアップグレードすることもできません。  
  
-   [データベース エンジンのアップグレード方法の選択](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md):サポートされるバージョンとエディションのアップグレードを確認して、適切なアップグレードの方法と手順を選択します。また、環境にインストールされているその他のコンポーネントに基づいて、正しい順序でコンポーネントをアップグレードします。  
  
-   [データベース エンジンのアップグレード計画の策定およびテスト](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md):リリース ノート、アップグレードに関する既知の問題、アップグレード前のチェックリストを確認して、アップグレードの計画を作成およびテストします。  
  
-   [SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md): [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] のインストールにおけるソフトウェア要件を確認します。 その他のソフトウェアが必要な場合は、ダウンタイムを最小限に抑えるために、アップグレード プロセスを開始する前に、各ノードにソフトウェアをインストールします。  
  
## <a name="perform-a-rolling-upgrade-or-update"></a>ローリング アップグレードまたは更新の実行  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターを [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]にアップグレードするには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップを使用して、フェールオーバー クラスター ノードをパッシブ ノードから 1 つずつアップグレードします。 各ノードをアップグレードする場合、ノードはフェールオーバー クラスターの実行可能な所有者から除外されます。 予期しないフェールオーバーが発生した場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップによりクラスター リソース グループの所有権がアップグレード済みのノードに移動するまで、アップグレード済みのノードはフェールオーバーに関与しません。  
  
 既定では、アップグレード済みのノードにフェールオーバーする時期は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップにより自動的に決まります。 決定の際に基準になるのは、フェールオーバー クラスター インスタンス内のノード総数、およびアップグレード済みのノード数です。 ノード総数の半数以上がアップグレード済みの場合、次のノードでアップグレードする際、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップにより、アップグレード済みのノードにフェールオーバーが発生します。 アップグレード済みのノードにフェールオーバーする際、クラスター グループはアップグレード済みのノードに移動します。 すべてのアップグレード済みノードは実行可能な所有者の一覧に格納され、まだアップグレードされていないすべてのノードは実行可能な所有者の一覧から削除されます。 残りの各ノードをアップグレードする場合、ノードはフェールオーバー クラスターの実行可能な所有者に追加されます。  
  
 ダウンタイムでのこのプロセス結果は、1 回のフェールオーバー時間、および全フェールオーバー クラスター アップグレード時のデータベース アップグレード スクリプトの実行時間に限定されます。  
  
 アップグレード プロセス中にクラスター ノードのフェールオーバーの動作を制御するには、コマンド プロンプトでアップグレード操作を実行して、/FAILOVERCLUSTERROLLOWNERSHIP パラメーターを使用します。 詳細については、「 [コマンド プロンプトからの SQL Server のインストール](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)」を参照してください。  
  
## <a name="next-steps"></a>次の手順  
 [インストール ウィザードを使用した SQL Server のアップグレード &#40;セットアップ&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [コマンド プロンプトからの SQL Server のインストール](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [SQL Server フェールオーバー クラスター インスタンスのアップグレード &#40;セットアップ&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
  
