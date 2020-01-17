---
title: クエリ調整アシスタントを使用したデータベースのアップグレード
ms.custom: seo-dt-2019
ms.date: 02/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- query statistics [SQL Server] live query stats
- live query statistics
- debugging [SQL Server], live query stats
- statistics [SQL Server], live query statistics
- query profiling
- lightweight query profiling
- lightweight profiling
ms.assetid: 07f8f594-75b4-4591-8c29-d63811e7753e
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 958445b0f07dc9624e7d284f408210c386ecfa9e
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165678"
---
# <a name="upgrading-databases-by-using-the-query-tuning-assistant"></a>クエリ調整アシスタントを使用したデータベースのアップグレード
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

古いバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降に移行する場合、および[データベース互換性レベル](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)を使用可能な最新のものにアップグレードする場合、ワークロードのパフォーマンスが低下するリスクにさらされる可能性があります。 程度はかなり低くなりますが、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] と新しいバージョン間のアップグレード時にもその可能性はあります。

[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 以降、およびすべての新しいバージョンでは、クエリ オプティマイザーのすべての変更が最新のデータベース互換レベルにゲーティングされるため、実行プランの変更は、アップグレードの時点ではなく、ユーザーが `COMPATIBILITY_LEVEL` データベース オプションを使用可能な最新のものに変更したときに発生します。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] で導入されたクエリ オプティマイザーの変更の詳細については、[カーディナリティ推定機能](../../relational-databases/performance/cardinality-estimation-sql-server.md)に関するページを参照してください。 互換性レベルとそれがアップグレードにどのように影響する可能性があるかについて詳しくは、「[互換性レベルとデータベース エンジンのアップグレード](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades)」を参照してください。

データベース互換レベルによって提供されるこのゲーティング機能と、クエリ ストアを組み合わせることで、アップグレードで以下の推奨されるワークフローに従う場合に、アップグレード プロセスのクエリ パフォーマンスを高いレベルで制御できます。 互換性レベルをアップグレードする場合に推奨されるワークフローの詳細については、「[Change the Database Compatibility Mode and Use the Query Store](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)」 (データベース互換モードの変更とクエリ ストアの使用) を参照してください。 

![クエリ ストアを使用した推奨されるデータベース アップグレードのワークフロー](../../relational-databases/performance/media/query-store-usage-5.png "クエリ ストアを使用した推奨されるデータベース アップグレードのワークフロー") 

このアップグレードの制御は、[自動調整](../../relational-databases/automatic-tuning/automatic-tuning.md)が導入されており、上記の推奨されるワークフローの最後のステップを自動化できる [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] でさらに強化されました。

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v18 以降では、新しい **クエリ調整アシスタント (QTA)** 機能を利用して、推奨されるワークフローに従うことで、新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョンへのアップグレード時のパフォーマンスの安定性を維持できます。これについては、「[クエリ ストアの使用シナリオ](../../relational-databases/performance/query-store-usage-scenarios.md#CEUpgrade)」の「*新しい SQL Server にアップグレードするときにパフォーマンスの安定性を維持する*」セクションに記載されています。 ただし、推奨されるワークフローの最後の手順で示されているように、QTA は以前の既知の適切なプランにロールバックしません。 代わりに、QTA は [クエリ ストアの **[機能低下したクエリ]** ](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#Regressed) ビューで見つかった回帰をすべて追跡し、適用できるオプティマイザー モデル バリエーションの可能な順列を反復処理することで、新しいより良いプランを作成できます。

> [!IMPORTANT]
> QTA では、ユーザー ワークロードは生成されません。 アプリケーションで使用されていない環境で QTA を実行する場合は、別の方法でターゲットとなる [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] で代表的なテスト ワークロードを引き続き確実に実行できるようにします。 

## <a name="the-query-tuning-assistant-workflow"></a>クエリ調整アシスタントのワークフロー
QTA の開始点では、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からデータベースが ([CREATE DATABASE ...FOR ATTACH](../..//relational-databases/databases/attach-a-database.md) または [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) を使用して) 新しいバージョンの [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] に移行され、アップグレード前のデータベース互換レベルがすぐには変更されないことが前提となります。 QTA を使用して、次のステップを行います。
1.  ユーザーが設定したワークロード期間 (日単位) の推奨される設定に従って、クエリ ストアを構成します。 一般的なビジネス サイクルに一致するワークロード期間について考えてみます。
2.  クエリ ストアでワークロード データのベースラインを収集できるように (まだ使用できるものがない場合)、必要なワークロードの開始を要求します。
3.  ユーザーが選択したターゲットのデータベース互換レベルにアップグレードします。
4.  比較と機能低下の検出のために、ワークロード データの 2 番目の受け渡しが収集されるように要求します。
5.  [クエリ ストアの **[機能低下したクエリ]** ](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#Regressed) ビューに基づいて検出された機能低下を繰り返し処理し、適用可能なオプティマイザー モデル バリエーションの可能な順列で実行時統計を収集して実験し、その結果を測定します。 
6.  測定された改善について報告し、必要に応じて、[プラン ガイド](../../relational-databases/performance/plan-guides.md)を使用して変更を保持できるようにします。

データベースのアタッチの詳細については、[データベースのデタッチとアタッチ](../../relational-databases/databases/database-detach-and-attach-sql-server.md#AttachDb)に関するページを参照してください。

前述のクエリ ストアを使用する互換性レベルのアップグレードの際に推奨されるワークロードの最後のステップのみが、QTA では基本的にどのように変わるかについては、以下を参照してください。 現在の非効率な実行プランと最新の既知の適切な実行プランのどちらかを選ぶのではなく、QTA では、選択された機能低下したクエリに固有の調整オプションが示され、調整された実行プランで新しい改善された状態を作成できます。

![QTA を使用した推奨されるデータベース アップグレードのワークフロー](../../relational-databases/performance/media/qta-usage.png "QTA を使用した推奨されるデータベース アップグレードのワークフロー")

### <a name="qta-tuning-internal-search-space"></a>QTA での内部検索領域の調整
QTA では、クエリ ストアから実行できる `SELECT` クエリのみがターゲットとなります。 コンパイル済みのパラメーターがわかっている場合は、パラメーター化されたクエリが対象となります。 一時テーブルやテーブル変数などの実行時の構造に依存するクエリは、ここでは対象となりません。 

QTA では、[カーディナリティ推定機能 (CE)](../../relational-databases/performance/cardinality-estimation-sql-server.md) バージョンでの変更によるクエリ パフォーマンス低下の既知の使用可能なパターンがターゲットとなります。 たとえば、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] およびデータベース互換レベル 110 から、[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] およびデータベース互換レベル 140 にデータベースをアップグレードするときに、一部のクエリは、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] に存在する CE バージョン (CE 70) での動作専用に設計されているため、その機能が低下する場合があります。 これは、CE 140 から CE 70 に戻すことが唯一のオプションであるという意味ではありません。 新しいバージョンの特定の変更のみが機能低下の原因である場合、特定のクエリではより適切に動作していた以前の CE バージョンの関連する部分のみを使用するようにクエリにヒントを示すことができ、新しい CE バージョンの他のすべての強化機能を引き続き利用できます。 また、機能が低下していない、ワークロード内の他のクエリでは、新しい CE の機能強化による利点が得られます。

QTA によって検索される CE パターンは、次のとおりです。 
-  **独立性と相関関係**: 独立性を想定することで特定のクエリをより適切に推定することができる場合、クエリ ヒント `USE HINT ('ASSUME_MIN_SELECTIVITY_FOR_FILTER_ESTIMATES')` によって、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、相関関係を考慮するフィルターの `AND` 述語を推定するときに、最低限の選択度を使用して実行プランが生成されます。 詳細については、[USE HINT クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md#use_hint)に関する記述と、「[CE のバージョン](../../relational-databases/performance/cardinality-estimation-sql-server.md#versions-of-the-ce)」を参照してください。
-  **単純な含有と基本含有**: 異なる結合含有で特定のクエリをより適切に推定できる場合、クエリ ヒント `USE HINT ('ASSUME_JOIN_PREDICATE_DEPENDS_ON_FILTERS')` では、既定の基本含有の推定ではなく、単純な含有の推定を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって実行プランが生成されます。 詳細については、[USE HINT クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md#use_hint)に関する記述と、「[CE のバージョン](../../relational-databases/performance/cardinality-estimation-sql-server.md#versions-of-the-ce)」を参照してください。
-  100 行の**複数ステートメントのテーブル値関数 (MSTVF) の固定のカーディナリティ推定**と1 行: 100 行の TVF の既定の固定カーディナリティ推定で、([!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 以前のバージョンのクエリ オプティマイザー CE モデルでの既定値に対応する) 1 行の TVF の固定推定を使用する場合よりも効率的なプランが得られない場合、実行プランを生成するためにクエリ ヒント `QUERYTRACEON 9488` が使用されます。 MSTVF の詳細については、「[ユーザー定義関数の作成 (データベース エンジン)](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)」を参照してください。

> [!NOTE]
> 最後の手段として、狭いスコープのヒントで、対象となるクエリ パターンに対して十分良い結果が得られない場合は、実行プランを生成するためにクエリ ヒント `USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION')` を使用して、CE 70 を最大限に活用することも考慮されます。

> [!IMPORTANT]
> ヒントでは、今後の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の更新で対応される可能性がある特定の動作が強制されます。 他のオプションが存在しない場合にのみヒントを適用し、新しいアップグレードのたびにヒント コードに再度アクセスするよう計画することをお勧めします。 動作を強制することで、ワークロードでは、新しいバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で導入された拡張機能の利点が得られなくなる場合があります。

## <a name="starting-query-tuning-assistant-for-database-upgrades"></a>データベース アップグレードのためのクエリ調整アシスタントの起動
QTA はセッション ベースの機能であり、セッションが初めて作成される、ユーザー データベースの `msqta` スキーマにセッション状態を格納します。 複数の調整セッションを単一データベースに時間をかけて作成することはできますが、特定のデータベースに存在できるのは 1 つのアクティブ セッションのみです。

### <a name="creating-a-database-upgrade-session"></a>データベースのアップグレード セッションの作成
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] で、オブジェクト エクスプローラーを開き、[!INCLUDE[ssDE](../../includes/ssde-md.md)] に接続します。

2.  データベース互換レベルをアップグレードすることを目的とするデータベースでは、データベース名をクリックして、 **[タスク]** 、 **[データベースのアップグレード]** の順に選択し、 **[新しいデータベースのアップグレード セッション]** をクリックします。

3.  QTA ウィザード ウィンドウで、セッションを構成するには、以下の 2 つのステップが必要です。

    1.  **[セットアップ]** ウィンドウで、分析して調整するワークロード データの 1 つの完全なビジネス サイクルに相当するものをキャプチャするように、クエリ ストアを構成します。 
        -  予期されるワークロード期間を日単位で入力します (最小値は 1 日)。 これは、ベースライン全体の収集を一時的に許可するために、推奨されるクエリ ストア設定を提案する場合に使用されます。 適切なベースラインのキャプチャは、データベース互換レベルの変更後に検出される機能低下したクエリを確実に分析できるようにするために重要なことです。 
        -  QTA ワークフローが完了した後、ユーザー データベースで使用する必要がある、目的のターゲット データベース互換レベルを設定します。
        完了したら、 **[次へ]** をクリックします。
    
       ![新しいデータベース アップグレード セッションの [セットアップ] ウィンドウ](../../relational-databases/performance/media/qta-new-session-setup.png "|::ref3::|")  
  
    2.  **[設定]** ウィンドウの 2 つの列には、ターゲットとなるデータベースのクエリ ストアの **[現在]** の状態と、 **[推奨]** 設定が表示されます。 
        -  既定では [推奨] 設定が選択されますが、[現在] 列のラジオ ボタンをクリックすると、現在の設定が受け入れられます。また、現在のクエリ ストア構成を微調整することもできます。 
        -  提案された *[期限切れクエリのしきい値]* 設定は、予期されるワークロード期間の日数の 2 倍になります。 これは、クエリ ストアでベースライン ワークロードとデータベースのアップグレード後のワークロードに関する情報を保持する必要があるためです。
        完了したら、 **[次へ]** をクリックします。

       ![新しいデータベース アップグレードの [設定] ウィンドウ](../../relational-databases/performance/media/qta-new-session-settings.png "新しいデータベース アップグレードの [設定] ウィンドウ")

       > [!IMPORTANT]
       > 提案された *[最大サイズ]* は、短い時間のワークロードに適している可能性がある任意の値です。   
       > しかし、非常に大きなワークロード (つまり、多くのさまざまなプランが生成される可能性がある場合) のベースラインおよびデータベース アップグレード後のワークロードに関する情報を保持するには十分でない可能性があることに注意してださい。   
       > このようになることが予測される場合は、適切なより高い値を入力してください。

4.  **[調整]** ウィンドウでセッション構成が終了し、次のステップでセッションを開いて続行するよう指示されます。 完了したら、 **[完了]** をクリックします。

    ![新しいデータベース アップグレードの [調整] ウィンドウ](../../relational-databases/performance/media/qta-new-session-tuning.png "新しいデータベース アップグレードの [調整] ウィンドウ")

> [!NOTE]
> データベースで既に推奨されるデータベース互換アップグレード ワークフローが実行された運用サーバーから、テスト サーバーにデータベース バックアップを復元することで、可能な代替シナリオが開始されます。

### <a name="executing-the-database-upgrade-workflow"></a>データベースのアップグレード ワークフローの実行
1.  データベース互換レベルをアップグレードすることを目的とするデータベースでは、データベース名をクリックして、 **[タスク]** 、 **[データベースのアップグレード]** の順に選択し、 **[モニター セッション]** をクリックします。

2.  **セッション管理**ページには、スコープ内のデータベースの現在および過去のセッションがリストされます。 目的のセッションを選択し、 **[詳細]** をクリックします。

    > [!NOTE]
    > 現在のセッションが存在しない場合は、 **[更新]** ボタンをクリックします。   
    
    このリストには、次の情報が含まれています。
    -  **セッション ID**
    -  **セッション名**: データベースの名前とセッションの作成日時で構成された、システムによって生成される名前。
    -  **状態**: セッションの状態 (アクティブまたは終了)。
    -  **説明**:システムによって生成され、ユーザーが選択したターゲット データベース互換レベルと、ビジネス サイクル ワークロードの日数で構成されます。
    -  **開始した時刻**: セッションが作成された日時。

    ![QTA のセッション管理ページ](../../relational-databases/performance/media/qta-session-management.png "QTA のセッション管理ページ")

    > [!NOTE]
    > **[セッションの削除]** では、選択されたセッションの格納データがすべて削除されます。    
    > しかし、終了したセッションを削除しても、以前に展開されたプラン ガイドは削除**されません**。   
    > プラン ガイドが展開されたセッションを削除する場合、QTA を使用してロールバックできません。    
    > 代わりに、[sys.plan_guides](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md) システム テーブルを使用してプラン ガイドを検索し、[sp_control_plan_guide](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md) を使用して手動で削除します。    
  
3.  新しいセッションのエントリ ポイントは、**データの収集**ステップです。 

    > [!NOTE]
    > **[セッション]** ボタンを押すと、**セッション管理**ページに戻り、アクティブなセッションはそのままになります。

    この手順には、次の 3 つのサブステップがあります。

    1.  **[ベースライン データの収集]** では、クエリ ストアでベースラインを収集できるように、ユーザーに代表的なワークロード サイクルの実行が要求されます。 そのワークロードが完了したら、 **[Done with workload run]\(ワークロードの実行完了\)** をオンにし、 **[次へ]** をクリックします。

        > [!NOTE]
        > ワークロードの実行中に、QTA ウィンドウを閉じてもかまいません。 後でアクティブ状態のままになっているセッションに戻ると、中断したステップから再開されます。 

        ![QTA のステップ 2 サブステップ 1](../../relational-databases/performance/media/qta-step2-substep1.png "QTA のステップ 2 サブステップ 1")

    2.  **[データベースのアップグレード]** では、データベース互換レベルを適切なターゲットにアップグレードするための許可が求められます。 次のサブステップに進むには、 **[はい]** をクリックします。

        ![QTA のステップ 2 サブステップ 2 - データベース互換性レベルのアップグレード](../../relational-databases/performance/media/qta-step2-substep2-prompt.png "QTA のステップ 2 サブステップ 2 - データベース互換性レベルのアップグレード")

        次のページでは、データベース互換レベルが正常にアップグレードされたことを確認します。

        ![QTA のステップ 2 サブステップ 2](../../relational-databases/performance/media/qta-step2-substep2.png "|::ref9::|")

    3.  **[観測されたデータの収集]** では、クエリストアで、最適化の機会を見つけるために使用される比較ベースラインを収集できるように、ユーザーに代表的なワークロード サイクルの再実行が要求されます。 ワークロードが実行されたら、 **[更新]** ボタンを使用して、機能低下したクエリ (検出された場合) のリストを更新し続けます。 **[表示するクエリ]** の値を変更し、表示されるクエリの数を制限します。 リストの順序は、 **[メトリック]** (期間または CpuTime) と **[集計]** (平均が既定値) に影響を受けます。 **表示するクエリ**の数も選択します。 そのワークロードが完了したら、 **[Done with workload run]\(ワークロードの実行完了\)** をオンにし、 **[次へ]** をクリックします。

        ![QTA のステップ 2 サブステップ 3](../../relational-databases/performance/media/qta-step2-substep3.png "QTA のステップ 2 サブステップ 3")

        このリストには、次の情報が含まれています。
        -  **クエリ ID** 
        -  **クエリ テキスト**: **[...]** ボタンをクリックすることで展開できる [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント。
        -  **実行**: ワークロード全体の収集に対するクエリの実行回数が表示されます。
        -  **ベースライン メトリック**: データベース互換性アップグレードの前のベースライン データ収集に対して選択されたミリ秒単位のメトリック (期間または CpuTime)。
        -  **観測されたメトリック**: データベース互換性アップグレードの後のデータデータ収集に対して選択されたミリ秒単位のメトリック (期間または CpuTime)。
        -  **変更 %** : データベース互換性アップグレードの前と後の状態の間の選択されたメトリックの変更率。 負の数は、クエリの観測された機能低下の量を表します。
        -  **調整可能**: クエリが実験の対象となるかどうかに応じて、*True* または *False* となります。

4.  **[分析の表示]** では、実験対象のクエリを選択し、最適化の機会を見つけることができます。 **[表示するクエリ]** の値は、実験対象となるクエリのスコープになります。 必要なクエリが確認されたら、 **[次へ]** をクリックして実験を開始します。  

    > [!NOTE]
    > [調整可能] が False のクエリを実験対象として選択することはできません。   
 
    > [!IMPORTANT]
    > プロンプトが表示され、QTA が実験フェーズに移ると、[分析の表示] ページには戻れないことが示されます。   
    > 実験フェーズに移る前に対象となるすべてのクエリを選択しない場合は、後で新しいセッションを作成し、ワークフローを繰り返す必要があります。 その場合、データベース互換レベルを元の値にリセットする必要があります。

    ![QTA のステップ 3](../../relational-databases/performance/media/qta-step3.png "QTA のステップ 3")

5.  **[結果の表示]** では、プラン ガイドとして提案された最適化を展開するクエリを選択できます。 

    このリストには、次の情報が含まれています。
    -  **クエリ ID** 
    -  **クエリ テキスト**: **[...]** ボタンをクリックすることで展開できる [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント。
    -  **状態**: クエリの現在の実験の状態が表示されます。
    -  **ベースライン メトリック**: データベース互換性アップグレードの後の機能低下したクエリを表す、**ステップ 2 のサブステップ 3** で実行されるクエリに対して選択されたミリ秒単位のメトリック (期間または CpuTime)。
    -  **観測されたメトリック**: 十分良好な提案された最適化について、実験後のクエリに対して選択されたミリ秒単位のメトリック (期間または CpuTime)。
    -  **変更 %** : 実験の前と後の状態の間の選択されたメトリックの変更率。提案された最適化による、クエリの観測された改善の量を表します。
    -  **クエリ オプション**: クエリ実行メトリックを改善する提案されたヒントへのリンク。
    -  **展開可能**: 提案されたクエリの最適化をプラン ガイドとして展開できるかどうかに応じて、*True* または *False* となります。

    ![QTA のステップ 4](../../relational-databases/performance/media/qta-step4.png "QTA のステップ 4")

6.  **[検証]** には、このセッションに対して前に選択されたクエリの展開状態が表示されます。 このページのリストは前のページとは異なり、 **[展開可能]** 列が **[ロールバック可能]** に変わっています。 この列は、展開されたクエリの最適化をロールバックし、そのプラン ガイドを削除できるかどうかに応じて、*True* または *False* にすることができます。

    ![QTA のステップ 5](../../relational-databases/performance/media/qta-step5.png "QTA のステップ 5")

    後日、提案された最適化でロールバックが必要な場合は、関連するクエリを選択してから **[ロールバック]** をクリックします。 そのクエリ プラン ガイドは削除され、リストはロールバックされたクエリを削除するために更新されます。 以下の図でクエリ 8 が削除されていることに注目してください。

    ![QTA のステップ 5 - ロールバック](../../relational-databases/performance/media/qta-step5-rollback.png "QTA のステップ 5 - ロールバック") 

    > [!NOTE]
    > 終了したセッションを削除しても、以前に展開されたプラン ガイドは削除**されません**。   
    > プラン ガイドが展開されたセッションを削除する場合、QTA を使用してロールバックできません。    
    > 代わりに、[sys.plan_guides](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md) システム テーブルを使用してプラン ガイドを検索し、[sp_control_plan_guide](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md) を使用して手動で削除します。  
  
## <a name="permissions"></a>アクセス許可  
**db_owner** ロールのメンバーシップが必要です。
  
## <a name="see-also"></a>参照  
 [互換性レベルとデータベース エンジンのアップグレード](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#compatibility-levels-and-database-engine-upgrades)    
 [パフォーマンス監視およびチューニング ツール](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [クエリのストアを使用した、パフォーマンスの監視](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)     
 [データベース互換性モードの変更とクエリ ストアの使用](../../database-engine/install-windows/change-the-database-compatibility-mode-and-use-the-query-store.md)       
 [トレース フラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)    
 [USE HINT クエリ ヒント](../../t-sql/queries/hints-transact-sql-query.md#use_hint)     
 [カーディナリティ推定機能](../../relational-databases/performance/cardinality-estimation-sql-server.md)     
 [自動調整](../../relational-databases/automatic-tuning/automatic-tuning.md)      
