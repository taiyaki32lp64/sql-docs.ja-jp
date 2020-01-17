---
title: データベース ミラーリングの監視 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- monitoring [SQL Server], database mirroring
- database mirroring [SQL Server], monitoring
ms.assetid: a7b1b9b0-7c19-4acc-9de3-3a7c5e70694d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bcc63d87bc71fa2497e1282364f87272438bbf97
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212290"
---
# <a name="monitoring-database-mirroring-sql-server"></a>データベース ミラーリングの監視 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ここでは、データベース ミラーリング モニターと **sp_dbmmonitor** システム ストアド プロシージャ、およびデータベース ミラーリングの監視に伴う作業 ( **データベース ミラーリング モニターのジョブ**など) について説明し、データベース ミラーリング セッションについて監視できる情報の概要を示します。 さらに、事前に定義された一連のデータベース ミラーリング イベントに対する警告しきい値を定義する方法、および任意のデータベース ミラーリング イベントでの警告の設定についても説明します。  
  
 ミラーリング セッション中にミラー化されたデータベースを監視すると、データ フローが発生しているかどうかや、データ フローがどの程度適切に行われているかを確認することができます。 サーバー インスタンス上にある 1 つ以上のミラー化されたデータベースの監視を設定および管理するには、データベース ミラーリング モニターまたは **sp_dbmmonitor** システム ストアド プロシージャを使用します。  
  
 **データベース ミラーリング モニターのジョブ**は、データベース ミラーリング モニターから独立して、バックグラウンドで実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが **データベース ミラーリング モニターのジョブ** を定期的に (既定では 1 分間に 1 回) 呼び出し、このジョブは、ミラーリング状態を更新するストアド プロシージャを呼び出します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してミラーリング セッションを開始した場合は、 **データベース ミラーリング モニターのジョブ** が自動的に作成されます。 ALTER DATABASE *<database_name>* SET PARTNER のみを使用してミラーリングを開始した場合は、ストアド プロシージャを実行してジョブを作成する必要があります。  
  
 **このトピックの内容**  
  
-   [ミラーリングの状態の監視](#MonitoringStatus)  
  
-   [ミラー化データベースに関する追加情報](#AdditionalSources)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="MonitoringStatus"></a> ミラーリングの状態の監視  
 サーバー インスタンス上の 1 つ以上のミラー化されたデータベースの監視を設定および管理するには、データベース ミラーリング モニターまたは **dbmmonitor** システム ストアド プロシージャを使用します。 ミラーリング セッション中にミラー化されたデータベースを監視すると、データ フローが発生しているかどうかや、データ フローがどの程度適切に行われているかを確認することができます。  
  
 ミラー化されたデータベースを監視した場合、具体的には次のことを行えます。  
  
-   ミラーリングが機能していることを確認する。  
  
     基本状態には、2 つのサーバー インスタンスが動作しているかどうかを判断するための情報や、それらのサーバーが接続されており、ログがプリンシパルからミラーへ移動中であることを示す情報が含まれています。  
  
-   ミラー データベースがプリンシパル データベースから遅延していないかどうかを特定する。  
  
     高パフォーマンス モードでは、プリンシパル サーバーからミラー サーバーへ送信する必要がある未送信のログ レコードのバックログをプリンシパル サーバーで作成できます。 さらに、どの動作モードの場合も、ログ ファイルに書き込まれ、かつ、ミラー データベースに復元する必要がある、復元されていないログ レコードのバックログをミラー サーバーで作成できます。  
  
-   高パフォーマンス モードにおいて、プリンシパル サーバー インスタンスが使用できなくなった場合に、損失したデータ量を特定する。  
  
     未送信のトランザクション ログ (存在する場合) の量と、失われたトランザクションがプリンシパルでコミットされた期間を調べることによって、データ損失を特定できます。  
  
-   現在のパフォーマンスを過去のパフォーマンスと比較する。  
  
     問題が発生した場合、データベース管理者は、ミラーリング パフォーマンスの履歴を表示することで、現在の状態の理解に役立てることができます。 履歴を調べると、パフォーマンスの傾向を検出することや、パフォーマンス上の問題のパターン (ネットワークが低速な時間帯やログに入力されるコマンド数が非常に多い場合など) を特定することができます。  
  
-   ミラーリング パートナー間のデータ フローが減少した原因のトラブルシューティングを行う。  
  
-   主要なパフォーマンス基準に警告しきい値を設定する。  
  
     しきい値を超える値が新しい状態行に含まれている場合、情報イベントが Windows イベント ログに送信されます。 その場合、システム管理者は、それらのイベントに基づいて手動で警告を構成できます。 詳細については、「 [ミラーリング パフォーマンス基準の警告しきい値および警告の使用 &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)」を参照してください。  
  
###  <a name="tools_for_monitoring_dbm_status"></a> データベース ミラーリングの状態を監視するためのツール  
 ミラーリングの状態は、データベース ミラーリング モニターまたは **sp_dbmmonitorresults** システム ストアド プロシージャを使用して監視できます。 これらのツールを使用すると、どちらのシステム管理者も、ローカル サーバー インスタンス上でミラー化されたデータベースのデータベース ミラーリングを監視できます。この場合のシステム管理者は、 **sysadmin** 固定サーバー ロールのメンバー、およびシステム管理者によって **msdb** データベースの **dbm_monitor** 固定データベース ロールに追加されたユーザーです。 どちらのツールを使用した場合も、システム管理者はミラーリングの状態を手動で更新することもできます。  
  
> [!NOTE]  
>  システム管理者は主要なパフォーマンス基準の警告しきい値を構成および表示することもできます。 詳細については、「 [ミラーリング パフォーマンス基準の警告しきい値および警告の使用 &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)」を参照してください。  
  
-   データベース ミラーリング モニター (Database Mirroring Monitor)  
  
     データベース ミラーリング モニターは、システム管理者が状態を表示および更新し、いくつかの主要なパフォーマンス基準の警告しきい値を構成できるグラフィカル ユーザー インターフェイス ツールです。 また、 **dbm_monitor** 固定データベース ロールのメンバーは、状態テーブルを更新することはできませんが、データベース ミラーリング モニターを使用して、ミラーリング状態テーブルの最新の行を表示できます。  
  
     データベース ミラーリング モニターでは、選択したデータベースの状態 (パフォーマンス基準を含む) が **[状態]** タブ ページに表示されます。 このページには、プリンシパル サーバー インスタンスとミラー サーバー インスタンスの両方から取得された情報が表示されます。 状態はプリンシパル サーバー インスタンスとミラー サーバー インスタンスへの別個の接続を使用して収集されるので、このページの値は非同期に設定されます。 データベース ミラーリング モニターでは、30 秒間隔で状態テーブルの更新を試行します。 更新が成功するのは、状態テーブルが 15 秒以内に更新されず、ユーザーが **sysadmin** 固定サーバー ロールのメンバーである場合だけです。 **[状態]** ページで報告される情報の概要については、後の「 [データベース ミラーリング モニターに表示される状態](#perf_metrics_of_dbm_monitor)」を参照してください。  
  
     データベース ミラーリング モニターのインターフェイスの概要については、「 [Database Mirroring Monitor Overview](../../database-engine/database-mirroring/database-mirroring-monitor-overview.md)」を参照してください。 データベース ミラーリング モニターの起動方法については、「 [データベース ミラーリング モニターの起動 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)」を参照してください。  
  
-   システム ストアド プロシージャ  
  
     **sp_dbmmonitorresults** システム ストアド プロシージャを実行することによって、現在の状態を取得または更新することもできます。 他の dbmmonitor ストアド プロシージャを使用すると、監視の設定、監視パラメーターの変更、現在の更新期間の表示、およびサーバー インスタンスの監視の削除を行えます。  
  
     次の表では、データベース ミラーリング モニターとは別にデータベース ミラーリングの監視を管理および使用するためのストアド プロシージャについて説明します。  
  
    |手順|[説明]|  
    |---------------|-----------------|  
    |[sp_dbmmonitoraddmonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)|サーバー インスタンス上のミラー化されたデータベースごとに、定期的に状態情報を更新するジョブを作成します。|  
    |[sp_dbmmonitorchangemonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)|データベース ミラーリング監視パラメーターの値を変更します。|  
    |[sp_dbmmonitorhelpmonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)|現在の更新間隔を返します。|  
    |[sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)|監視対象のデータベースの状態行を返すので、このプロシージャで事前に最新の状態を取得するかどうかを選択できます。|  
    |[sp_dbmmonitordropmonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)|サーバー インスタンスのすべてのデータベースに対し、ミラーリング監視ジョブを停止して削除します。|  
  
     **dbmmonitor** システム ストアド プロシージャは、データベース ミラーリング モニターを補完するものとして使用できます。 たとえば、 **sp_dbmmonitoraddmonitoring**を使用して監視が構成されていても、データベース ミラーリング モニターを使用して状態を表示できます。  
  
### <a name="how-monitoring-works"></a>監視のしくみ  
 ここでは、データベース ミラーリングの状態テーブル、データベース ミラーリング モニターのジョブとモニター、データベース ミラーリングの状態の監視方法、および監視ジョブの削除方法について説明します。  
  
#### <a name="database-mirroring-status-table"></a>データベース ミラーリング状態テーブル  
 データベース ミラーリングの状態は、 **msdb** データベース内部の、文書化されていないデータベース ミラーリング状態テーブルに格納されます。 この状態テーブルは、ミラーリングの状態がサーバー インスタンス上で最初に更新されたときに自動的に作成されます。  
  
 状態テーブルは、システム管理者が自動または手動のいずれかの方法で更新でき、最小更新間隔は 15 秒です。 最小更新間隔である 15 秒を設定すると、状態の要求によってサーバー インスタンスが過負荷になるのを防ぐことができます。  
  
 状態テーブルは、データベース ミラーリング モニターと、実行されている場合にはデータベース ミラーリング モニターのジョブの両方によって自動的に更新されます。 **[データベース ミラーリング モニターのジョブ]** では、既定により 1 分間に 1 回、状態テーブルを更新します (システム管理者は更新間隔として 1 ～ 120 分を指定できます)。 これに対しデータベース ミラーリング モニターでは、30 秒ごとに自動的に状態テーブルを更新します。 これらの更新では、 **[データベース ミラーリング モニターのジョブ]** およびデータベース ミラーリング モニターによって **sp_dbmmonitorupdate**が呼び出されます。  
  
 **sp_dbmmonitorupdate** 初回実行時には、 **msdb** データベース内に **データベース ミラーリングの状態** テーブルと固定データベース ロール **dbm_monitor** が作成されます。 **sp_dbmmonitorupdate** では、通常、サーバー インスタンス上のミラー化されたデータベースごとに、新しい行を状態テーブルに挿入することによってミラーリングの状態を更新します。詳細については、このトピックの「データベース ミラーリング状態テーブル」を参照してください。 また、このプロシージャは、新しい行のパフォーマンス基準を評価して、現在の保有期間 (既定では 7 日) よりも古い行を切り捨てます。 詳細については、「 [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)」を参照してください。  
  
> [!NOTE]  
>  状態テーブルは、 **[データベース ミラーリング モニターのジョブ]** が存在し、 **エージェントが実行されている場合にのみ、自動的に更新されます。ただし、データベース ミラーリング モニターが** sysadmin [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固定サーバー ロールのメンバーによって使用中の場合は除きます。  
  
#### <a name="database-mirroring-monitor-job"></a>データベース ミラーリング モニターのジョブ  
 データベース ミラーリング モニターのジョブである **[データベース ミラーリング モニターのジョブ]** の動作は、データベース ミラーリング モニターとは独立した動作です。 **[データベース ミラーリング モニターのジョブ]** は、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してミラーリング セッションを開始した場合にのみ、自動的に作成されます。 常に ALTER DATABASE *database_name* SET PARTNER コマンドを使用してミラーリングを開始している場合、このジョブは、システム管理者が **sp_dbmmonitoraddmonitoring** ストアド プロシージャを実行した場合にのみ存在します。  
  
 **[データベース ミラーリング モニターのジョブ]** が作成されると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されている場合、このジョブは既定により 1 分間に 1 回呼び出されます。 次に、このジョブによって **sp_dbmmonitorupdate** システム ストアド プロシージャが呼び出されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントでは、既定により **[データベース ミラーリング モニターのジョブ]** を 1 分間に 1 回呼び出し、このジョブによって **sp_dbmmonitorupdate** が呼び出され、状態テーブルが更新されます。 システム管理者は、 **sp_dbmmonitorchangemonitoring** システム ストアド プロシージャを使用して更新間隔を変更し、 **sp_dbmmonitorchangemonitoring** システム ストアド プロシージャを使用して現在の更新間隔を表示できます。 詳細については、「 [sp_dbmmonitoraddmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md) 」および「 [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)」を参照してください。  
  
#### <a name="monitoring-database-mirroring-status-by-system-administrators"></a>データベース ミラーリングの状態の監視 (システム管理者の場合)  
 **sysadmin** 固定サーバー ロールのメンバーは、状態テーブルの表示と更新を行えます。  
  
-   データベース ミラーリング モニターの使用  
  
     データベース ミラーリング モニターを使用すると、システム管理者は **[状態]** ページ、ナビゲーション ツリー、または **[履歴]** ページを手動で更新できます。 手動で更新した場合も、前回の更新から 15 秒以内に更新されていない限り、状態テーブルが更新されます。  
  
     システム管理者は、サーバー インスタンスの **[状態]** ページにある **[履歴]** ボタンをクリックして、特定のサーバー インスタンスのミラーリングの状態の履歴を表示することもできます。 履歴は、 **[データベース ミラーリングの履歴]** ダイアログ ボックスに表示されます。 システム管理者はこのダイアログ ボックスで、サーバー インスタンスの状態テーブルに含まれている一部またはすべての行を表示できます。  
  
     **[状態]** ページの基準に関する詳細については、後の「データベース ミラーリング モニターに表示されるパフォーマンス基準」を参照してください。  
  
-    **sp_dbmmonitorresults**の使用  
  
     システム管理者は、 **sp_dbmmonitorresults** システム ストアド プロシージャを使用して状態テーブルを表示できます。また、前回の更新から 15 秒以内に更新が行われていない場合には、必要に応じて状態テーブルを更新できます。 このプロシージャは、 **sp_dbmmonitorupdate** プロシージャを呼び出し、プロシージャ コールでの要求数に応じて 1 つ以上の履歴行を返します。 返される結果セットの状態に関する詳細については、「 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)」を参照してください。  
  
#### <a name="monitoring-database-mirroring-status-by-dbm_monitor-members"></a>データベース ミラーリングの状態の監視 (dbm_monitor メンバーの場合)  
 既に説明したように、 **sp_dbmmonitorupdate** の初回実行時に、 **dbm_monitor** 固定データベース ロールが **msdb** データベースに作成されます。 **dbm_monitor** 固定データベース ロールのメンバーは、データベース ミラーリング モニターまたは **sp_dbmmonitorresults** ストアド プロシージャを使用して既存のミラーリングの状態を表示できます。 ただし、これらのユーザーは状態テーブルを更新できません。 表示された状態の古さを調べるには、**[状態]** ページの **[プリンシパル ログ (**_\<time>_**)]** ラベルと **[ミラー ログ (**_\<time>_**)]** ラベルで時刻を確認できます。  
  
 **dbm_monitor** 固定データベース ロールのメンバーは、 **[データベース ミラーリング モニターのジョブ]** を使用して定期的に状態テーブルを更新します。 ジョブが存在しない場合や [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが停止している場合、状態が急速に古くなり、ミラーリング セッションの構成を反映しなくなることがあります。 たとえば、フェールオーバー後、パートナーがプリンシパルまたはミラーなどの同じロールを共有しているように見えたり、現在のプリンシパル サーバーがミラー サーバーとして表示され、その一方で現在のミラー サーバーがプリンシパルとして表示されたりすることがあります。  
  
#### <a name="dropping-the-database-mirroring-monitor-job"></a>データベース ミラーリング モニターのジョブの削除  
 データベース ミラーリング モニターのジョブである **[データベース ミラーリング モニターのジョブ]** は、削除するまでなくなりません。 監視ジョブは、システム管理者が管理する必要があります。 **[データベース ミラーリング モニターのジョブ]** を削除するには、 **sp_dbmmonitordropmonitoring**を使用します。 詳細については、「 [sp_dbmmonitordropmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)」を参照してください。  
  
###  <a name="perf_metrics_of_dbm_monitor"></a> データベース ミラーリング モニターに表示される状態  
 データベース ミラーリング モニターの **[状態]** ページには、パートナーと、ミラーリング セッションの状態が表示されます。 この情報には、トランザクション ログの状態、フェールオーバーを完了するために必要な時間を推測するのに役立つその他の情報、データ損失の可能性 (セッションが同期されていない場合) などのパフォーマンス基準が含まれます。 さらに、 **[状態]** ページには、ミラーリング セッションに関する一般的な状態と情報が表示されます。  
  
> [!NOTE]  
>  データベース ミラーリング モニターと **[状態]** ページの概要については、前述の「 [データベース ミラーリングの状態を監視するためのツール](#tools_for_monitoring_dbm_status)」を参照してください。  
  
 次のセクションでは、このページに表示される情報の概要を示します。  
  
#### <a name="partners"></a>パートナー  
 **[状態]** ページには、次の情報がパートナーごとに表示されます。  
  
-   サーバー インスタンス  
  
     **[状態]** 行に状態が表示されているサーバー インスタンス名。  
  
-   現在のロール  
  
     サーバー インスタンスの現在のロール。 表示される状態は次のとおりです。  
  
    -   プリンシパル  
  
    -   ミラー  
  
-   ミラーリング状態  
  
     表示される状態は次のとおりです。  
  
    -   Unknown  
  
    -   [同期中]  
  
    -   同期済み  
  
    -   中断  
  
    -   切断済み  
  
-   ミラーリング監視サーバーの接続  
  
     ミラーリング監視サーバーの接続状態。 表示される状態は次のとおりです。  
  
    -   Unknown  
  
    -   接続済み  
  
    -   [接続解除されました。]  
  
#### <a name="log-on-the-principal-server"></a>プリンパル サーバーへのログオン  
 **[状態]** ページには、表示された時点での、プリンシパル サーバーへのログオンの状態に関する次の情報が表示されます。  
  
-   未送信のログ  
  
     送信キューで待機中のログの量 (KB 単位)。  
  
-   最も古い未送信のトランザクション  
  
     送信キュー内で最も古い未送信トランザクションの経過期間。 トランザクションの経過期間は、トランザクションがミラー サーバー インスタンスに送信されないまま経過した時間を分単位で示します。 この値は、データ損失の可能性を時間の観点から測定するのに役立ちます。  
  
-   ログの送信時間 (推定)  
  
     プリンシパル サーバー インスタンスが、現在送信キューに格納されているログをミラー サーバー インスタンスに送信するのに必要な時間 (分)。現在の送信速度に基づく推定値です。 ログの送信にかかる実際の時間は、受信トランザクションの速度の影響を受け、大きく異なることがあります。 ただし、 **[ログの送信時間 (推定)]** の値は、手動フェールオーバーに必要な時間を大まかに推定する際に役立つことがあります。  
  
-   [現在の送信率]  
  
     トランザクションをミラー サーバー インスタンスに送信しているときの速度 (KB/秒)。  
  
-   新しいトランザクションの現在の比率  
  
     受信トランザクションをプリンシパルのログに入力しているときの速度 (KB/秒)。 ミラーリングで遅延、待機、遅延の解消が発生しているかどうかを特定するには、この値を **[ログの送信時間 (推定)]** の値と比較します。  
  
#### <a name="log-on-the-mirror-server"></a>ミラー サーバーへのログオン  
 **[状態]** ページには、表示された時点での、ミラー サーバーへのログオンの状態に関する次の情報が表示されます。  
  
-   未復元のログ  
  
     再実行キューで待機中のログの量 (KB 単位)。  
  
-   ログの復元時間 (推定)  
  
     現在再実行キューに格納されているログをミラー データベースに適用するために必要な時間の概算値 (分)。  
  
-   [現在の復元比率]  
  
     トランザクションをミラー データベースに復元するときの速度 (KB/秒)。  
  
#### <a name="mirroring-session"></a>ミラーリング セッション  
 さらに、 **[状態]** ページには、ミラーリング セッションについて次の情報が表示されます。  
  
-   ミラー コミットのオーバーヘッド  
  
     1 トランザクションあたりの平均遅延時間 (ミリ秒単位)。高い安全性モードのみに関連します。 この遅延時間は、ミラー サーバー インスタンスによってトランザクションのログ レコードが再実行キューに書き込まれるのをプリンシパル サーバー インスタンスが待機している間、発生したオーバーヘッドの量になります。  
  
-   現在のすべてのログを送信して復元する時間 (推定)  
  
     プリンシパルでコミットされていないすべての未送信ログを送信して、現在再実行キューに格納されているすべてのログを復元するために必要な時間の推定値。 送信と復元が並行して実行される可能性があるので、この推定値は、 **[ログの送信時間 (推定)]** フィールドの値と **[ログの復元時間 (推定)]** フィールドの値の和よりも小さい場合があります。  
  
-   ミラーリング監視アドレス  
  
     ミラーリング監視サーバー インスタンスのネットワーク アドレス。 このアドレスの形式の詳細については、「[サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)」を参照してください。  
  
-   動作モード  
  
     データベース ミラーリング セッションには、次の動作モードがあります。  
  
    -   [高パフォーマンス (非同期)]  
  
    -   [自動フェールオーバーを伴わない高い安全性 (同期)]  
  
    -   [自動フェールオーバーを伴う高い安全性 (同期)]  
  
##  <a name="AdditionalSources"></a> ミラー化データベースに関する追加情報  
 ミラー化されたデータベースの監視および監視対象のパフォーマンス変数に対する警告の設定を行う手段として、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] には、データベース ミラーリング モニターと dbmmonitor ストアド プロシージャ以外に、データベース ミラーリングに関するカタログ ビュー、パフォーマンス カウンター、およびイベント通知が用意されています。  
  
 **このセクションの内容**  
  
-   [データベース ミラーリング メタデータ](#DbmMetadata)  
  
-   [データベース ミラーリングのパフォーマンス カウンター](#DbmPerfCounters)  
  
-   [データベース ミラーリングのイベント通知](#DbmEventNotif)  
  
###  <a name="DbmMetadata"></a> データベース ミラーリング メタデータ  
 次のカタログ ビューまたは動的管理ビューによって公開されるメタデータに、各データベース ミラーリング セッションに関する説明が記述されています。  
  
-   **sys.database_mirroring**  
  
     このビューには、サーバー インスタンス内のミラー化されたそれぞれのデータベースのデータベース ミラーリング メタデータが表示されます。 詳細については、「[sys.database_mirroring &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)」を参照してください。  
  
-   **sys.database_mirroring_endpoints**  
  
     **sys.database_mirroring_endpoints** カタログ ビューには、サーバー インスタンスのデータベース ミラーリング エンドポイントに関する情報が表示されます。 詳細については、「[sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)」を参照してください。  
  
-   **sys.database_mirroring_witnesses**  
  
     このカタログ ビューには、サーバー インスタンスがミラーリング監視サーバーである、各セッションのデータベース ミラーリング メタデータが表示されます。 詳細については、「[sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)」を参照してください。  
  
-   **sys.dm_db_mirroring_connections**  
  
     この動的管理ビューにより、データベース ミラーリングのネットワーク接続ごとに 1 行が返されます。  
  
     詳細については、「[sys.dm_db_mirroring_connections &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections.md)」を参照してください。  
  
###  <a name="DbmPerfCounters"></a> データベース ミラーリングのパフォーマンス カウンター  
 パフォーマンス カウンターを使用すると、データベース ミラーリングのパフォーマンスを監視できます。 たとえば、データベース ミラーリングがプリンシパル サーバーのパフォーマンスに影響を及ぼしているかどうかを確認するには、 **Transaction Delay** カウンターを調べることができます。また、ミラー データベースとプリンシパル データベース間の遅延時間がいかに少ないかを確認するには、 **Redo Queue** カウンターと **Log Send Queue** カウンターを調べることができます。 1 秒間に送信されたログの量を監視する場合は、 **Log Bytes Sent/sec** カウンターを調べることができます。  
  
 パフォーマンス カウンターは、いずれかのパートナーのパフォーマンス モニターにあるデータベース ミラーリング パフォーマンス オブジェクト (**SQLServer:Database Mirroring**) で使用できます。 詳しくは、「 [SQL Server:Database Mirroring オブジェクト](../../relational-databases/performance-monitor/sql-server-database-mirroring-object.md)」を参照してください。  
  
 **パフォーマンス モニターを起動するには**  
  
-   [システム モニターの起動 &#40;Windows&#41;](../../relational-databases/performance/start-system-monitor-windows.md)  
  
###  <a name="DbmEventNotif"></a> データベース ミラーリングのイベント通知  
 イベント通知は、特殊なデータベース オブジェクトです。 さまざまな Transact-SQL データ定義言語 (DDL) ステートメントや SQL トレースのイベントに応答してイベント通知が行われ、サーバー イベントとデータベース イベントに関する情報を [!INCLUDE[ssSB](../../includes/sssb-md.md)] サービスに送信します。  
  
 データベース ミラーリングでは、次のイベントを使用できます。  
  
-   **Database Mirroring State Change** イベント クラス  
  
     ミラー化されたデータベースのミラーリングの状態が変更された時点を示します。 詳細については、「 [Database Mirroring State Change Event Class](../../relational-databases/event-classes/database-mirroring-state-change-event-class.md)」を参照してください。  
  
-   **Audit Database Mirroring Login** イベント クラス  
  
     このクラスでは、データベース ミラーリングのトランスポート セキュリティに関連する監査メッセージを報告します。 詳細については、「 [Audit Database Mirroring Login Event Class](../../relational-databases/event-classes/audit-database-mirroring-login-event-class.md)」を参照してください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [ミラーリング パフォーマンス基準の警告しきい値および警告の使用 &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md)  
  
-   [データベース ミラーリング モニターの起動 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [ミラー化されたデータベースの状態の確認 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/view-the-state-of-a-mirrored-database-sql-server-management-studio.md)  
  
 **ストアド プロシージャ**  
  
-   [sp_dbmmonitoraddmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)  
  
-   [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)  
  
-   [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)  
  
-   [sp_dbmmonitordropmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorhelpalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)  
  
-   [sp_dbmmonitorhelpmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)  
  
-   [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
-   [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [WMI Provider for Server Events の概念](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)  
  
  
