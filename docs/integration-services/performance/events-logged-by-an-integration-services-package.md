---
title: Integration Services パッケージによってログに記録されるイベント | Microsoft Docs
ms.custom: supportability
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- package [Integration Services], events
- events [Integration Services], package
ms.assetid: 55a0951a-46f3-4f0f-9972-74cec9cc26b7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4ed4722261ca83d95345c8d8fc5024f1076be839
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71282507"
---
# <a name="events-logged-by-an-integration-services-package"></a>Integration Services パッケージによってログに記録されるイベント

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、各種のイベント メッセージを Windows アプリケーション イベント ログに記録します。 これらのメッセージは、パッケージの起動時、パッケージの停止時、および特定の問題の発生時にログに記録されます。  
  
 このトピックでは、アプリケーション イベント ログに記録される一般的なイベント メッセージについて説明します。 既定では、パッケージのログ記録が有効になっていない場合でも、一部のメッセージはログに記録されます。 それ以外のメッセージは、パッケージのログ記録が有効になっている場合にのみログに記録されます。 既定でログに記録されたか、ログ記録を有効にしたことによってログに記録されたかに関係なく、これらのメッセージのイベント ソースは SQLISPackage になります。  
  
 SSIS パッケージの実行方法に関する一般的な情報については、「[プロジェクトとパッケージの実行](../packages/run-integration-services-ssis-packages.md)」をご覧ください。  
  
 パッケージの実行に関するトラブルシューティング方法については、「 [パッケージ実行のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)」をご覧ください。  
  
## <a name="messages-about-the-status-of-the-package"></a>パッケージの状態に関するメッセージ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを実行すると、通常、そのパッケージの進行状況と状態に関するさまざまなメッセージがログに記録されます。 次の表に、そのメッセージの一覧を示します。  
  
> [!NOTE]  
>  パッケージのログ記録が有効になっていない場合でも、次の表に示すメッセージはログに記録されます。  
  
|イベント ID|シンボル名|Text|注|  
|--------------|-------------------|----------|-----------|  
|12288|DTS_MSG_PACKAGESTART|パッケージ "" が起動されました。|パッケージの実行が開始されました。|  
|12289|DTS_MSG_PACKAGESUCCESS|パッケージ "" が正常に完了しました。|パッケージが正常に実行され、現在は実行されていません。|  
|12290|DTS_MSG_PACKAGECANCEL|パッケージ "%1!s!" は取り消されました。|パッケージが取り消されたため、現在は実行されていません。|  
|12291|DTS_MSG_PACKAGEFAILURE|パッケージ "" は失敗しました。|パッケージは正常に実行できずに、実行を停止しました。|  
  
 既定では、新規インストールで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] はパッケージの実行に関連する特定のイベントをアプリケーション イベント ログに記録しないように構成されます。 現在のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のデータ コレクター機能を使用すると、この設定により、大量のイベント ログ エントリは生成されません。 ログに記録されないイベントは、EventID 12288 の "パッケージが起動されました。" や EventID 12289 の "パッケージが正常に完了しました。" です。 これらのイベントをアプリケーション イベント ログに記録するには、レジストリを編集用に開きます。 次に、レジストリ内で HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS ノードを見つけ、LogPackageExecutionToEventLog 設定の DWORD 値を 0 から 1 に変更します。 ただし、アップグレード インストールでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] はこれらの 2 つのイベントをログに記録するように構成されます。 ログを無効にするには、LogPackageExecutionToEventLog 設定の値を 1 から 0 に変更します。  
  
## <a name="messages-associated-with-package-logging"></a>パッケージのログ記録に関連付けられているメッセージ  
 パッケージのログ記録が有効になっている場合、アプリケーション イベント ログは、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのオプションのログ記録機能によってサポートされる記録先の 1 つです。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
 パッケージのログ記録が有効になっていて、ログの場所がアプリケーション イベント ログである場合は、次の情報に関連するエントリがログに記録されます。  
  
-   実行中のパッケージの段階に関するメッセージ  
  
-   パッケージの実行中に発生する特定のイベントに関するメッセージ  
  
### <a name="messages-about-the-stages-of-package-execution"></a>パッケージ実行の段階に関するメッセージ  
  
|イベント ID|シンボル名|Text|注|  
|--------------|-------------------|----------|-----------|  
|12544|DTS_MSG_EVENTLOGENTRY|イベント名: %1%r メッセージ: %9%r 演算子: %2%r ソース名: %3%r ソース ID: %4%r 実行 ID: %5%r 開始時刻: %6%r 終了時刻: %7%r データ コード: %8|アプリケーション イベント ログへのログ記録を構成すると、さまざまなメッセージがこの一般的な形式で記録されます。|  
|12556|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|イベント名: %1%r メッセージ: %9%r 演算子: %2%r ソース名: %3%r ソース ID: %4%r 実行 ID: %5%r 開始時刻: %6%r 終了時刻: %7%r データ コード: %8|パッケージが開始されました。|  
|12547|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|イベント名: %1%r メッセージ: %9%r 演算子: %2%r ソース名: %3%r ソース ID: %4%r 実行 ID: %5%r 開始時刻: %6%r 終了時刻: %7%r データ コード: %8|オブジェクトの検証が開始されようとしています。|  
|12548|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|イベント名: %1%r メッセージ: %9%r 演算子: %2%r ソース名: %3%r ソース ID: %4%r 実行 ID: %5%r 開始時刻: %6%r 終了時刻: %7%r データ コード: %8|オブジェクトの検証が完了しました。|  
|12552|DTS_MSG_EVENTLOGENTRY_PROGRESS|イベント名: %1%r メッセージ: %9%r 演算子: %2%r ソース名: %3%r ソース ID: %4%r 実行 ID: %5%r 開始時刻: %6%r 終了時刻: %7%r データ コード: %8|この汎用メッセージはパッケージの進行状況を報告します。|  
|12546|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|イベント名: %1%r メッセージ: %9%r 演算子: %2%r ソース名: %3%r ソース ID: %4%r 実行 ID: %5%r 開始時刻: %6%r 終了時刻: %7%r データ コード: %8|オブジェクトの処理が完了しました。|  
|12557|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|イベント名: %1%r メッセージ: %9%r 演算子: %2%r ソース名: %3%r ソース ID: %4%r 実行 ID: %5%r 開始時刻: %6%r 終了時刻: %7%r データ コード: %8|パッケージの実行が完了しました。|  
  
### <a name="messages-about-events-that-occur"></a>発生したイベントに関するメッセージ  
 次の表に、イベントの結果として出力されるメッセージの一部を示します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で使用されるエラー メッセージ、警告メッセージ、および情報メッセージの詳細な一覧については、「 [Integration Services のエラーおよびメッセージのリファレンス](../../integration-services/integration-services-error-and-message-reference.md)」をご覧ください。  
  
|イベント ID|シンボル名|Text|注|  
|--------------|-------------------|----------|-----------|  
|12251|DTS_MSG_EVENTLOGENTRY_TASKFAILED|イベント名: %1%r メッセージ: %9%r 演算子: %2%r ソース名: %3%r ソース ID: %4%r 実行 ID: %5%r 開始時刻: %6%r 終了時刻: %7%r データ コード: %8|タスクは失敗しました。|  
|12250|DTS_MSG_EVENTLOGENTRY_ERROR|イベント名: %1%r メッセージ: %9%r 演算子: %2%r ソース名: %3%r ソース ID: %4%r 実行 ID: %5%r 開始時刻: %6%r 終了時刻: %7%r データ コード: %8|このメッセージは発生したエラーを報告します。|  
|12249|DTS_MSG_EVENTLOGENTRY_WARNING|イベント名: %1%r メッセージ: %9%r 演算子: %2%r ソース名: %3%r ソース ID: %4%r 実行 ID: %5%r 開始時刻: %6%r 終了時刻: %7%r データ コード: %8|このメッセージは発生した警告を報告します。|  
|12258|DTS_MSG_EVENTLOGENTRY_INFORMATION|イベント名: %1%r メッセージ: %9%r 演算子: %2%r ソース名: %3%r ソース ID: %4%r 実行 ID: %5%r 開始時刻: %6%r 終了時刻: %7%r データ コード: %8|このメッセージは、エラーまたは警告に関連しない情報メッセージです。|  

## <a name="view-log-entries-in-the-log-events-window"></a>[ログ イベント] ウィンドウでログ エントリを表示する
  この手順では、パッケージを実行して、パッケージが書き込むログ エントリを表示する方法について説明します。 ログ エントリはリアルタイムで表示できます。 **[ログ イベント]** ウィンドウに書き込まれたログ エントリは、さらに詳しく分析するためにコピーして保存することもできます。  
  
 **[ログ イベント]** ウィンドウにエントリを書き込むために、ログ エントリをログに書き込む必要はありません。  
  
### <a name="to-view-log-entries"></a>ログ エントリを表示するには  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  **[SSIS]** メニューの **[ログ イベント]** をクリックします。 必要に応じて、View.LogEvents コマンドを **[オプション]** ダイアログ ボックスの **[キーボード]** ページで選択したキーの組み合わせにマップすることによって、 **[ログ イベント]** ウィンドウを表示することもできます。  
  
3.  **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。  
  
     実行時に、ログ記録可能なイベントやカスタム メッセージが見つかると、各イベントまたはメッセージのログ エントリが **[ログ イベント]** ウィンドウに書き込まれます。  
  
4.  **[デバッグ]** メニューの **[デバッグの停止]** をクリックします。  
  
     **[ログ イベント]** ウィンドウのログ エントリは、パッケージを再実行するか、別のパッケージを実行するか、または [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]を終了するまでは、そのまま使用できます。  
  
5.  **[ログ イベント]** ウィンドウで、ログ エントリを表示します。  
  
6.  必要に応じて、コピーするログ エントリを右クリックして **[コピー]** をクリックします。  
  
7.  必要に応じて、ログ エントリをダブルクリックし、 **[ログ エントリ]** ダイアログ ボックスで、1 つのログ エントリの詳細を表示します。  
  
8.  **[ログ エントリ]** ダイアログ ボックスで、上矢印および下矢印をクリックして前後のログ エントリを表示し、コピー アイコンをクリックしてログ エントリをコピーします。  
  
9. テキスト エディターを開いて貼り付けた後、ログ エントリをテキスト ファイルに保存します。
