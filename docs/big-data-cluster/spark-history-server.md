---
title: Spark アプリケーションのデバッグと診断
titleSuffix: SQL Server big data clusters
description: Spark History Server を使用して、[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] 上で実行されている Spark アプリケーションをデバッグおよび診断します。
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: dd35de4111c5e18d8c8237e2935df5de458f19b1
ms.sourcegitcommit: b4ad3182aa99f9cbfd15f4c3f910317d6128a2e5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73706118"
---
# <a name="debug-and-diagnose-spark-applications-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-in-spark-history-server"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 上の Spark History Server の Spark アプリケーションのデバッグと診断

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

この記事では、拡張 Spark History Server を使用して、SQL Server ビッグ データ クラスターで Spark アプリケーションをデバッグおよび診断する方法に関するガイダンスを提供します。 これらのデバッグ機能と診断機能は、Microsoft が提供する Spark History Server に組み込まれています。 拡張機能には、データ タブ、グラフ タブ、診断タブがあります。データ タブで、ユーザーは Spark ジョブの入力データと出力データを確認できます。 グラフ タブで、ユーザーはデータフローを確認し、ジョブ グラフを再生できます。 診断タブで、ユーザーはデータ スキュー、時間のずれ、および実行プログラムの使用状況の分析を参照できます。

## <a name="get-access-to-spark-history-server"></a>Spark History Server へのアクセスを取得する

オープン ソースの Spark History Server ユーザー エクスペリエンスは、ジョブ固有のデータや、ビッグ データ クラスターのジョブ グラフとデータ フローの対話型の視覚化などの情報によって強化されています。 

### <a name="open-the-spark-history-server-web-ui-by-url"></a>URL を指定して Spark History Server Web UI を開く
次の URL を参照して Spark History Server を開き、`<Ipaddress>` と `<Port>` をビッグ データ クラスター固有の情報に置き換えます。 基本認証 (ユーザー名/パスワード) のビッグ クラスター セットアップでは、ゲートウェイ (Knox) エンドポイントにログインするように求められたとき、ユーザー **root** を指定する必要があります。 詳細については、次の情報を参照してください。[SQL Server ビッグ データ クラスターを展開する](quickstart-big-data-cluster-deploy.md)

```
https://<Ipaddress>:<Port>/gateway/default/sparkhistory
```

Spark History Server Web UI は次のような外観です。

![Spark History Server](./media/apache-azure-spark-history-server/spark-history-server.png)


## <a name="data-tab-in-spark-history-server"></a>Spark History Server の [Data]\(データ\) タブ
ジョブ ID を選択し、ツール メニューの **[Data]\(データ\)** をクリックしてデータ ビューを取得します。

+ 各タブを選択して **[Inputs]\(入力\)** 、 **[Outputs]\(出力\)** 、 **[Table Operations]\(テーブルの操作\)** を確認します。

    ![Spark History Server の [Data]\(データ\) タブ](./media/apache-azure-spark-history-server/sparkui-data-tabs.png)

+ すべての行をコピーするには、ボタン **[Copy]\(コピー\)** をクリックします。

    ![すべての行をコピーする](./media/apache-azure-spark-history-server/sparkui-data-copy.png)

+ ボタン **[csv]** をクリックして、すべてのデータを CSV ファイルとして保存します。

    ![データを CSV ファイルとして保存する](./media/apache-azure-spark-history-server/sparkui-data-save.png)

+ フィールド **[Search]\(検索\)** にキーワードを入力して検索すると、検索結果がすぐに表示されます。

    ![キーワードを使用した検索](./media/apache-azure-spark-history-server/sparkui-data-search.png)

+ 列ヘッダーをクリックするとテーブルが並べ替えられます。プラス記号をクリックすると、詳細が表示されます。マイナス記号をクリックすると、行が折りたたまれます。

    ![データ テーブルの機能](./media/apache-azure-spark-history-server/sparkui-data-table.png)

+ 右側にある **[Partial Download]\(部分的なダウンロード\)** ボタンをクリックして 1 つのファイルをダウンロードすると、選択したファイルがローカルの場所にダウンロードされます。 ファイルが存在しない場合は、新しいタブが開き、エラー メッセージが表示されます。

    ![データ行をダウンロードする](./media/apache-azure-spark-history-server/sparkui-data-download-row.png)

+ 完全なパスまたは相対パスをコピーするには、ダウンロード メニューから展開して **[Copy Full Path]\(完全なパスのコピー\)** 、 **[Copy Relative Path]\(相対パスのコピー\)** を選択します。 Azure データ レイク ストレージ ファイルの場合は、 **[Open in Azure Storage Explorer]\(Azure Storage Explorer で開く\)** を選択すると Azure Storage Explorer が起動します。 また、サインインするときに、正確なフォルダーを見つけます。

    ![完全なパスまたは相対パスをコピーする](./media/apache-azure-spark-history-server/sparkui-data-copy-path.png)

+ 1 ページに表示される行数が多すぎる場合、テーブルの下の数値をクリックするとページに移動します。 

    ![[Data]\(データ\) ページ](./media/apache-azure-spark-history-server/sparkui-data-page.png)

+ [Data]\(データ\) の横にある疑問符をポイントすると、ヒントが表示されます。また、疑問符をクリックすると、詳細情報が表示されます。

    ![データの詳細情報](./media/apache-azure-spark-history-server/sparkui-data-more-info.png)

+ 問題についてフィードバックを送信するには、 **[Provide us feedback]\(フィードバックの送信\)** をクリックします。

    ![グラフのフィードバック](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

## <a name="graph-tab-in-spark-history-server"></a>Spark History Server の [Graph]\(グラフ\) タブ

ジョブ ID を選択し、ツール メニューの **[Graph]\(グラフ\)** をクリックして、ジョブ グラフ ビューを取得します。

+ 生成されたジョブ グラフによるジョブの概要を確認します。 

+ 既定では、すべてのジョブが表示され、 **[Job ID]\(ジョブ ID\)** を指定してフィルター処理できます。

    ![グラフのジョブ ID](./media/apache-azure-spark-history-server/sparkui-graph-jobid.png)

+ **[Progress]\(進行状況\)** は既定値のままにします。 ユーザーがデータ フローを確認するには、 **[Display]\(表示\)** のドロップダウン リストで **[Read]\(読み取り\)** または **[Written]\(書き込み\)** を選択します。

    ![グラフの表示](./media/apache-azure-spark-history-server/sparkui-graph-display.png)

    グラフ ノードは、ヒートマップを示す色で表示されます。

    ![グラフのヒートマップ](./media/apache-azure-spark-history-server/sparkui-graph-heatmap.png)

+ **[Playback]\(再生\)** ボタンをクリックしてジョブを再生します。また、[Stop]\(停止\) ボタンをクリックしていつでも停止できます。 タスクは、再生時に別の状態を表示する色で表示されます。

    + 成功した場合は緑:ジョブは正常に完了しました。
    + 再試行の場合はオレンジ:失敗しましたが、ジョブの最終結果には影響しないタスクのインスタンス。 このようなタスクには、後で成功する可能性がある重複するインスタンスまたは再試行インスタンスがあります。
    + 実行中の場合は青:タスクは実行中です。
    + 待機中またはスキップ済みの場合は白:タスクは実行を待機しているか、ステージがスキップされました。
    + 失敗した場合は赤:タスクは失敗しました。

    ![グラフの色のサンプル、実行中](./media/apache-azure-spark-history-server/sparkui-graph-color-running.png)
 
    スキップされたステージは白で表示されます。
    ![グラフの色のサンプル、スキップ](./media/apache-azure-spark-history-server/sparkui-graph-color-skip.png)

    ![グラフの色のサンプル、失敗](./media/apache-azure-spark-history-server/sparkui-graph-color-failed.png)
 
    > [!NOTE]
    > 各ジョブを再生できます。 不完全なジョブの場合、再生はサポートされていません。


+ マウスをスクロールして、ジョブ グラフを拡大/縮小します。また、 **[Zoom to fit]\(ウィンドウのサイズに合わせる\)** をクリックして、画面のサイズに合わせることができます。
 
    ![グラフのウィンドウのサイズに合わせる](./media/apache-azure-spark-history-server/sparkui-graph-zoom2fit.png)

+ 失敗したタスクがある場合にツールヒントを表示するには、グラフ ノードをポイントします。また、ステージをクリックすると、ステージ ページが開きます。

    ![グラフのツールヒント](./media/apache-azure-spark-history-server/sparkui-graph-tooltip.png)

+ 次の条件を満たすタスクがある場合、ジョブ グラフ タブのステージにはツールヒントと小さいアイコンが表示されます。
    + データ スキュー: データの読み取りサイズ > このステージ内のすべてのタスクの平均データ読み取りサイズ * 2 とデータ読み取りサイズ > 10 MB
    + 時間のずれ: 実行時間 > このステージ内のすべてのタスクの平均実行時間 * 2 と実行時間 > 2 分

    ![グラフのスキュー アイコン](./media/apache-azure-spark-history-server/sparkui-graph-skew-icon.png)

+ ジョブ グラフ ノードには、各ステージの次の情報が表示されます。
    + ID。
    + 名前または説明。
    + 合計タスク数。
    + データ読み取り: 入力サイズとシャッフル読み取りサイズの合計。
    + データ書き込み: 出力サイズとシャッフル書き込みサイズの合計。
    + 実行時間: 最初の試行の開始時刻と最後の試行の完了時刻の間の時間。
    + 行数: 入力レコード、出力レコード、シャッフル読み取りレコード、シャッフル書き込みレコードの合計。
    + 進行状況。

    > [!NOTE]
    > 既定で、ジョブ グラフ ノードには各ステージの最後の試行の情報が表示されます (ステージの実行時間を除く)。ただし、再生中のグラフ ノードには、各試行の情報が表示されます。

    > [!NOTE]
    > 読み取りと書き込みのデータ サイズの場合は、1 MB = 1000 KB = 1000 * 1000 バイトを使用します。

+ 問題についてフィードバックを送信するには、 **[Provide us feedback]\(フィードバックの送信\)** をクリックします。

    ![グラフのフィードバック](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)


## <a name="diagnosis-tab-in-spark-history-server"></a>Spark History Server の [Diagnosis]\(診断\) タブ
ジョブ ID を選択し、ツール メニューの **[Diagnosis]\(診断\)** をクリックして、ジョブの [Diagnosis]\(診断\) ビューを取得します。 [Diagnosis]\(診断\) タブには、 **[Data Skew]\(データ スキュー\)** 、 **[Time Skew]\(時間のずれ\)** 、および **[Executor Usage Analysis]\(実行プログラムの使用状況の分析\)** が含まれます。
    
+ **[Data Skew]\(データ スキュー\)** 、 **[Time Skew]\(時間のずれ\)** 、および **[Executor Usage Analysis]\(実行プログラムの使用状況の分析\)** を確認するには、各タブを選択します。

    ![[Diagnosis]\(診断\) タブ](./media/apache-azure-spark-history-server/sparkui-diagnosis-tabs.png)

### <a name="data-skew"></a>[Data Skew]\(データ スキュー\)
**[Data Skew]\(データ スキュー\)** タブをクリックすると、指定したパラメーターに基づいて、対応する偏りのあるタスクが表示されます。 

+ **[Specify Parameters]\(パラメーターの指定\)** - 最初のセクションには、[Data Skew]\(データ スキュー\) の検出に使用されるパラメーターが表示されます。 組み込みの規則は次のとおりです。[Task Data Read]\(読み取られたタスク データ\) が、読み取られたタスクの平均読み取り回数の 3 倍を超えており、読み取られたタスク データが 10 MB を超えています。 偏りのあるタスクに対して独自の規則を定義する場合は、 **[Skewed Stage]\(偏りのあるステージ\)** パラメーターを選択します。それに応じて、 **[Skew Char]\(スキュー グラフ\)** セクションが更新されます。 

+ **[Skewed Stage]\(偏りのあるステージ\)** - 2 つ目のセクションには、上で指定した条件を満たす偏りのあるタスクがあるステージが表示されます。 ステージに偏りのあるタスクが複数ある場合、偏りのあるステージ テーブルには、最も偏りの大きなタスク (たとえば、データ スキューの最大データ) のみが表示されます。 

    ![データ スキュー section2](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section2.png)

+ **[Skew Chart]\(スキュー グラフ\)** - スキュー ステージ テーブルの行を選択すると、データの読み取りと実行時間に基づいて、スキュー グラフにさらに多くのタスク分布の詳細が表示されます。 偏りのあるタスクは赤でマークされ、通常のタスクは青でマークされます。 パフォーマンスを考慮し、グラフには最大 100 個のサンプル タスクのみが表示されます。 タスクの詳細は、右下のパネルに表示されます。

    ![データ スキュー section3](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section3.png)

### <a name="time-skew"></a>[Time Skew]\(時間のずれ\)
**[Time Skew]\(時間のずれ\)** タブには、タスクの実行時間に基づいて偏りのあるタスクが表示されます。 

+ **[Specify Parameters]\(パラメーターの指定\)** - 最初のセクションには、[Time Skew]\(時間のずれ\) の検出に使用されるパラメーターが表示されます。 時間のずれを検出する既定の条件は、タスクの実行時間が平均実行時間の 3 倍を超えており、タスクの実行時間が 30 秒を超えていることです。 必要に応じてパラメーターを変更できます。 **[Skewed Stage]\(偏りのあるステージ\)** と **[Skew Chart]\(スキュー グラフ\)** には、上の **[Data Skew]\(データ スキュー\)** タブと同様に対応するステージとタスクの情報が表示されます。

+ **[Time Skew]\(時間のずれ\)** をクリックすると、 **[Specify Parameters]\(パラメーターの指定\)** セクションに設定されたパラメーターに従って、フィルター処理された結果が **[Skewed Stage]\(偏りのあるステージ\)** セクションに表示されます。 **[Skewed Stage]\(偏りのあるステージ\)** セクションのいずれかの項目をクリックすると、section3 に対応するグラフの下書きが描写され、タスクの詳細が右下のパネルに表示されます。

    ![時間のずれ section2](./media/apache-azure-spark-history-server/sparkui-diagnosis-timeskew-section2.png)

### <a name="executor-usage-analysis"></a>実行プログラムの使用状況の分析
[Executor Usage Graph]\(実行プログラムの使用状況グラフ\) には、Spark ジョブの実際の実行プログラムの割り当てと実行状態が視覚化されます。  

+ **[Executor Usage Analysis]\(実行プログラムの使用状況の分析\)** をクリックすると、実行プログラムの使用状況に関する 4 種類の曲線の下書きが描写されます。 これには、 **[Allocated Executors]\(割り当て済みの実行プログラム\)** 、 **[Running Executors]\(実行中の実行プログラム\)** 、 **[idle Executors]\(アイドルの実行プログラム\)** 、 **[Max Executor Instances]\(最大実行プログラム インスタンス\)** が含まれます。 割り当て済みの実行プログラムについては、"Executor added" (実行プログラムの追加) イベントまたは "Executor removed" (実行プログラムの削除) イベントごとに割り当て済み実行プログラムが増減します。 詳細な比較については、[Jobs]\(ジョブ\) タブの [Event Timeline]\(イベントのタイムライン\) を確認します。

    ![[Executors]\(実行プログラム\) タブ](./media/apache-azure-spark-history-server/sparkui-diagnosis-executors.png)

+ 色アイコンをクリックして、すべての下書きの対応する内容を選択または選択解除します。

    ![グラフの選択](./media/apache-azure-spark-history-server/sparkui-diagnosis-select-chart.png)


## <a name="known-issues"></a>既知の問題
Spark History Server には、次の既知の問題があります。

+ 現時点では、Spark 2.3 クラスターに対してのみ機能します。

+ RDD を使用した入力/出力データは、[Data]\(データ\) タブに表示されません。

## <a name="next-steps"></a>次の手順

* [SQL Server ビッグ データ クラスターの概要](../big-data-cluster/deploy-get-started.md)
* Spark の設定を構成する
* [Spark の設定を構成する](/azure/hdinsight/spark/apache-spark-settings/)
