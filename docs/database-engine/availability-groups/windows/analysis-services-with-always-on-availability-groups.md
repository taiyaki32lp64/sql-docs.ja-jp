---
title: Analysis Services と可用性グループ
description: 高可用性ソリューションとして Always On 可用性グループを使用している場合、そのグループ内のデータベースを Analysis Services テーブルまたは多次元ソリューションのデータ ソースとして使用できます。
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 14d16bfd-228c-4870-b463-a283facda965
author: MashaMSFT
ms.author: mathoma
manager: erikre
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 293df346a7eac72f23fa3b3bdd7bbe7994fdc54c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892895"
---
# <a name="analysis-services-with-always-on-availability-groups"></a>Analysis Services と Always On 可用性グループ

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  AlwaysOn 可用性グループは SQL Server リレーショナル データベースの事前に定義されたコレクションで、その中の 1 つのデータベースが条件に従ってフェールオーバーするときに一緒にフェールオーバーし、同じ可用性グループの別のインスタンスのミラー化されたデータベースに要求をリダイレクトします。 高可用性ソリューションとして可用性グループを使用している場合、そのグループ内のデータベースを Analysis Services テーブルまたは多次元ソリューションのデータ ソースとして使用できます。 可用性データベースを使用すると、次の Analysis Services の操作はすべて予期したとおりに動作します。その操作とは、データの処理またはインポート、リレーショナル データへの直接クエリ (ROLAP ストレージまたは DirectQuery モードを使用)、および書き戻しです。  
  
 処理とクエリは、読み取り専用のワークロードです。 このようなワークロードを読み取り可能なセカンダリ レプリカにオフロードすると、パフォーマンスが向上することがあります。 このシナリオには、追加の構成が必要です。 このトピックのチェック リストを使用して、すべての手順に従っていることを確認してください。  
  
##  <a name="bkmk_prereq"></a> 前提条件  
 すべてのレプリカで SQL Server ログインが必要です。 可用性グループ、リスナー、およびデータベースを構成するには **sysadmin** である必要がありますが、ユーザーの場合は Analysis Services クライアントからデータベースにアクセスするためには **db_datareader** アクセス許可のみ必要です。  
  
 表形式データ ストリーム (TDS) プロトコル Version 7.4 以降をサポートするデータ プロバイダー (SQL Server Native Client 11.0、Data Provider for SQL Server in .NET Framework 4.02 など) を使用します。  
  
 **(読み取り専用ワークロードの場合)** 。 セカンダリ レプリカのロールは、読み取り専用接続に対して構成されている必要があり、可用性グループはルーティング リストを持つ必要があり、Analysis Services データ ソース内の接続は可用性グループのリスナーを指定する必要があります。 手順はこのトピックで説明します。  
  
##  <a name="bkmk_UseSecondary"></a> チェック リスト:読み取り専用操作でセカンダリ レプリカを使用する  
 Analysis Services ソリューションに書き戻しが含まれていない場合は、読み取り可能なセカンダリ レプリカを使用するようにデータ ソース接続を構成できます。 高速ネットワーク接続がある場合、セカンダリ レプリカのデータ待機時間は非常に短くなり、プライマリ レプリカとほとんど同一のデータを持つことになります。 Analysis Services 操作のためにセカンダリ レプリカを使用すると、プライマリ レプリカ上の読み取りと書き込みの競合が削減され、可用性グループのセカンダリ レプリカの利用率が向上します。  
  
 既定では、プライマリ レプリカへの読み取り/書き込みアクセスと読み取りを目的としたアクセスの両方が許可され、セカンダリ レプリカへの接続は許可されません。 セカンダリ レプリカへの読み取り専用クライアント接続をセットアップするには、さらに構成が必要です。 構成には、セカンダリ レプリカのプロパティ設定と、読み取り専用ルーティング リストを定義する T-SQL スクリプトの実行が必要です。 次のプロシージャを使用すると、両方の手順を確実に実行できます。  
  
> [!NOTE]  
>  次の手順は、既存の AlwaysOn 可用性グループとデータベースがあることを前提としています。 新しいグループを構成する場合は、新しい可用性グループ ウィザードを使用してグループを作成し、データベースを結合します。 このウィザードでは、前提条件のチェック、それぞれの手順のガイド、および初期同期を実行します。 詳細については、「[新しい可用性グループ ウィザードの使用 &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)」を参照してください。  
  
#### <a name="step-1-configure-access-on-an-availability-replica"></a>手順 1:可用性レプリカに対してアクセスを構成する  
  
1.  オブジェクト エクスプローラーで、プライマリ レプリカをホストするサーバー インスタンスに接続し、サーバー ツリーを展開します。  
  
    > [!NOTE]  
    >  これらの手順は「[可用性レプリカでの読み取り専用アクセスの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)」に記載されており、このタスクを実行するための追加情報と別の手順を示しています。  
  
2.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
3.  変更するレプリカが含まれる可用性グループをクリックします。 **[可用性レプリカ]** を展開します。  
  
4.  セカンダリ レプリカを右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[可用性レプリカ プロパティ]** ダイアログ ボックスで、セカンダリ ロールの接続アクセスを次のように変更します。  
  
    -   **[読み取り可能なセカンダリ]** ボックスの一覧の **[読み取り目的のみ]** をクリックします。  
  
    -   **[プライマリ ロールでの接続]** ボックスの一覧の **[すべての接続を許可]** をクリックします。 これは既定値です。  
  
    -   必要に応じて、 **[可用性モード]** ボックスの一覧の **[同期コミット]** をクリックします。 この手順は必須ではありませんが、これを設定するとプライマリ レプリカとセカンダリ レプリカの間にデータ パリティがあることが確認できます。  
  
         このプロパティは、計画的なフェールオーバーに必須です。 テスト目的で計画的な手動フェールオーバーを実行する場合、プライマリ レプリカとセカンダリ レプリカの両方に対して **[可用性モード]** を **[同期コミット]** に設定します。  
  
#### <a name="step-2-configure-read-only-routing"></a>手順 2:読み取り専用ルーティングを構成する  
  
1.  プライマリ レプリカに接続します。  
  
    > [!NOTE]  
    >  これらの手順は「[可用性グループの読み取り専用ルーティングの構成 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)」に記載されており、このタスクを実行するための追加情報と別の手順を示しています。  
  
2.  クエリ ウィンドウを開き、次のスクリプトを貼り付けます。 このスクリプトでは、次の 3 つのことを行います。セカンダリ レプリカへの読み取り可能な接続を有効にし (既定ではオフ)、読み取り専用ルーティング URL を設定し、接続要求をどのように送るかを優先度付けするルーティング リストを作成します。  読み取り可能な接続を許可する最初のステートメントは、 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]でプロパティを設定済みの場合は冗長ですが、完全を期すために含まれています。  
  
    ```  
    ALTER AVAILABILITY GROUP [AG1]  
     MODIFY REPLICA ON  
    N'COMPUTER01' WITH   
    (SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
  
    ALTER AVAILABILITY GROUP [AG1]  
     MODIFY REPLICA ON  
    N'COMPUTER01' WITH   
    (SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433'));  
  
    ALTER AVAILABILITY GROUP [AG1]  
     MODIFY REPLICA ON  
    N'COMPUTER02' WITH   
    (SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
  
    ALTER AVAILABILITY GROUP [AG1]  
     MODIFY REPLICA ON  
    N'COMPUTER02' WITH   
    (SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER02.contoso.com:1433'));  
  
    ALTER AVAILABILITY GROUP [AG1]   
    MODIFY REPLICA ON  
    N'COMPUTER01' WITH   
    (PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER02','COMPUTER01')));  
  
    ALTER AVAILABILITY GROUP [AG1]   
    MODIFY REPLICA ON  
    N'COMPUTER02' WITH   
    (PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER01','COMPUTER02')));  
    GO  
    ```  
  
3.  個別の配置に対応する値でプレースホルダーを置換して、スクリプトを修正します。  
  
    -   'Computer01' を、プライマリ レプリカをホストしているサーバー インスタンスの名前で置換します。  
  
    -   'Computer02' を、セカンダリ レプリカをホストしているサーバー インスタンスの名前で置換します。  
  
    -   ドメインの名前で 'contoso.com' を置換するか、すべてのコンピューターが同じドメインに含まれている場合はスクリプトからこのプレースホルダーを削除します。 リスナーが既定のポートを使用している場合、ポート番号を保持します。 リスナーが実際に使用したポートは、 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]のプロパティ ページの一覧に示されます。  
  
4.  スクリプトを実行します。  
  
     次に、構成したグループから、データベースを使用する Analysis Services モデルにデータ ソースを作成します。  
  
##  <a name="bkmk_ssasAODB"></a> AlwaysOn 可用性データベースを使用する Analysis Services データ ソースを作成する  
 ここでは、可用性グループのデータベースに接続する Analysis Services データ ソースを作成する方法について説明します。 これらの指示を使用して、前のセクションの手順に基づいて構成したプライマリ レプリカ (既定) または読み取り可能なセカンダリ レプリカへの接続を構成できます。 AlwaysOn 構成設定、およびクライアントで設定された接続プロパティによって、プライマリ レプリカとセカンダリ レプリカのどちらを使用するかが決まります。  
  
1.  [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]の Analysis Services の多次元およびデータ マイニング モデル プロジェクトで、 **[データ ソース]** を右クリックして **[新しいデータ ソース]** をクリックします。 新しいデータ ソースを作成するには、 **[新規作成]** をクリックします。  
  
     または、テーブル モデル プロジェクトの場合、[モデル] メニューをクリックし、 **[データ ソースからのインポート]** をクリックします。  
  
2.  接続マネージャーで、プロバイダーには、表形式のデータ ストリーム (TDS) プロトコルをサポートするプロバイダーを選択します。 SQL Server Native Client 11.0 は、このプロトコルをサポートしています。  
  
3.  接続マネージャーで、[サーバー名] に *可用性グループ リスナー*の名前を入力し、グループで使用可能なデータベースを選択します。  
  
     可用性グループ リスナーは、読み取り/書き込み要求の場合はクライアント接続をプライマリ レプリカにリダイレクトし、接続文字列内で読み取りを目的と指定している場合はセカンダリ レプリカにリダイレクトします。 フェールオーバー中にレプリカ ロールが変化する (プライマリがセカンダリになり、セカンダリがプライマリになる) ため、リスナーを常に指定してそれに従ってクライアント接続がリダイレクトされるようにする必要があります。  
  
     可用性グループ リスナーの名前を判断するには、データベース管理者に問い合わせるか、可用性グループ内のインスタンスに接続して AlwaysOn 可用性設定を表示します。   
  
4.  また、接続マネージャーで、左側のナビゲーション ウィンドウで **[すべて]** をクリックしてデータ プロバイダーのプロパティ グリッドを表示します。  
  
     セカンダリ レプリカへの読み取り専用クライアント接続を構成する場合は、 **[Application Intent]** を **[READONLY]** に設定します。 または、既定の **[READWRITE]** を保持して接続をプライマリ レプリカにリダイレクトします。  
  
5.  [権限借用情報] では **[特定の Windows ユーザー名とパスワードを使用する]** をクリックし、データベースに対して少なくとも **db_datareader** 権限を持つ、Windows ドメイン ユーザー アカウントを入力します。  
  
     **[現在のユーザーの資格情報を使用する]** または **[継承する]** を選択しないでください。 **[サービス アカウントを使用する]** を選択できますが、そのアカウントがデータベースに対する読み取り権限を持つ場合のみです。  
  
     データ ソースを完了してデータ ソース ウィザードを閉じます。  
  
6.  接続文字列に **MultiSubnetFailover=Yes** を追加して、アクティブなサーバーを迅速に検出して接続できるようにします。 この接続プロパティの詳細については、「 [SQL Server Native Client の HADR サポート](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)」を参照してください。  
  
     このプロパティは、プロパティ グリッドには表示されません。 プロパティを追加するには、データ ソースを右クリックして **[コードの表示]** をクリックします。 接続文字列に `MultiSubnetFailover=Yes` を追加します。  
  
 これで、データ ソースが定義されました。 これで、モデルを構築し、データ ソース ビューを開始するか、テーブル モデルの場合はリレーションシップを作成できるようになります。 データを可用性データベースから取得する必要があるときに (たとえば、ソリューションの処理や導入の準備ができたとき)、構成をテストしてセカンダリ レプリカからデータにアクセスできることを確認できます。  
  
##  <a name="bkmk_test"></a> 構成をテストする  
 Analysis Services でセカンダリ レプリカを構成してデータ ソース接続を作成したら、処理とクエリのコマンドがセカンダリ レプリカにリダイレクトされていることを確認できます。 また、計画された手動フェールオーバーを実行して、このシナリオの復元計画を確認できます。  
  
#### <a name="step-1-confirm-the-data-source-connection-is-redirected-to-the-secondary-replica"></a>手順 1:データ ソース接続がセカンダリ レプリカにリダイレクトされることを確認する  
  
1.  SQL Server Profiler を開始して、セカンダリ レプリカをホストしている SQL Server インスタンスに接続します。  
  
     トレースを実行すると、 **SQL:BatchStarting** イベントおよび **SQL:BatchCompleting** イベントによって、データベース エンジン インスタンス上で実行している Analysis Services から発行されたクエリが表示されます。 これらのイベントは既定で選択されるため、トレースを開始すればよいだけです。  
  
2.  [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]で、テストするデータ ソース接続を含む Analysis Services プロジェクトまたはソリューションを開きます。 データ ソースが可用性グループのリスナー (グループのインスタンスではなく) を指定していることを確認します。  
  
     このステップは重要です。 サーバー インスタンス名を指定している場合、セカンダリ レプリカへのルーティングは発生しません。  
  
3.  SQL Server Profiler と [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)] を並べて表示できるように、アプリケーション ウィンドウを整列します。  
  
4.  ソリューションを配置し、完了したらトレースを停止します。  
  
     トレース ウィンドウには、アプリケーション **Microsoft SQL Server Analysis Services**からのイベントが表示されます。 セカンダリ レプリカをホストしているサーバー インスタンスのデータベースからデータを取得する **SELECT** ステートメントが表示されます (リスナー経由でセカンダリ レプリカに接続された場合)。  
  
#### <a name="step-2-perform-a-planned-failover-to-test-the-configuration"></a>手順 2:計画されたフェールオーバーを実行して構成をテストする  
  
1.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] ではプライマリ レプリカとセカンダリ レプリカをチェックして、その両方で同期コミット モードが構成されていて、現在同期していることを確認します。  
  
     次の手順は、セカンダリ レプリカに同期コミット モードが構成されていることを前提としています。  
  
     同期を検証するには、プライマリ レプリカおよびセカンダリ レプリカをホストする各インスタンスへの接続を開き、データベース フォルダーを展開し、各レプリカ内でデータベースの名前に **(同期済み)** および **(同期中)** と追加されていることを確認します。  
  
    > [!NOTE]  
    >  これらの手順は「[可用性グループの計画的な手動フェールオーバーの実行 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)」に記載されており、このタスクを実行するための追加情報と別の手順を示しています。  
  
2.  SQL Server Profiler で、各レプリカに対してトレースを開始して、それらのトレースを並べて表示します。 次の手順では、トレースを比較し、Analysis Services からの処理またはクエリのために使用した SQL クエリが 1 つのレプリカから別のレプリカに切り替わっていることを確認します。  
  
3.  Analysis Services 内から処理またはクエリ コマンドを実行します。 データ ソースを読み取り専用接続用に構成したため、セカンダリ レプリカでのコマンド実行が表示されます。  
  
4.  [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]で、セカンダリ レプリカに接続します。  
  
5.  **[AlwaysOn 高可用性]** ノードと **[可用性グループ]** ノードを展開します。  
  
6.  フェールオーバーする [可用性グループ] ノードを右クリックし、 **[フェールオーバー]** を選択します。 可用性グループのフェールオーバー ウィザードが起動します。 このウィザードを使用して、どのレプリカを新しいプライマリ レプリカにするか選択します。  
  
7.  フェールオーバーが正常に実行されたことを確認します。  
  
    -   [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]で、可用性グループを展開して (プライマリ) 指定子と (セカンダリ) 指定子を表示します。 以前プライマリ レプリカだったインスタンスが、セカンダリ レプリカになっています。  
  
    -   ダッシュボードを表示して、正常性の問題が検出されていないかどうか判断します。 可用性グループを右クリックして **[ダッシュボードの表示]** をクリックします。  
  
8.  バックエンドでフェールオーバーが完了するまで、1、2 分待ちます。  
  
9. Analysis Services ソリューションで処理またはクエリ コマンドを繰り返し、SQL Server Profiler にトレースを並べて確認します。 その他のインスタンス (新しくセカンダリ レプリカになったインスタンス) での処理の証拠が表示されます。  
  
##  <a name="bkmk_whathappens"></a> フェールオーバー後に何が起きるか  
 フェールオーバー中に、セカンダリ レプリカはプライマリ ロールに移行し、元のプライマリ レプリカはセカンダリ レプリカに移行します。 すべてのクライアント接続が終了して、可用性グループ リスナーの所有権はプライマリ レプリカ ロールと共に新しい SQL Server インスタンスに移動し、リスナー エンドポイントは新しいインスタンスの仮想 IP アドレスと TCP ポートにバインドされます。 詳細については、「[可用性レプリカに対するクライアント接続アクセスについて &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)」を参照してください。  
  
 処理中にフェールオーバーした場合、Analysis Services のログ ファイルまたは出力ウィンドウで、次のエラーが発生します。"OLE DB エラー:OLE DB または ODBC エラー:通信リンクが失敗しました; 08S01; TPC プロバイダー:既存の接続はリモート ホストに強制的に切断されました。 ; 08S01。"  
  
 数分待ってから再試行すると、このエラーは解決されます。 可用性グループが読み取り可能なセカンダリ レプリカに対して正しく構成されている場合、処理を再試行すると、新しいセカンダリ レプリカで再開されます。  
  
 エラーが解決しない場合、多くは構成の問題が原因です。 T-SQL スクリプトを再実行すると、セカンダリ レプリカのルーティング リスト、読み取り専用ルーティング URL、および読み取り専用の問題を解決できます。 また、プライマリ レプリカがすべての接続を許可することを確認する必要があります。  
  
##  <a name="bkmk_writeback"></a> AlwaysOn 可用性データベースを使用しているときに書き戻す  
 書き戻しは、Excel で What If 分析をサポートする Analysis Services 機能です。 また、一般にはカスタム アプリケーションの予算タスクおよび予測タスクに使用されます。  
  
 書き戻しのサポートには、READWRITE クライアント接続が必要です。 Excel で、読み取り専用接続で書き戻しを試みた場合は、次のエラーが表示されます。"外部データ ソースのデータを取得できませんでした。" "外部データ ソースのデータを取得できませんでした。"  
  
 読み取り可能なセカンダリ レプリカに常時アクセスするように接続を構成している場合、プライマリ レプリカへの READWRITE 接続を使用する新しい接続を構成する必要があります。  
  
 そのために、Analysis Services モデルに追加のデータ ソースを作成して、読み取りと書き込みの接続をサポートします。 追加のデータ ソースを作成するとき、読み取り専用接続で指定したものと同じリスナー名とデータベースを使用しますが、 **Application Intent**を修正しないで、READWRITE 接続をサポートする既定値を保持します。 読み取りと書き込みのデータ ソースに基づいたデータ ソース ビューに新しいファクトまたはディメンション テーブルを追加し、新しいテーブルへの書き戻しを有効にできます。  
  
## <a name="see-also"></a>参照  
 [可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [アクティブなセカンダリ:読み取り可能なセカンダリ レプリカ &#40;Always On 可用性グループ&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [AlwaysOn 可用性グループでの運用上の問題のポリシー ベースの管理 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)   
 [データ ソースの作成 &#40;SSAS 多次元&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional)   
 [ディメンションの書き戻しの有効化](https://docs.microsoft.com/analysis-services/multidimensional-models/bi-wizard-enable-dimension-writeback)  
  
  
