---
title: メッセージ キュー タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.messagequeuetask.f1
- sql13.dts.designer.msgqueuetask.general.f1
- sql13.dts.designer.msgqueuetask.send.f1
- sql13.dts.designer.msgqueuetask.receive.f1
- sql13.dts.designer.selectvariables.f1
helpviewer_keywords:
- Message Queue task [Integration Services]
- receiving messages
- messages [Integration Services]
- sending messages
ms.assetid: ae1d8fad-6649-4e93-b589-14a32d07da33
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 486339cc1c5ef550dbf4eee227bec3ad67ce0e3a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294099"
---
# <a name="message-queue-task"></a>Message Queue Task

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  メッセージ キュー タスクでは、Message Queuing (MSMQ) を使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージ間でメッセージを送受信したり、カスタム アプリケーションによって処理されるアプリケーションのキューにメッセージを送信したりすることができます。 これらのメッセージは、簡単なテキスト形式、ファイル、変数、またはそれらの値です。  
  
 メッセージ キュー タスクを使用することにより、企業の組織全体の操作を調整できます。 送信先が使用できない場合やビジーの場合、メッセージをキューに入れ、後で配信できます。たとえば、送信先が販売担当者のオフラインのラップトップ コンピューターの場合、キューにメッセージが入れられ、販売担当者はネットワークに接続したときに受信できます。 メッセージ キュー タスクは、次の目的で使用できます。  
  
-   他のパッケージがチェックインするまでタスクの実行を遅らせることができます。 たとえば、各小売り店舗で夜間のメンテナンスが終了した後、メッセージ キュー タスクは本社のコンピューターにメッセージを送信します。 この本社のコンピューターで実行するパッケージには複数のメッセージ キュー タスクが含まれており、それぞれが個々の店舗からのメッセージを待機しています。 メッセージが店舗から到着すると、タスクは店舗のデータをアップロードします。 すべての店舗がチェックインしたら、パッケージは合計を集計します。  
  
-   データ ファイルを処理するコンピューターに、データ ファイルを送信できます。 たとえば、レストランの会計レジの出力をデータ ファイル メッセージとして給与計算システムに送信して、ウェイターのチップに関するデータを抽出できます。  
  
-   企業の組織全体にファイルを配信できます。 たとえば、あるパッケージでメッセージ キュー タスクを使用して、別のコンピューターにパッケージ ファイルを送信できます。 送信先のコンピューターで実行するパッケージは、メッセージ キュー タスクを使用してパッケージをローカルに取得し保存します。  
  
 メッセージ キュー タスクは、メッセージの送受信時に、"データ ファイル"、"文字列"、"文字列メッセージを変数に指定"、"変数" の 4 つのうちのいずれかのメッセージ型を使用します。 "文字列メッセージを変数に指定" メッセージ型は、メッセージの受信時にのみ使用できます。  
  
 タスクは MSMQ 接続マネージャーを使用して、メッセージ キューに接続します。 詳細については、「 [MSMQ 接続マネージャー](../../integration-services/connection-manager/msmq-connection-manager.md)」を参照してください。 メッセージ キューの詳細については、 [MSDN ライブラリ](https://go.microsoft.com/fwlink/?LinkId=7022)を参照してください。  
  
 メッセージ キュー タスクには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスのインストールが必要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードの **[インストールするコンポーネント]** ページまたは **[機能の選択]** ページでインストールの選択をした [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントによっては、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントのサブセットの一部がインストールされます。 これらのコンポーネントを使用して一部のタスクを実行することは可能ですが、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のすべての機能は使用できません。 たとえば、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] のオプションでは、パッケージをデザインするために必要な [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントがインストールされますが、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスはインストールされません。したがって、メッセージ キュー タスクは機能しません。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]を完全にインストールするには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] [インストールするコンポーネント] **ページで** を選択する必要があります。 メッセージ キュー タスクのインストールと実行の詳細については、「 [Integration Services のインストール](../../integration-services/install-windows/install-integration-services.md)」を参照してください。  
  
> [!NOTE]  
>  コンピューターのオペレーティング システムが FIPS モードで構成され、タスクで暗号化が使用されている場合は、メッセージ キュー タスクは Federal Information Processing Standard (FIPS) 140-2 に準拠することができません。 メッセージ キュー タスクで暗号化が使用されていない場合は、タスクを正常に実行することができます。  
  
## <a name="message-types"></a>メッセージ型  
 メッセージ キュー タスクで用意されているメッセージ型は、次の方法で構成できます。  
  
-   **[データ ファイル]** メッセージは、ファイルにメッセージが含まれることを指定します。 メッセージを受信するときに、タスクによってファイルを保存したり既存のファイルを上書きできるように、また、タスクによってメッセージを受信できるパッケージを指定するように、タスクを構成できます。  
  
-   **[文字列]** メッセージは、メッセージを文字列として指定します。 メッセージを受信するときに、タスクが受信した文字列とユーザー定義の文字列とを比較したり、比較に基づいて処理を実行するように構成できます。 文字列比較では、完全な比較、大文字と小文字を区別する比較、大文字と小文字を区別しない比較、またはサブストリングを使用した比較を設定できます。  
  
-   **[文字列メッセージを変数に指定]** では、基になるメッセージを、送信先の変数に送信される文字列として指定できます。 完全な比較、大文字と小文字を区別しない比較、またはサブストリングの比較を使用して、受信した文字列とユーザー定義の文字列とを比較するようにタスクを構成できます。 このメッセージ型は、タスクがメッセージを受信するときにのみ使用できます。  
  
-   **[変数]** は、メッセージが 1 つ以上の変数を含むことを指定します。 タスクは、メッセージに含まれる変数の名前を指定するように構成できます。 メッセージを受信するときに、メッセージを受信するパッケージおよびメッセージの送信先となる変数の両方を指定するようにタスクを構成できます。  
  
## <a name="sending-messages"></a>sending messages  
 メッセージ キュー タスクを構成してメッセージを送信する場合、メッセージ キュー テクノロジで現在サポートされている暗号化アルゴリズム (RC2 および RC4) のいずれかを使用してメッセージを暗号化できます。 現在、いずれの暗号化アルゴリズムも、メッセージ キュー テクノロジでまだサポートされていない最新のアルゴリズムと比較して、暗号強度の弱さが指摘されています。 そのため、メッセージ キュー タスクを使ってメッセージを送信する場合は、必要な暗号強度を満たすことができるかどうかを十分に検討する必要があります。  
  
## <a name="receiving-messages"></a>受信、メッセージ  
 メッセージ キュー タスクは、メッセージを受信する場合に次の方法で構成できます。  
  
-   メッセージをバイパスするか、またはメッセージをキューから削除します。  
  
-   タイムアウトを指定します。  
  
-   タイムアウトが発生した場合には失敗します。  
  
-   メッセージが **[データ ファイル]** に格納されている場合、既存のファイルを上書きします。  
  
-   メッセージが **[データ ファイル メッセージ]** 型を使用している場合、メッセージ ファイルを別のファイル名で保存します。  
  
## <a name="custom-logging-messages-available-on-the-message-queue-task"></a>メッセージ キュー タスクで使用できるカスタム ログ メッセージ  
 次の表は、メッセージ キュー タスクのカスタム ログ エントリの一覧です。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**MSMQAfterOpen**|タスクで開いていたメッセージ キューを終了したことを示します。|  
|**MSMQBeforeOpen**|タスクがメッセージ キューを開く操作を開始したことを示します。|  
|**MSMQBeginReceive**|タスクがメッセージの受信を開始したことを示します。|  
|**MSMQBeginSend**|タスクがメッセージの送信を開始したことを示します。|  
|**MSMQEndReceive**|タスクがメッセージの受信を終了したことを示します。|  
|**MSMQEndSend**|タスクがメッセージの送信を終了したことを示します。|  
|**MSMQTaskInfo**|タスクに関する説明情報を提供します。|  
|**MSMQTaskTimeOut**|タスクがタイムアウトしたことを示します。|  
  
## <a name="configuration-of-the-message-queue-task"></a>メッセージ キュー タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 プログラムによってこれらのプロパティを設定する方法の詳細については、開発者ガイドの **Microsoft.SqlServer.Dts.Tasks.MessageQueueTask.MessageQueueTask** クラスのドキュメントを参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 これらのプロパティを [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定する方法の詳細については、「 [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)」を参照してください。  
  
## <a name="message-queue-task-editor-general-page"></a>[メッセージ キュー タスク エディター] ([全般] ページ)
  **[メッセージ キュー タスク エディター]** の **[全般]** ページを使用すると、メッセージ キュー タスクの名前と説明を設定したり、メッセージの形式を指定したり、タスクでメッセージを送受信できるかどうかを指定したりできます。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 メッセージ キュー タスクの固有の名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 メッセージ キュー タスクの説明を入力します。  
  
 **[Use2000Format]**  
 Message Queuing (MSMQ) の 2000 形式を使用するかどうかを指定します。 既定値は **False**です。  
  
 **[MSMQConnection]**  
 既存の MSMQ 接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして、新しい接続マネージャーを作成します。  
  
 **関連トピック:** [MSMQ 接続マネージャー](../../integration-services/connection-manager/msmq-connection-manager.md)、[MSMQ 接続マネージャー エディター](../../integration-services/connection-manager/msmq-connection-manager-editor.md)  
  
 **メッセージ**  
 メッセージ キュー タスクでメッセージを送信するのか、受信するのかを指定します。 **[メッセージの送信]** を選択すると、ダイアログ ボックスの左側のペインに [送信] ページが表示されます。 **[メッセージの受信]** を選択すると、[受信] ページが表示されます。 既定では、 **[メッセージの送信]** に設定されています。  
  
## <a name="message-queue-task-editor-send-page"></a>[メッセージ キュー タスク エディター] ([送信] ページ)
  **[メッセージ キュー タスク エディター]** ダイアログ ボックスの **[送信]** ページを使用すると、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージからメッセージを送信するメッセージ キュー タスクを構成できます。  
  
### <a name="options"></a>オプション  
 **[UseEncryption]**  
 メッセージを暗号化するかどうかを示します。 既定値は **False**です。  
  
 **[EncryptionAlgorithm]**  
 暗号化を使用する場合は、使用する暗号化アルゴリズムを指定します。 メッセージ キュー タスクでは、RC2 と RC4 のアルゴリズムを使用できます。 既定値は **[RC2]** です。  
  
> [!NOTE]  
>  RC4 アルゴリズムは、旧バージョンとの互換性のためにのみサポートされています。 データベース互換性レベルが 90 または 100 の場合、新しい素材は RC4 または RC4_128 を使用してのみ暗号化できます (非推奨)。AES アルゴリズムのいずれかなど、新しいアルゴリズムを使用してください。 現在のリリースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、どの互換性レベルでも、RC4 または RC4_128 を使用して暗号化された素材を暗号化解除できます。  
  
> [!IMPORTANT]  
>  これらは、メッセージ キュー (MSMQ) テクノロジでサポートされる暗号化アルゴリズムです。 現在、いずれの暗号化アルゴリズムも、メッセージ キューでまだサポートされていない最新のアルゴリズムと比較して、暗号強度の弱さが指摘されています。 そのため、メッセージ キュー タスクを使ってメッセージを送信する場合は、必要な暗号強度を満たすことができるかどうかを十分に検討する必要があります。  
  
 **[MessageType]**  
 メッセージ型を指定します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[データ ファイル メッセージ]**|メッセージはファイルに格納されます。 この値を選択すると、動的オプションの **[DataFileMessage]** が表示されます。|  
|**[変数メッセージ]**|メッセージは変数に格納されます。 この値を選択すると、動的オプションの **[VariableMessage]** が表示されます。|  
|**[文字列メッセージ]**|メッセージはメッセージ キュー タスクに格納されます。 この値を選択すると、動的オプションの **[StringMessage]** が表示されます。|  
  
### <a name="messagetype-dynamic-options"></a>[MessageType] の動的オプション  
  
#### <a name="messagetype--data-file-message"></a>[MessageType] = [データ ファイル メッセージ]  
 **[DataFileMessage]**  
 データ ファイルのパスを入力します。または、参照ボタン ( **[...]** ) をクリックし、データ ファイルを指定します。  
  
#### <a name="messagetype--variable-message"></a>[MessageType] = [変数メッセージ]  
 **[VariableMessage]**  
 変数名を入力します。または、参照ボタン ( **[...]** ) をクリックし、変数を指定します。 変数はコンマで区切って指定します。  
  
 **関連トピック:** [変数の選択]  
  
#### <a name="messagetype--string-message"></a>[MessageType] = [文字列メッセージ]  
 **[StringMessage]**  
 文字列メッセージを入力します。または、参照ボタン ( **[...]** ) をクリックし、メッセージを **[メッセージの入力]** ダイアログ ボックスに入力します。  
  
## <a name="message-queue-task-editor-receive-page"></a>[メッセージ キュー タスク エディター] ([受信] ページ)
  **[メッセージ キュー タスク エディター]** ダイアログ ボックスの **[受信]** ページを使用して、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (MSMQ) メッセージを受信するためのメッセージ キュー タスクを構成します。  
  
### <a name="options"></a>オプション  
 **[RemoveFromMessageQueue]**  
 メッセージが受信された後にキューからメッセージを削除するかどうかを示します。 既定では、この値は **False**に設定されます。  
  
 **[ErrorIfMessageTimeOut]**  
 メッセージがタイムアウトになったときに、エラー メッセージを表示してタスクを中止するかどうかを示します。 既定値は **False**です。  
  
 **[TimeoutAfter]**  
 タスクが失敗したときにエラー メッセージを表示するように指定した場合、タイムアウト メッセージが表示されるまでの待機時間を秒数で指定します。  
  
 **[MessageType]**  
 メッセージ型を指定します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[データ ファイル メッセージ]**|メッセージはファイルに格納されます。 この値を選択すると、動的オプションの **[DataFileMessage]** が表示されます。|  
|**[変数メッセージ]**|メッセージは変数に格納されます。 この値を選択すると、動的オプションの **[VariableMessage]** が表示されます。|  
|**[文字列メッセージ]**|メッセージはメッセージ キュー タスクに格納されます。 この値を選択すると、動的オプションの **[StringMessage]** が表示されます。|  
|**[文字列メッセージを変数に指定]**|メッセージです。<br /><br /> この値を選択すると、動的オプションの **[StringMessage]** が表示されます。|  
  
### <a name="messagetype-dynamic-options"></a>[MessageType] の動的オプション  
  
#### <a name="messagetype--data-file-message"></a>[MessageType] = [データ ファイル メッセージ]  
 **[SaveFileAs]**  
 使用するファイルのパスを入力します。または、省略記号ボタン ( **[...]** ) をクリックし、ファイルを指定します。  
  
 **Overwrite**  
 データ ファイル メッセージの内容を保存するとき、既存のファイルのデータを上書きするかどうかを示します。 既定値は **False**です。  
  
 **[フィルター]**  
 メッセージにフィルターを適用するかどうかを指定します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[フィルターなし]**|メッセージにフィルターは適用されません。 この値を選択すると、動的オプションの **[IdentifierReadOnly]** が表示されます。|  
|**[パッケージから]**|指定したパッケージからのメッセージのみが受信されます。 この値を選択すると、動的オプションの **[Identifier]** が表示されます。|  
  
#### <a name="filter-dynamic-options"></a>[Filter] の動的オプション  
  
##### <a name="filter--no-filter"></a>[Filter] = [フィルターなし]  
 **[IdentifierReadOnly]**  
 このオプションは読み取り専用です。 [Filter] プロパティが以前に設定された場合、パッケージの GUID が表示されます。それ以外の場合は空です。  
  
##### <a name="filter--from-package"></a>[Filter] = [パッケージから]  
 **[Identifier]**  
 フィルターの適用を選択した場合、メッセージの受信元のパッケージを表す固有の識別子を入力するか、省略記号ボタン ( **[...]** ) をクリックしてパッケージを指定します。  
  
 **関連トピック:** [パッケージの選択](../../integration-services/control-flow/select-a-package.md)  
  
#### <a name="messagetype--variable-message"></a>[MessageType] = [変数メッセージ]  
 **Assert**  
 メッセージにフィルターを適用するかどうかを指定します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[フィルターなし]**|メッセージにフィルターは適用されません。 この値を選択すると、動的オプションの **[IdentifierReadOnly]** が表示されます。|  
|**[パッケージから]**|指定したパッケージからのメッセージのみが受信されます。 この値を選択すると、動的オプションの **[Identifier]** が表示されます。|  
  
 **変数**  
 変数の名前を入力するか、[\<**新しい変数...** >] をクリックして新しい変数を設定します。  
  
 **関連トピック:** [変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
#### <a name="filter-dynamic-options"></a>[Filter] の動的オプション  
  
##### <a name="filter--no-filter"></a>[Filter] = [フィルターなし]  
 **[IdentifierReadOnly]**  
 このオプションは空白です。  
  
##### <a name="filter--from-package"></a>[Filter] = [パッケージから]  
 **[Identifier]**  
 フィルターの適用を選択した場合、メッセージの受信元のパッケージを表す固有の識別子を入力するか、省略記号ボタン ( **[...]** ) をクリックしてパッケージを指定します。  
  
 **関連トピック:** [パッケージの選択](../../integration-services/control-flow/select-a-package.md)  
  
#### <a name="messagetype--string-message"></a>[MessageType] = [文字列メッセージ]  
 **[Compare]**  
 メッセージにフィルターを適用するかどうかを指定します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**なし**|メッセージは比較されません。|  
|**完全一致**|メッセージは **[CompareString]** オプションで指定した文字列と完全に一致する必要があります。|  
|**大文字と小文字を区別しない**|メッセージは **[CompareString]** オプションで指定した文字列と一致する必要がありますが、大文字と小文字は区別されません。|  
|**[含まれる文字列]**|メッセージに **[CompareString]** オプションで指定した文字列が含まれている必要があります。|  
  
 **[CompareString]**  
 **[Compare]** オプションが **[なし]** に設定されていない場合、メッセージと比較する文字列を入力します。  
  
#### <a name="messagetype--string-message-to-variable"></a>[MessageType] = [文字列メッセージを変数に指定]  
 **[Compare]**  
 メッセージにフィルターを適用するかどうかを指定します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**なし**|メッセージは比較されません。|  
|**完全一致**|メッセージは **[CompareString]** オプションで指定した文字列と完全に一致する必要があります。|  
|**大文字と小文字を区別しない**|メッセージは **[CompareString]** オプションで指定した文字列と一致する必要がありますが、大文字と小文字は区別されません。|  
|**[含まれる文字列]**|メッセージに **[CompareString]** オプションで指定した文字列が含まれている必要があります。|  
  
 **[CompareString]**  
 **[Compare]** オプションが **[なし]** に設定されていない場合、メッセージと比較する文字列を入力します。  
  
 **変数**  
 受信したメッセージを格納する変数の名前を入力するか、\<[**新しい変数...>]** をクリックして新しい変数を設定します。  
  
 **関連トピック:** [変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="select-variables"></a>[変数の選択]
  **[変数の選択]** ダイアログ ボックスを使用すると、メッセージ キュー タスクの 2 番目のメッセージ操作で使用する変数を指定できます。 **[利用可能な変数]** の一覧には、メッセージ キュー タスクまたは親コンテナーのスコープのシステム変数とユーザー定義変数が含まれます。 タスクは、 **[選択された変数]** の一覧の変数を使用します。  
  
### <a name="options"></a>オプション  
 **[利用可能な変数]**  
 1 つ以上の変数を選択します。  
  
 **[選択された変数]**  
 1 つ以上の変数を選択します。  
  
 **右矢印**  
 選択した変数を **[選択された変数]** の一覧に移動します。  
  
 **左矢印**  
 選択した変数を **[利用可能な変数]** の一覧に戻します。  
  
 **[新しい変数]**  
 新しい変数を作成します。  
  
 **関連トピック:** [変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
## <a name="see-also"></a>参照  
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [制御フロー](../../integration-services/control-flow/control-flow.md)  
  
  
