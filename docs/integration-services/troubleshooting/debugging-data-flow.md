---
title: データ フローのデバッグ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- progress reporting [Integration Services]
- data viewers [Integration Services]
- data flow [Integration Services], debugging
- debugging [Integration Services], data flow
- counting rows
ms.assetid: 1c574f1b-54f7-4c05-8e42-8620e2c1df0f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c6076e4c02ccb4c91c88a22df7cd7c4a50b0f877
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295120"
---
# <a name="debugging-data-flow"></a>データ フローのデバッグ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] と [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのデータ フローのトラブルシューティングを行うために使用できる機能とツールが含まれています。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、データ ビューアーが用意されています。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーと [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 変換では、行数が用意されています。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、実行時の進行状況レポートが用意されています。  
  
## <a name="data-viewers"></a>データ ビューアー  
 データ ビューアーは、データ フローの 2 つのコンポーネント間のデータを表示します。 データ ビューアーでデータを表示できるのは、データ ソースからデータが抽出され、最初にデータ フローに入るときと、変換によりデータが更新される前後、およびデータが変換先に読み込まれる前です。  
  
 データを表示するには、2 つのデータ フロー コンポーネントを連結するパスに、データ ビューアーをアタッチします。 データ フロー コンポーネント間のデータを表示する機能を使用すると、予期しないデータ値の識別、変換による列の値の変更方法の表示、および変換が失敗した原因の検出が容易になります。 たとえば、参照テーブル内の参照が失敗する場合、それを修正するために、既定データを空白の列に提供する変換を追加できます。  
  
 データ ビューアーでは、グリッドにデータを表示できます。 グリッドを使用する場合は、表示する列を選択します。 選択した列の値は、表形式で表示されます。  
  
 1 つのパスに、複数のデータ ビューアーを含めることもできます。 このため、同じデータをさまざまな形式で表示できます。たとえば、データのグラフ表示とグリッド表示を作成したり、データの列ごとに異なるデータ ビューアーを作成したりできます。  
  
 データ ビューアーをパスに追加すると、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、 **[データ フロー]** タブのデザイン画面のパスの隣に、データ ビューアーのアイコンが追加されます。 条件分割変換など、複数の出力を持つ変換には、パスごとにデータ ビューアーを含めることができます。  
  
 実行時には **[データ ビューアー]** ウィンドウが開き、データ ビューアーの形式で指定された情報が表示されます。 たとえば、グリッド形式を使用するデータ ビューアーでは、選択した列のデータ、データ フロー コンポーネントに渡される出力列の数、および表示される行数が表示されます。 この情報はバッファーごとに表示されますが、データ フローの行の幅に応じて、バッファーが表示する行数は増減します。  
  
 **[データ ビューアー]** ダイアログ ボックスでは、クリップボードへのデータのコピー、テーブルのすべてのデータの消去、データ ビューアーの再構成、データのフローの再開、およびデータ ビューアーのデタッチまたはアタッチを行うことができます。  
  
#### <a name="to-add-a-data-viewer"></a>データ ビューアーを追加するには  
  
-   [データ フローにデータ ビューアーを追加する](#add_viewer)  
  
## <a name="row-counts"></a>行数  
 **デザイナーでは、** [データ フロー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] タブのデザイン画面のパスの隣に、パスを通過した行数が表示されます。 データがパスを移動する間、表示される行数が定期的に更新されます。  
  
 また、データ フローに行数変換を追加して、最終的な行数を変数に取り込むこともできます。 詳細については、「 [Row Count Transformation](../../integration-services/data-flow/transformations/row-count-transformation.md)」を参照してください。  
  
## <a name="progress-reporting"></a>進行状況レポート  
 パッケージを実行すると、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[データ フロー]** タブのデザイン画面に、各データ フロー コンポーネントが状態を示す色で表示され、進行状況を確認できます。 各コンポーネントが作業を開始すると、コンポーネントは無色から黄色に変わり、正常に完了すると、緑色に変わります。 赤色は、コンポーネントが失敗したことを示します。  
  
 次の表では、色分けについて説明します。  
  
|色|[説明]|  
|-----------|-----------------|  
|無色|データ フロー エンジンによる呼び出しの待機中です。|  
|黄|変換の実行、データの抽出、またはデータの読み込みを行っています。|  
|[緑]|正常に実行されました。|  
|赤|実行されましたがエラーが発生しました。|  

## <a name="analysis-of-data-flow"></a>データ フローの分析
  [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) **SSISDB** データベース ビューを使用して、パッケージのデータ フローを分析できます。 このビューは、データ フロー コンポーネントが下流コンポーネントへデータを送信するたびに 1 行表示します。 この情報を使用して、各コンポーネントに送信される行をより詳しく理解できます。  
  
> [!NOTE]  
>  catalog.execution_data_statistics ビューに関する情報を取得するために、ログ レベルは **詳細** に設定する必要があります。  
  
 次の例では、パッケージのコンポーネント間で送信された行の数が表示されます。  
  
```sql
use SSISDB  
select package_name, task_name, source_component_name, destination_component_name, rows_sent  
from catalog.execution_data_statistics  
where execution_id = 132  
order by source_component_name, destination_component_name   
```  
  
 以下の例では、特定の実行で各コンポーネントによって送信された 1 ミリ秒あたりの行数が計算されます。 計算される値は次のとおりです。  
  
-   **total_rows** - コンポーネントによって送信されたすべての行の合計数  
  
-   **wall_clock_time_ms** - コンポーネントごとの実行の合計経過時間 (ミリ秒単位)  
  
-   **num_rows_per_millisecond** - 各コンポーネントによって送信された 1 ミリ秒あたりの行数  
  
 計算時の 0 除算エラーを防止するために **HAVING** 句が使用されています。  
  
```sql  
use SSISDB  
select source_component_name, destination_component_name,  
    sum(rows_sent) as total_rows,  
    DATEDIFF(ms,min(created_time),max(created_time)) as wall_clock_time_ms,  
    ((0.0+sum(rows_sent)) / (datediff(ms,min(created_time),max(created_time)))) as [num_rows_per_millisecond]  
from [catalog].[execution_data_statistics]  
where execution_id = 132  
group by source_component_name, destination_component_name  
having (datediff(ms,min(created_time),max(created_time))) > 0  
order by source_component_name desc  
```  

## <a name="configure-an-error-output-in-a-data-flow-component"></a>データ フロー コンポーネントでエラー出力を構成する
  多くのデータ フロー コンポーネントがエラー出力をサポートしており、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでエラー出力を構成する方法は、コンポーネントに応じて異なります。 エラー出力の構成以外に、エラー出力の列を構成することもできます。 これには、コンポーネントによって追加される **[ErrorCode]** 列や **[ErrorColumn]** 列の構成が含まれます。  
  
### <a name="configuring-an-error-output"></a>エラー出力の構成  
 エラー出力を構成する場合、2 つのオプションがあります。  
  
-   **[エラー出力の構成]** ダイアログ ボックスを使用します。 このダイアログ ボックスを使用すると、エラー出力をサポートするデータ フロー コンポーネントでエラー出力を構成できます。  
  
-   コンポーネントのエディター ダイアログ ボックスを使用します。 いくつかのコンポーネントでは、エディター ダイアログ ボックスから直接エラー出力を構成できます。 ただし、ADO NET ソース、列インポート変換、OLE DB コマンド変換、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 変換先のエディター ダイアログ ボックスからはエラー出力を構成できません。  
  
 次の手順では、これらのダイアログ ボックスを使用してエラー出力を構成する方法を説明します。  
  
#### <a name="to-configure-an-error-output-using-the-configure-error-output-dialog-box"></a>[エラー出力の構成] ダイアログ ボックスを使用してエラー出力を構成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[データ フロー]** タブをクリックします。  
  
4.  赤い矢印で表示されているエラー出力を、エラー元のコンポーネントからデータ フローの別のコンポーネントにドラッグします。  
  
5.  **[エラー出力の構成]** ダイアログ ボックスで、コンポーネントの入力の各列について、 **[エラー]** 列および **[切り捨て]** 列のアクションを選択します。  
  
6.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
#### <a name="to-add-an-error-output-using-the-editor-dialog-box-for-the-component"></a>コンポーネントのエディター ダイアログ ボックスを使用してエラー出力を追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[データ フロー]** タブをクリックします。  
  
4.  エラー出力を構成するデータ フロー コンポーネントをダブルクリックし、コンポーネントに応じて、次のいずれかの手順を実行します。  
  
    -   **[エラー出力の構成]** をクリックします。  
  
    -   **[エラー出力]** をクリックします。  
  
5.  各列の **[エラー]** オプションを設定します。  
  
6.  各列の **[切り捨て]** オプションを設定します。  
  
7.  **[OK]** をクリックします。  
  
8.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="configuring-error-output-columns"></a>エラー出力列の構成  
 エラー出力列を構成するには、 **[詳細エディター]** ダイアログ ボックスの **[入力プロパティと出力プロパティ]** タブを使用します。  
  
#### <a name="to-configure-error-output-columns"></a>エラー出力列を構成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[データ フロー]** タブをクリックします。  
  
4.  構成するエラー出力列が含まれているコンポーネントを右クリックし、 **[詳細エディターの表示]** をクリックします。  
  
5.  **[入力プロパティと出力プロパティ]** タブをクリックして、 **[\<コンポーネント名> のエラー出力]** を展開してから **[出力列]** を展開します。  
  
6.  列をクリックして、プロパティを更新します。  
  
    > [!NOTE]  
    >  列の一覧には、コンポーネントの入力列、前のエラー出力で追加された **[ErrorCode]** 列と **[ErrorColumn]** 列、このコンポーネントによって追加された **[ErrorCode]** 列と **[ErrorColumn]** 列が表示されます。  
  
7.  クリックして **OK.**  
  
8.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  

## <a name="add_viewer"></a> データ フローにデータ ビューアーを追加する
  このトピックでは、データ フローにデータ ビューアーを追加して構成する方法について説明します。 データ ビューアーには、2 つのデータ フロー コンポーネント間を移動するデータが表示されます。 たとえば、データ ビューアーでは、データ ソースから抽出されたデータを、データ フローの変換で変更される前の状態で表示できます。  
  
 パスは、データ フロー コンポーネントの出力を別のコンポーネントの入力に連結することにより、データ フロー内のコンポーネントを連結します。  
  
 データ ビューアーをパッケージに追加するには、パッケージにデータ フロー タスクが含まれていて、少なくとも 2 つのデータ フロー コンポーネントが接続されている必要があります。  
  
 データ ビューアーをエラー出力に追加すると、エラーの説明とエラーが発生した列の名前が表示されます。 既定では、エラー出力にはエラーと列の数値識別子のみが含まれます。  
  
### <a name="to-add-a-data-viewer-to-a-data-flow"></a>データ フローにデータ ビューアーを追加するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  アクティブになっていない場合は、 **[制御フロー]** タブをクリックします。  
  
4.  データ ビューアーをアタッチするデータ フローに対応するデータ フロー タスクをクリックし、 **[データ フロー]** タブをクリックします。  
  
5.  2 つのデータ フロー コンポーネント間のパスを右クリックし、 **[編集]** をクリックします。  
  
6.  **[全般]** ページで、パスのプロパティを表示および編集できます。 たとえば、 **[PathAnnotation]** ボックスの一覧で、パスの横に表示される注釈を選択できます。  
  
7.  **[メタデータ]** ページで、列のメタデータを表示し、メタデータをクリップボードにコピーできます。  
  
8.  **[データ ビューアー]** ページで、 **[データ ビューアーを有効にする]** をクリックします。  
  
9. [表示する列] 領域で、データ ビューアーに表示する列を選択します。 既定では、表示可能なすべての列が選択され、 **[表示する列]** の一覧に表示されます。 表示しない列は、選択してから左矢印をクリックして、 **[未使用の列]** の一覧に移動させます。  
  
    > [!NOTE]  
    >  グリッドでは、DT_DATE、DT_DBTIME2、DT_FILETIME、DT_DBTIMESTAMP、DT_DBTIMESTAMP2、および DT_DBTIMESTAMPOFFSET の各データ型を表す値は、ISO 8601 に従って書式設定された文字列として表示され、 **T** 区切りが空白区切りに置き換わります。 DT_DATE データ型および DT_FILETIME データ型を表す値には、秒の小数部を表す 7 桁が含まれています。 DT_FILETIME データ型では秒の小数部が 3 桁のみ格納されるため、残りの 4 桁についてはグリッドに 0 が表示されます。 DT_DBTIMESTAMP データ型を表す値には、秒の小数部を表す 3 桁が含まれています。 DT_DBTIME2、DT_DBTIMESTAMP2、および DT_DBTIMESTAMPOFFSET の各データ型を表す値については、秒を表す小数点以下桁数が、列のデータ型で指定された小数点以下桁数と一致します。 ISO 8601 形式の詳細については、「 [日付および時刻の形式](https://msdn.microsoft.com/library/bed6e2c1-791a-4fa1-b29f-cbfdd1fa8d39)」を参照してください。 データ型の詳細については、「 [Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
10. **[OK]** をクリックします。  

## <a name="data-flow-taps"></a>データ フロー タップ
 ランタイム時にパッケージのデータ フロー パスのデータ タップを追加し、データ タップから外部ファイルに出力できます。 この機能を使用するには、プロジェクト配置モデルを使用して、SSIS サーバーに SSIS プロジェクトを配置する必要があります。 サーバーにパッケージを配置した後、そのパッケージを実行する前に、SSISDB データベースに対して T-SQL スクリプトを実行してデータ タップを追加する必要があります。 次にシナリオの例を示します。  
  
1.  [catalog.create_execution (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md) ストアド プロシージャを使用してパッケージ実行インスタンスを作成します。  
  
2.  [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md) または [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md) ストアド プロシージャを使用してデータ タップを追加します。  
  
3.  [catalog.start_execution (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) を使用してパッケージ実行インスタンスを開始します。  
  
 前のシナリオで説明されているステップを実行するサンプル SQL スクリプトを次に示します:  
  
```sql
Declare @execid bigint  
EXEC [SSISDB].[catalog].[create_execution] @folder_name=N'ETL Folder', @project_name=N'ETL Project', @package_name=N'Package.dtsx', @execution_id=@execid OUTPUT  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt'  
EXEC [SSISDB].[catalog].[start_execution] @execid  
```  
  
 create_execution ストアド プロシージャのフォルダー名、プロジェクト名、およびパッケージ名パラメーターは、Integration Services カタログのフォルダー、プロジェクト、およびパッケージ名に対応しています。 次のイメージに示すように、create_execution 呼び出しで使用するフォルダー、プロジェクト、およびパッケージ名を SQL Server Management Studio から取得できます。 SSIS プロジェクトがここに表示されない場合は、プロジェクトを SSIS サーバーに配置していない可能性があります。 Visual Studio の SSIS プロジェクトを右クリックした後 [配置] をクリックし、適切な SSIS サーバーにプロジェクトを配置します。  
  
 SQL ステートメントを入力する代わりに、次のステップを実行し、実行パッケージのスクリプトを生成することができます:  
  
1.  **Package.dtsx** を右クリックし、 **[実行]** をクリックします。  
  
2.  **[スクリプト]** ツール バー ボタンをクリックしてスクリプトを生成します。  
  
3.  ここで、add_data_tap ステートメントを start_execution 呼び出しの前に追加します。  
  
 add_data_tap ストアド プロシージャの task_package_path パラメーターは、Visual Studio のデータ フロー タスクの PackagePath プロパティに対応しています。 Visual Studio で **[データ フロー タスク]** を右クリックし、 **[プロパティ]** をクリックして [プロパティ] ウィンドウを起動します。  add_data_tap ストアド プロシージャ呼び出しの task_package_path パラメーターの値として使用する、 **PackagePath** プロパティの値を確認します。  
  
 add_data_tap ストアド プロシージャの dataflow_path_id_string パラメーターは、データ タップを追加するデータ フロー パスの IdentificationString プロパティに対応しています。 dataflow_path_id_string を取得するには、データ フロー パス (データ フローのタスク間の矢印) をクリックし、[プロパティ] ウィンドウで **IdentificationString** プロパティの値を確認します。  
  
 スクリプトを実行すると、出力ファイルは \<Program Files>\Microsoft の SQL Server\110\DTS\DataDumps に格納されます。 その名前のファイルが既に存在する場合、新しいファイルはサフィックス付きで (例: output[1].txt) 作成されます。  
  
 既に説明したように、add_data_tap ストアド プロシージャを使用する代わりに、 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)ストアド プロシージャを使用することもできます。 このストアド プロシージャは、task_package_path の代わりにデータ フロー タスクの ID をパラメーターとして取得します。 Visual Studio プロパティ ウィンドウからデータ フロー タスクの ID を取得できます。  
  
### <a name="removing-a-data-tap"></a>データ タップの削除  
 [catalog.remove_data_tap](../../integration-services/system-stored-procedures/catalog-remove-data-tap.md) ストアド プロシージャを使用して、実行開始前にデータ タップを削除できます。 このストアド プロシージャは、add_data_tap ストアド プロシージャの出力として取得できるデータ タップの ID を、パラメーターとして取得します。  
  
```sql
DECLARE @tap_id bigint  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt' @data_tap_id=@tap_id OUTPUT  
EXEC [SSISDB].[catalog].remove_data_tap @tap_id  
```  
  
### <a name="listing-all-data-taps"></a>すべてのデータ タップを一覧表示する  
 catalog.execution_data_taps ビューを使用して、すべてのデータ タップを一覧することもできます。 次の例は、指定の実行インスタンス (ID: 54) のデータ タップを抽出します。  
  
```sql 
select * from [SSISDB].[catalog].execution_data_taps where execution_id=@execid  
```  
  
### <a name="performance-consideration"></a>パフォーマンスの注意点  
 詳細なログ記録レベルを有効にしてデータ タップを追加すると、データ統合ソリューションが実行する I/O 操作が増大します。 そのためデータ タップは、トラブルシューティングの場合に限り追加することをお勧めします  
  
### <a name="video"></a>ビデオ  
 この [TechNet のビデオ](https://technet.microsoft.com/sqlserver/dn600163) は、データ タップを SQL Server 2012 SSISDB カタログに追加、使用する方法を紹介しています。パッケージをプログラム処理によってデバッグし、実行時に結果の一部をキャプチャしています。 また、データ タップの一覧および削除の方法、SSIS パッケージ内でのデータ タップの使用に関するベスト プラクティスについても説明しています。  
 
## <a name="see-also"></a>参照  
 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)  
  
  
