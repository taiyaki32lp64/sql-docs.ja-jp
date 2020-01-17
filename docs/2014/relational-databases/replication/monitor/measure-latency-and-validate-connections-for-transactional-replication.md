---
title: トランザクション レプリケーションの待機時間の計測および接続の検証 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, performance
- tracer tokens [SQL Server replication]
- latency [SQL Server replication]
- transactional replication, tracer tokens
- monitoring performance [SQL Server replication], tracer tokens
ms.assetid: 4addd426-7523-4067-8d7d-ca6bae4c9e34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 89149645524adedf01b8d9fb7c116cf0ab0f26c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62667889"
---
# <a name="measure-latency-and-validate-connections-for-transactional-replication"></a>トランザクション レプリケーションの待機時間の計測および接続の検証
  このトピックでは、 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] でレプリケーション モニター、 [!INCLUDE[tsql](../../../includes/tsql-md.md)]、またはレプリケーション管理オブジェクト (RMO) を使用し、トランザクション レプリケーションの待機時間を計測して接続を検証する方法について説明します。 トランザクション レプリケーションには、トレーサー トークン機能が用意されており、これによって簡単にトランザクション レプリケーション トポロジにおける待機時間を計測したり、パブリッシャー、ディストリビューター、およびサブスクライバーの間の接続を検証したりすることができます。 トークン (小さなデータ) は、通常のレプリケートされたトランザクションのようにマークが付けられてパブリケーション データベースのトランザクション ログに書き込まれ、システムを介して送信されることで、次の計算が可能になります。  
  
-   パブリッシャーでコミットされるトランザクションと、ディストリビューターでディストリビューション データベース内に挿入される対応するコマンドの間での経過時間。  
  
-   ディストリビューション データベース内に挿入されるコマンドと、サブスクライバーでコミットされる対応するトランザクションの間での経過時間。  
  
 これらの計算結果から、以下のようなさまざまな内容を特定できます。  
  
-   変更内容をパブリッシャーから受信するのに最も時間がかかるのはどのサブスクライバーか。  
  
-   トレース トークンを受信することになっているサブスクライバーのうち、受信していないサブスクライバーがあるか。あるとすればどのサブスクライバーか。  
  
 **このトピックの内容**  
  
-   **作業を開始する準備:**  
  
     [制限事項と制約事項](#Restrictions)  
  
-   **接続の待機時間を計測して検証するために使用するもの:**  
  
     [SQL Server レプリケーション モニター](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [レプリケーション管理オブジェクト (Replication Management Objects)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
  
###  <a name="Restrictions"></a> 制限事項と制約事項  
 トレーサー トークンは、システムを停止する場合にも役立ちます。このとき、すべての処理を停止して、すべてのノードがすべての未処理の変更を受信したかどうかを検証します。 詳細については、「[レプリケーション トポロジの停止 &#40;レプリケーション Transact-SQL プログラミング&#41;](../administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)」を参照してください。  
  
 トレーサー トークンを使用するには、特定のバージョンの [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]を使用する必要があります。  
  
-   ディストリビューターは [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降である必要があります。  
  
-   パブリッシャーは [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降であるか、Oracle パブリッシャーである必要があります。  
  
-   プッシュ サブスクリプションでは、サブスクライバーが [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 以降である場合に、トレーサー トークン統計がパブリッシャー、ディストリビューター、およびサブスクライバーから収集されます。  
  
-   プル サブスクリプションでは、サブスクライバーが [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以降である場合にのみ、トレーサー トークン統計がサブスクライバーから収集されます。 サブスクライバーが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 7.0 または [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)]である場合は、統計はパブリッシャーおよびディストリビューターからのみ収集されます。  
  
 その他にも、次のような問題点と制限事項について注意する必要があります。  
  
-   トレーサー トークンを受信するには、サブスクリプションをアクティブにする必要があります。 サブスクリプションは、初期化されている場合はアクティブです。  
  
-   再初期化を行うと、関連するサブスクリプションに対する保留中のトレーサー トークンがすべて削除されます。  
  
-   サブスクライバーは、初期同期の完了後に作成されたトレーサー トークンのみを受信します。  
  
-   レーサ トークンは、再パブリッシュ サブスクライバーからは転送されません。  
  
-   セカンダリにフェールオーバーした後、レプリケーション モニターは [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のパブリッシング インスタンスの名前を調整できません。引き続き、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の元のプライマリ インスタンスの名前を使ってレプリケーション情報を表示します。 フェールオーバー後は、トレーサー トークンはレプリケーション モニターを使用して入力できませんが、新しいパブリッシャーで [!INCLUDE[tsql](../../../includes/tsql-md.md)]を使用して入力されたトレース トークンがレプリケーション モニターに表示されます。  
  
##  <a name="SSMSProcedure"></a> SQL Server レプリケーション モニターの使用  
 レプリケーション モニターの起動の詳細については、「[Start the Replication Monitor](start-the-replication-monitor.md)」 (レプリケーション モニターの開始) を参照してください。  
  
#### <a name="to-insert-a-tracer-token-and-view-information-on-the-token"></a>トレーサー トークンを挿入してトークンの情報を表示するには  
  
1.  左ペインでパブリッシャー グループを展開し、パブリッシャーを展開して、パブリケーションをクリックします。  
  
2.  **[トレーサー トークン]** タブをクリックします。  
  
3.  **[トレーサーの挿入]** をクリックします。  
  
4.  次の列にトレーサー トークンの経過時間を表示します。 **[Publisher to Distributor]\(パブリッシャーからディストリビューターまで\)** 、 **[Distributor to Subscriber]\(ディストリビューターからサブスクライバーまで\)** 、 **[合計待機時間]** 。 **[保留中]** と表示された場合は、トークンが特定のポイントに到達していないことを示します。  
  
#### <a name="to-view-information-on-a-tracer-token-inserted-previously"></a>以前に挿入したトレーサー トークンの情報を表示するには  
  
1.  左ペインでパブリッシャー グループを展開し、パブリッシャーを展開して、パブリケーションをクリックします。  
  
2.  **[トレーサー トークン]** タブをクリックします。  
  
3.  **[挿入された時間]** ボックスで時間を選択します。  
  
4.  次の列にトレーサー トークンの経過時間を表示します。 **[Publisher to Distributor]\(パブリッシャーからディストリビューターまで\)** 、 **[Distributor to Subscriber]\(ディストリビューターからサブスクライバーまで\)** 、 **[合計待機時間]** 。 **[保留中]** と表示された場合は、トークンが特定のポイントに到達していないことを示します。  
  
    > [!NOTE]  
    >  トレーサー トークン情報は、ディストリビューション データベースの履歴保持期間の制約を受けるその他の履歴データと同じ期間保持されます。 ディストリビューション データベースのプロパティの変更方法の詳細については、「[ディストリビューターとパブリッシャーのプロパティの表示および変更](../view-and-modify-distributor-and-publisher-properties.md)」を参照してください。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-post-a-tracer-token-to-a-transactional-publication"></a>トレーサー トークンをトランザクション パブリケーションに通知するには  
  
1.  (省略可) パブリッシャー側のパブリケーション データベースに対して、[sp_helppublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql) を実行します。 パブリケーションが存在すること、および状態がアクティブであることを確認します。  
  
2.  (省略可) パブリッシャー側のパブリケーション データベースに対して、[sp_helpsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql) を実行します。 サブスクリプションが存在すること、および状態がアクティブであることを確認します。  
  
3.  パブリッシャー側のパブリケーション データベースに対して、[sp_posttracertoken &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-posttracertoken-transact-sql) を実行して、 **@publication** を指定します。 **@tracer_token_id** 出力パラメーターの値をメモします。  
  
#### <a name="to-determine-latency-and-validate-connections-for-a-transactional-publication"></a>待機時間を決定し、トランザクション パブリケーションの接続を確認するには  
  
1.  上述の手順を使用して、トレーサー トークンをパブリケーションに通知します。  
  
2.  パブリッシャー側のパブリケーション データベースに対して、 **@publication** を指定して、[sp_helptracertokens &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql) を実行します。 パブリケーションに通知されたすべてのトレーサー トークンのリストが返されます。 結果セットの目的の **tracer_id** を確認します。  
  
3.  パブリッシャー側のパブリケーション データベースで、 **@publication** を指定し、 **@tracer_id** に手順 2 のトレーサー トークン ID を指定して、[sp_helptracertokenhistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptracertokenhistory-transact-sql) を実行します。 選択したトレーサー トークンの待機情報が返されます。  
  
#### <a name="to-remove-tracer-tokens"></a>トレーサー トークンを削除するには  
  
1.  パブリッシャー側のパブリケーション データベースに対して、 **@publication** を指定して、[sp_helptracertokens &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptracertokens-transact-sql) を実行します。 パブリケーションに通知されたすべてのトレーサー トークンのリストが返されます。 結果セットの削除するトレーサー トークンの **tracer_id** を確認します。  
  
2.  パブリッシャー側のパブリケーション データベースで、 **@publication** を指定し、 **@tracer_id** に手順 2 の削除するトレーサー トークン ID を指定して、[sp_deletetracertokenhistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-deletetracertokenhistory-transact-sql) を実行します。  
  
###  <a name="TsqlExample"></a> 例 (Transact-SQL)  
 次の例では、トレーサー トークン レコードを通知し、返された通知済みトレーサー トークンの ID を使用して待機時間情報を表示します。  
  
 [!code-sql[HowTo#sp_tracertokens](../../../snippets/tsql/SQL15/replication/howto/tsql/createtracertokens.sql#sp_tracertokens)]  
  
##  <a name="RMOProcedure"></a> レプリケーション管理オブジェクト (RMO) の使用  
  
#### <a name="to-post-a-tracer-token-to-a-transactional-publication"></a>トレーサー トークンをトランザクション パブリケーションに通知するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、パブリッシャーへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.TransPublication> クラスのインスタンスを作成します。  
  
3.  パブリケーションの <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> プロパティおよび <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに手順 1. で作成した接続を設定します。  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドが `false` を返す場合、手順 3. でパブリケーション プロパティを不適切に設定したか、パブリケーションが存在していません。  
  
5.  <xref:Microsoft.SqlServer.Replication.TransPublication.PostTracerToken%2A> メソッドを呼び出します。 このメソッドは、トレーサー トークンをパブリケーションのトランザクション ログに挿入します。  
  
#### <a name="to-determine-latency-and-validate-connections-for-a-transactional-publication"></a>待機時間を決定し、トランザクション パブリケーションの接続を確認するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、ディストリビューターへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A>、 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>、 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>、および <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> の各プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに手順 1. で作成した接続を設定します。  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドが `false` を返す場合は、手順 3. のパブリケーション モニター プロパティが正しく定義されていないか、またはパブリケーションが存在していません。  
  
5.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> メソッドを呼び出します。 返された <xref:System.Collections.ArrayList> オブジェクトを <xref:Microsoft.SqlServer.Replication.TracerToken> オブジェクトの配列にキャストします。  
  
6.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> メソッドを呼び出します。 手順 5. のトレーサー トークンに <xref:Microsoft.SqlServer.Replication.TracerToken.TracerTokenId%2A> の値を渡します。 これにより、 <xref:System.Data.DataSet> オブジェクトとして選択したトレーサー トークンの待機時間情報が返されます。 すべてのトレーサー トークン情報が返された場合、パブリッシャーとディストリビューターとの接続、およびディストリビューターとサブスクライバーの接続が両方とも存在し、レプリケーション トポロジは機能しています。  
  
#### <a name="to-remove-tracer-tokens"></a>トレーサー トークンを削除するには  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> クラスを使用して、ディストリビューターへの接続を作成します。  
  
2.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor> クラスのインスタンスを作成します。  
  
3.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A>、 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>、 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>、および <xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A> の各プロパティを設定し、 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> プロパティに手順 1. で作成した接続を設定します。  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> メソッドを呼び出して、オブジェクトのプロパティを取得します。 このメソッドが `false` を返す場合は、手順 3. のパブリケーション モニター プロパティが正しく定義されていないか、またはパブリケーションが存在していません。  
  
5.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> メソッドを呼び出します。 返された <xref:System.Collections.ArrayList> オブジェクトを <xref:Microsoft.SqlServer.Replication.TracerToken> オブジェクトの配列にキャストします。  
  
6.  <xref:Microsoft.SqlServer.Replication.PublicationMonitor.CleanUpTracerTokenHistory%2A> メソッドを呼び出します。 次の値のいずれかを渡します。  
  
    -   手順 5. のトレーサー トークンの <xref:Microsoft.SqlServer.Replication.TracerToken.TracerTokenId%2A> 。 これにより、選択したトークンの情報が削除されます。  
  
    -   <xref:System.DateTime> オブジェクト。 これにより、指定した日時より古いすべてのトークンの情報が削除されます。  
  
###  <a name="PShellExample"></a>  
