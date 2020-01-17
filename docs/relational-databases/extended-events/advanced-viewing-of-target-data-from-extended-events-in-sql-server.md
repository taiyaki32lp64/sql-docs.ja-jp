---
title: 拡張イベントからのターゲット データの詳細表示
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: b2e839d7-1872-46d9-b7b7-6dcb3984829f
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f5bf55c020e773e8d724a3c84bcee4dd78307a4f
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255762"
---
# <a name="advanced-viewing-of-target-data-from-extended-events-in-sql-server"></a>SQL Server での拡張イベントからのターゲット データの詳細表示

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


この記事では、SQL Server Management Studio (SSMS.exe) の高度な機能を使用して、拡張イベントからのターゲット データを詳細にわたって表示する方法を示します。 この記事では、以下の方法について説明します。


- さまざまな方法でターゲット データを開いて表示する。
- 拡張イベント用の特別なメニューやツール バーを使用して、ターゲット データをさまざまな形式にエクスポートする。
- 表示中またはエクスポート前にデータを操作する。



### <a name="prerequisites"></a>前提条件

この記事では、イベント セッションを作成して開始する方法を既に知っていることを前提としています。 イベント セッションを作成する方法については、次の記事の初めの部分で説明されています。

[クイック スタート:SQL Server の拡張イベント](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)


また、この記事では、SSMS の最新の月次リリースがインストールされていることを前提としています。 インストールに関するヘルプは、次を参照してください。

- [SQL Server Management Studio (SSMS) のダウンロード](../../ssms/download-sql-server-management-studio-ssms.md)



### <a name="differences-with-azure-sql-database"></a>Azure SQL Database との違い


Microsoft SQL Server と Azure SQL Database の 2 つの製品における拡張イベントの実装と機能は、かなり類似しています。 ただし、SSMS UI (ユーザー インターフェイス) に影響を与えるいくつかの違いがあります。


- SQL Database の場合、ローカル ディスク ドライブ上のファイルを package0.event_file ターゲットにすることはできません。 代わりに、Azure Storage コンテナーを使用する必要があります。 したがって、SQL Database に接続されている場合、SSMS UI はローカル パスとファイル名ではなく、ストレージ コンテナーを要求します。


- SSMS UI で **[ライブ データの監視]** チェック ボックスがグレー表示されて無効になっている場合は、その機能を SQL Database に対して使用できないことが理由です。


- いくつかの拡張イベントが SQL Server と共にインストールされます。 **[セッション]** ノードの下に、 **AlwaysOn_health** とその他の項目がいくつか表示されます。 これらは、SQL Database では存在しないため、SQL Database に接続されているときは表示されません。


この記事は、SQL Server の観点から書かれています。 この記事では、相違点の 1 つである event_file ターゲットを使用します。 その他の相違については、重要な相違または自明でない相違に限定して取り上げています。


Azure SQL Database に固有の拡張イベントに関するドキュメントについては、次を参照してください。

- [Azure SQL Database での拡張イベント](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)



## <a name="a-general-options"></a>A. [全般] オプション


一般に、拡張オプションは以下の方法でアクセスします。


- 通常のメニューの **[ファイル]**  >  **[開く]**  >  **[ファイル]** 。
- **[オブジェクト エクスプローラー]** で **[管理]**  >  **[拡張イベント]** を右クリックする。
- 特別なメニュー **[拡張イベント]** 、および拡張イベント用の特別なツール バー。
- ターゲット データが表示されたタブ付きペインを右クリックする。



## <a name="b-bring-target-data-into-ssms-for-display"></a>B. 表示するターゲット データを SSMS に取り込む


event_file ターゲット データを SSMS UI に取り込むには、さまざまな方法があります。 event_file ターゲットを指定するときに、そのファイル パスと名前を設定します。

- .XEL はファイル名の拡張子です。


- イベント セッションが開始されるたびに、システムは長精度整数を埋め込んで新しいファイル名にします。これによってファイル名が一意になり、前のセッション開始時とは異なる名前になります。
  - *例:* Checkpoint_Begins_ES_0_131103935140400000.xel


- .XEL の内容は、Notepad.exe で表示できるプレーン テキストではありません。
  - いくつかの .XEL ファイルを一緒に追加する場合は、メニュー **[ファイル]**  >  **[開く]**  >  **[拡張イベント ファイルの結合]** を使用します。



SSMS は、任意のターゲットからのデータを表示できます。 ただし、以下のように、ターゲットが異なれば表示も異なります。

- *event_file:* event_file ターゲットからのデータはわかりやすく表示され、さまざまな機能を使用できます。


- *ring_buffer:* リング バッファー ターゲットからのデータは未加工 XML として表示されます。


- 他のターゲットの場合の表示能力は、event_file と ring_buffer の中間です。
  - このようなターゲットには、event_counter、histogram、pair_matching なども含まれます。


- *etw_classic_sync_target:* SSMS はターゲット型 etw_classic_sync_target からのデータを表示できません。



### <a name="b1-open-xel-with-menu-file--open--file"></a>B.1 メニュー [ファイル] > [開く] > [ファイル] で .XEL を開く


標準メニュー **[ファイル]**  >  **[開く]**  >  **[ファイル]** を使用して、.XEL ファイルを個別に開くことができます。

SSMS UI のタブ バーに .XEL ファイルをドラッグ アンド ドロップすることもできます。



### <a name="b2-view-target-data"></a>B.2 ターゲット データの表示


**[ターゲット データの表示]** オプションを選択すると、これまでにキャプチャされたデータが表示されます。


**[オブジェクト エクスプローラー]** ペインで、ノードを展開し、右クリックして次のように選択します。

- **[管理]**  >  **[拡張イベント]**  >  **[セッション]**  >  *[対象のセッション]*  >  *[対象のターゲット ノード]*  >  **[ターゲット データの表示]** 。


SSMS のタブ付きペインにターゲット データが表示されます。 次のスクリーン ショットのようになります。


![[対象のターゲット] > [ターゲット データの表示]](../../relational-databases/extended-events/media/xevents-ssms-ui20-viewtargetdata.png)


> [!NOTE] 
> **[ターゲット データの表示]** を選択すると、指定したイベント セッションでの *複数の .XEL ファイルからの蓄積データ* が表示されます。 **開始**-**停止** のサイクルごとにファイルが作成され、より新しい時刻から生成された整数がその名前に埋め込まれますが、各ファイルは同じルート名を共有します。



#### <a name="b3-watch-live-data"></a>B.3 ライブ データの監視


イベント セッションが現在アクティブであれば、ターゲットが受け取っているイベント データをリアルタイムで監視することもできます。


- **[管理]**  >  **[拡張イベント]**  >  **[セッション]**  >  *[対象のセッション]*  >  **[ライブ データの監視]** 。


![[対象のセッション] > [ライブ データの監視]](../../relational-databases/extended-events/media/xevents-ssms-ui55-watchlivedata.png)


データの表示は、指定した間隔で更新されます。 **[ディスパッチの最大待機時間]** は、次の操作で確認できます。

- **[拡張イベント]**  >  **[セッション]**  >  *[対象のセッション]*  >  **[プロパティ]**  >  **[詳細設定]**  >  **[ディスパッチの最大待機時間]**



### <a name="b4-view-xel-with-sysfn_xe_file_target_read_file-function"></a>B.4 sys.fn_xe_file_target_read_file 関数を使用して .XEL を表示する


次のシステム関数は、.XEL ファイル内のレコードに対応する XML をバッチ処理で生成できます。

- [sys.fn\_xe\_file\_target\_read\_file](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)



## <a name="c-export-the-target-data"></a>C. ターゲット データのエクスポート


SSMS にターゲット データがあれば、次のようにしてデータをさまざまな形式にエクスポートできます。


1. データ表示にフォーカスを移動します。

    - 拡張イベント用の新しいツール バーと新しいメニュー項目が両方ともすぐに表示されます。

    ![表示データのエクスポート: [拡張イベント] > [エクスポート先] > (.csv、または .xel、またはテーブルへ)](../../relational-databases/extended-events/media/xevents-ssms-ui75-menuextevent-exportto-xel.png)

2. 新しいメニュー項目 **[拡張イベント]** をクリックします。
3. **[エクスポート先]** をクリックして、形式を選択します。



## <a name="d-manipulate-data-in-the-display"></a>D. 表示内のデータの操作


SSMS UI には、単にデータをそのまま表示するだけでなく、データを操作する手段がいくつか用意されています。



### <a name="d1-context-menus-in-the-data-display"></a>D.1 データ表示内のコンテキスト メニュー


データ表示内の右クリックする場所によって、表示されるコンテキスト メニューが異なります。



#### <a name="d11-right-click-a-data-cell"></a>D.1.1 データ セルを右クリックする


次のスクリーン ショットは、データ表示内のセルを右クリックすると表示されるコンテキスト メニューを示しています。 このスクリーン ショットは、 **[コピー]** メニュー項目の展開も示しています。


![データ表示内のセルを右クリックする](../../relational-databases/extended-events/media/xevents-ssms-ui25-rightclickcell.png)



#### <a name="d12-right-click-a-column-header"></a>D.1.2 列ヘッダーを右クリックする


次のスクリーン ショットは、 **timestamp** ヘッダーを右クリックしたときのコンテキスト メニューを示しています。


![データ表示内の列ヘッダーを右クリックする また、グリッドを詳細に示しています。](../../relational-databases/extended-events/media/xevents-ssms-ui40-toolbar.png)


前のスクリーン ショットは、拡張イベント用の特別なツール バーも示しています。 [詳細] ボタンが明るいのは、ボタンがアクティブであることを示しています。 したがって、この画像は **[詳細]** タブも示しており、グリッドはデータ表示の第 2 の部分として存在しています。



### <a name="d2-choose-columns-merge-columns"></a>D.2 列の選択、列のマージ


**[列の選択]** オプションを使用して、データ列の表示/非表示を制御できます。 **[列の選択]** メニュー項目は、次のように異なる場所に表示されます。

- **[拡張イベント]** メニュー上。
- 拡張イベントのツール バー上。
- データ表示内のヘッダーのコンテキスト メニュー上。


**[列の選択]** をクリックすると、同じ名前のダイアログが表示されます。


![[列の選択] ダイアログ ([列のマージ] オプションも含まれる)](../../relational-databases/extended-events/media/xevents-ssms-ui35-choosecolumns.png)



#### <a name="d21-merge-columns"></a>D.2.1 列のマージ


**[列の選択]** ダイアログには、次の目的で複数の列を 1 つにマージするためのセクションがあります。

- 表示。
- エクスポート。



### <a name="d3-filters"></a>D.3 フィルター


拡張イベントの領域では、指定できるフィルターの主な種類として、次の 2 つがあります。

- *事前ターゲット フィルター:* イベント エンジンからターゲットに送られるデータの量を減らすフィルター。

- *事後ターゲット フィルター:* 表示から一部のターゲット レコードを除外するために SSMS UI で選択できるフィルター。


SSMS 表示フィルターは、次のとおりです。

- *時間範囲* フィルター ( **timestamp** 列をチェック)。
- *列の値* フィルター。


時間フィルターと列フィルターの関係は、ブール値 '*AND*' です。


![[フィルター] ダイアログの時間範囲フィルターと列フィルター](../../relational-databases/extended-events/media/xevents-ssms-ui45-filters.png)



### <a name="d4-grouping-and-aggregation"></a>D.4 グループ化と集計


ある特定の列の値を対応させることによって複数の行を 1 つにグループ化することは、データの概要集計に向けての第一歩です。



#### <a name="d41-grouping"></a>D.4.1 グループ化


拡張イベントのツール バーの **[グループ化]** ボタンをクリックすると、ある特定の列を基準に表示データをグループ化できるダイアログが開きます。 次のスクリーン ショットは、*name* 列によるグループ化に使用されているダイアログを示しています。

![ツール バー > [グループ化] ボタンをクリックすると表示される [グループ化] ダイアログ](../../relational-databases/extended-events/media/xevents-ssms-ui53-grouping.png)

グループ化が完了すると、表示の外観が次のように新しくなります。

![グループ化後の表示の新しい外観](../../relational-databases/extended-events/media/xevents-ssms-ui54-grouped.png)



#### <a name="d42-aggregation"></a>D.4.2 集計


表示データがグループ化されたら、他の列のデータを集計できるようになります。  次のスクリーン ショットは、グループ化されたデータが *count*を基準に集計されていることを示しています。

![ツール バー > [集計] ボタンをクリックすると表示される [集計] ダイアログ](../../relational-databases/extended-events/media/xevents-ssms-ui51-aggregdialogcount.png)

集計が完了すると、表示の外観が次のように新しくなります。

![ツール バー > [集計] ボタンをクリックすると表示される [集計] ダイアログ](../../relational-databases/extended-events/media/xevents-ssms-ui52-aggregnewdisplay.png)



### <a name="d5-view-run-time-query-plan"></a>D.5 ランタイム クエリ プランの表示


**query_post_execution_showplan** イベントを使用すると、実際のクエリ プランを SSMS UI で調べることができます。 **[詳細]** ペインが表示されているときに、 **[クエリ プラン]** タブでクエリ プランのグラフを確認できます。クエリ プランのノードにカーソルを合わせると、そのノードのプロパティ名とその値の一覧が表示されます。


![あるノードのプロパティの一覧が表示されているクエリ プラン](../../relational-databases/extended-events/media/xevents-ssms-ui60-showplangraph.png)

## <a name="see-also"></a>参照

[XELite: XEL ファイルまたはライブ SQL ストリームから XEvents を読み取るためのクロスプラットフォーム ライブラリ](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite/)、2019 年 5 月リリース。

[Read-SQLXEvent PowerShell コマンドレット](https://www.powershellgallery.com/packages/SqlServer)、2019 年 7 月リリース。
