---
title: WMI データ リーダー タスク エディター ([WMI オプション] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.wmidatareadertask.wmiquery.f1
helpviewer_keywords:
- WMI Data Reader Task Editor
ms.assetid: 4b8d4716-882d-41b0-b77e-e0e2741a2cd5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8367f0ae57df5333808e4dfde25c5676a3bcf1d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054358"
---
# <a name="wmi-data-reader-task-editor-wmi-options-page"></a>[WMI データ リーダー タスク エディター] ([WMI オプション] ページ)
  **[WMI データ リーダー タスク エディター]** ダイアログ ボックスの **[WMI オプション]** ページを使用すると、WQL (Windows Management Instrumentation Query Language) クエリのソースおよびクエリ結果の出力先を指定できます。  
  
 このタスクの詳細については、「 [WMI Data Reader Task](control-flow/wmi-data-reader-task.md)」を参照してください。 WQL (WMI Query Language) の詳細については、MSDN ライブラリにある Windows Management Instrumentation のトピック「 [WQL を使用したクエリ](https://go.microsoft.com/fwlink/?LinkId=79045)」を参照してください。  
  
## <a name="static-options"></a>静的オプション  
 **[WMIConnectionName]**  
 WMI 接続マネージャーを一覧から選択するか、[\<**新しい WMI 接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [WMI 接続マネージャー](connection-manager/wmi-connection-manager.md)、[WMI 接続マネージャー エディター](../../2014/integration-services/wmi-connection-manager-editor.md)  
  
 **[WQLQuerySourceType]**  
 タスクで実行する WQL クエリのソースの種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|説明|  
|-----------|-----------------|  
|**[直接入力]**|ソースを WQL クエリに設定します。 この値を選択すると、動的オプションの **[WQLQuerySourceType]** が表示されます。|  
|**[ファイル接続]**|WQL クエリを含むファイルを選択します。 この値を選択すると、動的オプションの **[WQLQuerySourceType]** が表示されます。|  
|**変数**|WQL クエリを定義する変数に、ソースを設定します。 この値を選択すると、動的オプションの **[WQLQuerySourceType]** が表示されます。|  
  
 **[OutputType]**  
 データ テーブル、プロパティ値、またはプロパティ名と値のいずれを出力に含めるかを指定します。  
  
 **[OverwriteDestination]**  
 出力先のファイルまたは変数内の元のデータを変更しないか、上書きするか、データを追加するかを指定します。  
  
 **[DestinationType]**  
 タスクで実行する WQL クエリの出力先の種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|説明|  
|-----------|-----------------|  
|**[ファイル接続]**|WQL クエリの結果を保存するファイルを選択します。 この値を選択すると、動的オプションの **[DestinationType]** が表示されます。|  
|**変数**|WQL クエリの結果を保存する変数を設定します。 この値を選択すると、動的オプションの **[DestinationType]** が表示されます。|  
  
## <a name="wqlquerysourcetype-dynamic-options"></a>[WQLQuerySourceType] 動的オプション  
  
### <a name="wqlquerysourcetype--direct-input"></a>[WQLQuerySourceType] = [直接入力]  
 **[WQLQuerySource]**  
 クエリを指定します。または、参照 ( [...] ) をクリックし、 **[WQL クエリ]** ダイアログ ボックスを使用してクエリを入力します。  
  
### <a name="wqlquerysourcetype--file-connection"></a>[WQLQuerySourceType] = [ファイル接続]  
 **[WQLQuerySource]**  
 ファイル接続マネージャーを一覧から選択するか、\< **[新しい接続...]** をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="wqlquerysourcetype--variable"></a>[WQLQuerySourceType] = [変数]  
 **[WQLQuerySource]**  
 一覧で変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)、[変数の追加](../../2014/integration-services/add-variable.md)  
  
## <a name="destinationtype-dynamic-options"></a>[DestinationType] 動的オプション  
  
### <a name="destinationtype--file-connection"></a>[DestinationType] = [ファイル接続]  
 **変換先**  
 ファイル接続マネージャーを一覧から選択するか、\< **[新しい接続...]** をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="destinationtype--variable"></a>[DestinationType] = [変数]  
 **変換先**  
 一覧で変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)、[変数の追加](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>関連項目  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [WMI データ リーダー タスク エディター ([全般] ページ)](general-page-of-integration-services-designers-options.md)   
 [[式] ページ](expressions/expressions-page.md)   
 [WMI イベント監視タスク](control-flow/wmi-event-watcher-task.md)  
  
  
