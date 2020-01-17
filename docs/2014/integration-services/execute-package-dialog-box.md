---
title: 実行パッケージ ダイアログ ボックス |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackageexecute.f1
- sql12.ssis.ssms.executepackage.f1
ms.assetid: 4f7a806d-4867-4d1f-bc65-b00c1caee7b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b4b920b17e960059e1212be7dd15c176c0b25a47
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059184"
---
# <a name="execute-package-dialog-box"></a>Execute Package Dialog Box
  **[パッケージの実行]** ダイアログ ボックスでは、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに格納されているパッケージを実行できます。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージには、値が環境変数に格納されているパラメーターが含まれている場合があります。 こうしたパッケージを実行するには、環境変数の値の提供に使用する環境を事前に指定する必要があります。 プロジェクトには複数の環境を含めることができますが、実行時に環境変数の値をバインドするのに使用できる環境は 1 つだけです。 パッケージで環境変数が使用されない場合、環境は不要です。  
  
 目的に合ったトピックをクリックしてください  
  
-   [[パッケージの実行] ダイアログ ボックスを開く](#open_dialog)  
  
-   [[全般] ページのオプションの設定](#general)  
  
-   [[パラメーター] タブのオプションの設定](#parameters)  
  
-   [[接続マネージャー] タブのオプションの設定](#connection)  
  
-   [[詳細設定] タブのオプションの設定](#advanced)  
  
-   [[パッケージの実行] ダイアログ ボックスのオプションのスクリプト作成](#script)  
  
##  <a name="open_dialog"></a> [パッケージの実行] ダイアログ ボックスを開く  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]から [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに接続します。  
  
     SSISDB データベースをホストする [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] のインスタンスに接続されます。  
  
2.  オブジェクト エクスプローラーで、ツリーを展開して、 **[Integration Services カタログ]** ノードを表示します。  
  
3.  **[SSISDB]** ノードを展開します。  
  
4.  実行するパッケージを含むフォルダーを展開します。  
  
5.  パッケージを右クリックし、 **[実行]** をクリックします。  
  
##  <a name="general"></a> [全般] ページのオプションの設定  
 **[環境]** を選択して、実行するパッケージに適用される環境を指定します。  
  
##  <a name="parameters"></a> [パラメーター] タブのオプションの設定  
 **[パラメーター]** タブを使用して、パッケージの実行時に使用するパラメーターの値を変更します。  
  
##  <a name="connection"></a> [接続マネージャー] タブのオプションの設定  
 [接続マネージャー] タブを使用して、パッケージの接続マネージャーのプロパティを設定します。  
  
##  <a name="advanced"></a> [詳細設定] タブのオプションの設定  
 [詳細設定] タブを使用して、プロパティとその他のパッケージの設定を管理します。  
  
 **[追加]** 、 **[編集]** 、 **[削除]**  
 クリックしてプロパティを追加、編集、または削除します。  
  
 **ログ記録レベル**  
 パッケージ実行のログ記録レベルを選択します。 詳細については、「[catalog.set_execution_parameter_value (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)」を参照してください。  
  
 **エラー時にダンプする**  
 パッケージの実行中にエラーが発生した場合にダンプ ファイルを作成するかどうかを指定します。 詳細については、「 [パッケージ実行用のダンプ ファイルを生成する](troubleshooting/generating-dump-files-for-package-execution.md)」を参照してください。  
  
 **32 ビット ランタイム**  
 パッケージが 32 ビット システムで実行されるように指定します。  
  
##  <a name="script"></a> [パッケージの実行] ダイアログ ボックスのオプションのスクリプト作成  
 **[パッケージの実行]** ダイアログ ボックスが表示されているときに、ツール バーの **[スクリプト]** を使用すると、 [!INCLUDE[tsql](../includes/tsql-md.md)] コードを生成することもできます。 生成されたスクリプトからは、 **[パッケージの実行]** ダイアログ ボックスで選択したのと同じオプションを指定したストアド プロシージャ [catalog.start_execution (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) が呼び出されます。 このスクリプトは、[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] の新しいスクリプト ウィンドウに表示されます。  
  
  
