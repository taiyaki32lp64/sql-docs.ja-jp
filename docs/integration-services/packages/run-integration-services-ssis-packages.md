---
title: Integration Services (SSIS) パッケージの実行 | Microsoft Docs
ms.custom: ''
ms.date: 06/04/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.ispackageexecute.f1
- sql13.ssis.ssms.executepackage.f1
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
- executing packages [Integration Services]
- running packages [Integration Services]
- Integration Services, (See also Integration Services packages)
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fe82e7d6746f3a5fc76fda3f960f069ef4345525
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71282608"
---
# <a name="run-integration-services-ssis-packages"></a>Integration Services (SSIS) パッケージの実行

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを実行するには、それらのパッケージの格納場所に応じていくつかのツールのうちの 1 つを使用できます。 次の表にツールを示します。  

> [!NOTE]
> この記事では、SSIS パッケージを実行する方法 (全般) と、オンプレミスでパッケージを実行する方法について説明します。 次のプラットフォームで SSIS パッケージを実行することもできます。
> - **Microsoft Azure クラウド**。 詳細については、「[SQL Server Integration Services ワークロードをクラウドにリフト アンド シフトする](../lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)」と [Azure で SSIS パッケージを実行する](../lift-shift/ssis-azure-run-packages.md)方法に関するページを参照してください。
> - **Linux**。 詳しくは、「[SSIS で Linux 上のデータの抽出、変換、読み込みを行う](../../linux/sql-server-linux-migrate-ssis.md)」 をご覧ください。
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーにパッケージを格納するには、プロジェクト配置モデルを使用してプロジェクトをサーバーに配置します。 詳細については、「[Integration Services (SSIS) プロジェクトとパッケージの配置](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)」を参照してください。  
  
 SSIS パッケージ ストア、msdb データベース、またはファイル システムにパッケージを格納するには、パッケージ配置モデルを使用します。 詳細については、「[レガシー パッケージの配置 (SSIS)](../../integration-services/packages/legacy-package-deployment-ssis.md)」を参照してください。  
  
|ツール|Integration Services サーバーに格納されているパッケージ|SSIS パッケージ ストアまたは msdb データベースに格納されているパッケージ|ファイル システムに格納されているパッケージ (SSIS パッケージ ストアに含まれる場所の範囲外)|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|いいえ|いいえ<br /><br /> ただし、msdb データベースを含む [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアからプロジェクトに既存のパッケージを追加できます。 この方法でプロジェクトに既存のパッケージを追加すると、ファイル システム内にパッケージのローカル コピーが作成されます。|はい|  
|**SQL Server Management Studio (Integration Services サーバーをホストするデータベース エンジンのインスタンスに接続している場合)**<br /><br /> 詳細については、「 [[パッケージの実行] ダイアログ ボックス](#execute_package_dialog)」を参照してください。|はい|いいえ<br /><br /> ただし、これらの場所からサーバーにパッケージをインポートできます。|いいえ<br /><br /> ただし、ファイル システムからサーバーにパッケージをインポートできます。|
|**SQL Server Management Studio (Scale Out Master として有効になっている Integration Services サーバーをホストするデータベース エンジンのインスタンスに接続している場合)**<br /><br /> 詳しくは、「[Integration Services (SSIS) Scale Out でパッケージを実行する](../../integration-services/scale-out/run-packages-in-integration-services-ssis-scale-out.md)」をご覧ください。|はい|いいえ|いいえ|
|**SQL Server Management Studio (SSIS パッケージ ストアを管理する Integration Services サービスに接続している場合)**|いいえ|はい|いいえ<br /><br /> ただし、ファイル システムから [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストアにパッケージをインポートできます。|  
|**dtexec**<br /><br /> 詳しくは、「 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)」をご覧ください。|はい|はい|はい|  
|**dtexecui**<br /><br /> 詳細については、「[パッケージ実行ユーティリティ &#40;DtExecUI&#41; の UI リファレンス](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)」を参照してください。|いいえ|はい|はい|  
|**SQL Server エージェント**<br /><br /> パッケージのスケジュールを設定するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを使用します。<br /><br /> 詳細については、「 [パッケージに対する SQL Server エージェント ジョブ](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)」を参照してください。|はい|はい|はい|  
|**組み込みのストアド プロシージャ**<br /><br /> 詳細については、「[catalog.start_execution &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)」を参照してください。|はい|いいえ|いいえ|  
|**API (** <xref:Microsoft.SqlServer.Management.IntegrationServices> 名前空間の型およびメンバーを使用)|はい|いいえ|いいえ|  
|**API (** <xref:Microsoft.SqlServer.Dts.Runtime> 名前空間の型およびメンバーを使用)|現時点ではいいえ|はい|はい|  

## <a name="execution-and-logging"></a>実行とログ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージではログ記録を有効にできるので、実行時情報をログ ファイルに保存できます。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
 操作レポートを使用して、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置され、実行されている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを監視できます。 レポートは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で利用できます。 詳細については、「 [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)」を参照してください。  
  
## <a name="run-a-package-in-sql-server-data-tools"></a>SQL Server Data Tools でのパッケージの実行
  一般に、パッケージの開発、デバッグ、およびテストの段階では、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] でパッケージを実行します。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーからパッケージを実行すると、パッケージは常に即座に実行されます。  
  
 パッケージの実行中は、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[進行状況]** タブにパッケージの実行の進行状況が表示されます。パッケージおよびそのタスクおよびコンテナーの開始時間と終了時間に加え、パッケージ内で失敗したタスクまたはコンテナーに関する情報が表示されます。 パッケージの実行が完了した後は、 **[実行結果]** タブで実行時情報を確認できます。詳細については、 [「制御フローのデバッグ」](../../integration-services/troubleshooting/debugging-control-flow.md)の「進行状況レポート」を参照してください。  
  
 **デザイン時配置**。 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]でパッケージを実行すると、そのパッケージが構築されフォルダーに配置されます。 パッケージを実行する前に、パッケージを配置するフォルダーを指定できます。 フォルダーを指定しない場合、既定で **bin** フォルダーが使用されます。 こうした配置方法は、デザイン時配置と呼ばれます。  
  
### <a name="to-run-a-package-in-sql-server-data-tools"></a>SQL Server Data Tools でパッケージを実行するには  
  
1.  ソリューションに複数のプロジェクトが含まれている場合は、ソリューション エクスプローラーで、パッケージを含む [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを右クリックし、 **[スタートアップ オブジェクトに設定]** をクリックしてスタートアップ プロジェクトを設定します。  
  
2.  プロジェクトに複数のパッケージが含まれている場合は、ソリューション エクスプローラーで、パッケージの 1 つを右クリックし、 **[スタートアップ オブジェクトに設定]** をクリックしてスタートアップ パッケージを設定します。  
  
3.  パッケージを実行するには、次のいずれかの手順を実行します。  
  
    -   実行するパッケージを開き、メニュー バーの **[デバッグ開始]** をクリックするか、F5 キーを押します。 パッケージの実行が完了したら、Shift キーを押しながら F5 キーを押して、デザイン モードに戻ります。  
  
    -   ソリューション エクスプローラーでパッケージを右クリックし、 **[パッケージの実行]** をクリックします。  
  
### <a name="to-specify-a-different-folder-for-design-time-deployment"></a>デザイン時配置用に別のフォルダーを指定するには  
  
1.  ソリューション エクスプローラーで、実行するパッケージが含まれる [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクト フォルダーを右クリックし、 **[プロパティ]** をクリックします。  
  
2.  [ **\<プロジェクト名> プロパティ ページ**] ダイアログ ボックスで、 **[ビルド]** をクリックします。  
  
3.  OutputPath プロパティの値を更新して、デザイン時配置用に使用するフォルダーを指定し、 **[OK]** をクリックします。  


## <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>SQL Server Management Studio を使用した SSIS サーバーでのパッケージの実行
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーにプロジェクトを配置した後は、サーバーでパッケージを実行できます。  
  
 操作レポートを使用して、サーバー上で実行されたパッケージまたは現在実行中のパッケージに関する情報を表示できます。 詳細については、「 [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)」を参照してください。  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>SQL Server Management Studio を使用してサーバーでパッケージを実行するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開き、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カタログが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のインスタンスに接続します。  
  
2.  オブジェクト エクスプローラーで、 **[Integration Services カタログ]** ノード、 **[SSISDB]** ノードの順に展開し、配置したプロジェクトに含まれるパッケージに移動します。  
  
3.  パッケージ名を右クリックし、 **[実行]** を選択します。  
  
4.  **[パッケージの実行]** ダイアログ ボックスの **[パラメーター]** タブ、 **[接続マネージャー]** タブ、 **[詳細設定]** タブの設定を使用して、パッケージの実行を構成します。  
  
5.  **[OK]** をクリックしてパッケージを実行します。  
  
     \- または -  
  
     ストアド プロシージャを使用してパッケージを実行します。 **[スクリプト]** をクリックして、実行のインスタンスを作成し、実行のインスタンスを開始する Transact-SQL ステートメントを生成します。 ステートメントには catalog.create_execution、catalog.set_execution_parameter_value、および catalog.start_execution の各ストアド プロシージャの呼び出しが含まれています。 これらのストアド プロシージャの詳細については、「[catalog.create_execution (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)」、「[catalog.set_execution_parameter_value (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)」、および「[catalog.start_execution (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)」をご覧ください。  

## <a name="execute_package_dialog"></a> [パッケージの実行] ダイアログ ボックス
  **[パッケージの実行]** ダイアログ ボックスでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに格納されているパッケージを実行できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージには、値が環境変数に格納されているパラメーターが含まれている場合があります。 こうしたパッケージを実行するには、環境変数の値の提供に使用する環境を事前に指定する必要があります。 プロジェクトには複数の環境を含めることができますが、実行時に環境変数の値をバインドするのに使用できる環境は 1 つだけです。 パッケージで環境変数が使用されない場合、環境は不要です。  
  
 目的に合ったトピックをクリックしてください  
  
-   [[パッケージの実行] ダイアログ ボックスを開く](#open_dialog)  
  
-   [[全般] ページのオプションの設定](#general)  
  
-   [[パラメーター] タブのオプションの設定](#parameters)  
  
-   [[接続マネージャー] タブのオプションの設定](#connection)  
  
-   [[詳細設定] タブのオプションの設定](#advanced)  
  
-   [[パッケージの実行] ダイアログ ボックスのオプションのスクリプト作成](#script)  
  
###  <a name="open_dialog"></a> [パッケージの実行] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]から [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに接続します。  
  
     SSISDB データベースをホストする [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続されます。  
  
2.  オブジェクト エクスプローラーで、ツリーを展開して、 **[Integration Services カタログ]** ノードを表示します。  
  
3.  **[SSISDB]** ノードを展開します。  
  
4.  実行するパッケージを含むフォルダーを展開します。  
  
5.  パッケージを右クリックし、 **[実行]** をクリックします。  
  
###  <a name="general"></a> [全般] ページのオプションの設定  
 **[環境]** を選択して、実行するパッケージに適用される環境を指定します。  
  
###  <a name="parameters"></a> [パラメーター] タブのオプションの設定  
 **[パラメーター]** タブを使用して、パッケージの実行時に使用するパラメーターの値を変更します。  
  
###  <a name="connection"></a> [接続マネージャー] タブのオプションの設定  
 [接続マネージャー] タブを使用して、パッケージの接続マネージャーのプロパティを設定します。  
  
###  <a name="advanced"></a> [詳細設定] タブのオプションの設定  
 [詳細設定] タブを使用して、プロパティとその他のパッケージの設定を管理します。  
  
 **[追加]** 、 **[編集]** 、 **[削除]**  
 クリックしてプロパティを追加、編集、または削除します。  
  
 **ログ記録レベル**  
 パッケージ実行のログ記録レベルを選択します。 詳細については、「[catalog.set_execution_parameter_value (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md)」を参照してください。  
  
 **エラー時にダンプする**  
 パッケージの実行中にエラーが発生した場合にダンプ ファイルを作成するかどうかを指定します。 詳細については、「 [パッケージ実行用のダンプ ファイルを生成する](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)」を参照してください。  
  
 **32 ビット ランタイム**  
 パッケージが 32 ビット システムで実行されるように指定します。  
  
###  <a name="script"></a> [パッケージの実行] ダイアログ ボックスのオプションのスクリプト作成  
 **[パッケージの実行]** ダイアログ ボックスが表示されているときに、ツール バーの **[スクリプト]** を使用すると、 [!INCLUDE[tsql](../../includes/tsql-md.md)] コードを生成することもできます。 生成されたスクリプトからは、 **[パッケージの実行]** ダイアログ ボックスで選択したのと同じオプションを指定したストアド プロシージャ [catalog.start_execution (SSISDB データベース)](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) が呼び出されます。 このスクリプトは、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]の新しいスクリプト ウィンドウに表示されます。  

## <a name="see-also"></a>参照  
 [dtexec ユーティリティ](../../integration-services/packages/dtexec-utility.md)   
[SQL Server インポートおよびエクスポート ウィザードを起動する](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)
  
  
