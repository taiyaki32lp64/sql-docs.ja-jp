---
title: 'SQL Server モバイル レポート: エンド ツー エンドのチュートリアル'
description: Reporting Services Web ポータル上の SQL Server Mobile Report Publisher で任意の画面サイズのモバイル レポートを作成し、それを Power BI モバイル アプリで表示するチュートリアル。
ms.date: 12/07/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: e198575e-b154-4342-b944-2bf19ec49bfd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d5ec94bb96832574cec663d38690bec8078db6ff
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028895"
---
# <a name="sql-server-mobile-reports-end-to-end-walk-through"></a>SQL Server モバイル レポート: エンド ツー エンドのチュートリアル
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] Web ポータル上の [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] で任意の画面サイズのモバイル レポートを作成し、Power BI モバイル アプリで表示するチュートリアル。

調整可能なグリッド行とグリッド列、柔軟なモバイル レポート要素を備えたデザイン領域でモバイル レポートを作成します。 さまざまなオンプレミス データ ソースに接続するか、Excel ブックをアップロードしてモバイル レポートを作成します。 レポートを [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] Web ポータルに保存し、ブラウザーまたは Power BI モバイル アプリで表示します。  
  
この記事では、次について説明します。   
  
- サンプル データ ソースとして AdventureWorks データベースを使用して、 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] Web ポータル上で共有データ ソースとデータセットを作成する。  
- [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]  
- モバイル レポートを [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] Web ポータルにパブリッシュする。  
- Power BI モバイル アプリでモバイル レポートを表示する。  
  
## <a name="before-we-start"></a>開始前の準備  
このチュートリアルを実行するには、以下の製品が必要です。  
  
* データ ソースと KPI を作成し、データセットとモバイル レポートをパブリッシュするには、[Reporting Services のネイティブ モード レポート サーバー](../install-windows/install-reporting-services-native-mode-report-server.md)へのアクセスが必要です。  
* 共有データセットを作成するには、[レポート ビルダー](../install-windows/install-report-builder.md)をインストールします。  
* モバイル レポートを作成するには、 [SQL Server Mobile Report Publisher をインストールします](https://go.microsoft.com/fwlink/?LinkId=717766)。  
* [AdventureWorks サンプル データベース](https://github.com/Microsoft/sql-server-samples/releases)。  
*  または、[Microsoft SQL Server サンプル](../../sample/microsoft-sql-server-samples.md) ページから使用可能な、World Wide Importers サンプル データベース。
* 結果を表示するには: 
  *   [Power BI サービスにサインアップする](https://go.microsoft.com/fwlink/?LinkID=513879) および
  *  iOS、Android フォン、Windows 10 デバイスなどのモバイル デバイスに[Power BI モバイル アプリをダウンロードする](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-apps-for-mobile-devices)  

  
## <a name="create-a-shared-data-source"></a>共有データ ソースの作成  
  
Reporting Services でサポートされるデータ ソースのいずれもからモバイル レポートの共有データ ソースを作成できます。 「 [サポートされるデータ ソースの一覧](../report-data/data-sources-supported-by-reporting-services-ssrs.md)」を参照してください。  
  
1. [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] Web ポータルから、 **[新規作成]**  >  **[データソース]** をクリックします。  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
3. データ ソースの情報を入力し、 **[OK]** をクリックします。  
  
    既定では、データ ソースはポータルに表示されません。    
   
5. データ ソースを表示するには、 **[表示]**  >  **[データソース]** をクリックします。  
  
   ![PBI_SSMRP_DisplayDataSources](../../reporting-services/mobile-reports/media/pbi-ssmrp-displaydatasources.png)  
   
6. これで、 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] ポータル内にデータ ソースが表示されます。  
  
   ![PBI_SSMRP_PortlDataSource](../../reporting-services/mobile-reports/media/pbi-ssmrp-portldatasource.png)  
  
[Reporting Services の共有データ ソース](../report-data/create-modify-and-delete-shared-data-sources-ssrs.md)の詳細を参照してください。  
   
## <a name="shared-dataset">共有データセットを作成する</a>  
  
[!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] のレポート デザイナーなど、既存の [!INCLUDE[ssBIDevStudioFull_md](../../includes/ssbidevstudiofull-md.md)]クライアント ツールを使用して、共有データセットを作成します。  このチュートリアルでは [!INCLUDE[PRODUCT_NAME](../../includes/ssrbnoversion.md)]を使用します。 [レポート ビルダーをインストールする](../install-windows/install-report-builder.md)か、Web ポータルから起動します。 3 つのデータセットを Reporting Services モバイル レポートの KPI の値、KPI のトレンド、および詳細フィールド用に 1 つずつ作成します。     
  
1. [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] Web ポータルから、 **[新規作成]**  >  **[ページ分割されたレポート]** をクリックし、 [!INCLUDE[PRODUCT_NAME](../../includes/ssrbnoversion.md)]を起動します。  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)   
2. **[新しいデータセット]** をクリックします。  
  
   ![PBI_SSMRP_RBNewDataset](../../reporting-services/mobile-reports/media/pbi-ssmrp-rbnewdataset.png)  
   
3. **[他のデータ ソースを参照します]** をクリックします。  
   
4. [名前] フィールドに、この形式で、データ ソースを保存したサーバーの名前を入力します。   
   
   名前: https://*localhost*/ReportServer  
   アイテムの種類: データ ソース (*.rsds)  
   
5. **[開く]** をクリックし、そのサーバー上に作成したデータ ソースに移動します。  
   
6. データ ソースを選択し、 **[開く]** を再度クリックします。    
  
7. データセットを [!INCLUDE[PRODUCT_NAME](../../includes/ssrbnoversion.md)]でデザインします。  
  
   ![PBI_SSMRP_RB_QueryDesignr600](../../reporting-services/mobile-reports/media/pbi-ssmrp-rb-querydesignr600.png)  
   
8. 完了したら、データセットを [!INCLUDE[PRODUCT_NAME](../../includes/ssrs.md)] レポート サーバーに保存します。    
   
これで、KPI とモバイル レポートの基準としてデータセットを使用できます。  同じデータ ソースに対して複数のデータセットを作成できます。 さらに、これらの共有データセットに対して複数の KPI とモバイル レポートを作成できます。   
  
## <a name="create-KPI">KPI の作成</a>  
[!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] Web ポータルで KPI の権限を作成します。    
  
1. Web ポータルの右上隅で **[新規作成]**  >  **[新しい KPI]** をクリックします。   
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
      
   KPI の作成画面では、値を手動で入力するか、共有データセットを使用できます。    
2. **値** を **[手動設定]** から **[データセット フィールド]** に変更します。  
   
   ![PBI_SSMRP_KPI_DatasetField](../../reporting-services/mobile-reports/media/pbi-ssmrp-kpi-datasetfield.png)  
   
3. **[データセット フィールドの選択]** ボックスで、省略記号ボタン ( **...** ) をクリックし、前の手順からデータセットを選択します。  
   
   ![PBI_SSMRP_KPIPickDataset](../../reporting-services/mobile-reports/media/pbi-ssmrp-kpipickdataset.png)  
   
4. データセットのフィールドを選択します。    
   
   ![PBI_SSMRP_KPIPickField](../../reporting-services/mobile-reports/media/pbi-ssmrp-kpipickfield.png)  
     
5. 必要な集計を選択します。 KPI は 1 つの数値のみを表示できます。フィールドが集計されると、その数値が表示されます。

   ![reporting-services-kpi-pick-aggregation](../../reporting-services/mobile-reports/media/reporting-services-kpi-pick-aggregation.png)

6. **[OK]** をクリックします。

7. **[トレンド セット]** ボックスで、 **[データセット トレンド]** をクリックします。  
  
6. **[データセット トレンドの選択]** ボックスで、省略記号ボタン ( **...** ) をクリックします  
   
7. フィールドを選択し、 **[OK]** をクリックします。  

   ![PBI_SSMRP_KPIPickTrend](../../reporting-services/mobile-reports/media/pbi-ssmrp-kpipicktrend.png)  
  
8. KPI に名前を付けて、視覚エフェクトの種類を選択し、 **[作成]** をクリックします。   
  
   KPI が [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] Web ポータルに表示されます。  
   
    ![PBI_SSMRP_NewKPI](../../reporting-services/mobile-reports/media/pbi-ssmrp-newkpi.png)  
    
## <a name="create-mobile-report">Reporting Services モバイル レポートの作成</a>  
   
Reporting Services モバイル レポートを作成するには、 [SQL Server Mobile Report Publisher をインストールする](https://go.microsoft.com/fwlink/?LinkId=717766)か、 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] Web ポータルから起動します。 

[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]を初めて開く場合は、モバイル レポートを作成できる空白のキャンバスが表示されます。 最初にビジュアルを作成することで開始したり、データで開始したりできます。 最初にビジュアルを作成する場合、 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] はレポートに関連付けられているシミュレートされたデータを自動的に生成し、ビジュアルの選択内容を変更すると動的に変更します。 自身で実行してみてください。   
  
## <a name="start-with-the-visuals"></a>ビジュアルで開始する  
  
1. [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] Web ポータルから、 **[新規作成]**  >  **[モバイル レポート]** をクリックし、 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)]を起動します。  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)

   [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] により、マスター レイアウト グリッドが表示されます。  
  
2. **[レイアウト]** タブで、[グラフ] セクションまで下方向へスクロールします。  
  
   ![PBI_SSMRP_LayoutTabCharts2](../../reporting-services/mobile-reports/media/pbi-ssmrp-layouttabcharts2.png)  
  
2. **[ツリー マップ]** をグリッドにドラッグし、右下隅にドラッグし、3 つ分の列の幅、3 つ分の行の高さに調整します。  
  
   ![PBI_SSMRP_TreeMap](../../reporting-services/mobile-reports/media/pbi-ssmrp-treemap.png)  
  
3. 下部にあるビジュアルのプロパティを表示できます。 横方向にスクロールして、すべてを表示する必要があるかもしれません。   
  
   ![PBI_SSMRP_TreeMapVisProps](../../reporting-services/mobile-reports/media/pbi-ssmrp-treemapvisprops.png)  
  
4. ツリー マップ ビジュアルが選択されたら、左上隅にある **[データ]** タブを選択します。   
  
   これで、 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] が生成した、シミュレートされたフィールドと値を確認し、ツリー マップで表示されるサイズと色を確認できます。  
  
   ![PBI_SSMRP_TreeMapDataProps](../../reporting-services/mobile-reports/media/pbi-ssmrp-treemapdataprops.png)  
  
6. **[レイアウト]** タブをクリックします。  
  
7. オプションの歯車 ![PBI_SSMRP_Cog](../../reporting-services/mobile-reports/media/pbi-ssmrp-cog.png) (ツリー マップの右上隅にある) をクリックし、含まれるメニューを表示します。   
  
   ![PBI_SSMRP_OptionsWheel](../../reporting-services/mobile-reports/media/pbi-ssmrp-optionswheel.png)  
  
8. ホイールの真ん中にある矢印をクリックし、閉じます。  
  
## <a name="add-your-own-data"></a>独自のデータを追加する  
  
1. **[データ]** タブに切り替えます。    
   
2. 独自のデータを追加するには、右上隅にある **[データの追加]** をクリックし、データに移動します。    
  
3. ローカルの Excel ブックからデータを使用する場合がありますが、ここでは、 [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] Web ポータル上にある共有データセットから使用します。 "追加されたサーバー" メッセージが表示されます。  
  
4. サーバーを選択し、作成したデータセットを選択します。  
   
3. **[データ]** タブに戻り、 **[データ プロパティ]** ウィンドウで **[サイズが表すもの]** 、 **[色が表すもの]** 、およびその他のプロパティを独自のデータのフィールドに変更します。 
   
   *  **[サイズが表すもの]** 、 **[色が表すもの]** 、および **[カスタム中央値]** は、数値フィールドである必要があります。 
   *  **[グループ化]** はカテゴリであり、テキスト フィールドです。
   
   ![ssrs-mobile-report-data-properties](../../reporting-services/mobile-reports/media/ssrs-mobile-report-data-properties.png)
   
6. **[プレビュー]** を選択し、ツリー マップのデータが更新されたことを確認します。  

## <a name="add-a-gauge-to-your-mobile-report"></a>モバイル レポートにゲージを追加する

ゲージを追加し、同じデータセットを使用して、年度累計売上を昨年度の売上と比較する方法を確認します。

1. [レイアウト] タブで、半ドーナツをキャンバスにドラッグします。 ツリー マップの下に配置させ、右下隅をドラッグし、3 つ分の正方形の幅、2 つ分の正方形の高さに調整します。 

2. 再度、シミュレートされたデータから開始します。 

   **[ビジュアルのプロパティ]** では、既定は **[大きい値が適当]** であり、 **[差分ラベル]** は **[ターゲットの比率]** であることに注意してください。 既定の **[範囲停止]** を変更することはできますが、ここでは変更する必要はありません。

   ![ssrs-mobile-report-donut-visual-properties](../../reporting-services/mobile-reports/media/ssrs-mobile-report-donut-visual-properties.png)
   
3. **[データ]** タブで、データを含むテーブルを選択し、 **[主要な値]** フィールドと **[比較対象値]** で比較するフィールドを選択します。

4. 別の集計を選択し、 **[主要な値]** で 1 つの数値と **[比較対象値]** で 1 つの数値を作成することができます。 既定では合計です。

   ![ssrs-mobile-report-donut-sum](../../reporting-services/mobile-reports/media/ssrs-mobile-report-donut-sum.png)

5. **[プレビュー]** を選択し、外観を確認します。 

   ![ssrs-mobile-report-donut-preview](../../reporting-services/mobile-reports/media/ssrs-mobile-report-donut-preview.png)

## <a name="add-a-selection-list-as-a-filter"></a>選択一覧をフィルターとして追加する

選択一覧は、Power BI および Excel のスライサーと同様に機能します。 1 つ追加して、モバイル レポート内で他のビジュアルをフィルター処理できます。

1. **[レイアウト]** タブで、選択一覧をツリー マップの右にドラッグし、右下隅をドラッグし、2 つ分の正方形の幅、キャンバスと同じ高さの 5 つ分の正方形に調整します。 

   ![ssrs-mobile-report-selection-list](../../reporting-services/mobile-reports/media/ssrs-mobile-report-selection-list.png)

2. **[データ]** タブの **[データ プロパティ]** で、 **[キー]** と **[ラベル]** を、フィルター処理するデータのフィールドに設定します。

   ![ssrs-mobile-report-selection-list-data-properties](../../reporting-services/mobile-reports/media/ssrs-mobile-report-selection-list-data-properties.png)
   
## <a name="create-a-mobile-report-for-phones"></a>電話用モバイル レポートを作成する  
  
マスター レイアウトでビジュアルを作成したら、電話ユーザー用に最適化されたレイアウトを持つモバイル レポートを作成できます。    
  
1. 右上隅で、キャンバス アイコン、 **[電話]** の順にクリックします。  
  
2. [レイアウト] タブの **[Control Instances (コントロール インスタンス)]** で、作成した 2 つのグラフを確認します。   
  
3. ツリー マップを電話キャンバスにドラッグし、4 つ分の列の幅、3 つ分の行の高さに調整します。  
  

## <a name="save-your-mobile-report"></a>モバイル レポートを保存する  
ローカルで、または [!INCLUDE[PRODUCT_NAME](../../includes/ssrsnoversion.md)] Web ポータルにレポートを保存できます。 ローカルに保存する場合、 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] によりキャッシュされたデータで保存されるため、開いて操作を続行できます。 ただし、モバイル デバイスには表示できません。   
  
1. 左上隅の [保存] アイコンをクリックします。   
   
2. 他のユーザーと共有し、モバイル デバイスに表示するには、 **[サーバーに保存]** をクリックします。  
  
3. サーバー上で、モバイル レポートを保存するフォルダーを参照します。  
  
4. **[フォルダーの選択]**  >  **[保存]** をクリックします。  
  
   レポートの保存を確認するメッセージが表示されます。  
    
   保存した後、ポータルに戻り、モバイル レポートの縮小表示を確認できます。   
    
5. 縮小表示をタップし、Web ポータルでレポートを確認します。  
  
## <a name="view-your-report-on-the-web-portal"></a>Web ポータルでレポートを表示する

  
## <a name="view-your-report-on-a-mobile-device"></a>モバイル デバイスでレポートを表示する   
  
[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] レポートを表示するには、最初に次の作業が必要になります。

*  アカウントをまだ持っていない場合は、[Power BI サービスにサインアップする](https://go.microsoft.com/fwlink/?LinkID=513879)。
*  モバイル デバイスに[Power BI モバイル アプリをダウンロードする](https://powerbi.microsoft.com/documentation/powerbi-power-bi-apps-for-mobile-devices/) 。  

### <a name="view-your-mobile-report"></a>モバイル レポートを表示する
  
1.  モバイル デバイスで Power BI アプリを開き、サインインします。  
    
2.  Reporting Services モバイル レポートおよび KPI を表示するには、 **[Reporting Services]** をタップします。  
![PBI_iPad_GetStartedSm](../../reporting-services/mobile-reports/media/pbi-ipad-getstartedsm.png)  
  
3. 左上隅にあるオプション アイコン ![[PBI_iPad_OptionsIcon]](../../reporting-services/mobile-reports/media/pbi-ipad-optionsicon.png) をタップし、 **[サーバーに接続]** をタップします。  
  
   ![PBI_iPad_SSMRP_ConnectCrop](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-connectcrop.png)  
  
4. サーバーに名前を指定し、サーバー アドレス、メール アドレスとパスワードを次の形式で入力します。  
  
   ![PBI_iPad_SSMRP_ConnectContoso](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-connectcontoso.png)   
  
5.  これで、左側のナビゲーション バーにサーバーが表示されます。  
  
    ![PBI_iPad_SSMRP_LeftNavBiggr](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-leftnavbiggr.png)  
      
> [!TIP]
> オプション アイコン ![[PBI_iPad_OptionsIcon]](../../reporting-services/mobile-reports/media/pbi-ipad-optionsicon.png) をタップすると、Reporting Services Web ポータル内の Reporting Services モバイル レポートと Power BI サービス内のダッシュ ボード間をいつでも移動できます。  

  
## <a name="view-kpis-and-mobile-reports-in-the-power-bi-app"></a>Power BI アプリで KPI とモバイル レポートを表示する  
  
**[KPI]** または **[モバイル レポート]** タブをタップします。   
  
![PBI_iPad_SSMRP_Portal](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-portal.png)  
  
- KPI をタップし、フォーカス モードで表示します。  
  
    ![PBI_iPad_SSMRP_Tile](../../reporting-services/mobile-reports/media/pbi-ipad-ssmrp-tile.png)  
  
- モバイル レポートをタップし、Power BI アプリを開いて対話します。  
  
KPI とモバイル レポートは、Reporting Services Web ポータルにある同じフォルダーに表示されます。   
  
## <a name="see-also"></a>参照  
 
-  iOS と Android デバイス上の [Power BI モバイル アプリでオンプレミスのレポート サーバーのモバイル レポートと KPI](https://docs.microsoft.com/power-bi/consumer/mobile/mobile-app-ssrs-kpis-mobile-on-premises-reports) を表示する
-  [Windows 10 デバイス上の Power BI モバイル アプリでオンプレミスのレポート サーバーのモバイル レポートと KPI を表示する](https://powerbi.microsoft.com/documentation/powerbi-mobile-win10-kpis-mobile-reports/)    
  
   

