---
title: SSIS デザイナー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services, SSIS Designer
- Business Intelligence Development Studio, Integration Services in
- tools [Integration Services], SSIS Designer
- SSIS, SSIS Designer
- SSIS Designer, about SSIS Designer
- Integration Services, SSIS Designer
ms.assetid: 006d68ea-1b5c-4c1e-8079-3910288e012c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ea0776247555b9a5b63e2bbaa9ae9243abf6863c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62766432"
---
# <a name="ssis-designer"></a>SSIS デザイナー
  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーは、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージの作成および管理に使用できるグラフィカル ツールです。 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーは、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] で [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトの一部として使用できます。  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーを使用すると、次のタスクを実行できます。  
  
-   パッケージ内に制御フローを構築します。  
  
-   パッケージ内にデータ フローを構築します。  
  
-   パッケージおよびパッケージ オブジェクトにイベント ハンドラーを追加します。  
  
-   パッケージの内容を表示します。  
  
-   実行時に、パッケージの実行の進行状況を表示します。  
  
 次の図は、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーと **[ツールボックス]** ウィンドウを示しています。  
  
 ![SSIS デザイナーとツールボックスのスクリーンショット](media/denali-designerandtoolbox.gif "SSIS デザイナーとツールボックスのスクリーンショット")  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、さらに、パッケージに機能を追加するダイアログ ボックスとウィンドウが含まれており、 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] では、開発環境を構成しパッケージを使用するためのウィンドウとダイアログ ボックスが用意されています。 詳細については、「 [Integration Services のユーザー インターフェイス](integration-services-user-interface.md)」を参照してください。  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーは、パッケージを管理および監視する [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サービスに対して依存関係はなく、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでパッケージを作成または変更するために、このサービスを実行する必要はありません。 ただし、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーが開いている間にサービスを停止すると、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで提供されるダイアログ ボックスを開くことができなくなり、"RPC サーバーを利用できません。" というエラー メッセージが返されます。 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーをリセットして引き続きパッケージを処理するには、デザイナーを閉じて [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]を終了し、次に [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクト、およびパッケージを再度開く必要があります。  
  
## <a name="undo-and-redo"></a>元に戻す、やり直す  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーでの操作は、最大 20 件まで元に戻したり、やり直したりすることができます。 パッケージの場合、元に戻す/やり直すを使用できるのは、 **[制御フロー]** タブ、 **[データ フロー]** タブ、 **[イベント ハンドラー]** タブ、 **[パラメーター]** タブと、 **[変数]** ウィンドウです。 プロジェクトの場合、元に戻す/やり直すは **[プロジェクト パラメーター]** ウィンドウで使用できます。  
  
 **新しい SSIS ツールボックス**に対する変更を元に戻す/やり直すことはできません。  
  
 コンポーネント エディターを使用してコンポーネントを変更した場合、元に戻す/やり直す操作は個別の変更ではなく一連の変更に対して適用されます。 元に戻す/やり直す操作のドロップダウン リストでは、一連の変更が単一の操作として表示されます。  
  
 操作を元に戻すには、元に戻すツール バー ボタンまたは **[編集]/[元に戻す]** メニュー項目をクリックするか、または Ctrl キーを押しながら Z キーを押します。 操作をやり直すには、やり直しツール バー ボタンまたは **[編集]/[やり直し]** メニュー項目をクリックするか、または Ctrl キーを押しながら Y キーを押します。複数の操作を元に戻したり、やり直したりするには、ツール バー ボタンの横にある矢印をクリックし、ドロップダウン リストで複数の操作を強調表示にして、リストをクリックします。  
  
## <a name="parts-of-the-ssis-designer"></a>SSIS デザイナーの構成要素  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーには、パッケージ制御フロー、データ フロー、パラメーター、およびイベント ハンドラーを構築するタブが 1 つずつ、パッケージの内容を表示するタブが 1 つ、計 5 つのタブが常に表示されています。 実行時には、6 番目のタブが表示され、実行中のパッケージの進行状況と実行完了後の実行結果を表示します。  
  
 また、 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーには、パッケージがデータに接続するために使用する接続マネージャーを追加および構成する、[接続マネージャー] 領域が含まれています。  
  
### <a name="control-flow-tab"></a>[制御フロー] タブ  
 パッケージ内に制御フローを構築するには、 **[制御フロー]** タブのデザイン画面を使用します。アイテムを **[ツールボックス]** からデザイン画面にドラッグし、アイテムのアイコンをクリックして、矢印を別のアイテムにドラッグすると、アイテムが制御フローに連結されます。  
  
 詳細については、「 [Control Flow](control-flow/control-flow.md)」を参照してください。  
  
### <a name="data-flow-tab"></a>[データ フロー] タブ  
 パッケージ内にデータ フロー タスクが含まれている場合、データ フローをパッケージに追加できます。 パッケージ内にデータ フローを構築するには、 **[データ フロー]** タブのデザイン画面を使用します。アイテムを **[ツールボックス]** からデザイン画面にドラッグし、アイテムのアイコンをクリックして、矢印を別のアイテムにドラッグすると、アイテムがデータ フローに連結されます。  
  
 詳細については、「 [Data Flow](data-flow/data-flow.md)」を参照してください。  
  
### <a name="parameters-tab"></a>[パラメーター] タブ  
 Integration Services (SSIS) パラメーターを使用すると、パッケージの実行時にパッケージ内のプロパティに値を割り当てることができます。 プロジェクト パラメーターはプロジェクト レベル、パッケージ パラメーターはパッケージ レベルで作成できます。 プロジェクト パラメーターは、プロジェクトが受け取る外部入力をプロジェクト内の 1 つまたは複数のパッケージに指定するために使用します。 パッケージ パラメーターを使用すると、パッケージを編集したり再配置したりせずにパッケージ実行を変更できます。 このタブでは、パッケージ パラメーターを管理できます。  
  
 パラメーターの詳細については、「[Integration Services (SSIS) パラメーター](integration-services-ssis-package-and-project-parameters.md)」を参照してください。  
  
> [!IMPORTANT]  
>  パラメーターを使用できるのは、プロジェクトの配置モデル用に開発したプロジェクトに対してのみです。 したがって、プロジェクト配置モデルを使用するように構成されているプロジェクトの一部であるパッケージに対してのみ、[パラメーター] タブが表示されます。  
  
### <a name="event-handlers-tab"></a>[イベント ハンドラー] タブ  
 パッケージ内にイベントを構築するには、 **[イベント ハンドラー]** タブのデザイン画面を使用します。 **[イベント ハンドラー]** タブで、イベント ハンドラーを作成するパッケージまたはパッケージ オブジェクトを選択し、次にイベント ハンドラーに関連付けるイベントを選択します。 イベント ハンドラーには制御フローと、オプションでデータ フローが含まれます。  
  
 詳細については、「 [Add an Event Handler to a Package](../../2014/integration-services/add-an-event-handler-to-a-package.md)」を参照してください。  
  
### <a name="package-explorer-tab"></a>[パッケージ エクスプローラー] タブ  
 パッケージは、タスク、接続マネージャー、変数、その他の要素が多数含まれていて複雑な場合があります。 パッケージをエクスプローラー ビューで表示すると、パッケージ要素の全一覧を確認できます。  
  
 詳細については、「[パッケージ オブジェクトを表示する](view-package-objects.md)」を参照してください。  
  
#### <a name="progressexecution-result-tab"></a>[進行状況] タブと [実行結果] タブ  
 パッケージの実行中は、 **[進行状況]** タブにパッケージの実行の進行状況が表示されます。 パッケージの実行が完了すると、 **[実行結果]** タブに実行結果が表示され、そのまま使用できます。  
  
> [!NOTE]  
>  **[進行状況]** タブでのメッセージの表示を有効または無効にするには、 **[SSIS]** メニューの **[進行状況レポートのデバッグ]** オプションを切り替えます。  
  
##### <a name="connection-managers-area"></a>[接続マネージャー] 領域  
 パッケージで使用する接続マネージャーを追加および変更するには、 **[接続マネージャー]** 領域を使用します。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、テキスト ファイル、OLE DB データベース、.NET プロバイダーなど、さまざまなデータ ソースに接続するための接続マネージャーがあります。  
  
 詳細については、「[Integration Services (SSIS) の接続](connection-manager/integration-services-ssis-connections.md)」および「[接続マネージャーを作成する](../../2014/integration-services/create-connection-managers.md)」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [SQL Server データ ツールでのパッケージの作成](create-packages-in-sql-server-data-tools.md)  
  
## <a name="see-also"></a>参照  
 [Integration Services のユーザー インターフェイス](integration-services-user-interface.md)  
  
  
