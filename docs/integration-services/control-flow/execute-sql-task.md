---
title: SQL 実行タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executesqltask.f1
- sql13.dts.designer.executesqltask.general.f1
- sql13.dts.designer.executesqltask.parametermapping.f1
- sql13.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- batches [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1e331b974bee3017e17e75dbf8c3ecb8506349b2
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298302"
---
# <a name="execute-sql-task"></a>SQL 実行タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  SQL 実行タスクは、パッケージ内の SQL ステートメントやストアド プロシージャを実行します。 このタスクには、1 つの SQL ステートメントまたは順に実行される複数の SQL ステートメントを含めることができます。 SQL 実行タスクは、次の目的で使用できます。  
  
-   データを挿入する準備として、テーブルまたはビューを切り捨てます。  
  
-   テーブル、ビューなどのデータベース オブジェクトを、作成、変更、および削除します。  
  
-   データの読み込みを行う前にファクト テーブルとディメンション テーブルを再作成します。  
  
-   ストアド プロシージャを実行します。 SQL ステートメントで、一時テーブルから結果を返すストアド プロシージャが呼び出される場合は、WITH RESULT SETS オプションを使用して結果セットのメタデータを定義します。  
  
-   クエリから返された行セットを変数に保存します。  
  
 SQL 実行タスクを Foreach ループや For ループ コンテナーと組み合わせて使用すると、複数の SQL ステートメントを実行できます。 これらのコンテナーには、パッケージ内での繰り返し制御フローが実装されているため、SQL 実行タスクを繰り返して実行できます。 たとえば、Foreach ループ コンテナーを使用すると、パッケージはフォルダー内のファイルを列挙して SQL 実行タスクを繰り返して実行し、各ファイルに格納された SQL ステートメントを実行します。  
  
## <a name="connect-to-a-data-source"></a>データ ソースに接続する  
 SQL 実行タスクでは、さまざまな種類の接続マネージャーを使用して、SQL ステートメントまたはストアド プロシージャを実行するデータ ソースに接続できます。 このタスクが使用できる接続の種類の一覧を、次の表に示します。  
  
|接続の種類|[ODBC 入力先エディター]|  
|---------------------|------------------------|  
|EXCEL|[Excel 接続マネージャー](../../integration-services/connection-manager/excel-connection-manager.md)|  
|OLE DB (OLE DB)|[OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|[ODBC 接続マネージャー](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|ADO (ADO)|[ADO 接続マネージャー](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|[ADO.NET 接続マネージャー](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[SQL Server Compact Edition 接続マネージャー](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## <a name="create-sql-statements"></a>SQL ステートメントを作成する  
 このタスクでは、タスクのプロパティを SQL ステートメントの実行元として使用できます。タスクのプロパティには、ステートメント、単数または複数のステートメントが含まれるファイルへの接続、またはステートメントが含まれる変数名を含めることができます。 SQL ステートメントは、実行元のデータベース管理システム (DBMS) の言語仕様に従って作成する必要があります。 詳細については、「[Integration Services &#40;SSIS&#41; のクエリ](../../integration-services/integration-services-ssis-queries.md)」を参照してください。  
  
 SQL ステートメントがファイルに格納されている場合、タスクはファイル接続マネージャーを使用してそのファイルに接続します。 詳しくは「 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)」をご覧ください。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、 **[SQL 実行タスク エディター]** ダイアログ ボックスを使用して SQL ステートメントを入力できます。また、SQL クエリを作成するためのグラフィカル ユーザー インターフェイスである **クエリ ビルダー**を使用することもできます。 
  
> [!NOTE]  
>  有効な SQL ステートメントが SQL 実行タスクの外部に記述されている場合、SQL 実行タスクは解析に失敗することがあります。  
  
> [!NOTE]  
>  SQL 実行タスクは **RecognizeAll** ParseMode の列挙値を使用します。 詳細については、「 [ManagedBatchParser 名前空間](https://go.microsoft.com/fwlink/?LinkId=223617)」を参照してください。  
  
## <a name="send-multiple-statements-in-a-batch"></a>複数のステートメントを一括送信する  
 SQL 実行タスクに複数のステートメントが含まれる場合、それらをグループ化してバッチとして実行できます。 バッチの開始と終了を知らせるには、GO コマンドを使用します。 2 つの GO コマンド間にあるすべての SQL ステートメントは、OLE DB プロバイダーにバッチで送信されて実行されます。 SQL コマンドには、GO コマンドで分割された複数のバッチを含めることができます。  
  
 グループ化してバッチに含めることができる SQL ステートメントの種類には制限があります。 詳細については、「 [ステートメントのバッチ](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)」を参照してください。  
  
 SQL 実行タスクで SQL ステートメントのバッチを実行する場合、バッチには次の規則が適用されます。  
  
-   結果セットを返すことができるのは、バッチの最初のステートメント 1 つだけです。  
  
-   結果セットで結果のバインドを使用する場合、クエリは同じ数の列を返す必要があります。 クエリが異なる数の列を返した場合、タスクは失敗します。 ただし、タスクが失敗しても、そのタスクによって実行された DELETE や INSERT などのクエリは成功する場合があります。  
  
-   結果のバインドで列名を使用する場合、クエリは、タスクで使用される結果セットの名前と同じ名前の列を返す必要があります。 列が存在しない場合、タスクは失敗します。  
  
-   タスクでパラメーターのバインドを使用する場合、バッチ内のすべてのクエリは、同じ数と種類のパラメーターを持つ必要があります。  
  
## <a name="run-parameterized-sql-commands"></a>パラメーター化された SQL コマンドを実行する  
 SQL ステートメントとストアド プロシージャでは多くの場合、入力パラメーター、出力パラメーター、およびリターン コードを使用します。 SQL 実行タスクでは、 **Input** **Output** **ReturnValue** パラメーター型をサポートします。 入力パラメーターには **Input** 型、出力パラメーターには **Output** 型、およびリターン コードには **ReturnValue** 型を使用します。  
  
> [!NOTE]  
>  SQL 実行タスクでは、データ プロバイダーがサポートしている場合のみ、パラメーターを使用できます。  
  
## <a name="specify-a-result-set-type"></a>結果セットの種類を指定する  
 結果セットが SQL 実行タスクに返されるかどうかは、SQL コマンドの種類によって決まります。 たとえば、通常、SELECT ステートメントは結果セットを返しますが、INSERT ステートメントは返しません。 SELECT ステートメントからの結果セットに含まれる行数は、0 行、1 行、または多数行である場合があります。 また、ストアド プロシージャは、プロシージャの実行状態を示すリターン コードという整数値を返すこともできます。 この場合、結果セットは 1 行で構成されます。  
  
## <a name="configure-the-execute-sql-task"></a>SQL 実行タスクを構成する  
 SQL 実行タスクは、次の方法で構成できます。  
  
-   データベースへの接続に使用する接続マネージャーの種類を指定します。  
  
-   SQL ステートメントが返す結果セットの種類を指定します。  
  
-   SQL ステートメントのタイムアウトを指定します。  
  
-   SQL ステートメントの実行元を指定します。  
  
-   SQL ステートメントの準備フェーズをタスクがスキップするかどうかを指定します。  
  
-   ADO 接続の種類を使用している場合、SQL ステートメントがストアド プロシージャかどうかを指定する必要があります。 その他の接続の種類では、このプロパティは読み取り専用であり、値は常に **false**です。  
  
 プロパティはプログラムによって設定するか、または [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。  

## <a name="general-page---execute-sql-task-editor"></a>[全般] ページ - [SQL 実行タスク エディター]
 **[SQL 実行タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、SQL 実行タスクを構成したり、タスクが実行する SQL ステートメントを指定したりできます。  

Transact-SQL クエリ言語の詳細については、「[Transact-SQL リファレンス &#40;データベース エンジン&#41;](../../t-sql/transact-sql-reference-database-engine.md)」を参照してください。  
  
### <a name="static-options"></a>静的オプション  
 **[名前]**  
 ワークフロー内の SQL 実行タスクに一意な名前を指定します。 指定された名前は [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーに表示されます。  
  
 **[説明]**  
 SQL 実行タスクの説明です。 パッケージを自己文書化して目的を明確にし、保守が容易になるように、タスクの目的について記述することをお勧めします。  
  
 **[TimeOut]**  
 タスクがタイムアウトになるまでに実行される最大の秒数を指定します。この値に 0 を指定すると、時間は無制限になります。 既定値は 0 です。  
  
> [!NOTE]  
>  接続してトランザクションを完了するための時間を、 **[TimeOut]** で指定された秒数よりも長く指定することによってスリープ機能をエミュレートする場合、ストアド プロシージャはタイムアウトになりません。 ただし、クエリを実行するストアド プロシージャは、 **[TimeOut]** で指定された時間制限の影響を常に受けます。  
  
 **CodePage**  
 変数の Unicode 値を変換するときに使用するコード ページを指定します。 既定値は、ローカル コンピューターのコード ページです。  
  
> [!NOTE]  
>  SQL 実行タスクで ADO 接続マネージャーまたは ODBC 接続マネージャーを使用する場合、 **[CodePage]** プロパティは使用できません。 ソリューションでコード ページを使用する必要がある場合は、SQL 実行タスクで OLE DB 接続マネージャーまたは ADO.NET 接続マネージャーを使用します。  
  
 **[TypeConversionMode]**  
 このプロパティを **Allowed**に設定すると、SQL 実行タスクは出力パラメーターとクエリ結果を結果が割り当てられている変数のデータ型に変換します。 この機能は、結果セットの種類が **単一行** の場合に適用されます。  
  
 **[ResultSet]**  
 SQL ステートメントの実行によって予測される結果の型を指定します。 **[単一行]** 、 **[完全な結果セット]** 、 **[XML]** 、または **[なし]** から選択します。  
  
 **ConnectionType**  
 データ ソースへの接続に使用する接続マネージャーの種類を選択します。 使用可能な接続の種類は、 **[OLE DB]** 、 **[ODBC]** 、 **[ADO]** 、 **[ADO.NET]** 、および **[SQLMOBILE]** です。  
  
 **関連トピック:** [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)、[ODBC 接続マネージャー](../../integration-services/connection-manager/odbc-connection-manager.md)、[ADO 接続マネージャー](../../integration-services/connection-manager/ado-connection-manager.md)、[ADO.NET 接続マネージャー](../../integration-services/connection-manager/ado-net-connection-manager.md)、[SQL Server Compact Edition 接続マネージャー](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **[接続]**  
 定義済みの接続マネージャーの一覧から接続を選択します。 新しい接続を作成するには、[\<**新しい接続...** >] を選択します。  
  
 **[SQLSourceType]**  
 タスクが実行する SQL ステートメントのソースの種類を選択します。  
  
 SQL 実行タスクが使用する接続マネージャーの種類によって、パラメーター化された SQL ステートメントで特定のパラメーター マーカーを使用する必要があります。    
  
 このプロパティのオプションを次の表に示します。  
  
|ReplTest1|[説明]|  
|-----------|-----------------|  
|**[直接入力]**|Transact-SQL ステートメントをソースに設定します。 この値を選択すると、動的オプション **[SQLStatement]** が表示されます。|  
|**[ファイル接続]**|Transact-SQL ステートメントを含んでいるファイルを選択します。 この値を設定すると、動的オプション **[ファイル接続]** が表示されます。|  
|**変数**|Transact-SQL ステートメントを定義する変数をソースに設定します。 この値を選択すると、動的オプション **[SourceVariable]** が表示されます。|  
  
 **[QueryIsStoredProcedure]**  
 実行が指定された SQL ステートメントがストアド プロシージャかどうかを示します。 このプロパティは、タスクが ADO 接続マネージャーを使用する場合のみ、読み取り/書き込みになります。 それ以外の場合、このプロパティは読み取り専用となり、その値は **false**となります。  
  
 **[BypassPrepare]**  
 SQL ステートメントが準備されているかどうかを示します。  **true** の場合は準備がスキップされ、 **false** の場合は実行の前に SQL ステートメントが準備されます。 このオプションは、準備をサポートしている OLE DB 接続の場合のみ使用可能です。  
  
 **関連トピック:** [準備実行](../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、SQL ステートメントを含むファイルの場所を指定します。 ファイルを選択して、ファイルの内容を SQL ステートメントとして **[SQLStatement]** プロパティにコピーします。  
  
 **[クエリの作成]**  
 クエリの作成に使用するグラフィカルなツールである **[クエリ ビルダー]** ダイアログ ボックスを使用して SQL ステートメントを作成します。 このオプションは、 **[SQLSourceType]** オプションが **[直接入力]** に設定されている場合に使用可能です。  
  
 **[クエリの解析]**  
 SQL ステートメントの構文を検証します。  
  
### <a name="sqlsourcetype-dynamic-options"></a>[SQLSourceType] の動的オプション  
  
#### <a name="sqlsourcetype--direct-input"></a>[SQLSourceType] = [直接入力]  
 **[SQLStatement]**  
 実行する SQL ステートメントをオプション ボックスに入力するか、参照ボタン ([...]) をクリックして **[SQL クエリの入力]** ダイアログ ボックスに SQL ステートメントを入力するか、 **[クエリの作成]** をクリックして **[クエリ ビルダー]** ダイアログ ボックスでステートメントを作成します。  
  
 **関連トピック:** [クエリ ビルダー](https://msdn.microsoft.com/library/780752c9-6e3c-4f44-aaff-4f4d5e5a45c5)  
  
#### <a name="sqlsourcetype--file-connection"></a>[SQLSourceType] = [ファイル接続]  
 **[FileConnection]**  
 既存のファイル接続マネージャーを選択するか、[\<**新しい接続...** >] をクリックして新しい接続マネージャーを作成します。  
  
 **関連トピック:** [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)、[ファイル接続マネージャー エディター](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="sqlsourcetype--variable"></a>[SQLSourceType] = [変数]  
 **[SourceVariable]**  
 既存の変数を選択するか、\<**新しい変数...** > をクリックして新しい変数を作成します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)、[変数の追加](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
 
## <a name="parameter-mapping-page---execute-sql-task-editor"></a>[パラメーター マッピング] ページ - [SQL 実行タスク エディター]
**[SQL 実行タスク エディター]** ダイアログ ボックスの **[パラメーター マッピング]** ページを使用すると、SQL ステートメント内のパラメーターに変数をマップできます。  
  
### <a name="options"></a>オプション  
 **[変数名]**  
 **[追加]** をクリックしてパラメーター マッピングを追加した後で、システム変数またはユーザー定義変数を一覧から選択するか、[\<**新しい変数...** >] をクリックして **[変数の追加]** ダイアログ ボックスで新しい変数を追加します。  
  
 **関連トピック:** [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)  
  
 **[方向]**  
 パラメーターの方向を選択します。 各変数を入力パラメーター、出力パラメーター、またはリターン コードにマップします。  
  
 **[データ型]**  
 パラメーターのデータ型を選択します。 使用できるデータ型の一覧は、タスクによって使用される接続マネージャーで選択したプロバイダーに固有のものです。  
  
 **[パラメーター名]**  
 パラメーター名を指定します。  
  
 タスクで使用される接続マネージャーの種類によって、数字またはパラメーター名を使用する必要があります。 接続マネージャーの種類によっては、パラメーター名の先頭文字を \@ 記号にすること、\@Param1 などの特定の名前を使用すること、またはパラメーター名として列名を使用することが求められます。  
  
 **[パラメーター サイズ]**  
 文字列やバイナリ フィールドなどの可変長パラメーターのサイズを指定します。  
  
 この設定により、プロバイダーは可変長パラメーター値に十分な領域を割り当てることができるようになります。  
  
 **[追加]**  
 クリックすると、パラメーター マッピングが追加されます。  
  
 **[削除]**  
 一覧からパラメーター マッピングを選択してから **[削除]** をクリックします。  
 
## <a name="result-set-page---execute-sql-task-editor"></a>[結果セット] ページ - [SQL 実行タスク エディター]
**[SQL 実行タスク エディター]** ダイアログ ボックスの **[結果セット]** ページを使用すると、SQL ステートメントの結果を新しい変数または既存の変数にマップできます。 このダイアログ ボックスのオプションは、[全般] ページの **[ResultSet]** が **[なし]** に設定されている場合は無効です。  
  
### <a name="options"></a>オプション  
 **[結果名]**  
 **[追加]** をクリックして結果セットのマッピング設定を追加した後、結果に名前を付けます。 結果セットの種類によっては、特定の結果名を使用する必要があります。  
  
 結果セットの種類が " **単一行**" の場合、クエリによって返される列の名前か、クエリによって返される列の列リスト内で列の位置を示す数値を使用できます。  
  
 結果セットの種類が " **完全な結果セット** " または " **XML**" の場合、結果セット名には 0 を使用する必要があります。  
 
  
 **[変数名]**  
 変数を選択して変数に結果セットをマップするか、[\<**新しい変数...** >] をクリックして **[変数の追加]** ダイアログ ボックスで新しい変数を追加します。  
  
 **[追加]**  
 結果セットのマッピングを追加します。  
  
 **[削除]**  
 一覧で結果セットのマッピングを選択して、 **[削除]** をクリックします。  
 
## <a name="parameters-in-the-execute-sql-task"></a>SQL 実行タスクのパラメーター
SQL ステートメントとストアド プロシージャでは多くの場合、 **入力** パラメーター、 **出力** パラメーター、およびリターン コードを使用します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の SQL 実行タスクでは、**Input**、**Output**、**ReturnValue** パラメーター型をサポートします。 入力パラメーターには **Input** 型、出力パラメーターには **Output** 型、およびリターン コードには **ReturnValue** 型を使用します。  
  
> [!NOTE]  
>  SQL 実行タスクでは、データ プロバイダーがサポートしている場合のみ、パラメーターを使用できます。  
  
 クエリやストアド プロシージャなど、SQL コマンドのパラメーターは、SQL 実行タスクのスコープ内、親コンテナー、またはパッケージのスコープ内に作成されたユーザー定義変数にマップされます。 変数の値はデザイン時に設定することも、実行時に動的に設定することもできます。 パラメーターは、システム変数にマップすることもできます。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)」および「[システム変数](../../integration-services/system-variables.md)」を参照してください。  
  
 SQL 実行タスクでパラメーターやリターン コードを使用すると、タスクでサポートされるパラメーターの型やこれらのパラメーターのマップ方法を把握するだけでなく、その他の情報も取得できます。 SQL 実行タスクでパラメーターおよびリターン コードを正しく使用する際に必要となる、追加の使用要件やガイドラインがあります。 以降では、こうした使用要件およびガイドラインについて説明します。  
  
-   [パラメーター名とパラメーター マーカーの使用](#Parameter_names_and_markers)  
  
-   [日付と時刻のデータ型のパラメーターの使用](#Date_and_time_data_types)  
  
-   [WHERE 句でのパラメーターの使用](#WHERE_clauses)  
  
-   [ストアド プロシージャでのパラメーターの使用](#Stored_procedures)  
  
-   [リターン コードの値の取得](#Return_codes)    
  
###  <a name="Parameter_names_and_markers"></a> パラメーター名とパラメーター マーカー  
 SQL コマンドの構文では、SQL 実行タスクが使用する接続の種類によって、異なるパラメーター マーカーが使用されます。 たとえば、[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーの場合は、SQL コマンドが使用するパラメーター マーカーの形式を **\@varParameter** にする必要がありますが、OLE DB 接続の場合は疑問符 (?) パラメーター マーカーが必要です。  
  
 変数とパラメーターの間でのマッピングでパラメーター名として使用できる名前も、接続マネージャーの種類によって異なります。 たとえば、[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーでは \@ プレフィックス付きのユーザー定義名を使用し、OLE DB 接続マネージャーではパラメーター名として 0 から始まる序数の数値を使用する必要があります。  
  
 次の表に、SQL 実行タスクで使用できる接続マネージャーの種類の SQL コマンドの要件をまとめます。  
  
|接続の種類|パラメーター マーカー|[パラメーター名]|SQL コマンドの例|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO (ADO)|?|Param1、Param2、...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|\@\<パラメーター名>|\@\<パラメーター名>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = \@parmContactID|  
|ODBC|?|1、2、3、...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL および OLE DB|?|0、1、2、3、…|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
#### <a name="use-parameters-with-adonet-and-ado-connection-managers"></a>ADO.NET 接続マネージャーおよび ADO 接続マネージャーでのパラメーターの使用  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] および ADO 接続マネージャーでは、パラメーターを使用する SQL コマンドに関する特定の要件があります。  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーでは、SQL コマンド内のパラメーター マーカーとしてパラメーター名を使用することが必要になります。 これは、変数をパラメーターに直接マップできることを意味します。 たとえば、変数 `@varName` は、 `@parName` という名前のパラメーターにマップされ、パラメーター `@parName`に変数を提供します。  
  
-   ADO 接続マネージャーでは、SQL コマンド内のパラメーター マーカーとして疑問符 (?) を使用する必要があります。 ただし、パラメーター名として任意のユーザー定義名 (整数値を除く) を使用できます。  
  
 パラメーターに値を提供するプロセスで、変数がパラメーター名にマップされます。 その後、SQL 実行タスクがパラメーター リスト内にあるパラメーター名の序数値を使用して、変数からパラメーターに値を読み込みます。  
  
#### <a name="use-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>EXCEL、ODBC、および OLE DB 接続マネージャーでのパラメーターの使用  
 EXCEL、ODBC、および OLE DB の各接続マネージャーでは、SQL コマンド内のパラメーター マーカーとして疑問符 (?) を使用し、パラメーター名として 0 または 1 から始まる序数を使用する必要があります。 SQL 実行タスクで ODBC 接続マネージャーが使用される場合、クエリの最初のパラメーターにマップされるパラメーター名は 1 になります。それ以外の場合、パラメーター名は 0 になります。 後続のパラメーター名の数値は、パラメーター名のマップ先である SQL コマンドのパラメーターを示します。 たとえば、3 というパラメーター名は、SQL コマンド内の 3 番目の疑問符 (?) で表される、3 番目のパラメーターにマップされます。  
  
 パラメーターに値を提供するプロセスで、変数がパラメーター名にマップされ、SQL 実行タスクがパラメーター名の序数値を使用して、変数からパラメーターに値を読み込みます。  
  
 接続マネージャーが使用するプロバイダーによっては、一部の OLE DB データ型がサポートされないことがあります。 たとえば、Excel ドライバーは限定されたデータ型のセットしか認識しません。 Excel ドライバーでの Jet プロバイダーの動作の詳細については、「 [Excel ソース](../../integration-services/data-flow/excel-source.md)」を参照してください。  
  
#### <a name="use-parameters-with-ole-db-connection-managers"></a>OLE DB 接続マネージャーでのパラメーターの使用  
 SQL 実行タスクが OLE DB 接続マネージャーを使用する場合は、タスクの BypassPrepare プロパティを使用できます。 SQL 実行タスクが、パラメーターと共に SQL ステートメントを使用する場合は、このプロパティを **true** に設定する必要があります。  
  
 OLE DB 接続マネージャーを使用する場合、パラメーター化サブクエリは使用できません。これは、SQL 実行タスクが OLE DB プロバイダーを介してパラメーター情報を取得できないからです。 ただし、式を使用することで、パラメーター値をクエリ文字列に連結したり、タスクの SqlStatementSource プロパティを設定したりできます。  
  
###  <a name="Date_and_time_data_types"></a> 日付と時刻のデータ型のパラメーターの使用  
  
#### <a name="use-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>ADO.NET 接続マネージャーおよび ADO 接続マネージャーでの日付と時刻のパラメーターの使用  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 型 ( **time** および **datetimeoffset**) のデータを読み取る場合、 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーまたは ADO 接続マネージャーのいずれかを使用する SQL 実行タスクには、次の追加要件があります。  
  
-   **time** 型のデータの場合、[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーでは、パラメーターの型が **Input** または **Output** で、データ型が **string** のパラメーターにこのデータを格納する必要があります。  
  
-   **datetimeoffset** 型のデータの場合、[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーでは、次のいずれかのパラメーターにこのデータを格納する必要があります。  
  
    -   パラメーターの型が **Input** で、データ型が **string**のパラメーター。  
  
    -   パラメーターの型が **Output** または **ReturnValue**で、データ型が **datetimeoffset**、 **string**、または **datetime2**のパラメーター。 データ型が **string** または **datetime2** のパラメーターを選択した場合、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ではデータが string または datetime2 に変換されます。  
  
-   ADO 接続マネージャーでは、**time** 型または **datetimeoffset** 型のデータを、パラメーターの型が **Input** または **Output** で、データ型が **adVarWchar** のパラメーターに格納する必要があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型の詳細とそれを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型にマッピングする方法については、「[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)」と「[Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
#### <a name="use-date-and-time-parameters-with-ole-db-connection-managers"></a>OLE DB 接続マネージャーでの日付と時刻のパラメーターの使用  
 OLE DB 接続マネージャーを使用する場合、SQL 実行タスクには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型 ( **date**、 **time**、 **datetime**、 **datetime2**、および **datetimeoffset**) のデータに関して特定のストレージ要件があります。 このデータは、次のいずれかの型のパラメーターに格納する必要があります。  
  
-   NVARCHAR データ型の入力パラメーター。  
  
-   次の表に示す、適切なデータ型の出力パラメーター。  
  
    |**Output** パラメーターの型|Date データ型|  
    |-------------------------------|--------------------|  
    |DBDATE|**date**|  
    |DBTIME2|**time**|  
    |DBTIMESTAMP|**datetime**, **datetime2**|  
    |DBTIMESTAMPOFFSET|**datetimeoffset**|  
  
 データが適切な入力パラメーターまたは出力パラメーターに格納されないと、パッケージは失敗します。  
  
#### <a name="use-date-and-time-parameters-with-odbc-connection-managers"></a>ODBC 接続マネージャーでの日付と時刻のパラメーターの使用  
 ODBC 接続マネージャーを使用する場合、SQL 実行タスクには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型 ( **date**、 **time**、 **datetime**、 **datetime2**、または **datetimeoffset**) のいずれかのデータに関して特定のストレージ要件があります。 このデータは、次のいずれかの型のパラメーターに格納する必要があります。  
  
-   SQL_WVARCHAR データ型の **入力** パラメーター。  
  
-   次の表に示す、適切なデータ型の **出力** パラメーター。  
  
    |**Output** パラメーターの型|Date データ型|  
    |-------------------------------|--------------------|  
    |SQL_DATE|**date**|  
    |SQL_SS_TIME2|**time**|  
    |SQL_TYPE_TIMESTAMP<br /><br /> \- または -<br /><br /> SQL_TIMESTAMP|**datetime**, **datetime2**|  
    |SQL_SS_TIMESTAMPOFFSET|**datetimeoffset**|  
  
 データが適切な入力パラメーターまたは出力パラメーターに格納されないと、パッケージは失敗します。  
  
###  <a name="WHERE_clauses"></a> WHERE 句でのパラメーターの使用  
 SELECT、INSERT、UPDATE、および DELETE コマンドには、多くの場合、WHERE 句が含まれています。WHERE 句は、SQL コマンドを限定するために、ソース テーブル内の各行が満たすべき条件を定義したフィルターの役割を果たします。 パラメーターは、WHERE 句で使用されるフィルター値を提供します。  
  
 パラメーター マーカーを使用して、パラメーター値を動的に指定できます。 SQL ステートメントで使用できるパラメーター マーカーとパラメーター名に関する規則は、SQL 実行タスクで使用される接続マネージャーの種類によって異なります。  
  
 次の表に、SELECT コマンドの例を接続マネージャーの種類別に示します。 INSERT、UPDATE、および DELETE ステートメントでも同様です。 この例では、SELECT を使用して、2 つのパラメーターで指定された値よりも **ProductID** の値が大きい製品と小さい製品を、[!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] の **Product** テーブルから返します。  
  
|接続の種類|SELECT 構文|  
|---------------------|-------------------|  
|EXCEL、ODBC、OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO (ADO)|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 この例では、次の名前のパラメーターが必要になります。  
  
-   EXCEL 接続マネージャーと OLE DB 接続マネージャーでは、パラメーター名 0 と 1 を使用します。 ODBC 接続では、1 と 2 を使用します。  
  
-   ADO 接続では、Param1 や Param2 など、任意の 2 つのパラメーター名を使用します。ただし、これらのパラメーター名は、パラメーター リストの序数位置によってマップされる必要があります。  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続では、パラメーター名 \@parmMinProductID と \@parmMaxProductID を使用します。  
  
###  <a name="Stored_procedures"></a> ストアド プロシージャでのパラメーターの使用  
 ストアド プロシージャを実行する SQL コマンドでは、パラメーター マッピングを使用することもできます。 パラメーター マーカーとパラメーター名の使用方法に関する規則は、パラメーター化クエリの規則と同様に、SQL 実行タスクで使用される接続マネージャーの種類によって異なります。  
  
 次の表に、EXEC コマンドの例を接続マネージャーの種類別に示します。 この例では、[!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] の **uspGetBillOfMaterials** ストアド プロシージャを実行します。 このストアド プロシージャでは、 `@StartProductID` 入力 `@CheckDate` **入力** を使用します。  
  
|接続の種類|EXEC 構文|  
|---------------------|-----------------|  
|EXCEL および OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> ODBC の呼び出し構文の詳細については、MSDN ライブラリの ODBC プログラマ リファレンスにある「[プロシージャのパラメーター](https://go.microsoft.com/fwlink/?LinkId=89462)」を参照してください。|  
|ADO (ADO)|IsQueryStoredProcedure が **False** に設定されている場合、`EXEC uspGetBillOfMaterials ?, ?`<br /><br /> IsQueryStoredProcedure が **True** に設定されている場合、`uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|IsQueryStoredProcedure が **False** に設定されている場合、`EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> IsQueryStoredProcedure が **True** に設定されている場合、`uspGetBillOfMaterials`|  
  
 出力パラメーターを使用するには、構文で各パラメーター マーカーの後に OUTPUT キーワードを指定する必要があります。 たとえば、`EXEC myStoredProcedure ? OUTPUT` という出力パラメーターの構文は正しい構文です。  
  
 Transact-SQL ストアド プロシージャでの入力パラメーターと出力パラメーターの使用の詳細については、「[EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)」を参照してください。  
 
### <a name="map-query-parameters-to-variables"></a>クエリ パラメーターを変数にマッピングする
このセクションでは、SQL 実行タスクでパラメーター化された SQL ステートメントを使用して、SQL ステートメント内の変数とパラメーター間のマッピングを作成する方法を説明します。  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、操作する [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  SQL 実行タスクがまだパッケージに含まれていない場合、SQL 実行タスクをパッケージの制御フローに追加します。 詳細については、「 [制御フローのタスクまたはコンテナーを追加または削除する](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)」を参照してください。  
  
5.  SQL 実行タスクをダブルクリックします。  
  
6.  パラメーター化 SQL コマンドを、次のいずれかの方法で指定します。  
  
    -   直接入力を使用して、SQLStatement プロパティに SQL コマンドを入力します。  
  
    -   直接入力を使用して、 **[クエリの作成]** をクリックし、クエリ ビルダーで用意されているグラフィック ツールを使用して、SQL コマンドを作成します。  
  
    -   ファイル接続を使用し、SQL コマンドが含まれるファイルを参照します。  
  
    -   変数を使用し、SQL コマンドが含まれる変数を参照します。  
  
     パラメーター化された SQL ステートメントで使用するパラメーター マーカーは、SQL 実行タスクが使用する接続の種類によって異なります。  
  
    |接続の種類|パラメーター マーカー|  
    |---------------------|----------------------|  
    |ADO (ADO)|?|  
    |ADO.NET および SQLMOBILE|\@\<パラメーター名>|  
    |ODBC|?|  
    |EXCEL および OLE DB|?|  
  
     次の表に、SELECT コマンドの例を接続マネージャーの種類別に示します。 パラメーターは、WHERE 句で使用されるフィルター値を提供します。 この例では、SELECT を使用して、2 つのパラメーターで指定された値よりも **ProductID** の値が大きい製品と小さい製品を、 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] の **Product** テーブルから返します。  
  
    |接続の種類|SELECT 構文|  
    |---------------------|-------------------|  
    |EXCEL、ODBC、OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO (ADO)|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
   
7.  **[パラメーター マッピング]** をクリックします。  
  
8.  パラメーター マッピングを追加するには、 **[追加]** をクリックします。  
  
9. **[パラメーター名]** ボックスに名前を入力します。  
  
     使用するパラメーター名は、SQL 実行タスクが使用する接続の種類によって異なります。  
  
    |接続の種類|[パラメーター名]|  
    |---------------------|--------------------|  
    |ADO (ADO)|Param1、Param2、...|  
    |ADO.NET および SQLMOBILE|\@\<パラメーター名>|  
    |ODBC|1、2、3、...|  
    |EXCEL および OLE DB|0、1、2、3、…|  
  
10. **[変数名]** 一覧で、変数を選択します。 詳細については、「 [パッケージ内のユーザー定義変数のスコープの追加、削除、変更](https://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e)」を参照してください。  
  
11. **[方向]** 一覧で、パラメーターが入力、出力、または戻り値のいずれであるかを指定します。  
  
12. **[データ型]** 一覧で、パラメーターのデータ型を設定します。  
  
    > [!IMPORTANT]  
    >  パラメーターのデータ型は、変数のデータ型と互換性がある必要があります。  
  
13. SQL ステートメントの各パラメーターに対して、手順 8. ～ 11. を繰り返します。  
  
    > [!IMPORTANT]  
    >  パラメーター マッピングの順序は、SQL ステートメントで使用されるパラメーターの順序と同じである必要があります。  
  
14. **[OK]** をクリックします。  

##  <a name="Return_codes"></a> リターン コードの値の取得  
 ストアド プロシージャは、リターン コードという整数値を返してプロシージャの実行状態を表すことができます。 SQL 実行タスクにリターン コードを実装するには、 **ReturnValue** 型のパラメーターを使用します。  
  
 次の表に、リターン コードを実装する EXEC コマンドの一部の例を接続の種類別に示します。 すべての例で、 **入力** パラメーターを使用します。 パラメーター マーカーとパラメーター名の使用方法に関する規則は、すべてのパラメーター型 (**Input**、**Output**、および **ReturnValue**) に適用される規則と同じです。  
  
 一部の構文では、パラメーターのリテラルがサポートされません。 その場合は、変数を使用してパラメーター値を指定する必要があります。  
  
|接続の種類|EXEC 構文|  
|---------------------|-----------------|  
|EXCEL および OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> ODBC の呼び出し構文の詳細については、MSDN ライブラリの ODBC プログラマ リファレンスにある「[プロシージャのパラメーター](https://go.microsoft.com/fwlink/?LinkId=89462)」を参照してください。|  
|ADO (ADO)|IsQueryStoreProcedure が **False**に設定されている場合、`EXEC ? = myStoredProcedure 1`<br /><br /> IsQueryStoreProcedure が **True**に設定されている場合、`myStoredProcedure`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|IsQueryStoreProcedure を **True**に設定します。<br /><br /> `myStoredProcedure`|  
  
 前の表に示した構文では、SQL 実行タスクは **[直接入力]** ソース タイプを使用してストアド プロシージャを実行します。 SQL 実行タスクは **[ファイル接続]** ソース タイプを使用してストアド プロシージャを実行することもできます。 SQL 実行タスクで **[直接入力]** または **[ファイル接続]** のどちらのソース タイプを使用するかに関係なく、 **ReturnValue** 型のパラメーターを使用してリターン コードを実装します。
  
 Transact-SQL ストアド プロシージャでのリターン コードの使用の詳細については、「[RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)」を参照してください。  
  
## <a name="result-sets-in-the-execute-sql-task"></a>SQL 実行タスクにおける結果セット
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージでは、タスクが使用する SQL コマンドの種類によって、SQL 実行タスクに結果セットが返されるかどうかが決まります。 たとえば、通常、SELECT ステートメントは結果セットを返しますが、INSERT ステートメントは返しません。  
  
 結果セットに含まれる内容も、SQL コマンドによって異なります。 たとえば、SELECT ステートメントからの結果セットに含まれる行数は、0 行、1 行、または多数行である場合があります。 ただし、カウントや合計を返す SELECT ステートメントの結果セットに含まれるのは 1 行だけです。  
  
 SQL 実行タスクで結果セットを使用すると、SQL コマンドが結果セットを返すかどうかを確認したり、その結果セットの内容を把握するだけでなく、その他の情報も取得できます。 SQL 実行タスクで結果セットを正しく使用する際に必要となる、追加の使用要件やガイドラインがあります。 以降では、こうした使用要件およびガイドラインについて説明します。  
  
-   [結果セットの種類の指定](#Result_set_type)  
  
-   [結果セットによる変数の設定](#Populate_variable_with_result_set)  
  
###  <a name="Result_set_type"></a> 結果セットの種類を指定する  
 SQL 実行タスクでサポートされている結果セットの種類は、次のとおりです。  
  
-   " **なし** " は、クエリが結果を返さない場合に使用される結果セットです。 たとえば、テーブルのレコードを追加、変更、および削除するクエリで使用されます。  
  
-   " **単一行** " は、クエリが返す行が 1 行のみの場合に使用される結果セットです。 たとえば、カウントや合計を返す SELECT ステートメントでこの結果セットが使用されます。  
  
-   " **完全な結果セット** " は、クエリが複数行を返す場合に使用される結果セットです。 たとえば、テーブル内のすべての行を取得する SELECT ステートメントでこの結果セットが使用されます。  
  
-   " **XML** " は、クエリが結果セットを XML 形式で返す場合に使用される結果セットです。 たとえば、FOR XML 句を含む SELECT ステートメントでこの結果セットが使用されます。  
  
 SQL 実行タスクが " **完全な結果セット** " の結果セットを使用し、クエリが複数の行セットを返す場合、タスクは最初の行セットのみを返します。 この行セットでエラーが発生すると、タスクはそのエラーをレポートします。 他の行セットでエラーが発生しても、タスクはエラーをレポートしません。  
  
###  <a name="Populate_variable_with_result_set"></a> 結果セットによる変数の設定  
 結果セットの種類が、単一行、行セット、または XML の場合、クエリが返す結果セットをユーザー定義の変数にバインドできます。  
  
 結果セットの種類が " **単一行**" の場合、列名を結果セットの名前として使用し、返される結果の列を変数にバインドしたり、列一覧の列の序数を結果セットの名前として使用できます。 たとえば、クエリ `SELECT Color FROM Production.Product WHERE ProductID = ?` の結果セットの名前は **Color** または **0**となります。 クエリが複数の列を返す場合に、すべての列の値にアクセスするには、各列を異なる変数にバインドする必要があります。 数字を結果セットの名前として使用し、列を変数にマップする場合、その数字はクエリの列一覧に列が表示される順序を示します。 たとえば、クエリ `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`では、 **Color** 列に 0 を、 **ListPrice** 列に 1 を使用します。 列名を結果セットの名前として使用できるかどうかは、タスクの構成で指定されているプロバイダーによって異なります。 すべてのプロバイダーで列名が使用できるわけではありません。  
  
 単一の値を返す一部のクエリには、列名が含まれないことがあります。 たとえば、ステートメント `SELECT COUNT (*) FROM Production.Product` からは列名が返されません。 返される結果にアクセスするには、結果名として序数位置 0 を使用します。 列名で返される結果にアクセスするには、列名を指定する AS \<エイリアス名> 句をクエリに含める必要があります。 ステートメント `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`では、 **CountOfProduct** 列を指定します。 その後、 **CountOfProduct** 列名または序数位置 0 を使用して、返された結果列にアクセスできます。  
  
 結果セットの種類が " **完全な結果セット** " または " **XML**" の場合、結果セット名には 0 を使用する必要があります。  
  
 結果セットの種類が " **単一行** " の結果セットに変数をマップする場合、変数のデータ型と結果セットに含まれる列のデータ型は互換性がある必要があります。 たとえば、 **String** データ型の列を含む結果セットを、数値データ型の変数にマップすることはできません。 **TypeConversionMode** プロパティを **Allowed**に設定すると、SQL 実行タスクは出力パラメーターとクエリ結果を結果が割り当てられている変数のデータ型に変換します。  
  
 XML 結果セットをマップできるのは、 **String** または **Object** データ型の変数のみです。 変数が **String** データ型の場合、SQL 実行タスクは文字列を返し、XML ソースは XML データを使用できます。 変数が **Object** データ型の場合、SQL 実行タスクはドキュメント オブジェクト モデル (DOM) オブジェクトを返します。  
  
 **完全な結果セット** は、 **Object** データ型の変数にマップする必要があります。 結果は、行セット オブジェクトとして返されます。 Foreach ループ コンテナーを使用して、Object 変数に格納されたテーブル行の値をパッケージ変数に抽出し、その後、スクリプト タスクを使用して、パッケージ変数に格納されたデータをファイルに書き出すことができます。 Foreach ループ コンテナーとスクリプト タスクを使用したこの処理方法のデモについては、msftisprodsamples.codeplex.com の CodePlex サンプル「 [Execute SQL Parameters and Result Sets (SQL 実行パラメーターと結果セット)](https://go.microsoft.com/fwlink/?LinkId=157863)」を参照してください。  
  
 次の表は、結果セットにマップできる変数のデータ型をまとめたものです。  
  
|結果セットの種類|変数のデータ型|オブジェクトの種類|  
|---------------------|---------------------------|--------------------|  
|単一行|結果セット内の型列と互換性のあるすべての型|適用なし|  
|完全な結果セット|**オブジェクト**|タスクで ADO、OLE DB、Excel、および ODBC 接続マネージャーを含むネイティブ接続マネージャー使用する場合、返されるオブジェクトは ADO **Recordset**です。<br /><br /> タスクで [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーなどのマネージド接続マネージャーを使用する場合、返されるオブジェクトは **System.Data.DataSet** です。<br /><br /> 次の例に示すように、スクリプト タスクを使用して、 **System.Data.DataSet** オブジェクトにアクセスできます。<br /><br /> `Dim dt As Data.DataTable`<br /><br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet) dt = ds.Tables(0)`|  
|XML|**String**|**String**|  
|XML|**オブジェクト**|タスクで ADO、OLE DB、Excel、および ODBC 接続マネージャーを含むネイティブ接続マネージャー使用する場合、返されるオブジェクトは **MSXML6.IXMLDOMDocument**です。<br /><br /> タスクで [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーなどのマネージド接続マネージャーを使用する場合、返されるオブジェクトは **System.Xml.XmlDocument** です。|  
  
 変数は、SQL 実行タスクまたはパッケージのスコープ内で定義できます。 変数にパッケージ スコープがある場合、結果セットはパッケージ内の他のタスクやコンテナーで利用できます。また、パッケージ実行タスクや DTS 2000 パッケージ実行タスクが実行する任意のパッケージでも利用できます。  
  
 変数を **単一行** の結果セットにマップすると、次の条件が満たされている場合、SQL ステートメントによって返される、文字列以外の値が、文字列に変換されることがあります。  
  
-   **TypeConversionMode** プロパティが true に設定されている。 プロパティ値は、プロパティ ウィンドウで設定するか、 **SQL 実行タスク エディター**を使用して設定します。  
  
-   変換によってデータが切り捨てられない。  
  
## <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>結果セットを SQL 実行タスクの変数にマップする
このセクションでは、結果セットと SQL 実行タスクの変数との間のマッピングを作成する方法について説明します。 結果セットを変数にマップすることで、結果セットをパッケージ内の他の要素で使用できるようになります。 たとえば、スクリプト タスクのスクリプトでは、変数を読み取ってから、結果セットからの値を使用できます。XML ソースでは、変数に格納された結果セットを利用できます。 親パッケージで結果セットが生成される場合、パッケージ実行タスクから呼び出された子パッケージでその結果セットを使用できるようにするには、結果セットを親パッケージ内の変数にマップしてから、子パッケージ内で親パッケージの変数構成を作成して、親変数の値を格納します。  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  **ソリューション エクスプローラー**で、パッケージをダブルクリックして開きます。  
  
3.  **[制御フロー]** タブをクリックします。  
  
4.  SQL 実行タスクがまだパッケージに含まれていない場合、SQL 実行タスクをパッケージの制御フローに追加します。 詳細については、「 [制御フローのタスクまたはコンテナーを追加または削除する](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)」を参照してください。  
  
5.  SQL 実行タスクをダブルクリックします。  
  
6.  **[SQL 実行タスク エディター]** ダイアログ ボックスの **[全般]** ページで、 **[単一行]** 、 **[完全な結果セット]** 、 **[XML]** のいずれかの種類の結果セットを選択します。  

7.  **[結果セット]** をクリックします。  
  
8.  結果セット マッピングを追加するには、 **[追加]** をクリックします。  
  
9. **[変数名]** の一覧で、変数を選択するか、新しい変数を作成します。 詳細については、「 [パッケージ内のユーザー定義変数のスコープの追加、削除、変更](https://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e)」を参照してください。  
  
10. **[結果名]** の一覧で、必要に応じて結果セットの名前を変更します。  
  
     一般に、列名を結果セット名として使用することも、列リストでの列の序数位置を結果セットとして使用することもできます。 列名を結果セットの名前として使用できるかどうかは、タスクの構成で指定されているプロバイダーによって異なります。 すべてのプロバイダーで列名が使用できるわけではありません。  
  
11. **[OK]** をクリックします。  

## <a name="troubleshoot-the-execute-sql-task"></a>SQL 実行タスクのトラブルシューティング  
 SQL 実行タスクによる外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、SQL 実行タスクが実行する SQL コマンドに関するトラブルシューティングを行うことができます。 SQL 実行タスクによる外部データ プロバイダーの呼び出しのログを記録するには、パッケージ ログ記録を有効にして、パッケージ レベルで **Diagnostic** イベントを選択します。 詳細については、「[パッケージ実行のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。  
  
 SQL コマンドまたはストアド プロシージャから、複数の結果セットが返される場合があります。 このような結果セットには、 **SELECT** クエリの結果である行セットだけでなく、 **RAISERROR** ステートメントまたは **PRINT** ステートメントのエラーの結果である単一値も含まれています。 1 つ目以外の結果セット内のエラーがタスクで無視されるかどうかは、使用する接続マネージャーの種類によって異なります。  
  
-   OLE DB 接続マネージャーおよび ADO 接続マネージャーを使用する場合、1 つ目の結果セット以外はすべて無視されます。 したがって、これらの接続マネージャーでは、SQL コマンドまたはストアド プロシージャから返されるエラーは、1 つ目の結果セットに含まれていない限りタスクで無視されます。  
  
-   ODBC 接続マネージャーおよび ADO.NET 接続マネージャーを使用する場合、1 つ目の結果セット以外も無視されません。 これらの接続マネージャーでは、2 つ目以降の結果セットにエラーが含まれていると、エラーが発生してタスクが失敗します。  
  
### <a name="custom-log-entries"></a>カスタム ログ エントリ  
 次の表では、SQL 実行タスクのカスタム ログ エントリを説明します。 詳細については、「[Integration Services (SSIS) のログ記録](../../integration-services/performance/integration-services-ssis-logging.md)」をご覧ください。  
  
|ログ エントリ|[説明]|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|SQL ステートメントの実行フェーズに関する情報を提供します。 タスクがデータベースへの接続を取得したとき、SQL ステートメントの準備が開始されたとき、および SQL ステートメントの実行が完了した後に、ログ エントリが書き込まれます。 準備フェーズのログ エントリには、タスクで使用される SQL ステートメントが含まれます。|  

