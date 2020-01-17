---
title: SQL Server オブジェクトの転送タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transfersqlserverobjectstask.f1
- sql13.dts.designer.transfersqlserverobjects.general.f1
- sql13.dts.designer.transfersqlserverobjects.objects.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4f1a2e2122c4d141d8d702d027bf30d65db93f9c
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293843"
---
# <a name="transfer-sql-server-objects-task"></a>SQL Server オブジェクトの転送タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内の 1 つ以上の種類のオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス間で転送します。 たとえば、このタスクを使用して、テーブルやストアド プロシージャをコピーできます。 転送元として使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンに応じて、コピーできるオブジェクトの種類が異なります。 たとえば、スキーマとユーザー定義集計は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースだけに含まれます。  
  
## <a name="objects-to-transfer"></a>転送するオブジェクト  
 転送するオブジェクトの権限に加えて、指定したデータベースのサーバー ロール、ロール、およびユーザーもコピーできます。 関連付けられているユーザー、ロール、および権限をオブジェクトと一緒にコピーすることで、転送したオブジェクトを転送先サーバー上ですぐに利用できます。  
  
 次の表に、コピーできるオブジェクトを示します。  
  
|Object|  
|------------|  
|テーブル|  
|ビュー|  
|ストアド プロシージャ|  
|ユーザー定義関数|  
|デフォルト|  
|ユーザー定義のデータ型|  
|パーティション関数|  
|パーティション構成|  
|スキーマ|  
|アセンブリ|  
|ユーザー定義集計|  
|ユーザー定義型|  
|XML スキーマ コレクション|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで作成されたユーザー定義型 (UDT) には、共通言語ランタイム (CLR) アセンブリに対する依存関係があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクを使用して UDT を転送する場合、依存オブジェクトを転送するタスクを構成する必要もあります。 依存オブジェクトを転送するには、 **IncludeDependentObjects** プロパティを **True**に設定します。  
  
### <a name="table-options"></a>テーブル オプション  
 テーブルをコピーする際には、コピー プロセスに含めるテーブル関連のアイテムの種類を指定できます。 次の種類のアイテムは、関連するテーブルと共にコピーできます。  
  
-   インデックス  
  
-   トリガー  
  
-   フルテキスト インデックス  
  
-   主キー  
  
-   外部キー  
  
 また、タスクで生成するスクリプトを Unicode 形式にするかどうかも指定できます。  
  
## <a name="destination-options"></a>転送先に関するオプション  
 転送するオブジェクトのスキーマ名、データ、拡張プロパティ、および依存オブジェクトを転送に含めるように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクを構成できます。 データをコピーする場合、置換するか、既存のデータを追加できます。  
  
 一部のオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のみに適用されます。 たとえば、スキーマは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのみサポートされます。  
  
## <a name="security-options"></a>セキュリティ オプション  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクでは、転送元の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースレベルのユーザーとロール、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン、および転送するオブジェクトの権限を含めることができます。 たとえば、転送するテーブルの権限を転送に含めることができます。  
  
## <a name="transfer-objects-between-instances-of-sql-server"></a>SQL Server のインスタンス間でのオブジェクトの転送  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の転送元および転送先をサポートします。  
  
## <a name="events"></a>イベント  
 このタスクは、転送されたオブジェクトを報告する情報イベントを生成する以外に、オブジェクトが上書きされたときに警告イベントを生成します。 情報イベントは、データベース テーブルの切り捨てなどのアクションに対しても生成されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクでは、オブジェクト転送の進捗状況は報告されません。0% または 100% 完了した場合のみ報告されます。  
  
## <a name="execution-value"></a>実行値  
 このタスクの **ExecutionValue** プロパティに格納される実行値は、転送されたオブジェクトの数を返します。 SQL Server オブジェクトの転送タスクの **ExecValueVariable** プロパティにユーザー定義変数を割り当てると、オブジェクト転送に関する情報をパッケージの他のオブジェクトで使用できるようになります。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)」と「[パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)」をご覧ください。  
  
## <a name="log-entries"></a>ログ エントリ  
 SQL Server オブジェクトの転送タスクには、次のようなカスタム ログ エントリがあります。  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects   転送が開始されたことを報告するログ エントリです。 ログ エントリには、開始時刻が含まれます。  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects    転送が完了したことを報告このログ エントリです。 ログ エントリには、終了時刻が含まれます。  
  
 また、 **OnInformation** イベントのログ エントリは、転送対象として選択された種類のオブジェクトの数、転送されたオブジェクトの数、およびテーブルと一緒にデータが転送されたときはテーブルの切り捨てなどのアクションを報告します。 **OnWarning** イベントのログ エントリは転送先でオブジェクトが上書きされると書き込まれます。  
  
## <a name="security-and-permissions"></a>セキュリティおよび権限  
 ユーザーは、転送元サーバー上でオブジェクトを参照する権限、および転送先サーバー上でオブジェクトを削除および作成する権限を持っていることに加えて、指定したデータベースおよびデータベース オブジェクトにアクセスできる必要があります。  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>SQL Server オブジェクトの転送タスクの構成  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクを構成して、すべてのオブジェクト、特定の種類のすべてのオブジェクト、または特定の種類の指定したオブジェクトを転送の対象とすることができます。 たとえば、AdventureWorks データベース内の選択したテーブルのみをコピーするように指定できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクを使用してテーブルを転送する場合は、テーブルと一緒にコピーする、テーブルに関連するオブジェクトの種類を指定できます。 たとえば、テーブルと一緒に主キーをコピーするように指定できます。  
  
 転送するオブジェクトの機能をさらに強化するため、転送するオブジェクトのスキーマ名、データ、拡張プロパティ、および依存オブジェクトを転送に含めるように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクを構成できます。 データをコピーする場合は、既存のデータを置き換えるかまたは追加するかを指定できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクは実行時、2 つの SMO 接続マネージャーを使用して、転送元サーバーおよび転送先サーバーに接続します。 SMO 接続マネージャーの構成は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクとは別に行い、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクは SMO 接続マネージャーを参照します。 SMO 接続マネージャーは、サーバーと、サーバーに接続する際に使用する認証モードを指定します。 詳しくは、「 [SMO 接続マネージャー](../../integration-services/connection-manager/smo-connection-manager.md)」をご覧ください。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>プログラムによる SQL Server オブジェクトの転送タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
## <a name="transfer-sql-server-objects-task-editor-general-page"></a>[SQL オブジェクトの転送タスク エディター] ([全般] ページ)
  **[SQL オブジェクトの転送タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクの名前と説明を入力できます。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクを作成するユーザーは、転送元サーバー オブジェクトをコピー用に選択するために必要な権限と、オブジェクトの転送先の転送先サーバー データベースにアクセスするために必要な権限を持っている必要があります。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクの一意な名前を入力します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクの説明を入力します。  
  
## <a name="transfer-sql-server-objects-task-editor-objects-page"></a>[SQL Server オブジェクトの転送タスク エディター] ([オブジェクト] ページ)
  **[SQL Server オブジェクトの転送タスク エディター]** ダイアログ ボックスの **[オブジェクト]** ページを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス間で 1 つまたは複数の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトをコピーするためのプロパティを指定できます。 コピーできる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトには、テーブル、ビュー、ストアド プロシージャ、およびユーザー定義関数などがあります。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクを作成するユーザーは、転送元サーバー オブジェクトをコピー用に選択するために必要な権限と、オブジェクトの転送先の転送先サーバー データベースにアクセスするために必要な権限を持っている必要があります。  
  
### <a name="static-options"></a>静的オプション  
 **SourceConnection**  
 SMO 接続マネージャーを一覧から選択するか、 **\<[新しい接続...]>** をクリックしてコピー元のサーバーへの新しい接続を作成します。  
  
 **[SourceDatabase]**  
 オブジェクトのコピー元の転送元サーバー上のデータベースを選択します。  
  
 **DestinationConnection**  
 SMO 接続マネージャーを一覧から選択するか、 **\<[新しい接続...]>** をクリックしてコピー先のサーバーへの新しい接続を作成します。  
  
 **[DestinationDatabase]**  
 オブジェクトのコピー先の転送先サーバー上のデータベースを選択します。  
  
 **[DropObjectsFirst]**  
 選択したオブジェクトをコピーを開始する前に転送先サーバー上で削除するかどうかを選択します。  
  
 **[IncludeExtendedProperties]**  
 転送元サーバーから転送先サーバーにオブジェクトをコピーするときに拡張プロパティを含めるかどうかを選択します。  
  
 **[CopyData]**  
 転送元サーバーから転送先サーバーにオブジェクトをコピーするときにデータを含めるかどうかを選択します。  
  
 **[ExistingData]**  
 転送先サーバーにデータをどのようにコピーするかを指定します。 このプロパティには、次の表に示すオプションがあります。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**[置換]**|転送先サーバー上のデータは上書きされます。|  
|**追加**|転送元サーバーからコピーされたデータは、転送先サーバー上の既存のデータに追加されます。|  
  
> [!NOTE]  
>  **[ExistingData]** オプションは、 **[CopyData]** が **[True]** に設定されている場合にのみ使用できます。  
  
 **[CopySchema]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクによる処理中にスキーマをコピーするかどうかを選択します。  
  
> [!NOTE]  
>  **[CopySchema]** は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのみ使用できます。  
  
 **[UseCollation]**  
 転送元サーバー上で指定されている照合順序をオブジェクトの転送に含めるかどうかを選択します。  
  
 **[IncludeDependentObjects]**  
 コピーの対象として選択されたオブジェクトをコピーするときに、そのオブジェクトに依存している他のオブジェクトもコピーするかどうかを選択します。  
  
 **[CopyAllObjects]**  
 指定した転送元データベース内のすべてのオブジェクトをコピーするか、選択したオブジェクトだけをコピーするかを選択します。  このオプションを [False] に設定すると、オブジェクトを転送するためのオプションが表示され、さらに **[CopyAllObjects]** セクションに動的オプションが表示されます。  
  
 **[ObjectsToCopy]**  
 **[ObjectsToCopy]** を展開して、転送元データベースから転送先データベースにコピーするオブジェクトを指定します。  
  
> [!NOTE]  
>  **[ObjectsToCopy]** は、 **[CopyAllObjects]** が **[False]** に設定されている場合にのみ使用できます。  
  
 次の種類のオブジェクトをコピーするオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのみサポートされます。  
  
 アセンブリ  
  
 パーティション関数  
  
 パーティション構成  
  
 スキーマ  
  
 ユーザー定義集計  
  
 ユーザー定義データ型  
  
 XML スキーマ コレクション  
  
 **[CopyDatabaseUsers]**  
 データベース ユーザーを転送に含めるかどうかを指定します。  
  
 **[CopyDatabaseRoles]**  
 データベース ロールを転送に含めるかどうかを指定します。  
  
 **[CopySqlServerLogins]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを転送に含めるかどうかを指定します。  
  
 **[CopyObjectLevelPermissions]**  
 オブジェクトレベルの権限を転送に含めるかどうかを指定します。  
  
 **[CopyIndexes]**  
 インデックスを転送に含めるかどうかを指定します。  
  
 **[CopyTriggers]**  
 トリガーを転送に含めるかどうかを指定します。  
  
 **[CopyFullTextIndexes]**  
 フルテキスト インデックスを転送に含めるかどうかを指定します。  
  
 **[CopyPrimaryKeys]**  
 主キーを転送に含めるかどうかを指定します。  
  
 **[CopyForeignKeys]**  
 外部キーを転送に含めるかどうかを指定します。  
  
 **[GenerateScriptsInUnicode]**  
 転送スクリプトを Unicode 形式で生成するかどうかを指定します。  
  
### <a name="dynamic-options"></a>動的オプション  
  
#### <a name="copyallobjects--false"></a>[CopyAllObjects] = [False]  
 **[CopyAllTables]**  
 指定した転送元データベース内のすべてのテーブルをコピーするか、選択したテーブルだけをコピーするかを選択します。  
  
 **[TablesList]**  
 **[テーブルの選択]** ダイアログ ボックスが開きます。  
  
 **[CopyAllViews]**  
 指定した転送元データベース内のすべてのビューをコピーするか、選択したビューだけをコピーするかを選択します。  
  
 **[ViewsList]**  
 **[ビューの選択]** ダイアログ ボックスが開きます。  
  
 **[CopyAllStoredProcedures]**  
 指定した転送元データベース内のすべてのユーザー定義ストアド プロシージャをコピーするか、選択したプロシージャだけをコピーするかを選択します。  
  
 **[StoredProceduresList]**  
 **[ストアド プロシージャの選択]** ダイアログ ボックスが開きます。  
  
 **[CopyAllUserDefinedFunctions]**  
 指定した転送元データベース内のすべてのユーザー定義関数 (UDF) をコピーするか、選択した UDF だけをコピーするかを選択します。  
  
 **[UserDefinedFunctionsList]**  
 **[ユーザー定義関数の選択]** ダイアログ ボックスが開きます。  
  
 **[CopyAllDefaults]**  
 指定した転送元データベース内のすべての既定値をコピーするか、選択した既定値だけをコピーするかを選択します。  
  
 **[DefaultsList]**  
 **[既定値の選択]** ダイアログ ボックスが開きます。  
  
 **[CopyAllUserDefinedDataTypes]**  
 指定した転送元データベース内のすべてのユーザー定義データ型をコピーするか、選択したユーザー定義データ型だけをコピーするかを選択します。  
  
 **[UserDefinedDataTypesList]**  
 **[ユーザー定義データ型の選択]** ダイアログ ボックスが開きます。  
  
 **[CopyAllPartitionFunctions]**  
 指定した転送元データベース内のすべてのユーザー定義パーティション関数をコピーするか、選択したパーティション関数だけをコピーするかを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのみサポートされます。  
  
 **[PartitionFunctionsList]**  
 **[パーティション関数の選択]** ダイアログ ボックスが開きます。  
  
 **[CopyAllPartitionSchemes]**  
 指定した転送元データベース内のすべてのパーティション構成をコピーするか、選択したパーティション構成だけをコピーするかを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのみサポートされます。  
  
 **[PartitionSchemesList]**  
 **[パーティション構成の選択]** ダイアログ ボックスが開きます。  
  
 **[CopyAllSchemas]**  
 指定した転送元データベース内のすべてのスキーマをコピーするか、選択したスキーマだけをコピーするかを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのみサポートされます。  
  
 **[SchemasList]**  
 **[スキーマの選択]** ダイアログ ボックスが開きます。  
  
 **[CopyAllSqlAssemblies]**  
 指定した転送元データベース内のすべての SQL アセンブリをコピーするか、選択した SQL アセンブリだけをコピーするかを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのみサポートされます。  
  
 **[SqlAssembliesList]**  
 **[SQL アセンブリの選択]** ダイアログ ボックスが開きます。  
  
 **[CopyAllUserDefinedAggregates]**  
 指定した転送元データベース内のすべてのユーザー定義集計をコピーするか、選択したユーザー定義集計だけをコピーするかを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのみサポートされます。  
  
 **[UserDefinedAggregatesList]**  
 **[ユーザー定義集計の選択]** ダイアログ ボックスが開きます。  
  
 **[CopyAllUserDefinedTypes]**  
 指定した転送元データベース内のすべてのユーザー定義型 (UDT) をコピーするか、選択した UDT だけをコピーするかを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのみサポートされます。  
  
 **[UserDefinedTypes]**  
 **[ユーザー定義型の選択]** ダイアログ ボックスが開きます。  
  
 **[CopyAllXmlSchemaCollections]**  
 指定した転送元データベース内のすべての XML スキーマ コレクションをコピーするか、選択した XML スキーマ コレクションだけをコピーするかを選択します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのみサポートされます。  
  
 **[XmlSchemaCollectionsList]**  
 **[XML スキーマ コレクションの選択]** ダイアログ ボックスが開きます。  
  
## <a name="see-also"></a>参照  
 [Integration Services のエラーおよびメッセージのリファレンス](../../integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services タスク](../../integration-services/control-flow/integration-services-tasks.md)   
 [[SQL Server オブジェクトの転送タスク エディター] &#40;[全般] ページ&#41;](../../integration-services/control-flow/transfer-sql-server-objects-task-editor-general-page.md)   
 [[式] ページ](../../integration-services/expressions/expressions-page.md)   
 [一括インポートまたは一括エクスポートのデータ形式 &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [SQL Server インストールにおけるセキュリティの考慮事項](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
