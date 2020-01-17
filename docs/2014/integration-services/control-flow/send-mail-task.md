---
title: メール送信タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sendmailtask.f1
helpviewer_keywords:
- mail [Integration Services]
- Send Mail task
- e-mail [Integration Services]
- messages [Integration Services]
- sending messages
ms.assetid: fe0b7cbc-fe8e-4fe2-95b4-2953efff5869
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3308899190aa63ebb9be93c4c9af15d5e0f94600
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62830396"
---
# <a name="send-mail-task"></a>メール送信タスク
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
  
 メッセージ テキストには、指定する文字列、テキストを含むファイルへの接続、またはテキストを含む変数名を使用できます。 タスクは、ファイル接続マネージャーを使用してファイルに接続します。 詳しくは、「 [フラット ファイル接続マネージャー](../connection-manager/file-connection-manager.md)」をご覧ください。  
  
 タスクは、SMTP 接続マネージャーを使用してメール サーバーに接続します。 詳しくは、「 [SMTP 接続マネージャー](../connection-manager/smtp-connection-manager.md)」をご覧ください。  
  
## <a name="custom-logging-messages-available-on-the-send-mail-task"></a>メール送信タスクで使用できるカスタム ログ メッセージ  
 次の表は、メール送信タスクのカスタム ログ エントリの一覧です。 詳しくは、「[Integration Services &#40;SSIS&#41; のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」をご覧ください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`SendMailTaskBegin`|タスクが電子メール メッセージの送信を開始したことを示します。|  
|`SendMailTaskEnd`|タスクが電子メール メッセージの送信を終了したことを示します。|  
|`SendMailTaskInfo`|タスクに関する説明情報を提供します。|  
  
## <a name="configuring-the-send-mail-task"></a>メール送信タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[メール送信タスク エディター] &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [[メール送信タスク エディター] &#40;[メール] ページ&#41;](../send-mail-task-editor-mail-page.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 プログラムによってこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.SendMailTask.SendMailTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 これらのプロパティを [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定する方法の詳細については、「 [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)」をご覧ください。  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   shareourideas.com の技術記事「 [配信通知付きで電子メールを送信する方法 (C#)](https://go.microsoft.com/fwlink/?LinkId=237625)」  
  
## <a name="see-also"></a>関連項目  
 [Integration Services タスク](integration-services-tasks.md)   
 [制御フロー](control-flow.md)  
  
  
