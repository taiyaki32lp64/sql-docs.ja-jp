---
title: Analysis Services | で管理タスクをスクリプト化するMicrosoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- automatic Analysis Services administration
- administering Analysis Services
ms.assetid: 106415df-81ff-4ec3-b2e1-ca66324f4cab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 69ccdaf9bf0f8b67309a1f88c0c44a90f3167b6b
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69530919"
---
# <a name="script-administrative-tasks-in-analysis-services"></a>Analysis Services の管理タスクのスクリプト作成
  SQL Server エージェントで手動、またはスケジュールして実行できるスクリプトを記述または生成することで、 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 管理タスクを自動化できます。 次の表は、使用可能なスクリプト作成オプションについてまとめ、詳細情報へのリンクを提供します。  
  
 以下に示したすべての手法は、ファイルに保存でき、独立した操作として実行できるスクリプトをサポートしています。 テーブル モデルおよび PowerPivot ブックで使用する Data Analysis Expression (DAX) 言語は、条件を満たしていないため、以下の表には含まれていません。  
  
|手法|ファイル形式|説明|リンク|  
|-----------------|-----------------|-----------------|-----------|  
|PowerShell|.ps1|Analysis Services は、SQL Server PowerShell のスクリプト環境を、新しいプロバイダーを通じてサポートします。このプロバイダーは、コマンド ラインからのオブジェクトのナビゲーションと、バックアップ、復元、処理、ロール管理などの管理タスク用の新しいコマンドレットからのオブジェクトのナビゲーションを追加します。<br /><br /> さらに、SQL Server PowerPivot (SQLPS) プロバイダーには、汎用コマンドレット、`Invoke-ASCmd` も含まれ、XMLA、MDX、または、DMX スクリプトを PowerShell セッション内で実行することができます。<br /><br /> Analysis Services の PowerShell スクリプトは、多次元モデルとテーブル モデルの両方でサポートされますが、SharePoint からアクセスする PowerPivot ブックではサポートされません。|[PowerShell の Analysis Services](analysis-services-powershell.md)<br /><br /> [Windows PowerShell のサバイバルガイド](https://go.microsoft.com/fwlink/?LinkId=233747)|  
|ASSL または XMLA スクリプト|.xmla|Analysis Services スクリプト言語 (ASSL) は、テーブル モデルまたは多次元モデルで実行される Analysis Services 上のオブジェクトと操作のデータ アクセスを提供する XMLA の拡張機能です。 ASSL には、XML 形式での Analysis Services オブジェクトと操作の完全な式を有効化するデータ定義とコマンド言語のサポートが含まれます。 ASSL で提供されるオブジェクトとコマンドを使用するスクリプトは、.xmla ファイルとして保存されます。 Analysis Services のコンテキスト内では、ASSL を XMLA スクリプトとして参照するのが一般的です。 以下の要件が含まれる場合、この方法を選択してください。<br /><br /> スクリプトがサーバー上に直接オブジェクトを作成する、またはデータ定義と操作の両方のタスクを実行する (たとえば、データベースの再作成と処理)。<br /><br /> 複数のツールとテクノロジでスクリプトの再利用を最大限行うことが必要 SSIS パッケージまたは PowerShell スクリプトで参照される SQL Server エージェントで XMLA スクリプトは、Analysis Services コマンド タスクに追加できます。<br /><br /> スクリプトは自動的に実行する必要がある。 SQL Server エージェントを使用して、XMLA スクリプトまたは XMLA を含む SSIS パッケージを含むジョブをスケジュールできます。<br /><br /> XMLA を使用するアプリケーション要件がある。 XMLA は、マネージド コード環境を必要としないインターフェイスです。 .NET Framework を使用しないアプリケーションで XMLA スクリプトを実行することができます。|[Management Studio での Analysis Services スクリプトの作成](instances/create-analysis-services-scripts-in-management-studio.md)<br /><br /> [SQL Server Management Studio での Analysis Services テンプレートの使用](instances/use-analysis-services-templates-in-sql-server-management-studio.md)<br /><br /> [SQL Server エージェントで SSAS 管理タスクのスケジュール設定を行う](instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)<br /><br /> [Analysis Services スクリプト言語 (ASSL) での開発](multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)<br /><br /> [Invoke-ASCmd コマンドレット](/powershell/module/sqlserver/invoke-ascmd)|  
|||XMLA スクリプトを作成するには、Management Studio でスクリプト ジェネレーターを使用することができます。 オブジェクト レベルでは、オブジェクトを右クリックして、オブジェクトを作成、変更、または削除するスクリプトを生成します。 コマンド レベルでは、バックアップや復元の処理、集計のデザイン、その他のコマンドなどに対して、ダイアログ ボックスでスクリプト機能を使用してスクリプトを生成することができます。ダイアログ ボックスでは、スクリプトの出力先を新しいウィンドウ、ファイル、またはクリップボードのオプションから選択できます。 また、テキスト エディターまたはコード エディターで、XMLA スクリプトを手動で作成したり、テンプレート エクスプ ローラーで、テンプレートを使用することもできます。 スクリプトを実行するには、次のいずれかの方法を実行します。<br /><br /> Management Studio を使用して、[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] インスタンスでオブジェクトを直接作成または変更する。<br /><br /> SQL Server エージェントを使用して、Analysis Services コマンドのタスクを含むジョブをスケジュールする。<br /><br /> Invoke ASCmd コマンドレットを使用して、PowerShell セッションでスクリプトを実行する。||  
|MDX Script|.mdx|多次元式 (MDX) 言語は、分析データ ソースに対する業界標準クエリ言語で、XMLA 仕様の一部でもあります。<br /><br /> データまたはシステム情報をクエリするスタンドアロンの MDX スクリプト ファイルを作成することができます。 たとえば、ローカル サーバーの操作やサーバーの正常性に関する情報を公開する動的管理ビュー (DMV) は、MDX の Select ステートメントを介してアクセスします。<br /><br /> MDX スクリプトは、多次元モードとテーブル モードの両方のサーバーで実行されます。 SQL Server Management Studio、または `Invoke-ASCmd` を使用して PowerShell セッションから対話的にスクリプトを実行することができます。|[MDX スクリプティングの基礎 (Analysis Services)](multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)<br /><br /> [動的管理ビュー (DMV) を使用した Analysis Services の監視](instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)<br /><br /> [SQL Server Management Studio での Analysis Services テンプレートの使用](instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|DMX Script|.dmx|データ マイニング拡張機能 (DMX) は、データ マイニング モデルに対するデータ定義、データ操作、およびデータ クエリ言語です。 最初に、テンプレートを使用できます。|[SQL Server Management Studio で DMX クエリを作成する](data-mining/create-a-dmx-query-in-sql-server-management-studio.md)<br /><br /> [SQL Server Management Studio での Analysis Services テンプレートの使用](instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] パッケージ|.dtsx|[!INCLUDE[ssIS](../includes/ssis-md.md)] は、データ マイニング モデルを含む、Analysis Services オブジェクトを作成、変更、削除、および処理するタスクとデータ フローを提供します。 SQL Server エージェントを使用して、パッケージの実行をスケジュールできます。|[Analysis Services DDL 実行タスク](../integration-services/control-flow/analysis-services-execute-ddl-task.md)<br /><br /> [Analysis Services 処理タスク](../integration-services/control-flow/analysis-services-processing-task.md)<br /><br /> [Data Mining Query Task](../integration-services/control-flow/data-mining-query-task.md)<br /><br /> [データ マイニング モデル トレーニング変換先](../integration-services/data-flow/data-mining-model-training-destination.md)<br /><br /> [ディメンション処理変換先](../integration-services/data-flow/dimension-processing-destination.md)<br /><br /> [パーティション処理変換先](../integration-services/data-flow/partition-processing-destination.md)|  
|分析管理オブジェクト (Analysis Management Objects)||分析管理オブジェクト (AMO) は、管理操作を自動化するカスタム アプリケーションを開発するために、プログラマが使用できる管理インターフェイスです。 AMO を使用して、指定した XMLA、MDX または DMX スクリプトを実行するカスタム アプリケーションを開発することができます。|[AMO による管理タスクのプログラミング](https://docs.microsoft.com/bi-reference/amo/programming-administrative-tasks-with-amo)|  
  
## <a name="see-also"></a>関連項目  
 [Analysis Services スクリプト言語&#40;assl&#41;リファレンス](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [分析管理オブジェクト (AMO) による開発](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)   
 [多次元モデルオブジェクトの処理](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
