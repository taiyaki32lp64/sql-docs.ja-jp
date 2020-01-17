---
title: メッセージ キュー タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.messagequeuetask.f1
helpviewer_keywords:
- Message Queue task [Integration Services]
- receiving messages
- messages [Integration Services]
- sending messages
ms.assetid: ae1d8fad-6649-4e93-b589-14a32d07da33
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e7857294534f1c3c434f43c302cee8864925d953
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62831479"
---
# <a name="message-queue-task"></a>Message Queue Task
  メッセージ キュー タスクでは、Message Queuing (MSMQ) を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ間でメッセージを送受信したり、カスタム アプリケーションによって処理されるアプリケーションのキューにメッセージを送信したりすることができます。 これらのメッセージは、簡単なテキスト形式、ファイル、変数、またはそれらの値です。  
  
 メッセージ キュー タスクを使用することにより、企業の組織全体の操作を調整できます。 送信先が使用できない場合やビジーの場合、メッセージをキューに入れ、後で配信できます。たとえば、送信先が販売担当者のオフラインのラップトップ コンピューターの場合、キューにメッセージが入れられ、販売担当者はネットワークに接続したときに受信できます。 メッセージ キュー タスクは、次の目的で使用できます。  
  
-   他のパッケージがチェックインするまでタスクの実行を遅らせることができます。 たとえば、各小売り店舗で夜間のメンテナンスが終了した後、メッセージ キュー タスクは本社のコンピューターにメッセージを送信します。 この本社のコンピューターで実行するパッケージには複数のメッセージ キュー タスクが含まれており、それぞれが個々の店舗からのメッセージを待機しています。 メッセージが店舗から到着すると、タスクは店舗のデータをアップロードします。 すべての店舗がチェックインしたら、パッケージは合計を集計します。  
  
-   データ ファイルを処理するコンピューターに、データ ファイルを送信できます。 たとえば、レストランの会計レジの出力をデータ ファイル メッセージとして給与計算システムに送信して、ウェイターのチップに関するデータを抽出できます。  
  
-   企業の組織全体にファイルを配信できます。 たとえば、あるパッケージでメッセージ キュー タスクを使用して、別のコンピューターにパッケージ ファイルを送信できます。 送信先のコンピューターで実行するパッケージは、メッセージ キュー タスクを使用してパッケージをローカルに取得し保存します。  
  
 メッセージ キュー タスクは、メッセージの送受信時に、"データ ファイル"、"文字列"、"文字列メッセージを変数に指定"、"変数" の 4 つのうちのいずれかのメッセージ型を使用します。 "文字列メッセージを変数に指定" メッセージ型は、メッセージの受信時にのみ使用できます。  
  
 タスクは MSMQ 接続マネージャーを使用して、メッセージ キューに接続します。 詳細については、「 [MSMQ 接続マネージャー](../connection-manager/msmq-connection-manager.md)」を参照してください。 メッセージ キューの詳細については、 [MSDN ライブラリ](https://go.microsoft.com/fwlink/?LinkId=7022)を参照してください。  
  
 メッセージ キュー タスクには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスのインストールが必要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードの **[インストールするコンポーネント]** ページまたは **[機能の選択]** ページでインストールの選択をした [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントによっては、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントのサブセットの一部がインストールされます。 これらのコンポーネントを使用して一部のタスクを実行することは可能ですが、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のすべての機能は使用できません。 たとえば、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] のオプションでは、パッケージをデザインするために必要な [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントがインストールされますが、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスはインストールされません。したがって、メッセージ キュー タスクは機能しません。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]を完全にインストールするには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] [インストールするコンポーネント] **ページで** を選択する必要があります。 メッセージ キュー タスクのインストールと実行の詳細については、「 [Integration Services のインストール](../install-windows/install-integration-services.md)」を参照してください。  
  
> [!NOTE]  
>  コンピューターのオペレーティング システムが FIPS モードで構成され、タスクで暗号化が使用されている場合は、メッセージ キュー タスクは Federal Information Processing Standard (FIPS) 140-2 に準拠することができません。 メッセージ キュー タスクで暗号化が使用されていない場合は、タスクを正常に実行することができます。  
  
## <a name="message-types"></a>メッセージ型  
 メッセージ キュー タスクで用意されているメッセージ型は、次の方法で構成できます。  
  
-   "`Data file`" メッセージは、ファイルにメッセージが含まれることを指定します。 メッセージを受信するときに、タスクによってファイルを保存したり既存のファイルを上書きできるように、また、タスクによってメッセージを受信できるパッケージを指定するように、タスクを構成できます。  
  
-   "`String`" メッセージは、メッセージを文字列として指定します。 メッセージを受信するときに、タスクが受信した文字列とユーザー定義の文字列とを比較したり、比較に基づいて処理を実行するように構成できます。 文字列比較では、完全な比較、大文字と小文字を区別する比較、大文字と小文字を区別しない比較、またはサブストリングを使用した比較を設定できます。  
  
-   "`String message to variable`" では、基になるメッセージを、送信先の変数に送信される文字列として指定できます。 完全な比較、大文字と小文字を区別しない比較、またはサブストリングの比較を使用して、受信した文字列とユーザー定義の文字列とを比較するようにタスクを構成できます。 このメッセージ型は、タスクがメッセージを受信するときにのみ使用できます。  
  
-   "`Variable`" メッセージは、メッセージが 1 つ以上の変数を含むことを指定します。 タスクは、メッセージに含まれる変数の名前を指定するように構成できます。 メッセージを受信するときに、メッセージを受信するパッケージおよびメッセージの送信先となる変数の両方を指定するようにタスクを構成できます。  
  
## <a name="sending-messages"></a>sending messages  
 メッセージ キュー タスクを構成してメッセージを送信する場合、メッセージ キュー テクノロジで現在サポートされている暗号化アルゴリズム (RC2 および RC4) のいずれかを使用してメッセージを暗号化できます。 現在、いずれの暗号化アルゴリズムも、メッセージ キュー テクノロジでまだサポートされていない最新のアルゴリズムと比較して、暗号強度の弱さが指摘されています。 そのため、メッセージ キュー タスクを使ってメッセージを送信する場合は、必要な暗号強度を満たすことができるかどうかを十分に検討する必要があります。  
  
## <a name="receiving-messages"></a>受信、メッセージ  
 メッセージ キュー タスクは、メッセージを受信する場合に次の方法で構成できます。  
  
-   メッセージをバイパスするか、またはメッセージをキューから削除します。  
  
-   タイムアウトを指定します。  
  
-   タイムアウトが発生した場合には失敗します。  
  
-   メッセージが "`Data file`" に格納されている場合、既存のファイルを上書きします。  
  
-   メッセージが "`Data file message`" 型を使用している場合、メッセージ ファイルを別のファイル名で保存します。  
  
## <a name="custom-logging-messages-available-on-the-message-queue-task"></a>メッセージ キュー タスクで使用できるカスタム ログ メッセージ  
 次の表は、メッセージ キュー タスクのカスタム ログ エントリの一覧です。 詳しくは、「[Integration Services &#40;SSIS&#41; のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」をご覧ください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`MSMQAfterOpen`|タスクで開いていたメッセージ キューを終了したことを示します。|  
|`MSMQBeforeOpen`|タスクがメッセージ キューを開く操作を開始したことを示します。|  
|`MSMQBeginReceive`|タスクがメッセージの受信を開始したことを示します。|  
|`MSMQBeginSend`|タスクがメッセージの送信を開始したことを示します。|  
|`MSMQEndReceive`|タスクがメッセージの受信を終了したことを示します。|  
|`MSMQEndSend`|タスクがメッセージの送信を終了したことを示します。|  
|`MSMQTaskInfo`|タスクに関する説明情報を提供します。|  
|`MSMQTaskTimeOut`|タスクがタイムアウトしたことを示します。|  
  
## <a name="configuration-of-the-message-queue-task"></a>メッセージ キュー タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[メッセージ キュー タスク エディター] &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [[メッセージ キュー タスク エディター] &#40;[受信] ページ&#41;](../message-queue-task-editor-receive-page.md)  
  
-   [[メッセージ キュー タスク エディター] &#40;[送信] ページ&#41;](../message-queue-task-editor-send-page.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 プログラムによってこれらのプロパティを設定する方法の詳細については、開発者ガイドの **Microsoft.SqlServer.Dts.Tasks.MessageQueueTask.MessageQueueTask** クラスのドキュメントを参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 これらのプロパティを [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定する方法の詳細については、「 [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services タスク](integration-services-tasks.md)   
 [制御フロー](control-flow.md)  
  
  
