---
title: OLE DB 変換先 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbdest.f1
- sql13.dts.designer.oledbdestadapter.connection.f1
- sql13.dts.designer.oledbdestadapter.mappings.f1
- sql13.dts.designer.oledbdestadapter.errorhandling.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a81d65cfd0716ba386db98b3d9973fb4e57876a7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298186"
---
# <a name="ole-db-destination"></a>OLE DB 変換先

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  OLE DB 変換先は、データベースのテーブルやビュー、または SQL コマンドを使用して、OLE DB に準拠するさまざまなデータベースにデータを読み込みます。 たとえば、OLE DB ソースにより、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータベースのテーブルにデータを読み込むことができます。  
  
> [!NOTE]  
>  データ ソースが [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 である場合、Excel の以前のバージョンとは異なる接続マネージャーが必要になります。 詳細については、「 [Excel ブックに接続する](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)」を参照してください。  
  
 OLE DB 変換先には、データを読み込むために、次の 5 つの異なるデータ アクセス モードが用意されています。  
  
-   テーブルまたはビュー。 既存のテーブルまたはビューを指定できます。または、新しいテーブルを作成できます。  
  
-   テーブルまたはビュー (高速読み込みオプションを使用)。 既存のテーブルを指定できます。または新しいテーブルを作成できます。  
  
-   変数で指定されたテーブルまたはビュー。  
  
-   変数で指定されたテーブルまたはビュー (高速読み込みオプションを使用)。  
  
-   SQL ステートメントの結果。  
  
> [!NOTE]  
>  OLE DB 変換先ではパラメーターがサポートされません。 パラメーター化された INSERT ステートメントを実行する必要がある場合は、OLE DB コマンド変換を検討してください。 詳細については、「 [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md)」を参照してください。  
  
 OLE DB 変換先で 2 バイト文字セット (DBCS) を使用するデータを読み込む際に、データ アクセス モードで高速読み込みオプションを使用せず、OLE DB 接続マネージャーが [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB) を使用している場合、そのデータは破損する可能性があります。 DBCS データの整合性を保持するには、OLE DB 接続マネージャーで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client を使用するように構成するか、次のどちらかの高速読み込みモードを使用する必要があります: **[テーブルまたはビュー - 高速読み込み]** または **[テーブル名またはビュー名の変数 - 高速読み込み]** 。 どちらのオプションも、 **[OLE DB 変換先エディター]** ダイアログ ボックスから使用できます。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] オブジェクト モデルをプログラミングするときは、AccessMode プロパティを **[OpenRowset での FastLoad の使用]** または **[Variable から FastLoad を使用して OpenRowset]** に設定する必要があります。  
  
> [!NOTE]  
>  **デザイナーの** [OLE DB 変換先エディター] [!INCLUDE[ssIS](../../includes/ssis-md.md)] ダイアログ ボックスを使用して、OLE DB 変換先がデータを挿入する変換先テーブルを作成する際に、新しく作成したテーブルを手動で選択する必要がある場合があります。 手動で選択する必要があるのは、OLE DB provider for DB2 などの OLE DB プロバイダーが、スキーマの識別子を自動的にテーブル名に追加した場合です。  
  
> [!NOTE]  
>  変換先の種類に応じて、 **[OLE DB 変換先エディター]** ダイアログ ボックスによって生成される CREATE TABLE ステートメントの変更が必要になる場合があります。 たとえば、変換先によっては CREATE TABLE ステートメントで使用されるデータ型をサポートしない場合もあります。  
  
 OLE DB 変換先は、OLE DB 接続マネージャーを使用してデータ ソースに接続します。OLE DB 接続マネージャーでは、使用する OLE DB プロバイダーを指定します。 詳細については、「 [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトでは、OLE DB 接続マネージャーを作成できるデータ ソース オブジェクトも用意されています。このオブジェクトは、データ ソースとデータ ソース ビューを OLE DB 変換先で使用できるようにします。  
  
 OLE DB 変換先には、入力列と変換先データ ソースの列との間のマッピングが含まれています。 入力列をすべての変換先列にマップする必要はありませんが、変換先列のプロパティによっては、変換先列にマップされる入力列がない場合、エラーが発生することがあります。 たとえば、入力先列で NULL 値が許容されていない場合は、入力列をその列にマップする必要があります。 また、マップされる列のデータ型には互換性がある必要があります。 たとえば、文字列データ型の入力列を数値データ型の変換先列にマップすることはできません。  
  
 OLE DB 変換先は、1 つの標準入力と 1 つのエラー出力をとります。  
  
 データ型の詳細については、「 [Integration Services のデータ型](../../integration-services/data-flow/integration-services-data-types.md)」を参照してください。  
  
## <a name="fast-load-options"></a>高速読み込みオプション  
 OLE DB 変換先で高速読み込みデータ アクセス モードが使用される場合、 **[OLE DB 変換先エディター]** のユーザー インターフェイスで、変換先に対して次の高速読み込みオプションを指定できます。  
  
-   インポートしたデータ ファイルの ID 値を保持します。または、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって割り当てられた一意の値を使用します。  
  
-   一括読み込み操作中に、NULL 値を保持します。  
  
-   一括インポート操作中に、インポート先のテーブルまたはビューに対して CHECK 制約を実行します。  
  
-   一括読み込み操作中に、テーブルレベルのロックを取得します。  
  
-   バッチの行数およびコミット サイズを指定します。  
  
 一部の高速読み込みオプションは、OLE DB 変換先の特定のプロパティに格納されています。 たとえば、ID 値を保持するかどうかを指定する FastLoadKeepIdentity、NULL 値を保持するかどうかを指定する FastLoadKeepNulls、バッチとしてコミットする行数を指定する FastLoadMaxInsertCommitSize などがあります。 その他の高速読み込みオプションは、FastLoadOptions プロパティのコンマ区切りリストで格納されます。 OLE DB 変換先で、FastLoadOptions に格納されている高速読み込みオプションと **[OLE DB 変換先エディター]** ダイアログ ボックスに一覧表示されている高速読み込みオプションをすべて使用する場合は、このプロパティの値を **TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000**に設定します。 値 1000 を設定すると、1,000 行のバッチを使用するように変換先が構成されます。  
  
> [!NOTE]  
>  変換先で制約が失敗すると、FastLoadMaxInsertCommitSize で定義された行数のバッチ全体が失敗します。  
  
 **[OLE DB 変換先エディター]** ダイアログ ボックスで公開される高速読み込みオプションに加えて、 **[詳細エディター]** ダイアログ ボックスで、FastLoadOptions プロパティに次の一括読み込みオプションを入力することにより、それらのオプションを使用するように OLE DB 変換先を構成できます。  
  
|高速読み込みオプション|[説明]|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|挿入するサイズを KB 単位で指定します。 このオプションの形式は、**KILOBYTES_PER_BATCH** = \<正の整数 **>** です。|  
|FIRE_TRIGGERS|挿入テーブルでトリガーを起動するかどうかを指定します。 このオプションの形式は、 **FIRE_TRIGGERS**です。 このオプションが指定されている場合は、トリガーが起動されます。|  
|ORDER|入力データの並べ替え方法を指定します。 このオプションの形式は、ORDER \<列名> ASC&#124;DESC です。 並べ替える列のリストには任意の数列を指定できます。並べ替え順序の指定は省略することもできます。 並べ替え順序を指定しなかった場合は、データを並べ替えないと見なして挿入操作が実行されます。<br /><br /> 注:ORDER オプションを使用してテーブル上のクラスター化インデックスに従って入力データを並べ替えると、パフォーマンスが向上する可能性があります。|  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] キーワードは慣例として通常は大文字で入力しますが、これらのキーワードの大文字小文字は区別されません。  
  
 高速読み込みオプションの詳細については、「[BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)」を参照してください。  
  
## <a name="troubleshooting-the-ole-db-destination"></a>OLE DB 変換先のトラブルシューティング  
 OLE DB 変換先による外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、OLE DB 変換先による外部データ ソースへのデータ保存に関するトラブルシューティングを行うことができます。 OLE DB 変換先による外部データ プロバイダーの呼び出しのログを記録するには、パッケージ ログ記録を有効にして、パッケージ レベルで **Diagnostic** イベントを選択します。 詳細については、「 [パッケージ実行のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。  
  
## <a name="configuring-the-ole-db-destination"></a>OLE DB 変換先の構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [OLE DB カスタム プロパティ](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
 プロパティの設定方法の詳細については、次のトピックのいずれかを参照してください。  
  
-   [OLE DB 変換先を使用してデータを読み込む](../../integration-services/data-flow/load-data-by-using-the-ole-db-destination.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="ole-db-destination-editor-connection-manager-page"></a>[OLE DB 変換先エディター] ([接続マネージャー] ページ)
  **[OLE DB 変換先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、変換先の OLE DB 接続を選択できます。 さらにこのページを使用して、データベースのテーブルやビューを選択できます。  
  
> [!NOTE]  
>  データ ソースが [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 である場合、Excel の以前のバージョンとは異なる接続マネージャーが必要になります。 詳細については、「 [Excel ブックに接続する](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)」を参照してください。  
  
> [!NOTE]  
>  OLE DB 変換先の **CommandTimeout** プロパティは、 **[OLE DB 変換先エディター]** ではアクセスできませんが、 **[詳細エディター]** を使用して設定できます。 また、一部の高速読み込みオプションは **[詳細エディター]** でしか使用できません。 これらのプロパティの詳細については、「 [OLE DB カスタム プロパティ](../../integration-services/data-flow/ole-db-custom-properties.md)」の OLE DB 変換先に関するセクションを参照してください。  
  
### <a name="static-options"></a>静的オプション  
 **[キャッシュなし]**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[OLE DB 接続マネージャーの構成]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **[データ アクセス モード]**  
 データを変換先に読み込む方法を指定します。 2 バイト文字セット (DBCS) データを読み込むには、高速読み込みオプションのいずれかを使用する必要があります。 一括挿入用に最適化された高速読み込みデータ アクセス モードの詳細については、「 [OLE DB 変換先](../../integration-services/data-flow/ole-db-destination.md)」を参照してください。  
  
|オプション|[説明]|  
|------------|-----------------|  
|[テーブルまたはビュー]|データを OLE DB 変換先のテーブルまたはビューに読み込みます。|  
|[テーブルまたはビュー - 高速読み込み]|高速読み込みオプションを使用し、データを OLE DB 変換先のテーブルまたはビューに読み込みます。 一括挿入用に最適化された高速読み込みデータ アクセス モードの詳細については、「 [OLE DB 変換先](../../integration-services/data-flow/ole-db-destination.md)」を参照してください。|  
|[テーブル名またはビュー名の変数]|テーブル名またはビュー名を変数で指定します。<br /><br /> **関連情報**:[パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|[テーブル名またはビュー名の変数 - 高速読み込み]|高速読み込みオプションを使用し、テーブル名またはビュー名を変数で指定します。 一括挿入用に最適化された高速読み込みデータ アクセス モードの詳細については、「 [OLE DB 変換先](../../integration-services/data-flow/ole-db-destination.md)」を参照してください。|  
|[SQL コマンド]|SQL クエリを使用し、データを OLE DB 変換先に読み込みます。|  
  
 **プレビュー**  
 **[クエリ結果のプレビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 プレビューでは、最大で 200 行を表示できます。  
  
### <a name="data-access-mode-dynamic-options"></a>データ アクセス モードの動的オプション  
 **[データ アクセス モード]** の各設定には、その設定に固有のオプションの動的なセットが表示されます。 次のセクションでは、各 **[データ アクセス モード]** 設定で使用可能な各動的オプションについて説明します。  
  
#### <a name="data-access-mode--table-or-view"></a>[データ アクセス モード] = [テーブルまたはビュー]  
 **[テーブル名またはビュー名]**  
 データ ソースで使用できるテーブルまたはビューの一覧から、テーブルまたはビューの名前を選択します。  
  
 **[新規作成]**  
 **[テーブルの作成]** ダイアログ ボックスを使用して新しいテーブルを作成します。  
  
> [!NOTE]  
>  **[新規作成]** をクリックすると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] により、接続されているデータ ソースに基づいて既定の CREATE TABLE ステートメントが生成されます。 基になるテーブルの列に FILESTREAM 属性が宣言されていても、この既定の CREATE TABLE ステートメントには FILESTREAM 属性が含まれません。 FILESTREAM 属性を使用して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントを実行するには、まず対象データベースに FILESTREAM ストレージを実装します。 次に、 **[テーブルの作成]** ダイアログ ボックスで CREATE TABLE ステートメントに FILESTREAM 属性を追加します。 詳細については、「[バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)」を参照してください。  
  
#### <a name="data-access-mode--table-or-view---fast-load"></a>[データ アクセス モード] = [テーブルまたはビュー - 高速読み込み]  
 **[テーブル名またはビュー名]**  
 この一覧を使用してデータベースからテーブルまたはビューを選択するか、 **[新規作成]** をクリックして新しいテーブルを作成します。  
  
 **[新規作成]**  
 **[テーブルの作成]** ダイアログ ボックスを使用して新しいテーブルを作成します。  
  
> [!NOTE]  
>  **[新規作成]** をクリックすると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] により、接続されているデータ ソースに基づいて既定の CREATE TABLE ステートメントが生成されます。 基になるテーブルの列に FILESTREAM 属性が宣言されていても、この既定の CREATE TABLE ステートメントには FILESTREAM 属性が含まれません。 FILESTREAM 属性を使用して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントを実行するには、まず対象データベースに FILESTREAM ストレージを実装します。 次に、 **[テーブルの作成]** ダイアログ ボックスで CREATE TABLE ステートメントに FILESTREAM 属性を追加します。 詳細については、「[バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)」を参照してください。  
  
 **[ID を保持する]**  
 データが読み込まれるときに ID 値をコピーするかどうかを指定します。 このプロパティは、高速読み取りオプションを指定した場合にのみ使用できます。 このプロパティの既定値は **false**です。  
  
 **[NULL を保持する]**  
 データが読み込まれるときに NULL 値をコピーするかどうかを指定します。 このプロパティは、高速読み取りオプションを指定した場合にのみ使用できます。 このプロパティの既定値は **false**です。  
  
 **[テーブル ロック]**  
 読み込み中にテーブルをロックするかどうかを指定します。 このプロパティの既定値は **true**です。  
  
 **CHECK 制約**  
 データの読み込み中に変換先で制約をチェックするかどうかを指定します。 このプロパティの既定値は **true**です。  
  
 **[バッチごとの行数]**  
 バッチ内の行数を指定します。 このプロパティの既定値は、 **-1**です。これは、割り当てられた値がないことを示します。  
  
> [!NOTE]  
>  このプロパティにカスタム値を割り当てない場合、 **[OLE DB 変換先エディター]** のテキスト ボックスをクリアします。  
  
 **[挿入コミット サイズの最大値]**  
 高速読み込み操作の実行中に OLE DB 変換先でコミットを試行するバッチ サイズを指定します。 値 **0** は、すべての行が処理された後、すべてのデータを 1 つのバッチでコミットすることを示します。  
  
> [!NOTE]  
>  値を **0** にすると、OLE DB 変換先と別のデータ フロー コンポーネントが同じソース テーブルを更新している場合に、実行中のパッケージが応答を停止する可能性があります。 パッケージが停止しないようにするには、 **[挿入コミット サイズの最大値]** オプションを **2147483647**に設定します。  
  
 このプロパティに値を指定すると、変換先で **[挿入コミット サイズの最大値]** 未満の行数のバッチがコミットされます。値を指定しない場合は、現在処理されているバッファー内の残りの行数がコミットされます。  
  
> [!NOTE]  
>  変換先で制約が失敗すると、 **[挿入コミット サイズの最大値]** で定義された行数のバッチ全体が失敗します。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>[データ アクセス モード] = [テーブル名またはビュー名の変数]  
 **[変数名]**  
 テーブル名またはビュー名を含む変数を選択します。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable---fast-load"></a>[データ アクセス モード] = [テーブル名またはビュー名の変数 - 高速読み込み]  
 **[変数名]**  
 テーブル名またはビュー名を含む変数を選択します。  
  
 **[新規作成]**  
 **[テーブルの作成]** ダイアログ ボックスを使用して新しいテーブルを作成します。  
  
> [!NOTE]  
>  **[新規作成]** をクリックすると、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] により、接続されているデータ ソースに基づいて既定の CREATE TABLE ステートメントが生成されます。 基になるテーブルの列に FILESTREAM 属性が宣言されていても、この既定の CREATE TABLE ステートメントには FILESTREAM 属性が含まれません。 FILESTREAM 属性を使用して [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] コンポーネントを実行するには、まず対象データベースに FILESTREAM ストレージを実装します。 次に、 **[テーブルの作成]** ダイアログ ボックスで CREATE TABLE ステートメントに FILESTREAM 属性を追加します。 詳細については、「[バイナリ ラージ オブジェクト &#40;Blob&#41; データ &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)」を参照してください。  
  
 **[ID を保持する]**  
 データが読み込まれるときに ID 値をコピーするかどうかを指定します。 このプロパティは、高速読み取りオプションを指定した場合にのみ使用できます。 このプロパティの既定値は **false**です。  
  
 **[NULL を保持する]**  
 データが読み込まれるときに NULL 値をコピーするかどうかを指定します。 このプロパティは、高速読み取りオプションを指定した場合にのみ使用できます。 このプロパティの既定値は **false**です。  
  
 **[テーブル ロック]**  
 読み込み中にテーブルをロックするかどうかを指定します。 このプロパティの既定値は **false**です。  
  
 **CHECK 制約**  
 タスクで制約をチェックするかどうかを指定します。 このプロパティの既定値は **false**です。  
  
 **[バッチごとの行数]**  
 バッチ内の行数を指定します。 このプロパティの既定値は、 **-1**です。これは、割り当てられた値がないことを示します。  
  
> [!NOTE]  
>  このプロパティにカスタム値を割り当てない場合、 **[OLE DB 変換先エディター]** のテキスト ボックスをクリアします。  
  
 **[挿入コミット サイズの最大値]**  
 高速読み込み操作の実行中に OLE DB 変換先でコミットを試行するバッチ サイズを指定します。 既定値の **2147483647** は、すべての行が処理された後、すべてのデータを 1 つのバッチでコミットすることを示します。  
  
> [!NOTE]  
>  値を **0** にすると、OLE DB 変換先と別のデータ フロー コンポーネントが同じソース テーブルを更新している場合に、実行中のパッケージが応答を停止する可能性があります。 パッケージが停止しないようにするには、 **[挿入コミット サイズの最大値]** オプションを **2147483647**に設定します。  
  
#### <a name="data-access-mode--sql-command"></a>[データ アクセス モード] = [SQL コマンド]  
 **[SQL コマンド テキスト]**  
 SQL クエリのテキストを入力し、 **[クエリの作成]** をクリックしてクエリを作成するか、 **[参照]** をクリックしてクエリ テキストを含むファイルを指定します。  
  
> [!NOTE]  
>  OLE DB 変換先ではパラメーターがサポートされません。 パラメーター化された INSERT ステートメントを実行する必要がある場合は、OLE DB コマンド変換を検討してください。 詳細については、「 [OLE DB Command Transformation](../../integration-services/data-flow/transformations/ole-db-command-transformation.md)」を参照してください。  
  
 **[クエリの作成]**  
 SQL クエリを視覚的に作成するには、 **[クエリ ビルダー]** ダイアログ ボックスを使用します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、SQL クエリのテキストが含まれているファイルを指定します。  
  
 **[クエリの解析]**  
 クエリ テキストの構文を検査します。  
  
## <a name="ole-db-destination-editor-mappings-page"></a>[OLE DB 変換先エディター] ([マッピング] ページ)
  **[OLE DB 変換先エディター]** ダイアログ ボックスの **[マッピング]** ページを使用すると、入力列を変換先列にマップできます。  
  
### <a name="options"></a>オプション  
 **使用できる入力列**  
 使用できる入力列の一覧を表示します。 ドラッグ アンド ドロップ操作により、テーブル内の使用できる入力列を変換先列にマップします。  
  
 **使用できる変換先列**  
 使用できる変換先列の一覧を表示します。 ドラッグ アンド ドロップ操作により、テーブル内の使用できる変換先列を入力列にマップします。  
  
 **入力列**  
 選択した入力列を表示します。 出力から列を除外するために **\<無視>** を選択することで、マッピングを削除できます。  
  
 **変換先列**  
 マップするかどうかにかかわらず、使用できる変換先列を表示します。  
  
## <a name="ole-db-destination-editor-error-output-page"></a>[OLE DB 変換先エディター] ([エラー出力] ページ)
  **[OLE DB 変換先エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを指定できます。  
  
### <a name="options"></a>オプション  
 **[入力または出力]**  
 入力の名前を表示します。  
  
 **列**  
 使用されていません。  
  
 **Error**  
 エラーが発生した場合に、障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **関連項目:** [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **切り捨て**  
 使用されていません。  
  
 **[説明]**  
 操作の説明を表示します。  
  
 **[選択したセルに設定する値]**  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルに対して障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **[適用]**  
 選択したセルにエラー処理オプションを適用します。  
  
## <a name="related-content"></a>関連コンテンツ  
 [OLE DB ソース](../../integration-services/data-flow/ole-db-source.md)  
  
 [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)  
  
 [データ フロー](../../integration-services/data-flow/data-flow.md)  
  
  
