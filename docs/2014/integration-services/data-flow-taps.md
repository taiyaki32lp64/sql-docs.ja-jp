---
title: データ フロー タップ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2d847adf-4b3d-4949-a195-ef43de275077
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a1938f2389f64d7a869ae924690b8b22fa209f82
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059906"
---
# <a name="data-flow-taps"></a>データ フロー タップ
  [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] の新機能を使用して、ランタイム時にパッケージのデータ フロー パスのデータ タップを追加し、データ タップから外部ファイルに出力できます。 この機能を使用するには、プロジェクト配置モデルを使用して、SSIS サーバーに SSIS プロジェクトを配置する必要があります。 サーバーにパッケージを配置した後、そのパッケージを実行する前に、SSISDB データベースに対して T-SQL スクリプトを実行してデータ タップを追加する必要があります。 次にシナリオの例を示します。  
  
1.  [catalog.create_execution (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) ストアド プロシージャを使用してパッケージ実行インスタンスを作成します。  
  
2.  [catalog.add_data_tap](/sql/integration-services/system-stored-procedures/catalog-add-data-tap) または [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid) ストアド プロシージャを使用してデータ タップを追加します。  
  
3.  [catalog.start_execution (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) を使用してパッケージ実行インスタンスを開始します。  
  
 前のシナリオで説明されているステップを実行するサンプル SQL スクリプトを次に示します:  
  
```  
  
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
  
 既に説明したように、add_data_tap ストアド プロシージャを使用する代わりに、 [catalog.add_data_tap_by_guid](/sql/integration-services/system-stored-procedures/catalog-add-data-tap-by-guid)ストアド プロシージャを使用することもできます。 このストアド プロシージャは、task_package_path の代わりにデータ フロー タスクの ID をパラメーターとして取得します。 Visual Studio プロパティ ウィンドウからデータ フロー タスクの ID を取得できます。  
  
## <a name="removing-a-data-tap"></a>データ タップの削除  
 [catalog.remove_data_tap](/sql/integration-services/system-stored-procedures/catalog-remove-data-tap) ストアド プロシージャを使用して、実行開始前にデータ タップを削除できます。 このストアド プロシージャは、add_data_tap ストアド プロシージャの出力として取得できるデータ タップの ID を、パラメーターとして取得します。  
  
```  
  
DECLARE @tap_id bigint  
EXEC [SSISDB].[catalog].add_data_tap @execution_id = @execid, @task_package_path = '\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[Flat File Source.Flat File Source Output]', @data_filename = 'output.txt' @data_tap_id=@tap_id OUTPUT  
EXEC [SSISDB].[catalog].remove_data_tap @tap_id  
  
```  
  
## <a name="listing-all-data-taps"></a>すべてのデータ タップを一覧表示する  
 catalog.execution_data_taps ビューを使用して、すべてのデータ タップを一覧することもできます。 次の例は、指定の実行インスタンス (ID: 54) のデータ タップを抽出します。  
  
```  
select * from [SSISDB].[catalog].execution_data_taps where execution_id=@execid  
```  
  
## <a name="performance-consideration"></a>パフォーマンスの注意点  
 詳細なログ記録レベルを有効にしてデータ タップを追加すると、データ統合ソリューションが実行する I/O 操作が増大します。 そのためデータ タップは、トラブルシューティングの場合に限り追加することをお勧めします  
  
## <a name="video"></a>ビデオ  
 この [TechNet のビデオ](https://technet.microsoft.com/sqlserver/dn600163) は、データ タップを SQL Server 2012 SSISDB カタログに追加、使用する方法を紹介しています。パッケージをプログラム処理によってデバッグし、実行時に結果の一部をキャプチャしています。 また、データ タップの一覧および削除の方法、SSIS パッケージ内でのデータ タップの使用に関するベスト プラクティスについても説明しています。  
  
## <a name="related-tasks"></a>Related Tasks  
 [データ フローのデバッグ](troubleshooting/debugging-data-flow.md)  
  
 [パッケージ実行のトラブルシューティング ツール](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
  
