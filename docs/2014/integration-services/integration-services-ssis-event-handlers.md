---
title: Integration Services (SSIS) のイベント ハンドラー | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, events
- run-time [Integration Services]
- SQL Server Integration Services packages, events
- event handlers [Integration Services], about event handlers
- events [Integration Services]
- packages [Integration Services], events
- event handlers [Integration Services]
- SSIS packages, events
- containers [Integration Services], events
- events [Integration Services], about events
ms.assetid: 6f60cf93-35dc-431c-908d-2049c4ab66ba
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 54702cd96ba9327fe8bba8e4c82275dbdaef1bf8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62767728"
---
# <a name="integration-services-ssis-event-handlers"></a>Integration Services (SSIS) のイベント ハンドラー
  実行可能ファイル (パッケージ、Foreach ループ コンテナー、For ループ コンテナー、シーケンス コンテナー、およびタスク ホスト コンテナー) は実行時にイベントを発生させます。 たとえば、エラーが発生すると、OnError イベントが発生します。 これらのイベントに対してカスタム イベント ハンドラーを作成し、パッケージ機能を拡張すると、実行時のパッケージを容易に管理できます。 イベント ハンドラーは、次のタスクを実行できます。  
  
-   パッケージまたはタスクの実行が完了したとき、一時データ ストレージをクリーンアップします。  
  
-   システム情報を取得して、パッケージを実行する前にリソースの可用性を評価します。  
  
-   参照テーブル内の参照が失敗したとき、テーブル内のデータを更新します。  
  
-   エラーまたは警告が発生したとき、またはタスクが失敗したときに、電子メール メッセージを送信します。  
  
 イベントにイベント ハンドラーがない場合、パッケージのコンテナー階層で上位にあたる次のコンテナーでイベントが発生します。 このコンテナーにイベント ハンドラーがある場合、イベントに応答してイベント ハンドラーが実行されます。 イベント ハンドラーがない場合、コンテナー階層で上位にあたる次のコンテナーでイベントが発生します。  
  
 次の図は、1 つの SQL 実行タスクを含む For ループ コンテナーを持つ、簡単なパッケージを示しています。  
  
 ![パッケージ、For ループ、タスク ホスト、および SQL 実行タスク](media/mw-dts-eventhandlerpkg.gif "パッケージ、For ループ、タスク ホスト、および SQL 実行タスク")  
  
 `OnError` イベントに対するイベント ハンドラーを持つのは、パッケージのみです。 SQL 実行タスクの実行時にエラーが発生した場合、パッケージの `OnError` イベント ハンドラーが実行されます。 次の図は、パッケージの `OnError` イベント ハンドラーにより実行される呼び出しの順序を示しています。  
  
 ![イベント ハンドラーのフロー](media/mw-dts-eventhandlers.gif "イベント ハンドラーのフロー")  
  
 イベント ハンドラーは、イベント ハンドラー コレクションのメンバーであり、このコレクションはすべてのコンテナーに含まれています。 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーを使用してパッケージを作成すると、イベント ハンドラー コレクションのメンバーは、 **デザイナーの** [パッケージ エクスプローラー] **タブ上の** [イベント ハンドラー] [!INCLUDE[ssIS](../includes/ssis-md.md)] フォルダー内に表示されます。  
  
 イベント ハンドラーのコンテナーは、次の方法で構成できます。  
  
-   イベント ハンドラーの名前と説明を指定します。  
  
-   イベント ハンドラーを実行するかどうか、イベント ハンドラーが失敗した場合にパッケージが失敗するかどうか、イベント ハンドラーが失敗するまでに発生するエラーの最大数を示します。  
  
-   実行時にイベント ハンドラーが返す実際の実行結果の代わりに、返される実行結果を指定します。  
  
-   イベント ハンドラーのトランザクション オプションを指定します。  
  
-   イベント ハンドラーが使用するログ モードを指定します。  
  
## <a name="event-handler-content"></a>イベント ハンドラーの内容  
 イベント ハンドラーの作成方法は、パッケージの構築方法と同様です。つまり、イベント ハンドラーには、制御フロー内で順序付けられたタスクとコンテナーがあります。また、イベント ハンドラーにデータ フローを含めることもできます。 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーには **[イベント ハンドラー]** タブが含まれており、これを使用してカスタム イベント ハンドラーを作成します。 詳細については、次を参照してください。 [SSIS パッケージのイベント ハンドラー](integration-services-ssis-event-handlers.md)します。  
  
 イベント ハンドラーは、プログラムによって作成することもできます。 詳細については、「 [プログラムによるイベントの処理](building-packages-programmatically/handling-events-programmatically.md)」を参照してください。  
  
## <a name="run-time-events"></a>実行時イベント  
 次の表に、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] で用意されているイベント ハンドラーの一覧を示します。また、イベント ハンドラーによって実行される実行時イベントについて説明します。  
  
|イベント ハンドラー|イベント|  
|-------------------|-----------|  
|`OnError`|イベント ハンドラー、`OnError`イベント。 このイベントは、エラー発生時に実行可能ファイルから発生します。|  
|**OnExecStatusChanged**|**OnExecStatusChanged** イベントのイベント ハンドラーです。 このイベントは、実行状態が変化したときに実行可能ファイルから発生します。|  
|**OnInformation**|**OnInformation** イベントのイベント ハンドラーです。 このイベントは、実行可能ファイルの検証時および実行時に、情報をレポートするために発生します。 このイベントは情報を伝達するだけのもので、エラーや警告は発生しません。|  
|**OnPostExecute**|**OnPostExecute** イベントのイベント ハンドラーです。 このイベントは、実行可能ファイルの実行完了直後に、実行可能ファイルから発生します。|  
|**OnPostValidate**|**OnPostValidate** イベントのイベント ハンドラーです。 このイベントは、実行可能ファイルの検証が完了したときに、実行可能ファイルから発生します。|  
|**OnPreExecute**|**OnPreExecute** イベントのイベント ハンドラーです。 このイベントは、実行可能ファイルが実行される直前に、実行可能ファイルから発生します。|  
|**OnPreValidate**|**OnPreValidate** イベントのイベント ハンドラーです。 このイベントは、実行可能ファイルの検証を開始するときに、実行可能ファイルから発生します。|  
|**OnProgress**|**OnProgress** イベントのイベント ハンドラーです。 このイベントは、実行可能ファイルで重要な進行があったときに、実行可能ファイルから発生します。|  
|**OnQueryCancel**|**OnQueryCancel** イベントのイベント ハンドラーです。 このイベントは、実行可能ファイルの実行を停止するかどうかを決定するために、実行可能ファイルから発生します。|  
|**OnTaskFailed**|**OnTaskFailed** イベントのイベント ハンドラーです。 このイベントは、タスクが失敗したときにタスクから発生します。|  
|**OnVariableValueChanged**|**OnVariableValueChanged** イベントのイベント ハンドラーです。 このイベントは、変数の値が変化したときに実行可能ファイルから発生します。 イベントは、変数が定義されている実行可能ファイルで発生します。 設定した場合、このイベントは発生しませんが、 **RaiseChangeEvent**プロパティに変数を`False`します。 詳細については、「 [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)」を参照してください。|  
|**OnWarning**|**OnWarning** イベントのイベント ハンドラーです。 このイベントは、警告の発生時に実行可能ファイルから発生します。|  
  
## <a name="configuration-of-an-event-handler"></a>イベント ハンドラーの構成  
 プロパティは、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] の **[プロパティ]** ウィンドウで設定することも、プログラムで設定することもできます。  
  
 これらのプロパティを [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で設定する方法については、「 [タスクまたはコンテナーのプロパティを設定する](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)」を参照してください。  
  
 これらのプロパティのプログラムでの設定については、「 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 パッケージにイベント ハンドラーを追加する方法については、「[パッケージにイベント ハンドラーを追加する](../../2014/integration-services/add-an-event-handler-to-a-package.md)」を参照してください。  
  
  
