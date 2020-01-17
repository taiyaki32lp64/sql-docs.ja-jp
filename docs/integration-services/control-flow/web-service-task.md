---
title: Web サービス タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.webservicetask.f1
- sql13.dts.designer.webservicestask.general.f1
- sql13.dts.designer.webservicestask.input.f1
- sql13.dts.designer.webservicestask.output.f1
helpviewer_keywords:
- Web Service task [Integration Services]
ms.assetid: 5c7206f1-7d6a-4923-8dff-3c4912da4157
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 343d3d0d16a19e6d7e1610eff84f6e1aa8ff860a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293799"
---
# <a name="web-service-task"></a>Web サービス タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Web サービス タスクは、Web サービス メソッドを実行します。 Web サービス タスクは、次の目的で使用できます。  
  
-   Web サービス メソッドが返す値を変数に書き込みます。 たとえば、Web サービス メソッドから 1 日の最高気温を取得し、その値を使用して、列の値を設定する式で使用する変数を更新できます。  
  
-   Web サービス メソッドが返す値をファイルに書き込みます。 たとえば、見込み客の一覧をファイルに書き込み、データをデータベースに書き込む前にそのデータをクリーンにするためのパッケージのデータ ソースとして、そのファイルを使用できます。  
  
## <a name="wsdl-file"></a>WSDL ファイル  
 Web サービス タスクは、HTTP 接続マネージャーを使用して Web サービスに接続します。 HTTP 接続マネージャーは、Web サービス タスクとは別に構成され、タスク内で参照されます。 HTTP 接続マネージャーは、サーバーの URL、Web サービスのサーバーにアクセスするための資格情報、タイムアウト長などの、サーバーのプロキシ設定を指定します。 詳細については、「 [HTTP 接続マネージャー](../../integration-services/connection-manager/http-connection-manager.md)」を参照してください。  
  
> [!IMPORTANT]  
>  HTTP 接続マネージャーでは、匿名認証と基本認証のみがサポートされています。 Windows 認証はサポートされていません。  
  
 HTTP 接続マネージャーは、Web サイトまたは Web サービス記述言語 (WSDL) ファイルを参照できます。 WSDL ファイルを参照する HTTP 接続マネージャーの URL には、 `?WSDL` パラメーターが含まれます。たとえば、 `https://MyServer/MyWebService/MyPage.asmx?WSDL`と指定します。  
  
 **デザイナーで用意されている** [Web サービス タスク エディター] [!INCLUDE[ssIS](../../includes/ssis-md.md)] ダイアログ ボックスを使用して Web サービス タスクを構成するには、WSDL ファイルがローカルで使用できる必要があります。  
  
-   HTTP 接続マネージャーが Web サイトを参照する場合、WSDL ファイルを手動でローカル コンピューターにコピーする必要があります。  
  
-   HTTP 接続マネージャーが WSDL ファイルを参照する場合、Web サービス タスクを使用して、Web サイトからその WSDL ファイルをローカル ファイルにダウンロードできます。  
  
 WSDL ファイルには、Web サービスが提供するメソッド、メソッドに必要な入力パラメーター、メソッドが返す応答、および Web サービスとの通信方法が一覧表示されます。  
  
 メソッドが入力パラメーターを使用する場合、Web サービス タスクにはパラメーター値が必要です。 たとえば、身長に基づいて購入するスキーの長さをアドバイスする Web サービス メソッドでは、入力パラメーターに身長を送信する必要があります。 パラメーター値は、タスク内で定義されている文字列、またはタスクのスコープか親コンテナーで定義されている変数によって指定できます。 変数を使用すると、パッケージ構成またはスクリプトを使用してパラメーター値を動的に更新できるという利点があります。 詳細については、「[Integration Services (SSIS) の変数](../../integration-services/integration-services-ssis-variables.md)」と「[パッケージ構成](../../integration-services/packages/package-configurations.md)」を参照してください。  
  
 多くの Web サービス メソッドでは、入力パラメーターを使用しません。 たとえば、今月が誕生月の大統領の名前を取得する Web サービス メソッドでは、入力パラメーターは必要ありません。これは、Web サービスで現在の月をローカルに判別できるためです。  
  
 Web サービス メソッドの結果は、変数またはファイルに書き込むことができます。 結果を書き込むファイルを指定するか、変数の名前を指定するには、ファイル接続マネージャーを使用します。 詳細については、「[ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)」および「[Integration Services (SSIS) の変数](../../integration-services/integration-services-ssis-variables.md)」を参照してください。  
  
## <a name="custom-logging-messages-available-on-the-web-service-task"></a>Web サービス タスクで使用できるカスタム ログ メッセージ  
 次の表は、Web サービス タスクに対して有効にできるカスタム ログ エントリの一覧です。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**WSTaskBegin**|タスクが Web サービスへのアクセスを開始しました。|  
|**WSTaskEnd**|タスクが Web サービス メソッドを完了しました。|  
|**WSTaskInfo**|タスクに関する説明情報を提供します。|  
  
## <a name="configuration-of-the-web-service-task"></a>Web サービス タスクの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-web-service-task"></a>プログラムによる Web サービス タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.WebServiceTask.WebServiceTask>  
  
## <a name="web-service-task-editor-general-page"></a>[Web サービス タスク エディター] ([全般] ページ)
  **[Web サービス タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、HTTP 接続マネージャーの指定、Web サービス タスクで使用する WSDL (Web サービス記述言語) ファイルの場所の指定、Web サービス タスクの記述、WSDL ファイルのダウンロードなどの操作を実行できます。  
  
### <a name="options"></a>オプション  
 **[HTTPConnection]**  
 接続マネージャーを一覧から選択するか、\<[**新しい接続...>]** をクリックして新しい接続マネージャーを作成します。  
  
> [!IMPORTANT]  
>  HTTP 接続マネージャーでは、匿名認証と基本認証のみがサポートされています。 Windows 認証はサポートされていません。  
  
 **関連トピック:** [HTTP 接続マネージャー](../../integration-services/connection-manager/http-connection-manager.md)、[HTTP 接続マネージャー エディター &#40;[サーバー] ページ&#41;](../../integration-services/connection-manager/http-connection-manager-editor-server-page.md)  
  
 **[WSDLFile]**  
 コンピューターのローカルにある WSDL ファイルの完全修飾パスを入力するか、参照ボタン ( **[...]** ) をクリックしてファイルを指定します。  
  
 WSDL ファイルを既に手動でコンピューターにダウンロードしている場合は、そのファイルを選択します。 ただし、WSDL ファイルをまだダウンロードしていない場合は、次の手順に従います。  
  
-   ファイル名拡張子が ".wsdl" の空のファイルを作成します。  
  
-   **[WSDLFile]** オプションで、この空のファイルを選択します。  
  
-   **[OverwriteWSDLFile]** の値を **True** に設定して、空のファイルを実際の WSDL ファイルで上書きできるようにします。  
  
-   **[WSDL のダウンロード]** をクリックして実際の WSDL ファイルをダウンロードし、空のファイルを上書きします。  
  
    > [!NOTE]  
    >  **[WSDL のダウンロード]** オプションは、 **[WSDLFile]** ボックスに既存のローカル ファイルの名前を指定するまで有効になりません。  
  
 **[OverwriteWSDLFile]**  
 Web サービス タスクの WSDL ファイルを上書きできるかどうかを示します。  
  
 **[WSDL のダウンロード]** ボタンを使用して WSDL ファイルをダウンロードする場合は、この値を **True**に設定します。  
  
 **[名前]**  
 Web サービス タスクの一意な名前を指定します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 Web サービス タスクの説明を入力します。  
  
 **[WSDL のダウンロード]**  
 WSDL ファイルをダウンロードします。  
  
 このボタンは、 **[WSDLFile]** ボックスに既存のローカル ファイルの名前を指定するまで有効になりません。  
  
## <a name="web-service-task-editor-input-page"></a>[Web サービス タスク エディター] ([入力] ページ)
  **[Web サービス タスク エディター]** ダイアログ ボックスの **[入力]** ページを使用すると、Web サービス、Web メソッド、および Web メソッドの入力値を指定できます。 値を指定するには、[値] 列に直接文字列を入力するか、[値] 列から変数を選択します。  
  
### <a name="options"></a>オプション  
 **サービス**  
 Web メソッドを実行するために使用する Web サービスを一覧から選択します。  
  
 **方法**  
 タスクで実行する Web メソッドを一覧から選択します。  
  
 **[WebMethodDocumentation]**  
 Web メソッドの説明を入力するか、参照ボタン ( **[...]** ) をクリックして **[Web メソッド ドキュメント]** ダイアログ ボックスに説明を入力します。  
  
 **[名前]**  
 Web メソッドへの入力の名前を一覧表示します。  
  
 **Type**  
 入力のデータ型を一覧表示します。  
  
> [!NOTE]  
>  Web サービス タスクがサポートするパラメーターのデータ型は、整数や文字列などのプリミティブ型、プリミティブ型の配列とシーケンス、および列挙型のみです。  
  
 **変数**  
 変数を使って入力値を指定する場合は、チェック ボックスをオンにします。  
  
 **Value**  
 [Variable] のチェック ボックスをオンにした場合、一覧から変数を選択して入力値を指定します。それ以外の場合は、入力値として使用する値をキーボードから入力します。  
  
## <a name="web-service-task-editor-output-page"></a>[Web サービス タスク エディター] ([出力] ページ)
  **[Web サービス タスク エディター]** ダイアログ ボックスの **[出力]** ページを使用すると、Web メソッドから返された結果を格納する場所を指定できます。  
  
### <a name="static-options"></a>静的オプション  
 **[OutputType]**  
 結果を格納するときに使用するストレージ型を選択します。 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[ファイル接続]**|結果をファイルに格納します。 この値を選択すると、動的オプションの **[ファイル]** が表示されます。|  
|**変数**|結果を変数に格納します。 この値を選択すると、動的オプションの **[変数]** が表示されます。|  
  
### <a name="outputtype-dynamic-options"></a>[OutputType] の動的オプション  
  
#### <a name="outputtype--file-connection"></a>[OutputType] = [ファイル接続]  
 **[最近使ったファイル]**  
 ファイル接続マネージャーを一覧から選択するか、\<[**新しい接続...>]** をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="outputtype--variable"></a>[OutputType] = [変数]  
 **変数**  
 一覧で変数を選択するか、\<[**新しい変数...>]** をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
  
## <a name="related-content"></a>関連コンテンツ  
 MSDN ライブラリのビデオ「[Web サービス タスクを使用して Web サービスを呼び出す方法 (SQL Server ビデオ)](https://go.microsoft.com/fwlink/?LinkId=259642) (technet.microsoft.com)  
