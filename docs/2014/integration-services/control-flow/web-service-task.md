---
title: Web サービス タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.webservicetask.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f21a5f938b2dcd7b90fa71ab946d2986b0633987
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62829411"
---
# <a name="web-service-task"></a>Web サービス タスク
  Web サービス タスクは、Web サービス メソッドを実行します。 Web サービス タスクは、次の目的で使用できます。  
  
-   Web サービス メソッドが返す値を変数に書き込みます。 たとえば、Web サービス メソッドから 1 日の最高気温を取得し、その値を使用して、列の値を設定する式で使用する変数を更新できます。  
  
-   Web サービス メソッドが返す値をファイルに書き込みます。 たとえば、見込み客の一覧をファイルに書き込み、データをデータベースに書き込む前にそのデータをクリーンにするためのパッケージのデータ ソースとして、そのファイルを使用できます。  
  
## <a name="wsdl-file"></a>WSDL ファイル  
 Web サービス タスクは、HTTP 接続マネージャーを使用して Web サービスに接続します。 HTTP 接続マネージャーは、Web サービス タスクとは別に構成され、タスク内で参照されます。 HTTP 接続マネージャーは、サーバーの URL、Web サービスのサーバーにアクセスするための資格情報、タイムアウト長などの、サーバーのプロキシ設定を指定します。 詳細については、「 [HTTP 接続マネージャー](../connection-manager/http-connection-manager.md)」を参照してください。  
  
> [!IMPORTANT]  
>  HTTP 接続マネージャーでは、匿名認証と基本認証のみがサポートされています。 Windows 認証はサポートされていません。  
  
 HTTP 接続マネージャーは、Web サイトまたは Web サービス記述言語 (WSDL) ファイルを参照できます。 WSDL ファイルを参照する HTTP 接続マネージャーの URL には、 `?WSDL` パラメーターが含まれます。たとえば、 `http://MyServer/MyWebService/MyPage.asmx?WSDL`と指定します。  
  
 **デザイナーで用意されている** [Web サービス タスク エディター] [!INCLUDE[ssIS](../../includes/ssis-md.md)] ダイアログ ボックスを使用して Web サービス タスクを構成するには、WSDL ファイルがローカルで使用できる必要があります。  
  
-   HTTP 接続マネージャーが Web サイトを参照する場合、WSDL ファイルを手動でローカル コンピューターにコピーする必要があります。  
  
-   HTTP 接続マネージャーが WSDL ファイルを参照する場合、Web サービス タスクを使用して、Web サイトからその WSDL ファイルをローカル ファイルにダウンロードできます。  
  
 WSDL ファイルには、Web サービスが提供するメソッド、メソッドに必要な入力パラメーター、メソッドが返す応答、および Web サービスとの通信方法が一覧表示されます。  
  
 メソッドが入力パラメーターを使用する場合、Web サービス タスクにはパラメーター値が必要です。 たとえば、身長に基づいて購入するスキーの長さをアドバイスする Web サービス メソッドでは、入力パラメーターに身長を送信する必要があります。 パラメーター値は、タスク内で定義されている文字列、またはタスクのスコープか親コンテナーで定義されている変数によって指定できます。 変数を使用すると、パッケージ構成またはスクリプトを使用してパラメーター値を動的に更新できるという利点があります。 詳細については、「[Integration Services (SSIS) の変数](../integration-services-ssis-variables.md)」と「[パッケージ構成](../package-configurations.md)」を参照してください。  
  
 多くの Web サービス メソッドでは、入力パラメーターを使用しません。 たとえば、今月が誕生月の大統領の名前を取得する Web サービス メソッドでは、入力パラメーターは必要ありません。これは、Web サービスで現在の月をローカルに判別できるためです。  
  
 Web サービス メソッドの結果は、変数またはファイルに書き込むことができます。 結果を書き込むファイルを指定するか、変数の名前を指定するには、ファイル接続マネージャーを使用します。 詳細については、「[ファイル接続マネージャー](../connection-manager/file-connection-manager.md)」および「[Integration Services (SSIS) の変数](../integration-services-ssis-variables.md)」を参照してください。  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Web サービス タスクで使用できるカスタム ログ メッセージ  
 次の表は、Web サービス タスクに対して有効にできるカスタム ログ エントリの一覧です。 詳しくは、「[Integration Services &#40;SSIS&#41; のログ記録](../performance/integration-services-ssis-logging.md)」と「[ログ記録用のカスタム メッセージ](../custom-messages-for-logging.md)」をご覧ください。  
  
|ログ エントリ|説明|  
|---------------|-----------------|  
|`WSTaskBegin`|タスクが Web サービスへのアクセスを開始しました。|  
|`WSTaskEnd`|タスクが Web サービス メソッドを完了しました。|  
|`WSTaskInfo`|タスクに関する説明情報を提供します。|  
  
## <a name="configuration-of-the-web-service-task"></a>Web サービス タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Web サービス タスク エディター &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Web サービス タスク エディター &#40;[入力] ページ&#41;](../web-service-task-editor-input-page.md)  
  
-   [Web サービス タスク エディター &#40;[出力] ページ&#41;](../web-service-task-editor-output-page.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>プログラムによる Web サービス タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="related-content"></a>関連コンテンツ  
 MSDN ライブラリのビデオ「[Web サービス タスクを使用して Web サービスを呼び出す方法 (SQL Server ビデオ)](https://go.microsoft.com/fwlink/?LinkId=259642) (technet.microsoft.com)  
  
 [SSIS パッケージから Web サービスを使用する方法](https://www.c-sharpcorner.com/article/how-to-consume-web-service-through-ssis-package/)します。  
  
  
