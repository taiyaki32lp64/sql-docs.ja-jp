---
title: エラー メッセージ転送タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfererrormessagestask.f1
- sql13.dts.designer.transfererrormessagestask.general.f1
- sql13.dts.designer.transfererrormessagestask.errormessages.F1
helpviewer_keywords:
- Transfer Error Messages task [Integration Services]
ms.assetid: da702289-035a-4d14-bd74-04461fbfee1b
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 363a2761472f544e2c995fba25f4650ee6242b36
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293881"
---
# <a name="transfer-error-messages-task"></a>エラー メッセージ転送タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  エラー メッセージ転送タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス間で 1 つ以上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ユーザー定義エラー メッセージを転送します。 ユーザー定義メッセージとは、ID の値が 50000 以上のメッセージのことです。 ID の値が 50000 未満のメッセージはシステム エラー メッセージなので、エラー メッセージ転送タスクを使用して転送することはできません。  
  
 エラー メッセージ転送タスクは、すべてのエラー メッセージを転送するか、指定したエラー メッセージだけを転送できるように、構成することができます。 ユーザー定義エラー メッセージはさまざまな言語で利用できます。このタスクでは、選択した言語のメッセージだけを転送するように構成できます。 他言語バージョンのメッセージを転送先サーバーに転送するには、コード ページ 1033 を使用した us_english バージョンのメッセージが転送先サーバーにあらかじめ存在している必要があります。  
  
 master データベースの sysmessages テーブルには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用されるすべてのシステム エラー メッセージおよびユーザー定義エラー メッセージが格納されます。  
  
 転送対象のユーザー定義メッセージは、転送先に既に存在している可能性があります。 エラー メッセージは、その識別子と言語が同じ場合は、重複エラー メッセージとして定義されます。 エラー メッセージ転送タスクでは、既存のエラー メッセージの処理方法を次のように構成できます。  
  
-   既存のエラー メッセージを上書きします。  
  
-   重複するメッセージが存在する場合、タスクを失敗とします。  
  
-   重複エラー メッセージをスキップします。  
  
 実行時、エラー メッセージ転送タスクは、1 つまたは 2 つの SMO 接続マネージャーを使用して、転送元サーバーと転送先サーバーに接続します。 SMO 接続マネージャーの構成はエラー メッセージ転送タスクとは別に行い、エラー メッセージ転送タスクは接続マネージャーを参照します。 SMO 接続マネージャーは、サーバーと、このサーバーにアクセスするときに使用する認証モードを指定します。 詳細については、「 [SMO 接続マネージャー](../../integration-services/connection-manager/smo-connection-manager.md)」をご覧ください。  
  
 エラー メッセージ転送タスクは、転送元および転送先として [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をサポートしています。 転送元または転送先として使用するバージョンに関する制限はありません。  
  
## <a name="events"></a>イベント  
 このタスクは、転送されたエラー メッセージの数を報告する情報イベントを発生させます。  
  
 エラー メッセージ転送タスクでは、エラー メッセージ転送の進捗状況は報告されません。0% または 100% 完了した場合のみ報告されます。  
  
## <a name="execution-value"></a>実行値  
 このタスクの **ExecutionValue** プロパティに定義される実行値は、転送されたエラー メッセージの数を返します。 エラー メッセージ転送タスクの **ExecValueVariable** プロパティにユーザー定義変数を割り当てると、エラー メッセージ転送に関する情報をパッケージ内の他のオブジェクトで利用できるようになります。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)」と「[パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)」をご覧ください。  
  
## <a name="log-entries"></a>ログ エントリ  
 エラー メッセージ転送タスクには、次のようなカスタム ログ エントリがあります。  
  
-   TransferErrorMessagesTaskStartTransferringObjects: 転送が開始されたことを報告するログ エントリです。 ログ エントリには、開始時刻が含まれます。  
  
-   TransferErrorMessagesTaskFinishedTransferringObjects: 転送が終了したことを報告するログ エントリです。 ログ エントリには、終了時刻が含まれます。  
  
 また、 **OnInformation** イベントのログ エントリは転送されたエラー メッセージの数をレポートし、 **OnWarning event** のログ エントリは転送先でエラー メッセージが上書きされるたびに書き込まれます。  
  
## <a name="security-and-permissions"></a>セキュリティおよび権限  
 新しいエラー メッセージを作成する場合、パッケージを実行するユーザーは、転送先サーバーで sysadmin または serveradmin サーバー ロールのメンバーである必要があります。  
  
## <a name="configuration-of-the-transfer-error-messages-task"></a>エラー メッセージ転送タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 プログラムによってこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferErrorMessagesTask.TransferErrorMessagesTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="transfer-error-messages-task-editor-general-page"></a>[エラー メッセージ転送タスク エディター] ([全般] ページ)
  **[エラー メッセージ転送タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、エラー メッセージ転送タスクに名前を付けて説明を記述することができます。 エラー メッセージ転送タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス間で 1 つ以上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ユーザー定義エラー メッセージを転送します。   
  
### <a name="options"></a>オプション  
 **[名前]**  
 エラー メッセージ転送タスクの一意の名前を入力します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 エラー メッセージ転送タスクの説明を入力します。  
  
## <a name="transfer-error-messages-task-editor-messages-page"></a>[エラー メッセージ転送タスク エディター] ([メッセージ] ページ)
  **[エラー メッセージ転送タスク エディター]** ダイアログ ボックスの **[メッセージ]** ページを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスからインスタンスへ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーザー定義エラー メッセージをコピーする際のプロパティを指定できます。 
  
### <a name="options"></a>オプション  
 **SourceConnection**  
 SMO 接続マネージャーを一覧から選択するか、 **\<[新しい接続...]>** をクリックしてコピー元のサーバーへの新しい接続を作成します。  
  
 **DestinationConnection**  
 SMO 接続マネージャーを一覧から選択するか、 **\<[新しい接続...]>** をクリックしてコピー先のサーバーへの新しい接続を作成します。  
  
 **[IfObjectExists]**  
 転送先サーバーに同じ名前のエラー メッセージが既に存在していた場合に、既存のユーザー定義エラー メッセージを上書きするか、既存のメッセージをスキップするか、タスクを失敗させるかを選択します。  
  
 **[TransferAllErrorMessages]**  
 転送元サーバーから転送先サーバーにすべてのユーザー定義メッセージをコピーするか、指定したユーザー定義メッセージだけをコピーするかを選択します。  
  
 このプロパティには、次の表に示すオプションがあります。  
  
|[値]|Description|  
|-----------|-----------------|  
|**True**|すべてのユーザー定義メッセージをコピーします。|  
|**False**|指定されたユーザー定義メッセージのみをコピーします。|  
  
 **[ErrorMessagesList]**  
 **[...]** ボタンをクリックして、コピーするエラー メッセージを選択します。  
  
> [!NOTE]  
>  コピーするエラー メッセージを選択する前に **[SourceConnection]** を指定する必要があります。  
  
 **[ErrorMessageLanguagesList]**  
 **[...]** ボタンをクリックして、転送先サーバーにコピーするユーザー定義エラー メッセージの言語を選択します。 us_english (コード ページ 1033) バージョンのメッセージが、他言語バージョンのメッセージを転送先サーバーに転送する前に、そのサーバーに既に存在している必要があります。  
  
> [!NOTE]  
>  コピーするエラー メッセージを選択する前に **[SourceConnection]** を指定する必要があります。  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [制御フロー](../../integration-services/control-flow/control-flow.md)  
  
  
