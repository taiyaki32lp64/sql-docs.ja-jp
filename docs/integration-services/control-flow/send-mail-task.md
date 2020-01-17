---
title: メール送信タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sendmailtask.f1
- sql13.dts.designer.sendmailtask.general.f1
- sql13.dts.designer.sendmailtask.mail.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f35ec3ad66199e6c13c648c9a2208f5bf88f439a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293930"
---
# <a name="send-mail-task"></a>メール送信タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  メール送信タスクは、電子メール メッセージを送信します。 メール送信タスクを使用すると、パッケージ ワークフロー内のタスクが成功または失敗した場合にパッケージからメッセージを送信したり、実行時にパッケージで発生するイベントに応答してメッセージを送信したりできます。 たとえば、データベースのバックアップ タスクが成功または失敗したことを、メール送信タスクからデータベース管理者に通知できます。  
  
 メール送信タスクは、次の方法で構成できます。  
  
-   電子メール メッセージで使用するメッセージ テキストを指定します。  
  
-   電子メール メッセージの件名行を指定します。  
  
-   メッセージの優先度レベルを設定します。 タスクでは、標準、低、高の 3 種類の優先度レベルがサポートされています。  
  
-   [宛先]、[CC]、[BCC] 行に受信者を指定します。 タスクで複数の受信者を指定する場合、セミコロンで区切られます。  
  
    > [!NOTE]  
    >  [宛先]、[CC]、[BCC] 行の文字数は、インターネット標準に従って 256 文字に制限されています。  
  
-   添付ファイルを含めます。 タスクで複数の添付ファイルを指定する場合、パイプ (|) 文字で区切られます。  
  
    > [!NOTE]  
    >  パッケージの実行時に添付ファイルが存在しない場合、エラーが発生します。  
  
-   使用する SMTP 接続マネージャーを指定します。  
  
    > [!IMPORTANT]  
    >  SMTP 接続マネージャーでは、匿名認証と Windows 認証のみがサポートされています。 基本認証はサポートされていません。  
  
 メッセージ テキストには、指定する文字列、テキストを含むファイルへの接続、またはテキストを含む変数名を使用できます。 タスクは、ファイル接続マネージャーを使用してファイルに接続します。 詳しくは、「 [フラット ファイル接続マネージャー](../../integration-services/connection-manager/flat-file-connection-manager.md)」をご覧ください。  
  
 タスクは、SMTP 接続マネージャーを使用してメール サーバーに接続します。 詳しくは、「 [SMTP 接続マネージャー](../../integration-services/connection-manager/smtp-connection-manager.md)」をご覧ください。  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>メール送信タスクで使用できるカスタム ログ メッセージ  
 次の表は、メール送信タスクのカスタム ログ エントリの一覧です。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**SendMailTaskBegin**|タスクが電子メール メッセージの送信を開始したことを示します。|  
|**SendMailTaskEnd**|タスクが電子メール メッセージの送信を終了したことを示します。|  
|**SendMailTaskInfo**|タスクに関する説明情報を提供します。|  
  
## <a name="configuring-the-send-mail-task"></a>メール送信タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 プログラムによってこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 これらのプロパティを [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定する方法の詳細については、「 [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)」をご覧ください。  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   shareourideas.com の技術記事「 [配信通知付きで電子メールを送信する方法 (C#)](https://go.microsoft.com/fwlink/?LinkId=237625)」  
  
## <a name="send-mail-task-editor-general-page"></a>[メール送信タスク エディター] ([全般] ページ)
  **[メール送信タスク エディター]** の **[全般]** ページを使用すると、メール送信タスクに名前を付けて説明を記述できます。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 メール送信タスクに一意の名前を提供します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
 **注** &#xA0;&#xA0;&#xA0;タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 メール送信タスクの説明を入力します。  
  
## <a name="send-mail-task-editor-mail-page"></a>[メール送信タスク エディター] ([メール] ページ)
  **[メール送信タスク エディター]** ダイアログ ボックスの **[メール]** ページを使用すると、受信者、メッセージの種類、メッセージの重要度を指定できます。 メッセージにファイルを添付することもできます。 メッセージ テキストは、入力した文字列、テキストが含まれるファイルへのファイル接続、またはテキストが含まれる変数の名前になります。  
  
### <a name="options"></a>オプション  
 **[SMTPConnection]**  
 一覧で SMTP 接続マネージャーを選択するか、[ **\<新しい接続...>** ] をクリックして新しい接続マネージャーを作成します。  
  
> [!IMPORTANT]  
>  SMTP 接続マネージャーでは、匿名認証と Windows 認証のみがサポートされています。 基本認証はサポートされていません。  
  
 **関連トピック:** [SMTP 接続マネージャー](../../integration-services/connection-manager/smtp-connection-manager.md)  
  
 **From**  
 送信者の電子メール アドレスを指定します。  
  
 **変換先**  
 受信者の電子メール アドレスを指定します。受信者はセミコロンで区切ります。  
  
 **[Cc]**  
 メッセージのコピーを受け取る受信者の電子メール アドレスを指定します。受信者はセミコロンで区切ります。  
  
 **[Bcc]**  
 メッセージのコピーを Bcc として受け取る受信者の電子メール アドレスを指定します。受信者はセミコロンで区切ります。  
  
 **[Subject]**  
 電子メール メッセージの件名を指定します。  
  
 **[MessageSourceType]**  
 メッセージのソースの種類を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|メッセージ テキストをソースとして設定します。 この値を選択すると、動的オプション **[MessageSource]** が表示されます。|  
|**[ファイル接続]**|メッセージ テキストが含まれるファイルをソースとして設定します。 この値を選択すると、動的オプション **[MessageSource]** が表示されます。|  
|**変数**|メッセージ テキストが含まれる変数をソースとして設定します。 この値を選択すると、動的オプション **[MessageSource]** が表示されます。|  
  
 **[Priority]**  
 メッセージの重要度を設定します。  
  
 **[Attachments]**  
 電子メール メッセージに添付するファイル名を指定します。ファイル名はパイプ文字 (|) で区切ります。  
  
> [!NOTE]  
>  [宛先]、[CC]、[BCC] 行の文字数は、インターネット標準に従って 256 文字に制限されています。  
  
### <a name="messagesourcetype-dynamic-options"></a>MessageSourceType 動的オプション  
  
#### <a name="messagesourcetype--direct-input"></a>[MessageSourceType] = [直接入力]  
 **[MessageSource]**  
 メッセージ テキストを入力するか、参照ボタン ( [...] ) をクリックして **[メッセージの送信元]** ダイアログ ボックスにメッセージを入力します。  
  
#### <a name="messagesourcetype--file-connection"></a>[MessageSourceType] = [ファイル接続]  
 **[MessageSource]**  
 ファイル接続マネージャーを一覧から選択するか、[\<**新しい接続...>** ] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="messagesourcetype--variable"></a>[MessageSourceType] = [変数]  
 **[MessageSource]**  
 一覧で変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="see-also"></a>参照  
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [制御フロー](../../integration-services/control-flow/control-flow.md)  
  
  
