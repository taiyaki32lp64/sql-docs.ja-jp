---
title: Integration Services (SSIS) のログ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], logs
- Windows Event log provider [Integration Services]
- XML File log provider [Integration Services]
- SQL Server Profiler, log provider
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- tasks [Integration Services], logs
- logs [Integration Services], log providers
- Integration Services packages, logs
- log providers [Integration Services]
- packages [Integration Services], logs
- Text File log provider
- SQL Server log provider
ms.assetid: 65e17889-371f-4951-9a7e-9932b2d0dcde
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2478f1605b7fb67d8328be905956cbaae8e3c243
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62889814"
---
# <a name="integration-services-ssis-logging"></a>Integration Services (SSIS) のログ記録
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、パッケージ、コンテナー、およびタスクにログ記録を実装するために使用できる、ログ プロバイダーが含まれています。 ログ記録を行うと、パッケージに関する実行時の情報をキャプチャできるので、パッケージを実行するたびに監査やトラブルシューティングに役立ちます。 たとえば、パッケージを実行した演算子の名前と、パッケージの開始および完了時刻をログにキャプチャできます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーでのパッケージ実行中に発生するログ記録のスコープを構成できます。 詳細については、「 [SSIS サーバーでのパッケージ実行のログ記録を有効にする](../enable-logging-for-package-execution-on-the-ssis-server.md)」を参照してください。  
  
 **dtexec** コマンド プロンプト ユーティリティを使用してパッケージを実行する際にも、ログ記録を使用できます。 ログ記録をサポートするコマンド プロンプトの引数の詳細については、「 [dtexec Utility](../packages/dtexec-utility.md)」を参照してください。  
  
## <a name="configure-logging-in-sql-server-data-tools"></a>SQL Server Data Tools でのログ記録の構成  
 ログはパッケージに関連付けられ、パッケージ レベルで設定します。 パッケージ内の各タスクやコンテナーによって、パッケージのログに情報を書き込むこともできます。 パッケージのログ機能が有効にされていない場合でも、そのパッケージに含まれるタスクやコンテナーのログ機能を有効にできます。 たとえば、親パッケージのログ機能を有効にしなくても、SQL 実行タスクのログ機能を有効にできます。 パッケージ、コンテナー、およびタスクは、複数のログに対して書き込みが可能です。 パッケージにのみログ機能を有効にできます。または、そのパッケージに含まれる任意の個別のタスクまたはコンテナーを選択して、ログ機能を有効にできます。  
  
 パッケージにログを追加するには、ログ プロバイダーとログの場所を選択します。 ログ プロバイダーは、ログ データの形式を指定します。たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースやテキスト ファイルなどを指定できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、次のログ プロバイダーが含まれています。  
  
-   テキスト ファイルのログ プロバイダー。ログ エントリを、コンマ区切り (CSV) 形式で、ASCII テキスト ファイルに書き込みます。 このプロバイダーで使用されるファイル名の既定の拡張子は、.log です。  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] のログ プロバイダー。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler を使用して表示できるトレースを書き込みます。 このプロバイダーで使用されるファイル名の既定の拡張子は、.trc です。  
  
    > [!NOTE]  
    >  64 ビット モードで実行されているパッケージでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] のログ プロバイダーを使用できません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログ エントリを書き込むログ プロバイダー、`sysssislog`テーブルに、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース。  
  
-   Windows イベント ログのログ プロバイダー。エントリを、ローカル コンピューター上にある Windows イベント ログのアプリケーション ログに書き込みます。  
  
-   XML ファイルのログ プロバイダー。ログ ファイルを XML ファイルに書き込みます。 このプロバイダーで使用されるファイル名の既定の拡張子は、.xml です。  
  
 ログ プロバイダーをパッケージに追加したり、ログ記録をプログラムによって構成する場合、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[SSIS ログの構成]** ダイアログ ボックスに表示される名前を使用せず、ProgID または ClassID のどちらかを使用してログ プロバイダーを識別できます。  
  
 次の表に、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれるログ プロバイダーの ProgID と ClassID、およびログ プロバイダーが書き込むログの場所の一覧を示します。  
  
|ログ プロバイダー|ProgID|ClassID|場所|  
|------------------|------------|-------------|--------------|  
|テキスト ファイル|DTS.LogProviderTextFile|{0A039101-ACC1-4E06-943F-279948323883}|ログ プロバイダーが使用するファイル接続マネージャーでテキスト ファイルのパスを指定します。|  
|SQL Server Profiler|DTS.LogProviderSQLProfiler|{E93F6300-AE0C-4916-A7BF-A8D0CE12C77A}|ログ プロバイダーが使用するファイル接続マネージャーで [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]が使用するファイルのパスを指定します。|  
|SQL Server|DTS.LogProviderSQLServer|{94150B25-6AEB-4C0D-996D-D37D1C4FDEDA}|ログ プロバイダーが使用する OLE DB 接続マネージャーで、ログ エントリ用の sysssislog テーブルを格納する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを指定します。|  
|Windows イベント ログ|DTS.LogProviderEventLog|{071CC8EB-C343-4CFF-8D58-564B92FCA3CF}|Windows イベント ビューアーのアプリケーション ログには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のログ情報が表示されます。|  
|XML ファイル|DTS.LogProviderXMLFile|{440945A4-2A22-4F19-B577-EAF5FDDC5F7A}|ログ プロバイダーが使用するファイル接続マネージャーで XML ファイルのパスを指定します。|  
  
 また、カスタム ログ プロバイダーを作成することもできます。 詳細については、「 [Creating a Custom Log Provider](../extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)」を参照してください。  
  
 パッケージ内のログ プロバイダーは、パッケージのログ プロバイダー コレクションのメンバーです。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーを使用してパッケージを作成し、ログ記録を実装する際、 **デザイナーの** [パッケージ エクスプローラー] **タブ上の** [ログ プロバイダー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] フォルダーに、コレクション メンバーの一覧が表示されます。  
  
 ログ プロバイダーを構成するには、ログ プロバイダーの名前と説明を入力し、ログ プロバイダーが使用する接続マネージャーを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログ プロバイダーでは、OLE DB 接続マネージャーが使用されます。 テキスト ファイル、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]、および XML ファイルのログ プロバイダーでは、ファイル接続マネージャーが使用されます。 Windows イベント ログのログ プロバイダーでは、Windows イベント ログに直接書き込まれるので、接続マネージャーが使用されません。 詳細については、「 [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md) 」および「 [File Connection Manager](../connection-manager/file-connection-manager.md)」を参照してください。  
  
### <a name="logging-customization"></a>ログ記録のカスタマイズ  
 イベント メッセージまたはカスタム メッセージのログ機能をカスタマイズするために、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、ログ エントリに通常書き込まれる情報のスキーマが用意されています。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のログ スキーマは、ログ記録できる情報を定義します。 ログ エントリごとにログ スキーマから要素を選択します。  
  
 パッケージおよびパッケージ内のコンテナーやタスクが、同じ情報をログ記録する必要はありません。また、同一パッケージやコンテナーのタスクが別々の情報をログ記録することができます。 たとえば、パッケージではパッケージが開始されたときにオペレーターに関する情報をログに書き込み、あるタスクではタスク失敗の原因を書き込み、別のタスクではエラー発生時に情報を書き込むという処理が可能です。 パッケージおよびパッケージ内のコンテナーやタスクが複数のログを使用する場合、同じ情報がすべてのログに書き込まれます。  
  
 ログ記録するイベントと各イベントに対して書き込む情報を指定して、必要に応じたログ記録のレベルを選択できます。 これにより、他のイベントに比べて有益な情報が得られるイベントがわかります。 たとえば、 **PreExecute** イベントについてはコンピューター名とオペレーター名のみをログ記録し、 **Error** イベントについては利用可能なすべての情報を記録するとよいでしょう。  
  
 ログ ファイルがディスク領域を大量に消費したり、過剰にログが記録されたりするとパフォーマンスが低下します。これを防止するため、特定のイベントとログ記録する情報項目を選択して、ログ記録を制限することができます。 たとえば、エラーが発生した日付とコンピューター名のみを記録するようにログを設定できます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[SSIS ログの構成]** ダイアログ ボックスを使用して、ログ オプションを定義できます。  
  
#### <a name="log-schema"></a>ログ スキーマ  
 次の表に、ログ スキーマの要素を示します。  
  
|要素|説明|  
|-------------|-----------------|  
|[Computer]|ログ イベントが発生したコンピューターの名前。|  
|演算子|パッケージを起動したユーザーの ID。|  
|SourceName|ログ イベントが発生したコンテナーまたはタスクの名前。|  
|[SourceID]|ログ イベントが発生したパッケージ、For ループ コンテナー、Foreach ループ コンテナー、シーケンス コンテナー、またはタスクの一意識別子。|  
|[ExecutionID]|パッケージ実行インスタンスの GUID。<br /><br /> 注:単一のパッケージを実行すると、ExecutionID 要素の値が異なるログ エントリが作成される場合があります。 たとえば、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で 1 つのパッケージを実行すると、検証フェーズでは [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]に対応する ExecutionID 要素を持つログ エントリが作成されます。 一方、実行フェーズでは、dtshost.exe に対応する ExecutionID 要素を持つログ エントリが作成されます。 また、パッケージ実行タスクを含むパッケージを実行すると、これらの各タスクで子パッケージが実行されます。 これらの子パッケージでは、親パッケージが作成するログ エントリとは異なる ExecutionID 要素を持つログ エントリが作成される場合があります。|  
|[MessageText]|ログ エントリに関連付けられているメッセージ。|  
|[DataBytes]|ログ エントリ固有のバイト配列。 このフィールドの意味は、ログ エントリによって異なります。|  
  
 次の表は、 **[SSIS ログの構成]** ダイアログ ボックスの **[詳細]** タブでは利用できないログ スキーマ内の 3 つの追加要素について説明しています。  
  
|要素|説明|  
|-------------|-----------------|  
|StartTime|コンテナーまたはタスクの実行が開始した時間。|  
|EndTime|コンテナーまたはタスクの実行が停止した時間。|  
|DataCode|コンテナーまたはタスクの実行結果を示す <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 列挙体の値を通常含んだ整数値 (省略可能)。<br /><br /> 0 - 成功<br /><br /> 1 - 失敗<br /><br /> 2 - 完了<br /><br /> 3 - キャンセル|  
  
##### <a name="log-entries"></a>ログ エントリ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、あらかじめ定義されたイベントのログ エントリをサポートし、多くの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクトにカスタム ログ エントリを提供します。 **デザイナーの** [SSIS ログの構成] [!INCLUDE[ssIS](../../includes/ssis-md.md)] ダイアログ ボックスに、これらのイベントとカスタム ログ エントリが一覧表示されます。  
  
 次の表に、実行時イベント発生時にログ エントリを書き込むために有効にできる、あらかじめ定義されたイベントを示します。 これらのログ エントリは、実行可能ファイル、パッケージ、そのパッケージに含まれるタスクおよびコンテナーに適用されます。 ログ エントリ名は、ログ エントリが書き込まれる原因となった、発生実行時イベントの名前と同じです。  
  
|イベント|説明|  
|------------|-----------------|  
|**OnError**|エラー発生時にログ エントリを書き込みます。|  
|**OnExecStatusChanged**|デバッグ中に (コンテナー以外の) タスクが中断または再開されたときにログ エントリを書き込みます。|  
|**OnInformation**|実行可能ファイルの検証および実行中に、情報を報告するログ エントリを書き込みます。|  
|**OnPostExecute**|実行可能ファイルの実行が終了した直後にログ エントリを書き込みます。|  
|**OnPostValidate**|実行可能ファイルの検証が終了したときにログ エントリを書き込みます。|  
|**OnPreExecute**|実行可能ファイルの実行直前にログ エントリを書き込みます。|  
|**OnPreValidate**|実行可能ファイルの検証が開始される前にログ エントリを書き込みます。|  
|**OnProgress**|実行可能ファイルの処理で測定可能な進捗があったときにログ エントリを書き込みます。|  
|**OnQueryCancel**|タスク処理中に、実行のキャンセルが可能な時点に達したときにログ エントリを書き込みます。|  
|**OnTaskFailed**|タスクが失敗したときにログ エントリを書き込みます。|  
|**OnVariableValueChanged**|変数の値が変更されたときにログ エントリを書き込みます。|  
|**OnWarning**|警告が発生したときにログ エントリを書き込みます。|  
|**PipelineComponentTime**|各データ フロー コンポーネントに対する検証および実行の各フェーズのログ エントリを書き込みます。 ログ エントリは、各フェーズの処理時間を示します。|  
|**Diagnostic**|診断情報を提供するログ エントリを書き込みます。<br /><br /> たとえば、外部データ プロバイダーを呼び出す前と後にメッセージをログに書き込むことができます。 詳細については、「 [パッケージ実行のトラブルシューティング ツール](../troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。|  
  
 パッケージおよび多くのタスクには、ログ機能を有効にできるカスタム ログ エントリがあります。 たとえば、メール送信タスクには **SendMailTaskBegin** カスタム ログ エントリがあります。これを使用すると、電子メール メッセージの送信前に、メール送信タスクの実行開始時の情報をログに書き込むことができます。 詳細については、「 [Custom Messages for Logging](../custom-messages-for-logging.md)」を参照してください。  
  
### <a name="differentiating-package-copies"></a>パッケージのコピーの区別  
 ログ データには、ログ エントリが属しているパッケージの名前と GUID が含まれます。 既存のパッケージをコピーして新しいパッケージを作成する場合、既存のパッケージの名前と GUID もコピーされます。 したがって、同じ GUID と名前が付いたパッケージが 2 つになり、ログ データ内のパッケージの区別が困難になります。  
  
 このようなあいまいさを回避するには、新しいパッケージの名前と GUID を更新する必要があります。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] のプロパティ ウィンドウで、`ID` プロパティの GUID を再生成し、`Name` の値を更新できます。 プログラムから、または **dtutil** コマンド プロンプトを使用して、GUID と名前を変更することもできます。 詳細については、「 [パッケージのプロパティを設定する](../set-package-properties.md) 」と「 [dtutil ユーティリティ](../dtutil-utility.md)」を参照してください。  
  
### <a name="parent-logging-options"></a>親のログ オプション  
 一般的に、タスク、For ループ コンテナー、Foreach ループ コンテナー、シーケンス コンテナーのログ オプションは、それらが含まれているパッケージや親コンテナーのログ オプションと同じです。 この場合、親コンテナーからログ オプションを継承するように設定できます。 たとえば、SQL 実行タスクが含まれている For ループ コンテナーがある場合、SQL 実行タスクでは For ループ コンテナーに設定されたログ オプションを使用できます。 親のログ オプションを使用するには、コンテナーの LoggingMode プロパティを **UseParentSetting**に設定します。 このプロパティは、 **の** [プロパティ] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ウィンドウ、または **デザイナーの** [SSIS ログの構成] [!INCLUDE[ssIS](../../includes/ssis-md.md)] ダイアログ ボックスで設定できます。  
  
### <a name="logging-templates"></a>ログのテンプレート  
 **[SSIS ログの構成]** ダイアログ ボックスでは、頻繁に使用するログ構成をテンプレートとして作成および保存して、複数のパッケージでそのテンプレート使用できます。 これにより、複数のパッケージで一貫したログ記録の方法を簡単に使用でき、テンプレートを更新して適用することによって簡単にパッケージのログ設定を修正できます。 テンプレートは XML ファイルとして格納されます。  
  
 **[SSIS ログの構成] ダイアログ ボックスを使用してログ機能を設定するには**  
  
1.  パッケージおよびタスクのログ記録を有効にします。 ログは、パッケージ レベル、コンテナー レベル、またはタスク レベルで記録できます。 パッケージ、コンテナー、タスクに対して、それぞれ異なるログを指定できます。  
  
2.  ログ プロバイダーを選択して、パッケージのログを追加します。 ログはパッケージ レベルでのみ作成可能で、タスクやコンテナーではパッケージで作成されたログのいずれかを使用します。 各ログは、テキスト ファイル、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Windows のイベント ログ、または XML ファイルのいずれかのログ プロバイダーに関連付けられます。 詳細については、「 [SQL Server Data Tools でパッケージのログ記録を有効にする](../enable-package-logging-in-sql-server-data-tools.md)」を参照してください。  
  
3.  ログに取り込むイベントと、各イベントのログ スキーマ情報を選択します。 詳細については、「 [保存されている構成ファイルを使用してログ記録を構成する](../configure-logging-by-using-a-saved-configuration-file.md)」を参照してください。  
  
### <a name="configuration-of-log-provider"></a>ログ プロバイダーの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 ログ プロバイダーは、パッケージにログ記録を実装する手順の中で作成して構成します。 詳細については、次を参照してください。 [Integration Services のログ記録](integration-services-ssis-logging.md)します。  
  
 ログ プロバイダーを作成した後にプロパティを表示および変更するには、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のプロパティ ウィンドウを使用します。  
  
 プログラムによってこれらのプロパティを設定する方法の詳細については、 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> クラスのドキュメントを参照してください。  
  
### <a name="logging-for-data-flow-tasks"></a>データ フロー タスクのログ機能の構成  
 データ フロー タスクには、パフォーマンスの監視と調整に使用できるカスタム ログ エントリが数多くあります。 たとえば、メモリ リークを起こす可能性のあるコンポーネントを監視したり、特定のコンポーネントの実行所要時間を追跡できます。 カスタム ログ エントリの一覧とサンプルのログ出力については、「 [Data Flow Task](../control-flow/data-flow-task.md)」を参照してください。  
  
#### <a name="use-the-pipelinecomponenttime-event"></a>PipelineComponentTime イベントの使用  
 カスタム ログ エントリの中で最も役に立つのは、PipelineComponentTime イベントです。 このログ エントリは、データ フローの各コンポーネントが主要な 5 つの処理手順それぞれで要するミリ秒数を報告します。 次の表で、これらの処理手順について説明します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の開発者は、これらの手順を <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>」を参照してください。  
  
|手順|説明|  
|----------|-----------------|  
|[検証]|コンポーネントは、有効なプロパティ値と構成設定を確認します。|  
|PreExecute|コンポーネントは、データ行の処理を開始する前に 1 回限りの処理を実行します。|  
|PostExecute|コンポーネントは、すべてのデータ行を処理した後に 1 回限りの処理を実行します。|  
|ProcessInput|変換コンポーネントまたは変換先コンポーネントは、上流変換元または変換から渡されたデータの受信行を処理します。|  
|PrimeOutput|変換元コンポーネントまたは変換コンポーネントは、下流変換コンポーネントまたは変換先コンポーネントに渡されるデータのバッファーを入力します。|  
  
 PipelineComponentTime イベントを有効にすると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、各コンポーネントが実行した処理手順ごとに 1 つのメッセージをログに記録します。 以下のログ エントリに、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] CalculatedColumns パッケージ サンプルでログに記録されるメッセージのサブセットを示します。  
  
 `The component "Calculate LineItemTotalCost" (3522) spent 356 milliseconds in ProcessInput.`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 79 milliseconds in ProcessInput.`  
  
 `The component "Calculate Average Cost" (3662) spent 16 milliseconds in ProcessInput.`  
  
 `The component "Sort by ProductID" (3717) spent 125 milliseconds in ProcessInput.`  
  
 `The component "Load Data" (3773) spent 0 milliseconds in ProcessInput.`  
  
 `The component "Extract Data" (3869) spent 688 milliseconds in PrimeOutput filling buffers on output "OLE DB Source Output" (3879).`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 141 milliseconds in PrimeOutput filling buffers on output "Aggregate Output 1" (3621).`  
  
 `The component "Sort by ProductID" (3717) spent 16 milliseconds in PrimeOutput filling buffers on output "Sort Output" (3719).`  
  
 これらのログ エントリは、データ フロー タスクが、次の手順にほとんどの時間を要することを示しています。ここでは、手順を降順に示します。  
  
-   "Extract Data" という名前の OLE DB ソースは、データの読み込みに 688 ミリ秒費やしました。 データの読み込み  
  
-   "Calculate LineItemTotalCost" という名前の派生列変換は、 受信行での計算の実行に 356 ミリ秒費やしました。  
  
-   "Sum Quantity and LineItemTotalCost" という名前の集計変換は、計算の実行と次の変換へのデータの受け渡しに合計 220 ミリ秒 (PrimeOutput に 141 ミリ秒、ProcessInput に 79 秒) 費やしました。  
  
## <a name="related-tasks"></a>Related Tasks  
 次の一覧では、ログ記録機能に関連するタスクの実行方法を示すトピックへのリンクを示します。  
  
-   [[SSIS ログの構成] ダイアログ ボックス](../configure-ssis-logs-dialog-box.md)  
  
-   [SQL Server Data Tools でパッケージのログ記録を有効にする](../enable-package-logging-in-sql-server-data-tools.md)  
  
-   [SSIS サーバーでのパッケージ実行のログ記録を有効にする](../enable-logging-for-package-execution-on-the-ssis-server.md)  
  
-   [[ログ イベント] ウィンドウでログ エントリを表示する](../view-log-entries-in-the-log-events-window.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [完全かつ詳細なログ記録用の DTLoggedExec ツール (CodePlex プロジェクト)](https://go.microsoft.com/fwlink/?LinkId=150579)  
  
## <a name="see-also"></a>参照  
 [[ログ イベント] ウィンドウでログ エントリを表示する](../view-log-entries-in-the-log-events-window.md)  
  
  
