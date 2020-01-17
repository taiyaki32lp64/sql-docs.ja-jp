---
title: イベント ハンドラーをパッケージに追加します |。Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- event handlers [Integration Services], creating
ms.assetid: 5e56885d-8658-480a-bed9-3f2f8003fd78
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 589d90b52647241b22929473efc9c6e54eb3b75f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062026"
---
# <a name="add-an-event-handler-to-a-package"></a>パッケージにイベント ハンドラーを追加する
  コンテナーとタスクは実行時にイベントを発生させます。 こうしたイベントが発生したときにワークフローを実行して、イベントに応答するカスタム イベント ハンドラーを作成できます。 たとえば、タスクが失敗したときに電子メール メッセージを送信するイベント ハンドラーを作成できます。  
  
 イベント ハンドラーは、パッケージと同様です。 イベント ハンドラーでは、パッケージと同様に変数のスコープが用意され、制御フローとオプションのデータ フローが含まれています。 パッケージ、Foreach ループ コンテナー、For ループ コンテナー、シーケンス コンテナー、およびすべてのタスクに対してイベント ハンドラーを作成できます。  
  
 イベント ハンドラーを作成するには、 **デザイナーにある** [イベント ハンドラー] [!INCLUDE[ssIS](../includes/ssis-md.md)] タブのデザイン画面を使用します。  
  
 **[イベント ハンドラー]** タブがアクティブな場合、 **デザイナーにあるツールボックスの** [制御フロー項目] **および** [メンテナンス プランのタスク] [!INCLUDE[ssIS](../includes/ssis-md.md)] ノードには、イベント ハンドラーで制御フローを作成するためのタスクとコンテナーが含まれます。 **[データ フローの変換元]** 、 **[変換]** 、および **[データ フローの変換先]** ノードには、イベント ハンドラーでデータ フローを作成するためのデータ ソース、変換、および変換先が含まれます。 詳細については、「 [制御フロー](control-flow/control-flow.md) 」と「 [データ フロー](data-flow/data-flow.md)」を参照してください。  
  
 **[イベント ハンドラー]** タブには、 **[接続マネージャー]** 領域も含まれ、イベント ハンドラーがサーバーおよびデータ ソースに接続するために使用する、接続マネージャーの作成および変更を行うことができます。 詳細については、「 [接続マネージャーを作成する](../../2014/integration-services/create-connection-managers.md)」を参照してください。  
  
### <a name="to-create-an-event-handler"></a>イベント ハンドラーを作成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[イベント ハンドラー]** タブをクリックします。  
  
     ![イベント ハンドラーが表示されたデザイン画面のスクリーンショット](media/eventhandlers.gif "イベント ハンドラーが表示されたデザイン画面のスクリーンショット")  
  
     イベント ハンドラー内で制御フローとデータ フローを作成する手順は、パッケージ内で制御フローとデータ フローを作成する手順と同様です。 詳細については、「 [制御フロー](control-flow/control-flow.md) 」と「 [データ フロー](data-flow/data-flow.md)」を参照してください。  
  
4.  **[実行可能ファイル]** の一覧から、イベント ハンドラーを作成する実行可能ファイルを選択します。  
  
5.  **[イベント ハンドラー]** の一覧から、作成するイベント ハンドラーを選択します。  
  
6.  **[イベント ハンドラー]** タブのデザイン画面のリンクをクリックします。  
  
7.  制御フロー アイテムをイベント ハンドラーに追加し、優先順位制約を使用してアイテムを接続します。これは、制御フロー アイテムから別の制御フロー アイテムに制約をドラッグして行います。 詳細については、「 [Control Flow](control-flow/control-flow.md)」を参照してください。  
  
8.  必要に応じてデータ フロー タスクを追加し、 **[データ フロー]** タブのデザイン画面で、イベント ハンドラーのデータ フローを作成します。 詳細については、「 [Data Flow](data-flow/data-flow.md)」を参照してください。  
  
9. **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックし、新しいパッケージを保存します。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Integration Services](../../2014/integration-services/sql-server-integration-services.md)   
 [Integration Services &#40;SSIS&#41; のログ記録](performance/integration-services-ssis-logging.md)  
  
  
