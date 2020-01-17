---
title: レプリケーション エージェントの管理 | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, administering
- Log Reader Agent, administering
- Queue Reader Agent, administering
- shared agents [SQL Server replication]
- Merge Agent, administering
- Distribution Agent, administering
- agents [SQL Server replication], administering
- replication cleanup jobs [SQL Server]
- administering replication, agents
- replication [SQL Server], administering
- independent agents [SQL Server replication]
ms.assetid: f27186b8-b1b2-4da0-8b2b-91f632c2ab7e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 93527accb44bd192e1468ea4176702173bf74114
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768221"
---
# <a name="replication-agent-administration"></a>レプリケーション エージェントの管理
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  レプリケーション エージェントは、レプリケーションに関連した数多くのタスクを実行します。たとえば、スキーマとデータのコピーの作成、パブリッシャーまたはサブスクライバーでの更新の検出、およびサーバー間での変更の反映などを行います。 既定では、レプリケーション エージェントは [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェントのジョブ ステップで実行されます。 エージェントは単なる実行可能ファイルであるため、コマンド ラインやバッチ スクリプトから直接呼び出すこともできます。 各レプリケーション エージェントでは、ランタイム パラメーターのセットを使用して実行方法を制御できます。このパラメーターはエージェント プロファイルまたはコマンド ラインで指定します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインストール時に、サービスがインストール中に自動開始されるように明示的に選択しない限り、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エージェント サービスは既定で無効になります。  
  
 レプリケーション エージェントのファイルは、 [!INCLUDE[ssInstallPathVar](../../../includes/ssinstallpathvar-md.md)]\COM に保存されています。 次の表は、レプリケーション実行可能ファイル名およびファイル名を示しています。 パラメーター参照を表示するにはエージェントのリンクをクリックしてください。  
  
|エージェント実行可能ファイル|[ファイル名]|  
|----------------------|---------------|  
|[レプリケーション スナップショット エージェント](../../../relational-databases/replication/agents/replication-snapshot-agent.md)|snapshot.exe|  
|[Replication Distribution Agent](../../../relational-databases/replication/agents/replication-distribution-agent.md)|distrib.exe|  
|[レプリケーション ログ リーダー エージェント](../../../relational-databases/replication/agents/replication-log-reader-agent.md)|logread.exe|  
|[レプリケーション キュー リーダー エージェント](../../../relational-databases/replication/agents/replication-queue-reader-agent.md)|qrdrsvc.exe|  
|[Replication Merge Agent](../../../relational-databases/replication/agents/replication-merge-agent.md)|replmerg.exe|  
  
 レプリケーション エージェントに加え、レプリケーションには定期的なメンテナンスおよび要求時メンテナンスを実行するさまざまなジョブがあります。  
  
 **エージェントおよびメンテナンス ジョブを実行するには**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] およびレプリケーション モニター: [レプリケーション エージェントを起動および停止する &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)  
  
-   レプリケーション プログラミング: [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
## <a name="agent-profiles"></a>[エージェント プロファイル]  
 レプリケーションを構成すると、エージェント プロファイルのセットがディストリビューターにインストールされます。 エージェント プロファイルには、エージェントが実行されるたびに使用されるパラメーターのセットが含まれています。スタートアップ処理中に各エージェントはディストリビューターにログインし、各エージェントのプロファイルのパラメーターをクエリします。 レプリケーションでは、各エージェント用の既定のプロファイルの他に、ログ リーダー エージェント、ディストリビューション エージェント、およびマージ エージェント用の追加の定義済みプロファイルが利用できます。 提供されているプロファイルに加えて、アプリケーションの要件に合わせてプロファイルを作成することもできます。 詳しくは、「 [レプリケーション エージェント プロファイル](../../../relational-databases/replication/agents/replication-agent-profiles.md)」をご覧ください。  
  
 コマンド ラインでパラメーターを直接指定する方法の詳細については、「[レプリケーション エージェント実行可能ファイルの概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)」を参照してください。  
  
## <a name="monitoring-replication-agents"></a>レプリケーション エージェントの監視  
 レプリケーション モニターを使用すると、各レプリケーション エージェントに関連する情報を表示し、タスクを実行できます。 次の一覧に、各エージェント、各エージェントを利用できるレプリケーション モニターのタブ、およびそれらのタブへのアクセス方法について説明しているトピックへのリンクを示します。  
  
-   以下のエージェントは、レプリケーション モニターでパブリケーションと関連付けられています。  
  
    -   スナップショット エージェント  
  
    -   ログ リーダー エージェント (Log Reader Agent)  
  
    -   キュー リーダー エージェント (Queue Reader Agent)  
  
     これらのエージェントに関連付けられている情報およびタスクにアクセスするには、 **[エージェント]** タブを使用します。詳細については、「[View information and perform tasks using Replication Monitor](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)」 (レプリケーション モニターを使用して情報を表示し、タスクを実行する) を参照してください。  
  
-   以下のエージェントは、レプリケーション モニターでサブスクリプションと関連付けられています。  
  
    -   ディストリビューション エージェント  
  
    -   [マージ エージェント]  
  
     これらのエージェントに関連付けられている情報およびタスクにアクセスするには、次のタブを使用します。 **[サブスクリプション ウォッチ リスト]** (各パブリッシャーで使用可能)、または **[すべてのサブスクリプション]** タブ (各パブリケーションで使用可能)。 詳細については、「[レプリケーション モニターを使用して情報を表示し、タスクを実行する](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)」を参照してください。  
  
## <a name="independent-and-shared-agents"></a>独立したエージェントと共有エージェント  
 独立したエージェントとは、1 つのサブスクリプションを処理するエージェントのことです。 共有エージェントは複数のサブスクリプションにサービスを提供します。同じ共有エージェントを使用している複数のサブスクリプションで同期する必要がある場合、既定では、それらのサブスクリプションはキューに格納されて待機し、共有エージェントがそれらを一度に 1 つずつ処理します。 独立したエージェントは、サブスクリプションが必要に応じていつでも同期できるように常に待機しているので、待機時間が短くなります。 マージ レプリケーションでは常に独立したエージェントが使用され、トランザクション レプリケーションでは、既定ではパブリケーションの新規作成ウィザードで作成されたパブリケーションに対して独立したエージェントが使用されます (以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]では、トランザクション レプリケーションは既定で共有エージェントを使用していました)。  
  
## <a name="replication-maintenance-jobs"></a>レプリケーション メンテナンス ジョブ  
 レプリケーションでは、次のジョブを使用して定期的なメンテナンスおよび要求時メンテナンスを実行します。  
  
|クリーンアップ ジョブ|[説明]|既定のスケジュール|  
|------------------|-----------------|----------------------|  
|エージェント履歴のクリーンアップ: Distribution|ディストリビューション データベースからレプリケーション エージェントの履歴を削除します。|10 分おきに実行されます。|  
|ディストリビューションのクリーンアップ: Distribution|ディストリビューション データベースからレプリケートされたトランザクションを削除します。 |10 分おきに実行されます。|  
|有効期限が切れたサブスクリプションのクリーンアップ|パブリケーション データベースから期限切れのサブスクリプションを検出し、削除します。 ディストリビューターで、ディストリビューションの最大保有期間内に同期されなかったサブスクリプションを非アクティブ化します。|毎日、午前 1 時に実行されます。| 
|データ検証で問題が見つかったサブスクリプションの再初期化|データ検証に失敗したすべてのサブスクリプションを検出し、再初期化のマークを付けます。 次回マージ エージェントまたはディストリビューション エージェントが実行されたときに、サブスクライバーで新しいスナップショットが適用されます。|既定のスケジュールはありません。既定では、有効ではありません。|  
|レプリケーション エージェントの検査|履歴をログに記録していないレプリケーション エージェントを検出します。 ジョブ ステップが失敗した場合に、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows イベント ログに書き込みます。|10 分おきに実行されます。|  
|ディストリビューションのレプリケーション モニターの状態更新機能|レプリケーション モニターで使用される、キャッシュされたクエリを更新します。|連続的に実行されます。|  
  
## <a name="see-also"></a>参照  
 [レプリケーションの監視](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
