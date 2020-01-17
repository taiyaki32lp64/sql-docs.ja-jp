---
title: Integration Services (SSIS) のログ | Microsoft Docs
ms.custom: supportability
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.configuredtslogs.containers.f1
- sql13.dts.designer.configuredtslogs.loggingdetails.f1
- sql13.dts.designer.configuredtslogs.providersandlogs.f1
- SQL13.SSIS.SSMS.ISMANAGECUSTOMIZEDLOGGINGLEVEL.F1
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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: baad15da62c4452361fe8ff3cdf46582dd3727ea
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71282564"
---
# <a name="integration-services-ssis-logging"></a>Integration Services (SSIS) のログ記録

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、パッケージ、コンテナー、およびタスクにログ記録を実装するために使用できる、ログ プロバイダーが含まれています。 ログ記録を行うと、パッケージに関する実行時の情報をキャプチャできるので、パッケージを実行するたびに監査やトラブルシューティングに役立ちます。 たとえば、パッケージを実行した演算子の名前と、パッケージの開始および完了時刻をログにキャプチャできます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーでのパッケージ実行中に発生するログ記録のスコープを構成できます。 詳細については、「 [SSIS サーバーでのパッケージ実行のログ記録を有効にする](#server_logging)」を参照してください。  
  
 **dtexec** コマンド プロンプト ユーティリティを使用してパッケージを実行する際にも、ログ記録を使用できます。 ログ記録をサポートするコマンド プロンプトの引数の詳細については、「 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)」を参照してください。  
  
## <a name="configure-logging-in-sql-server-data-tools"></a>SQL Server Data Tools でのログ記録の構成  
 ログはパッケージに関連付けられ、パッケージ レベルで設定します。 パッケージ内の各タスクやコンテナーによって、パッケージのログに情報を書き込むこともできます。 パッケージのログ機能が有効にされていない場合でも、そのパッケージに含まれるタスクやコンテナーのログ機能を有効にできます。 たとえば、親パッケージのログ機能を有効にしなくても、SQL 実行タスクのログ機能を有効にできます。 パッケージ、コンテナー、およびタスクは、複数のログに対して書き込みが可能です。 パッケージにのみログ機能を有効にできます。または、そのパッケージに含まれる任意の個別のタスクまたはコンテナーを選択して、ログ機能を有効にできます。  
  
 パッケージにログを追加するには、ログ プロバイダーとログの場所を選択します。 ログ プロバイダーは、ログ データの形式を指定します。たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースやテキスト ファイルなどを指定できます。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、次のログ プロバイダーが含まれています。  
  
-   テキスト ファイルのログ プロバイダー。ログ エントリを、コンマ区切り (CSV) 形式で、ASCII テキスト ファイルに書き込みます。 このプロバイダーで使用されるファイル名の既定の拡張子は、.log です。  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] のログ プロバイダー。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler を使用して表示できるトレースを書き込みます。 このプロバイダーで使用されるファイル名の既定の拡張子は、.trc です。  
  
    > [!NOTE]  
    >  64 ビット モードで実行されているパッケージでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] のログ プロバイダーを使用できません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログ プロバイダー。ログ エントリを、 **データベースの** sysssislog [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに書き込みます。  
  
-   Windows イベント ログのログ プロバイダー。エントリを、ローカル コンピューター上にある Windows イベント ログのアプリケーション ログに書き込みます。  
  
-   XML ファイルのログ プロバイダー。ログ ファイルを XML ファイルに書き込みます。 このプロバイダーで使用されるファイル名の既定の拡張子は、.xml です。  
  
 ログ プロバイダーをパッケージに追加したり、ログ記録をプログラムによって構成する場合、 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[SSIS ログの構成]** ダイアログ ボックスに表示される名前を使用せず、ProgID または ClassID のどちらかを使用してログ プロバイダーを識別できます。  
  
 次の表に、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に含まれるログ プロバイダーの ProgID と ClassID、およびログ プロバイダーが書き込むログの場所の一覧を示します。  
  
|ログ プロバイダー|ProgID|ClassID|Location|  
|------------------|------------|-------------|--------------|  
|テキスト ファイル|DTS.LogProviderTextFile|{0A039101-ACC1-4E06-943F-279948323883}|ログ プロバイダーが使用するファイル接続マネージャーでテキスト ファイルのパスを指定します。|  
|SQL Server プロファイラー|DTS.LogProviderSQLProfiler|{E93F6300-AE0C-4916-A7BF-A8D0CE12C77A}|ログ プロバイダーが使用するファイル接続マネージャーで [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]が使用するファイルのパスを指定します。|  
|SQL Server|DTS.LogProviderSQLServer|{94150B25-6AEB-4C0D-996D-D37D1C4FDEDA}|ログ プロバイダーが使用する OLE DB 接続マネージャーで、ログ エントリ用の sysssislog テーブルを格納する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを指定します。|  
|Windows イベント ログ|DTS.LogProviderEventLog|{071CC8EB-C343-4CFF-8D58-564B92FCA3CF}|Windows イベント ビューアーのアプリケーション ログには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のログ情報が表示されます。|  
|XML ファイル|DTS.LogProviderXMLFile|{440945A4-2A22-4F19-B577-EAF5FDDC5F7A}|ログ プロバイダーが使用するファイル接続マネージャーで XML ファイルのパスを指定します。|  
  
 また、カスタム ログ プロバイダーを作成することもできます。 詳細については、「 [Creating a Custom Log Provider](../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)」を参照してください。  
  
 パッケージ内のログ プロバイダーは、パッケージのログ プロバイダー コレクションのメンバーです。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーを使用してパッケージを作成し、ログ記録を実装する際、 **デザイナーの** [パッケージ エクスプローラー] **タブ上の** [ログ プロバイダー] [!INCLUDE[ssIS](../../includes/ssis-md.md)] フォルダーに、コレクション メンバーの一覧が表示されます。  
  
 ログ プロバイダーを構成するには、ログ プロバイダーの名前と説明を入力し、ログ プロバイダーが使用する接続マネージャーを指定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のログ プロバイダーでは、OLE DB 接続マネージャーが使用されます。 テキスト ファイル、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]、および XML ファイルのログ プロバイダーでは、ファイル接続マネージャーが使用されます。 Windows イベント ログのログ プロバイダーでは、Windows イベント ログに直接書き込まれるので、接続マネージャーが使用されません。 詳細については、「 [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md) 」および「 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)」を参照してください。  
  
### <a name="logging-customization"></a>ログ記録のカスタマイズ  
 イベント メッセージまたはカスタム メッセージのログ機能をカスタマイズするために、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、ログ エントリに通常書き込まれる情報のスキーマが用意されています。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のログ スキーマは、ログ記録できる情報を定義します。 ログ エントリごとにログ スキーマから要素を選択します。  
  
 パッケージおよびパッケージ内のコンテナーやタスクが、同じ情報をログ記録する必要はありません。また、同一パッケージやコンテナーのタスクが別々の情報をログ記録することができます。 たとえば、パッケージではパッケージが開始されたときにオペレーターに関する情報をログに書き込み、あるタスクではタスク失敗の原因を書き込み、別のタスクではエラー発生時に情報を書き込むという処理が可能です。 パッケージおよびパッケージ内のコンテナーやタスクが複数のログを使用する場合、同じ情報がすべてのログに書き込まれます。  
  
 ログ記録するイベントと各イベントに対して書き込む情報を指定して、必要に応じたログ記録のレベルを選択できます。 これにより、他のイベントに比べて有益な情報が得られるイベントがわかります。 たとえば、 **PreExecute** イベントについてはコンピューター名とオペレーター名のみをログ記録し、 **Error** イベントについては利用可能なすべての情報を記録するとよいでしょう。  
  
 ログ ファイルがディスク領域を大量に消費したり、過剰にログが記録されたりするとパフォーマンスが低下します。これを防止するため、特定のイベントとログ記録する情報項目を選択して、ログ記録を制限することができます。 たとえば、エラーが発生した日付とコンピューター名のみを記録するようにログを設定できます。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの **[SSIS ログの構成]** ダイアログ ボックスを使用して、ログ オプションを定義できます。  
  
#### <a name="log-schema"></a>ログ スキーマ  
 次の表に、ログ スキーマの要素を示します。  
  
|要素|[説明]|  
|-------------|-----------------|  
|[Computer]|ログ イベントが発生したコンピューターの名前。|  
|演算子|パッケージを起動したユーザーの ID。|  
|SourceName|ログ イベントが発生したコンテナーまたはタスクの名前。|  
|[SourceID]|ログ イベントが発生したパッケージ、For ループ コンテナー、Foreach ループ コンテナー、シーケンス コンテナー、またはタスクの一意識別子。|  
|[ExecutionID]|パッケージ実行インスタンスの GUID。<br /><br /> 注:単一のパッケージを実行すると、ExecutionID 要素の値が異なるログ エントリが作成される場合があります。 たとえば、 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で 1 つのパッケージを実行すると、検証フェーズでは [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]に対応する ExecutionID 要素を持つログ エントリが作成されます。 一方、実行フェーズでは、dtshost.exe に対応する ExecutionID 要素を持つログ エントリが作成されます。 また、パッケージ実行タスクを含むパッケージを実行すると、これらの各タスクで子パッケージが実行されます。 これらの子パッケージでは、親パッケージが作成するログ エントリとは異なる ExecutionID 要素を持つログ エントリが作成される場合があります。|  
|[MessageText]|ログ エントリに関連付けられているメッセージ。|  
|[DataBytes]|ログ エントリ固有のバイト配列。 このフィールドの意味は、ログ エントリによって異なります。|  
  
 次の表は、 **[SSIS ログの構成]** ダイアログ ボックスの **[詳細]** タブでは利用できないログ スキーマ内の 3 つの追加要素について説明しています。  
  
|要素|[説明]|  
|-------------|-----------------|  
|StartTime|コンテナーまたはタスクの実行が開始した時間。|  
|EndTime|コンテナーまたはタスクの実行が停止した時間。|  
|DataCode|コンテナーまたはタスクの実行結果を示す <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> 列挙体の値を通常含んだ整数値 (省略可能)。<br /><br /> 0 - 成功<br /><br /> 1 - 失敗<br /><br /> 2 - 完了<br /><br /> 3 - キャンセル|  
  
#### <a name="log-entries"></a>ログ エントリ  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] では、あらかじめ定義されたイベントのログ エントリをサポートし、多くの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクトにカスタム ログ エントリを提供します。 **デザイナーの** [SSIS ログの構成] [!INCLUDE[ssIS](../../includes/ssis-md.md)] ダイアログ ボックスに、これらのイベントとカスタム ログ エントリが一覧表示されます。  
  
 次の表に、実行時イベント発生時にログ エントリを書き込むために有効にできる、あらかじめ定義されたイベントを示します。 これらのログ エントリは、実行可能ファイル、パッケージ、そのパッケージに含まれるタスクおよびコンテナーに適用されます。 ログ エントリ名は、ログ エントリが書き込まれる原因となった、発生実行時イベントの名前と同じです。  
  
|イベント|[説明]|  
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
|**Diagnostic**<br /><br /> **DiagnosticEx**|診断情報を提供するログ エントリを書き込みます。<br /><br /> たとえば、外部データ プロバイダーを呼び出す前と後にメッセージをログに書き込むことができます。 詳細については、「 [パッケージ実行のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。<br /><br /> エラーが発生したデータ フロー内の列の列名を調べるには、 **DiagnosticEx** イベントを記録します。 このイベントは、データ フロー系列マップをログに書き込みます。 エラー出力でキャプチャされた列識別子を使用して、この系列マップの列名を調べることができます。 詳細については、「[データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。<br /><br /> **DiagnosticEx** イベントでは XML 出力に含まれる空白が維持されないので、ログのサイズを軽減できます。 読みやすくするために、XML 書式と構文の強調表示をサポートする XML エディター (たとえば Visual Studio) にログをコピーします。<br /><br /> 注:SQL Server ログ プロバイダーを使用して **DiagnosticEx** イベントを記録する場合、出力が切り捨てられる可能性があります。 SQL Server ログ プロバイダーの **メッセージ** フィールドは、nvarchar (2048) 型です。 出力が切り捨てられないようにするには、 **DiagnosticEx** イベントを記録するときに別のログ プロバイダーを使用してください。|  
  
 パッケージおよび多くのタスクには、ログ機能を有効にできるカスタム ログ エントリがあります。 たとえば、メール送信タスクには **SendMailTaskBegin** カスタム ログ エントリがあります。これを使用すると、電子メール メッセージの送信前に、メール送信タスクの実行開始時の情報をログに書き込むことができます。 詳細については、「 [Custom Messages for Logging](#custom_messages)」を参照してください。  
  
### <a name="differentiating-package-copies"></a>パッケージのコピーの区別  
 ログ データには、ログ エントリが属しているパッケージの名前と GUID が含まれます。 既存のパッケージをコピーして新しいパッケージを作成する場合、既存のパッケージの名前と GUID もコピーされます。 したがって、同じ GUID と名前が付いたパッケージが 2 つになり、ログ データ内のパッケージの区別が困難になります。  
  
 このようなあいまいさを回避するには、新しいパッケージの名前と GUID を更新する必要があります。 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]の [プロパティ] ウィンドウで、 **ID** プロパティの GUID を再生成し、 **Name** プロパティの値を更新できます。 プログラムから、または **dtutil** コマンド プロンプトを使用して、GUID と名前を変更することもできます。 詳細については、「 [パッケージのプロパティを設定する](../../integration-services/set-package-properties.md) 」と「 [dtutil ユーティリティ](../../integration-services/dtutil-utility.md)」を参照してください。  
  
### <a name="parent-logging-options"></a>親のログ オプション  
 一般的に、タスク、For ループ コンテナー、Foreach ループ コンテナー、シーケンス コンテナーのログ オプションは、それらが含まれているパッケージや親コンテナーのログ オプションと同じです。 この場合、親コンテナーからログ オプションを継承するように設定できます。 たとえば、SQL 実行タスクが含まれている For ループ コンテナーがある場合、SQL 実行タスクでは For ループ コンテナーに設定されたログ オプションを使用できます。 親のログ オプションを使用するには、コンテナーの LoggingMode プロパティを **UseParentSetting**に設定します。 このプロパティは、 **の** [プロパティ] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] ウィンドウ、または **デザイナーの** [SSIS ログの構成] [!INCLUDE[ssIS](../../includes/ssis-md.md)] ダイアログ ボックスで設定できます。  
  
### <a name="logging-templates"></a>ログのテンプレート  
 **[SSIS ログの構成]** ダイアログ ボックスでは、頻繁に使用するログ構成をテンプレートとして作成および保存して、複数のパッケージでそのテンプレート使用できます。 これにより、複数のパッケージで一貫したログ記録の方法を簡単に使用でき、テンプレートを更新して適用することによって簡単にパッケージのログ設定を修正できます。 テンプレートは XML ファイルとして格納されます。  
  
 **[SSIS ログの構成] ダイアログ ボックスを使用してログ機能を設定するには**  
  
1.  パッケージおよびタスクのログ記録を有効にします。 ログは、パッケージ レベル、コンテナー レベル、またはタスク レベルで記録できます。 パッケージ、コンテナー、タスクに対して、それぞれ異なるログを指定できます。  
  
2.  ログ プロバイダーを選択して、パッケージのログを追加します。 ログはパッケージ レベルでのみ作成可能で、タスクやコンテナーではパッケージで作成されたログのいずれかを使用します。 各ログは、テキスト ファイル、[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、Windows のイベント ログ、または XML ファイルのいずれかのログ プロバイダーに関連付けられます。 詳細については、「 [SQL Server Data Tools でパッケージのログ記録を有効にする](#ssdt)」を参照してください。  
  
3.  ログに取り込むイベントと、各イベントのログ スキーマ情報を選択します。 詳細については、「 [保存されている構成ファイルを使用してログ記録を構成する](#saved_config)」を参照してください。  
  
### <a name="configuration-of-log-provider"></a>ログ プロバイダーの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 ログ プロバイダーは、パッケージにログ記録を実装する手順の中で作成して構成します。  
  
 ログ プロバイダーを作成した後にプロパティを表示および変更するには、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]のプロパティ ウィンドウを使用します。  
  
 プログラムによってこれらのプロパティを設定する方法の詳細については、 <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> クラスのドキュメントを参照してください。  
  
### <a name="logging-for-data-flow-tasks"></a>データ フロー タスクのログ機能の構成  
 データ フロー タスクには、パフォーマンスの監視と調整に使用できるカスタム ログ エントリが数多くあります。 たとえば、メモリ リークを起こす可能性のあるコンポーネントを監視したり、特定のコンポーネントの実行所要時間を追跡できます。 カスタム ログ エントリの一覧とサンプルのログ出力については、「 [Data Flow Task](../../integration-services/control-flow/data-flow-task.md)」を参照してください。  
  
#### <a name="capture-the-names-of-columns-in-which-errors-occur"></a>エラーが発生した列の名前をキャプチャする  
 データ フローのエラー出力を構成した場合、既定でエラーが発生した列の数値識別子のみがエラー出力に含まれます。 詳細については、「[データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。  
  
 列の名前を確認するには、ログ記録を有効にして、 **DiagnosticEx** イベントを選択します。 このイベントは、データ フロー系列マップをログに書き込みます。 その後、この列マップの識別子から列名を参照できます。 **DiagnosticEx** イベントでは XML 出力に含まれる空白が維持されないので、ログのサイズを軽減できます。 読みやすくするために、XML 書式と構文の強調表示をサポートする XML エディター (たとえば Visual Studio) にログをコピーします。  
  
#### <a name="use-the-pipelinecomponenttime-event"></a>PipelineComponentTime イベントの使用  
 カスタム ログ エントリの中で最も役に立つのは、PipelineComponentTime イベントです。 このログ エントリは、データ フローの各コンポーネントが主要な 5 つの処理手順それぞれで要するミリ秒数を報告します。 次の表で、これらの処理手順について説明します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の開発者は、これらの手順を <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>」を参照してください。  
  
|手順|[説明]|  
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

## <a name="ssdt"></a> SQL Server Data Tools でパッケージのログ記録を有効にする
  この手順では、パッケージにログを追加し、パッケージ レベルのログ記録を構成し、ログ構成を XML ファイルに保存する方法について説明します。 ログはパッケージ レベルでのみ追加できますが、パッケージに含まれるコンテナーでのログを有効にするためにパッケージでログ記録を実行する必要はありません。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置した場合、パッケージ実行に対して設定したログ記録レベルは、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] を使用して構成したパッケージのログ記録レベルをオーバーライドします。  
  
 既定では、パッケージに含まれるコンテナーは、親コンテナーと同じログ構成を使用します。 それぞれのコンテナーのログ オプションの設定については、「 [保存されている構成ファイルを使用してログ記録を構成する](#saved_config)」をご覧ください。  
  
### <a name="to-enable-logging-in-a-package"></a>パッケージ内でのログ記録を有効にするには  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  次に、 **[SSIS]** メニューの **[ログ記録]** をクリックします。  
  
3.  **[プロバイダーの種類]** 一覧からログ プロバイダーを選択し、 **[追加]** をクリックします。  
  
4.  **[構成]** 列で、接続マネージャーを選択するか、または **[\<新しい接続>]** をクリックしてこのログ プロバイダーに適した種類の接続マネージャーを新しく作成します。 選択したプロバイダーに応じて、次のいずれかの接続マネージャーを使用します。  
  
    -   テキスト ファイル用には、ファイル接続マネージャーを使用します。 詳細については、「 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)」(ファイル接続マネージャー) をご覧ください。  
  
    -   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]用には、ファイル接続マネージャーを使用します。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用には、OLE DB 接続マネージャーを使用します。 詳細については、「 [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)」をご覧ください。  
  
    -   Windows イベント ログ用には何も指定しません。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] によってログが自動的に作成されます。  
  
    -   XML ファイル用には、ファイル接続マネージャーを使用します。  
  
5.  パッケージで使用するそれぞれのログについて、手順 3. ～ 4. を繰り返します。  
  
    > [!NOTE]  
    >  パッケージでは、それぞれの種類で複数のログを使用できます。  
  
6.  必要に応じて、パッケージレベルのチェック ボックスをオンにします。次に、パッケージレベルのログ記録で使用するログを選択し、 **[詳細]** タブをクリックします。  
  
7.  **[詳細]** タブで、 **[イベント]** をオンにしてすべてのログ エントリのログを記録することを指定するか、または **[イベント]** をオフにしてイベントを個別に選択します。  
  
8.  必要に応じて、 **[詳細設定]** をクリックし、ログに記録する情報を指定します。  
  
    > [!NOTE]  
    >  既定では、すべての情報がログに記録されます。  
  
9. **[詳細]** タブで、 **[保存]** をクリックします。 **[名前を付けて保存]** ダイアログ ボックスが表示されます。 ログ構成を保存するフォルダーに移動し、新しいログ構成のファイル名を入力し、 **[保存]** をクリックします。  
  
10. **[OK]** をクリックします。  
  
11. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  

## <a name="configure_logs"></a> [SSIS ログの構成] ダイアログ ボックス
  **SSIS ログの構成** ダイアログ ボックスを使用して、パッケージのログ記録オプションを定義します。  
  
 **目的に合ったトピックをクリックしてください**  
  
1.  [[SSIS ログの構成] ダイアログ ボックスを開く](#open_dialog)  
  
2.  [[コンテナー] ペインでオプションを構成する](#container)  
  
3.  [[プロバイダーとログ] タブでオプションを構成する](#provider)  
  
4.  [[詳細] タブでオプションを構成する](#detail)  
  
###  <a name="open_dialog"></a> [SSIS ログの構成] ダイアログ ボックスを開く  
 **[SSIS ログの構成] ダイアログ ボックスを開くには**  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで、 **[SSIS]** メニューの **[ログ記録]** をクリックします。  
  
###  <a name="container"></a> [コンテナー] ペインでオプションを構成する  
 **[SSIS ログの構成]** ダイアログ ボックスの **[コンテナー]** ペインを使用すると、パッケージおよびパッケージのコンテナーでログを有効できます。  
  
#### <a name="options"></a>オプション  
 **[SSIS ログの構成]**  
 パッケージとパッケージのコンテナーでログを有効にするには、階層ビューのチェック ボックスをオンにします。  
  
-   オフになっている場合、そのコンテナーでログは無効になります。 ログを有効にする場合はオンにします。  
  
-   淡色表示になっている場合、コンテナーは親のログ オプションを使用します。 このオプションは、パッケージには使用できません。  
  
-   オンにすると、コンテナーは固有のログ オプションを定義します。  
  
 コンテナーが淡色表示になっている場合に、そのコンテナーにログ オプションを設定するには、チェック ボックスを 2 回クリックします。 最初のクリックでチェック ボックスがオフになった後、2 番目のクリックでオンになったら、使用するログ プロバイダーを選択し、ログに記録する情報を指定できます。  
  
###  <a name="provider"></a> [プロバイダーとログ] タブでオプションを構成する  
 **[SSIS ログの構成]** ダイアログ ボックスの **[プロバイダーとログ]** タブを使用すると、ランタイム イベントをキャプチャするログを作成したり構成したりできます。  
  
#### <a name="options"></a>オプション  
 **[プロバイダーの種類]**  
 ログ プロバイダーの種類を一覧から選択します。  
  
 **[追加]**  
 パッケージのログ プロバイダーのコレクションに、指定した種類のログを追加します。  
  
 **[名前]**  
 **[SSIS ログの構成]** ダイアログ ボックスの **[コンテナー]** ペインで選択したコンテナーまたはタスクについて、ログを有効または無効にします。 [名前] フィールドは編集可能です。 プロバイダーの既定の名前を使用するか、わかりやすい一意な名前を入力します。  
  
 **[説明]**  
 [説明] フィールドは編集可能です。 クリックして、ログの既定の説明を変更します。  
  
 **Configuration**  
 既存の接続マネージャーを一覧から選択するか、 **[\<新しい接続>]** をクリックして新しい接続マネージャーを作成します。 ログ プロバイダーの種類によっては、OLE DB 接続マネージャーやファイル接続マネージャーを構成できます。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows イベント ログ用のログ プロバイダーの場合、接続は不要です。  
  
 関連トピック:[OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md) マネージャー、[File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)  
  
 **削除**  
 ログ プロバイダーを選択して、 **[削除]** をクリックします。  
  
###  <a name="detail"></a> [詳細] タブでオプションを構成する  
 **[SSIS ログの構成]** ダイアログ ボックスの **[詳細]** タブで、ログ記録を有効にするイベントと、ログ記録する詳細情報を指定します。 選択した情報は、パッケージ内のすべてのログ プロバイダーに適用されます。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスとテキスト ファイルに別々の情報を書き込むことはできません。  
  
#### <a name="options"></a>オプション  
 **イベント**  
 イベントのログ記録を有効または無効にします。  
  
 **[説明]**  
 イベントの説明が表示されます。  
  
 **[詳細設定]**  
 ログ記録するイベントをオンまたはオフにし、各イベントでログ記録する情報をオンまたはオフにします。 **[標準]** をクリックすると、ログの詳細情報がイベントの一覧を除いてすべて非表示になります。 次の情報をログ記録できます。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**[Computer]**|ログ記録されたイベントが発生したコンピューターの名前。|  
|**[オペレーター]**|パッケージを起動した人物のユーザー名。|  
|**[SourceName]**|ログ記録されたイベントが発生したパッケージ、コンテナー、またはタスクの名前。|  
|**[SourceID]**|ログ記録されたイベントが発生したパッケージ、コンテナー、またはタスクの GUID (global unique identifier)。|  
|**[ExecutionID]**|パッケージ実行インスタンスの GUID。|  
|**[MessageText]**|ログ エントリに関連付けられているメッセージ。|  
|**[DataBytes]**|将来の使用のために予約されています。|  
  
 **[標準]**  
 ログ記録するイベントをオンまたはオフにします。 イベントの一覧を除いて、ログの詳細情報が非表示になります。 イベントを選択すると、既定でそのイベントのすべてのログ詳細情報が選択されます。 **[詳細設定]** をクリックすると、ログの詳細情報がすべて表示されます。  
  
 **[読み込み]**  
 ログのオプションを設定するテンプレートとして使用される、既存の XML ファイルを指定します。  
  
 **および**  
 構成の詳細をテンプレートとして XML ファイルに保存します。  

## <a name="saved_config"></a> 保存されている構成ファイルを使用してログ記録を構成する
  この手順では、以前に保存したログ構成ファイルを読み込んでパッケージ内の新しいコンテナーのログ記録を構成する方法について説明します。  
  
 既定では、パッケージに含まれるすべてのコンテナーは、親コンテナーと同じログ構成を使用します。 たとえば、Foreach ループ内のタスクは、Foreach ループと同じログ構成を使用します。  
  
### <a name="to-configure-logging-for-a-container"></a>コンテナーのログ記録を構成するには  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  次に、 **[SSIS]** メニューの **[ログ記録]** をクリックします。  
  
3.  パッケージ ツリー ビューを展開し、構成するコンテナーを選択します。  
  
4.  **[プロバイダーとログ]** タブで、コンテナーに対して使用するログを選択します。  
  
    > [!NOTE]  
    >  ログは、パッケージ レベルでのみ作成できます。 詳しくは、「 [SQL Server Data Tools でパッケージのログ記録を有効にする](#ssdt)」をご覧ください。  
  
5.  **[詳細]** タブをクリックし、 **[読み込み]** をクリックします。  
  
6.  使用するログ構成ファイルを参照し、 **[開く]** をクリックします。  
  
7.  必要に応じて、 **[イベント]** 列のチェック ボックスをオンにして、ログ記録を行う異なるログ エントリを選択することもできます。 **[詳細設定]** をクリックして、このエントリのログ記録を行うための情報の種類を選択します。  
  
    > [!NOTE]  
    >  最初にログ構成を作成するときに使用されたコンテナーでは使用できない追加のログ エントリが新しいコンテナーに含まれている場合があります。 これらの追加のログ エントリをログに記録するには、手動で選択する必要があります。  
  
8.  **[保存]** をクリックして、ログ構成の更新バージョンを保存します。  
  
9. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  

## <a name="server_logging"></a> SSIS サーバーでのパッケージ実行のログ記録を有効にする
  このトピックでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サーバーに配置したパッケージを実行するときに、パッケージのログ記録レベルを設定または変更する方法について説明します。 パッケージを実行するときに設定したログ記録レベルは、[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] での設計時に構成したパッケージのログ記録レベルをオーバーライドします。 詳細については、「 [SQL Server Data Tools でパッケージのログ記録を有効にする](#ssdt) 」を参照してください。  
  
 SQL Server の **[サーバーのプロパティ]** のサーバーの **[ログ記録レベル]** プロパティで、既定のサーバー全体のログ記録レベルを選択できます。 このトピックで説明している組み込みのログ記録レベルのいずれかを選択するか、既存のカスタマイズしたログ記録レベルを選択できます。 選択したログ記録レベルは、既定で SSIS カタログに展開されているすべてのパッケージに適用されます。 また、既定で SSIS パッケージを実行する SQL エージェント ジョブにも適用されます。  
  
 また、次のいずれかの方法で、個々のパッケージのログ記録レベルを指定することもできます。 このトピックでは最初の方法について説明します。  
  
-   [パッケージの実行] ダイアログ ボックスを使用してパッケージ実行インスタンスを構成する  
  
-   [catalog.set_execution_parameter_value &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) を使用して、実行のインスタンスのパラメーターを設定する  
  
-   [新しいジョブ ステップ] ダイアログ ボックスを使用してパッケージ実行用の SQL Server エージェント ジョブを構成する  
  
### <a name="set-the-logging-level-for-a-package-by-using-the-execute-package-dialog-box"></a>[パッケージの実行] ダイアログ ボックスを使用して、パッケージのログ記録レベルを設定します。  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のオブジェクト エクスプローラーで、パッケージに移動します。  
  
2.  パッケージを右クリックし、 **[実行]** をクリックします。  
  
3.  **[パッケージの実行]** ダイアログ ボックスで、 **[詳細設定]** タブをクリックします。  
  
4.  **[ログ記録レベル]** で、ログ記録レベルを選択します。 このトピックでは、使用できる値について説明します。  
  
5.  他のパッケージの構成を完了し、 **[OK]** をクリックしてパッケージを実行します。  
  
### <a name="select-a-logging-level"></a>ログ記録レベルを選択する  
 次の組み込みレベルを使用できます。 また、既存のカスタマイズされたログ記録レベルを選択することもできます。 このトピックでは、カスタマイズのログ記録レベルについて説明します。  
  
|[ログ記録レベル]|[説明]|  
|-------------------|-----------------|  
|なし|ログ記録をオフにします。 パッケージの実行状態のみがログに記録されます。|  
|Basic|カスタム イベントと診断イベントを除く、すべてのイベントをログに記録します。 これが既定値です。|  
|RuntimeLineage|データ フロー内の系列情報を追跡するために必要なデータを収集します。 この系列情報を解析して、タスク間の系列の関係をマッピングできます。 ISV や開発者は、この情報を利用して、ユーザー設定の系列マッピング ツールを構築できます。|  
|パフォーマンス|パフォーマンス統計、および OnError イベントと OnWarning のイベントのみをログに記録します。<br /><br /> **"実行のパフォーマンス"** レポートは、パッケージ データ フロー コンポーネントのアクティブな時間と合計時間を示します。 この情報は、最後のパッケージの実行のログ記録レベルが **[パフォーマンス]** または **[詳細]** に設定されていた場合にのみ表示されます。 詳細については、「 [Reports for the Integration Services Server](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports)」を参照してください。<br /><br /> [catalog.execution_component_phases](../../integration-services/system-views/catalog-execution-component-phases.md) ビューは、実行の各フェーズでのデータ フロー コンポーネントの開始時刻と終了時刻を表示します。 これらのコンポーネントの情報は、パッケージの実行のログ記録レベルが **[パフォーマンス]** または **[詳細]** に設定されている場合にのみ、このビューに表示されます。|  
|"詳細"|カスタム イベントと診断イベントを含む、すべてのイベントをログに記録されます。<br /><br /> カスタム イベントには、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] タスクによってログに記録されるイベントが含まれます。 カスタム イベントの詳細については、「 [Custom Messages for Logging](#custom_messages)」を参照してください。<br /><br /> **DiagnosticEx** イベントは、診断イベントの例です。 パッケージ実行タスクで子パッケージを実行するたびに、このイベントは、子パッケージに渡されたパラメーター値をキャプチャします。<br /><br /> また、 **DiagnosticEx** イベントを使用すると、行レベルのエラーが発生した列名も取得できます。 このイベントは、データ フロー系列マップをログに書き込みます。 エラー出力でキャプチャされた列識別子を使用して、この系列マップの列名を調べることができます。  詳細については、「[データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。<br /><br /> **DiagnosticEx** のメッセージ列の値は XML テキストです。 パッケージ実行のメッセージ テキストを表示するには、[catalog.operation_messages &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) ビューのクエリを実行します。 **DiagnosticEx** イベントでは XML 出力に含まれる空白が維持されないので、ログのサイズを軽減できます。 読みやすくするために、XML 書式と構文の強調表示をサポートする XML エディター (たとえば Visual Studio) にログをコピーします。<br /><br /> [catalog.execution_data_statistics](../../integration-services/system-views/catalog-execution-data-statistics.md) ビューは、パッケージ実行で、データ フロー コンポーネントが下流コンポーネントへデータを送信するたびに 1 行を表示します。 ビューにこの情報を取得するには、ログ記録レベルを **[詳細]** に設定する必要があります。|  
  
### <a name="create-and-manage-customized-logging-levels-by-using-the-customized-logging-level-management-dialog-box"></a>[カスタマイズされたログ記録レベルの管理] ダイアログ ボックスを使用して、カスタマイズされたログ記録レベルを作成して管理する  
 必要な統計情報とイベントのみを収集するカスタマイズされたログ記録レベルを作成できます。 また、必要に応じて、変数値、接続文字列、コンポーネントのプロパティなど、イベントのコンテキストもキャプチャできます。 パッケージを実行するときに、組み込みのログ記録レベルを選択できる場所であればどこでも、カスタマイズされたログ記録レベルを選択できます。  
  
> [!TIP]  
>  パッケージ変数の値をキャプチャするには、変数の **IncludeInDebugDump** プロパティを **True**に設定する必要があります。  
  
1.  カスタマイズされたログ記録レベルを作成および管理するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、SSISDB データベースを右クリックし、 **[カスタマイズされたログ記録レベル]** を選択し、 **[カスタマイズされたログ記録レベルの管理]** ダイアログ ボックスを開きます。 **[カスタマイズされたログ記録レベル]** リストには、既存のカスタマイズされたログ記録レベルがすべて含まれています。  
  
2.  新しいカスタマイズされたログ記録レベルを **作成** するには、 **[作成]** をクリックし、名前と説明を入力します。 **[統計情報]** タブと **[イベント]** タブで、収集する統計情報とイベントを選択します。 **[イベント]** タブで、必要に応じて個々のイベントについて **[コンテキストを含める]** を選択します。 **[保存]** をクリックします。  
  
3.  既存のカスタマイズされたログ記録レベルを **更新** するには、リストから選択し、再構成して **[保存]** をクリックします。  
  
4.  既存のカスタマイズされたログ記録レベルを **削除** するには、リストから選択し、 **[削除]** をクリックします。  
  
 **カスタマイズされたログ記録レベルのアクセス許可**  
  
-   SSISDB データベースのすべてのユーザーは、パッケージの実行時に、カスタマイズされたログ記録レベルを表示し、カスタマイズされたログ記録レベルを選択できます。  
  
-   ssis_admin 管理者または sysadmin ロールのユーザーのみが、カスタマイズされたログ記録レベルの作成、更新、または削除を行うことができます。  

## <a name="custom_messages"></a> Custom Messages for Logging
SQL Server Integration Services には、パッケージや多くのタスクのログ エントリを書き込むための豊富なカスタム イベントが用意されています。 記録したエントリを使用すれば、定義済みのイベントやユーザー定義メッセージを後の分析用に記録しておくことで、実行の進行状況、結果、および問題点に関する詳細を保管できます。 たとえば、一括挿入の開始時刻と終了時刻を記録しておけば、パッケージ実行時のパフォーマンスの問題を特定できます。  
  
 カスタム ログ エントリとは、パッケージ、すべてのコンテナー、およびタスクに使用できる一連の標準的なログ記録イベントとは異なるエントリのセットです。 カスタム ログ エントリは、パッケージ内の特定のタスクに関する有益な情報を取得するように調整されます。 たとえば、SQL 実行タスクのカスタム ログ エントリの 1 つに、そのタスクで実行される SQL ステートメントをログに記録するものがあります。  
  
 すべてのログ エントリには、パッケージの開始時と終了時に自動的に書き込まれるログ エントリなど、日付と時刻に関する情報が含まれます。 多くのログ イベントでは、ログに複数のエントリが書き込まれます。 通常、イベントにいくつか異なるフェーズが含まれている場合に複数のエントリが書き込まれます。 たとえば、 **ExecuteSQLExecutingQuery** ログ イベントでは、3 つのエントリが書き込まれます。1 つ目はタスクがデータベースへの接続を取得した後、2 つ目は SQL ステートメントの準備が開始された後、3 つ目は SQL ステートメントの実行が完了した後に書き込まれます。  
  
 次の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] オブジェクトには、カスタム ログ エントリがあります。  
  
 [[パッケージ]](#Package)  
  
 [一括挿入タスク](#BulkInsert)  
  
 [[データ フロー タスク]](#DataFlow)  
  
 [DTS 2000 実行タスク](#ExecuteDTS200)  
  
 [プロセス実行タスク](#ExecuteProcess)  
  
 [SQL 実行タスク](#ExecuteSQL)  
  
 [ファイル システム タスク](#FileSystem)  
  
 [FTP タスク](#FTP)  
  
 [メッセージ キュー タスク](#MessageQueue)  
  
 [スクリプト タスク](#Script)  
  
 [メール送信タスク](#SendMail)  
  
 [データベース転送タスク](#TransferDatabase)  
  
 [エラー メッセージ転送タスク](#TransferErrorMessages)  
  
 [ジョブ転送タスク](#TransferJobs)  
  
 [ログイン転送タスク](#TransferLogins)  
  
 [Master ストアド プロシージャ転送タスク](#TransferMasterStoredProcedures)  
  
 [SQL Server オブジェクトの転送タスク](#TransferSQLServerObjects)  
  
 [Web サービス タスク](#WebServices)  
  
 [WMI データ リーダー タスク](#WMIDataReader)  
  
 [WMI イベント監視タスク](#WMIEventWatcher)  
  
 [XML タスク](#XML)  
  
### <a name="log-entries"></a>ログ エントリ  
  
####  <a name="Package"></a> [パッケージ]  
 次の表は、パッケージのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**PackageStart**|パッケージの実行が開始されたことを示します。 このログ エントリは自動的にログに書き込まれます。 除外することはできません。|  
|**PackageEnd**|パッケージが完了したことを示します。 このログ エントリは自動的にログに書き込まれます。 除外することはできません。|  
|**Diagnostic**|同時実行できる実行可能ファイル数など、パッケージの実行に影響するシステム構成に関する情報を提供します。<br /><br /> **診断** ログ エントリに、外部データ プロバイダーの呼び出し前後のエントリも含まれています。|  
  
####  <a name="BulkInsert"></a> 一括挿入タスク  
 次の表は、一括挿入タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**DTSBulkInsertTaskBegin**|一括挿入が開始されたことを示します。|  
|**DTSBulkInsertTaskEnd**|一括挿入が終了したことを示します。|  
|**DTSBulkInsertTaskInfos**|タスクに関する説明情報を提供します。|  
  
####  <a name="DataFlow"></a> [データ フロー タスク]  
 次の表は、データ フロー タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**BufferSizeTuning**|データ フロー タスクでバッファーのサイズが変更されたことを示します。 このログ エントリはサイズ変更の理由を説明し、一時的な新しいバッファー サイズを表示します。|  
|**OnPipelinePostEndOfRowset**|**ProcessInput** メソッドの最終呼び出しで設定される、行セットの終了シグナルがコンポーネントに通知されたことを示します。 エントリは、データ フロー内で入力を処理するコンポーネントごとに書き込まれます。 このエントリには、コンポーネント名が含まれます。|  
|**OnPipelinePostPrimeOutput**|コンポーネントが **PrimeOutput** メソッドの最終呼び出しを完了したことを示します。 データ フローによっては、複数のログ エントリが書き込まれる場合があります。 コンポーネントがソースの場合、コンポーネントが行の処理を完了したことを意味します。|  
|**OnPipelinePreEndOfRowset**|**ProcessInput** メソッドの最終呼び出しで設定される、行セットの終了シグナルをコンポーネントがまもなく受信することを示します。 エントリは、データ フロー内で入力を処理するコンポーネントごとに書き込まれます。 このエントリには、コンポーネント名が含まれます。|  
|**OnPipelinePrePrimeOutput**|コンポーネントが、 **PrimeOutput** メソッドからの呼び出し行セットの終了シグナルをまもなく受信することを示します。 データ フローによっては、複数のログ エントリが書き込まれる場合があります。|  
|**OnPipelineRowsSent**|**ProcessInput** メソッドの呼び出しによってコンポーネント入力に指定された行数を報告します。 ログ エントリにはコンポーネント名が含まれます。|  
|**PipelineBufferLeak**|バッファー マネージャーの終了後もバッファーを保持しているコンポーネントに関する情報を提供します。 つまり、バッファー リソースが解放されていないため、メモリ リークの原因になる可能性があります。 このログ エントリは、コンポーネントの名前とバッファーの ID を含みます。|  
|**PipelineExecutionPlan**|データ フローの実行プランを報告します。 バッファーをコンポーネントに送信する方法に関する情報を提供します。 この情報は、PipelineExecutionTrees エントリと組み合わせて、タスク内での実行内容を示します。|  
|**PipelineExecutionTrees**|データ フロー内のレイアウトの実行ツリーを報告します。 データ フロー エンジンのスケジューラは、このツリーを使用して、データ フローの実行プランを構築します。|  
|**PipelineInitialization**|タスクに関する初期化情報を提供します。 この情報には、BLOB データの一時的な保存に使用するディレクトリ、既定のバッファー サイズ、およびバッファー内の行数が含まれます。 データ フロー タスクの構成によっては、複数のログ エントリが書き込まれる場合があります。|  
  
####  <a name="ExecuteDTS200"></a> DTS 2000 実行タスク  
 次の表は、DTS 2000 実行タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**ExecuteDTS80PackageTaskBegin**|タスクが DTS 2000 パッケージの実行を開始したことを示します。|  
|**ExecuteDTS80PackageTaskEnd**|タスクが終了したことを示します。<br /><br /> 注:DTS 2000 パッケージは、タスク終了後も引き続き実行される場合があります。|  
|**ExecuteDTS80PackageTaskTaskInfo**|タスクに関する説明情報を提供します。|  
|**ExecuteDTS80PackageTaskTaskResult**|タスクで実行された DTS 2000 パッケージの実行結果を報告します。|  
  
####  <a name="ExecuteProcess"></a> プロセス実行タスク  
 次の表は、プロセス実行タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|Description|  
|---------------|-----------------|  
|**ExecuteProcessExecutingProcess**|タスクで実行するように構成されている実行可能ファイルの実行プロセスに関する情報を提供します。<br /><br /> 2 つのログ エントリが書き込まれます。 1 つのエントリには、タスクで実行される実行可能ファイルの名前と場所が含まれ、もう 1 つのエントリは、実行可能ファイルの終了を記録します。|  
|**ExecuteProcessVariableRouting**|実行可能ファイルの入力と出力にルーティングされる変数に関する情報を提供します。 ログ エントリは、stdin (入力)、stdout (出力)、および stderr (エラー出力) に書き込まれます。|  
  
####  <a name="ExecuteSQL"></a> SQL 実行タスク  
 次の表では、SQL 実行タスクのカスタム ログ エントリを説明します。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|SQL ステートメントの実行フェーズに関する情報を提供します。 タスクがデータベースへの接続を取得したとき、SQL ステートメントの準備が開始されたとき、および SQL ステートメントの実行が完了した後に、ログ エントリが書き込まれます。 準備フェーズのログ エントリには、タスクで使用される SQL ステートメントが含まれます。|  
  
####  <a name="FileSystem"></a> ファイル システム タスク  
 次の表では、ファイル システム タスクのカスタム ログ エントリを説明します。  
  
|ログ エントリ|Description|  
|---------------|-----------------|  
|**FileSystemOperation**|タスクで実行される操作を報告します。 ログ エントリは、ファイル システム操作の開始時に書き込まれます。これには、操作の基になるファイルと操作対象のファイルに関する情報が含まれます。|  
  
####  <a name="FTP"></a> FTP タスク  
 次の表は、FTP タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**FTPConnectingToServer**|タスクで FTP サーバーへの接続が開始されたことを示します。|  
|**FTPOperation**|タスクで実行された FTP 操作の開始および種類を報告します。|  
  
####  <a name="MessageQueue"></a> メッセージ キュー タスク  
 次の表は、メッセージ キュー タスクのカスタム ログ エントリの一覧です。  
  
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
  
####  <a name="Script"></a> スクリプト タスク  
 次の表では、スクリプト タスクのカスタム ログ エントリを説明します。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**ScriptTaskLogEntry**|スクリプト内でのログ記録の実装結果を報告します。 ログ エントリは、 **Dts** オブジェクトの **Log** メソッドを呼び出すたびに書き込まれます。 このエントリは、コードの実行時に書き込まれます。 詳細については、 [「スクリプト タスクでのログ記録」](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)をご覧ください。|  
  
####  <a name="SendMail"></a> メール送信タスク  
 次の表は、メール送信タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**SendMailTaskBegin**|タスクが電子メール メッセージの送信を開始したことを示します。|  
|**SendMailTaskEnd**|タスクが電子メール メッセージの送信を終了したことを示します。|  
|**SendMailTaskInfo**|タスクに関する説明情報を提供します。|  
  
####  <a name="TransferDatabase"></a> データベース転送タスク  
 次の表は、データベース転送タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**SourceDB**|タスクでコピーされたデータベースを示します。|  
|**SourceSQLServer**|データベースのコピー元のコンピューターを示します。|  
  
####  <a name="TransferErrorMessages"></a> エラー メッセージ転送タスク  
 次の表は、エラー メッセージ転送タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**TransferErrorMessagesTaskFinishedTransferringObjects**|タスクがエラー メッセージの転送を終了したことを示します。|  
|**TransferErrorMessagesTaskStartTransferringObjects**|タスクがエラー メッセージの転送を開始したことを示します。|  
  
####  <a name="TransferJobs"></a> ジョブ転送タスク  
 次の表は、ジョブ転送タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**TransferJobsTaskFinishedTransferringObjects**|タスクが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブの転送を終了したことを示します。|  
|**TransferJobsTaskStartTransferringObjects**|タスクが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブの転送を開始したことを示します。|  
  
####  <a name="TransferLogins"></a> ログイン転送タスク  
 次の表は、ログイン転送タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**TransferLoginsTaskFinishedTransferringObjects**|タスクがログインの転送を終了したことを示します。|  
|**TransferLoginsTaskStartTransferringObjects**|タスクがログインの転送を開始したことを示します。|  
  
####  <a name="TransferMasterStoredProcedures"></a> Master ストアド プロシージャ転送タスク  
 次の表は、Master ストアド プロシージャ転送タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**TransferStoredProceduresTaskFinishedTransferringObjects**|**master** データベースに格納されている、ユーザー定義ストアド プロシージャの転送をタスクが完了したことを示します。|  
|**TransferStoredProceduresTaskStartTransferringObjects**|**master** データベースに格納されている、ユーザー定義ストアド プロシージャの転送をタスクが開始したことを示します。|  
  
####  <a name="TransferSQLServerObjects"></a> SQL Server オブジェクトの転送タスク  
 次の表は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**TransferSqlServerObjectsTaskFinishedTransferringObjects**|タスクが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース オブジェクトの転送を終了したことを示します。|  
|**TransferSqlServerObjectsTaskStartTransferringObjects**|タスクが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース オブジェクトの転送を開始したことを示します。|  
  
####  <a name="WebServices"></a> Web サービス タスク  
 次の表は、Web サービス タスクに対して有効にできるカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**WSTaskBegin**|タスクが Web サービスへのアクセスを開始しました。|  
|**WSTaskEnd**|タスクが Web サービス メソッドを完了しました。|  
|**WSTaskInfo**|タスクに関する説明情報を提供します。|  
  
####  <a name="WMIDataReader"></a> WMI データ リーダー タスク  
 次の表は、WMI データ リーダー タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**WMIDataReaderGettingWMIData**|タスクが WMI データの読み取りを開始したことを示します。|  
|**WMIDataReaderOperation**|タスクで実行された WQL クエリを報告します。|  
  
####  <a name="WMIEventWatcher"></a> WMI イベント監視タスク  
 次の表は、WMI イベント監視タスクのカスタム ログ エントリの一覧です。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**WMIEventWatcherEventOccurred**|タスクが監視しているイベントが発生したことを示します。|  
|**WMIEventWatcherTimedout**|タスクがタイムアウトしたことを示します。|  
|**WMIEventWatcherWatchingForWMIEvents**|タスクが WQL クエリの実行を開始したことを示します。 このエントリには、クエリが含まれています。|  
  
####  <a name="XML"></a> XML タスク  
 次の表では、XML タスクのカスタム ログ エントリを説明します。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**XMLOperation**|タスクで実行される操作に関する情報を提供します。|  

## <a name="related-tasks"></a>Related Tasks  
 次の一覧では、ログ記録機能に関連するタスクの実行方法を示すトピックへのリンクを示します。  
  
-   [Integration Services パッケージによってログに記録されるイベント](../../integration-services/performance/events-logged-by-an-integration-services-package.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [完全かつ詳細なログ記録用の DTLoggedExec ツール (CodePlex プロジェクト)](https://go.microsoft.com/fwlink/?LinkId=150579)  
