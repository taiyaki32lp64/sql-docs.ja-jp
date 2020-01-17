---
title: メール送信タスク エディター ([メール] ページ) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sendmailtask.mail.f1
helpviewer_keywords:
- Send Mail Task Editor
ms.assetid: adb385d5-ef24-4d18-b9ea-b39e00a7075e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d80ca8e475bf9c2b56c11118a44e5282573f280d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055828"
---
# <a name="send-mail-task-editor-mail-page"></a>[メール送信タスク エディター] ([メール] ページ)
  **[メール送信タスク エディター]** ダイアログ ボックスの **[メール]** ページを使用すると、受信者、メッセージの種類、メッセージの重要度を指定できます。 メッセージにファイルを添付することもできます。 メッセージ テキストは、入力した文字列、テキストが含まれるファイルへのファイル接続、またはテキストが含まれる変数の名前になります。  
  
 このタスクの詳細については、「 [Send Mail Task](control-flow/send-mail-task.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[SMTPConnection]**  
 一覧で SMTP 接続マネージャーを選択するか、[ **\<新しい接続...>** ] をクリックして新しい接続マネージャーを作成します。  
  
> [!IMPORTANT]  
>  SMTP 接続マネージャーでは、匿名認証と Windows 認証のみがサポートされています。 基本認証はサポートされていません。  
  
 **関連トピック:** [SMTP 接続マネージャー](connection-manager/smtp-connection-manager.md)  
  
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
  
|ReplTest1|説明|  
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
  
## <a name="messagesourcetype-dynamic-options"></a>MessageSourceType 動的オプション  
  
### <a name="messagesourcetype--direct-input"></a>[MessageSourceType] = [直接入力]  
 **[MessageSource]**  
 メッセージ テキストを入力するか、参照ボタン ( [...] ) をクリックして **[メッセージの送信元]** ダイアログ ボックスにメッセージを入力します。  
  
### <a name="messagesourcetype--file-connection"></a>[MessageSourceType] = [ファイル接続]  
 **[MessageSource]**  
 ファイル接続マネージャーを一覧から選択するか、[\<**新しい接続...>** ] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="messagesourcetype--variable"></a>[MessageSourceType] = [変数]  
 **[MessageSource]**  
 一覧で変数を選択するか、[\<**新しい変数...** >] をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)、[変数の追加](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>関連項目  
 [Integration Services のエラーおよびメッセージのリファレンス](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [[メール送信タスク エディター] &#40;[全般] ページ&#41;](general-page-of-integration-services-designers-options.md)   
 [[式] ページ](expressions/expressions-page.md)  
  
  
