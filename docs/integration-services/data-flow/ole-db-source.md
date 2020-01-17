---
title: OLE DB ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbsource.f1
- sql13.dts.designer.oledbsourceadapter.connection.f1
- sql13.dts.designer.oledbsourceadapter.columns.f1
- sql13.dts.designer.oledbsourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b0793c48a6ea531dbca499b07ca28be9601e5843
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292233"
---
# <a name="ole-db-source"></a>OLE DB ソース

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  OLE DB ソースは、データベース テーブル、ビュー、または SQL コマンドを使用して、OLE DB に準拠するさまざまなリレーショナル データベースからデータを抽出します。 たとえば、OLE DB ソースにより、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのテーブルからデータを抽出できます。  
  
> [!NOTE]  
>  データ ソースが [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 である場合、Excel の以前のバージョンとは異なる接続マネージャーが必要になります。 詳細については、「 [Excel ブックに接続する](../../integration-services/connection-manager/connect-to-an-excel-workbook.md)」を参照してください。  
  
 OLE DB ソースには、データを抽出するために、次の 4 つの異なるデータ アクセス モードが用意されています。  
  
-   テーブルまたはビュー。  
  
-   変数で指定されたテーブルまたはビュー。  
  
-   SQL ステートメントの結果。 クエリにはパラメーター化クエリを使用できます。  
  
-   変数に格納された SQL ステートメントの結果。  
  
> [!NOTE]  
>  SQL ステートメントを使用して、一時テーブルから結果を返すストアド プロシージャが呼び出す場合は、WITH RESULT SETS オプションを使用して結果セットのメタデータを定義します。  
  
 パラメーター化クエリを使用すると、変数をパラメーターにマップして、SQL ステートメント内の個別のパラメーターの値を指定できます。  
  
 OLE DB ソースは、OLE DB 接続マネージャーを使用してデータ ソースに接続します。OLE DB 接続マネージャーは、使用する OLE DB プロバイダーを指定します。 詳細については、「 [OLE DB 接続マネージャー](../../integration-services/connection-manager/ole-db-connection-manager.md)」を参照してください。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] プロジェクトでは、OLE DB 接続マネージャーを作成できるデータ ソース オブジェクトも用意されています。このオブジェクトは、データ ソースとデータ ソース ビューを OLE DB ソースで使用できるようにします。  
  
 OLE DB プロバイダーによっては、OLE DB ソースに次のような制限が生じる場合があります。  
  
-   Oracle 用の [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB プロバイダーは、Oracle データ型の BLOB、CLOB、NCLOB、BFILE、および UROWID 型をサポートしていないため、OLE DB ソースは、これらのデータ型の列が含まれるテーブルからデータを抽出できません。  
  
-   IBM OLE DB DB2 プロバイダーおよび [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB DB2 プロバイダーは、ストアド プロシージャを呼び出す SQL コマンドの使用をサポートしていません。 この種類のコマンドを使用すると、OLE DB ソースは列のメタデータを作成できません。その結果、データ フロー内で OLE DB ソースの後に実行されるデータ フロー コンポーネントでは、使用できる列データがないため、データ フローの実行が失敗します。  
  
 OLE DB ソースは、1 つの標準出力と 1 つのエラー出力をとります。  
  
## <a name="using-parameterized-sql-statements"></a>パラメーター化された SQL ステートメントの使用  
 OLE DB ソースは、SQL ステートメントを使用してデータを抽出できます。 使用できるのは、SELECT ステートメントまたは EXEC ステートメントです。  
  
 OLE DB ソースは、OLE DB 接続マネージャーを使用して、データの抽出元からデータ ソースに接続します。 OLE DB 接続マネージャーが使用するプロバイダー、および接続マネージャーの接続先であるリレーショナル データベース管理システム (RDBMS) によって、異なる規則がパラメーターの名前付けや一覧表示に適用されます。 パラメーター名が RDBMS から返される場合、パラメーター名を使用して、パラメーター リストのパラメーターを SQL ステートメントのパラメーターにマップできます。それ以外の場合は、パラメーターがパラメーター リストの序数位置によって SQL ステートメントのパラメーターにマップされます。 サポートされるパラメーター名の種類は、プロバイダーによって異なります。 たとえば、変数名または列名の使用を必要とするプロバイダーや、0 や Param0 などのシンボルの名前の使用を必要とするプロバイダーがあります。 SQL ステートメントで使用するパラメーター名の詳細については、プロバイダー固有のマニュアルを参照してください。  
  
 OLE DB 接続マネージャーを使用する場合、パラメーター化サブクエリは使用できません。これは、OLE DB ソースが OLE DB プロバイダーを介してパラメーター情報を取得できないからです。 ただし、式を使用することで、パラメーター値をクエリ文字列に連結したり、ソースの SqlCommand プロパティを設定したりできます。 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでは、 **[OLE DB ソース エディター]** ダイアログ ボックスを使用して OLE DB ソースを構成し、 **[クエリ パラメーターの設定]** ダイアログ ボックスで変数にパラメーターをマップします。  
  
### <a name="specifying-parameters-by-using-ordinal-positions"></a>序数位置を使用したパラメーターの指定  
 パラメーター名が返されない場合は、 **[クエリ パラメーターの設定]** ダイアログ ボックスの **[パラメーター]** ボックスの一覧にパラメーターが表示されている順序で、実行時にパラメーターがどのパラメーター マーカーにマップされるかが決まります。 一覧に表示されている最初のパラメーターは SQL ステートメントの最初の ? にマップされ、 2 番目のパラメーターは 2 番目の ? にマップされ、それ以降同様にマップされます  
  
 次の SQL ステートメントは、 **データベースの** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] テーブルから行を選択します。 **[マッピング]** ボックスの一覧に表示される最初のパラメーターは **Color** 列の最初のパラメーターに、2 番目のパラメーターは **Size** 列にマップされます。  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 パラメーター名は順序に影響しません。 たとえば、パラメーターの名前が適用先の列と同じ名前で、そのパラメーターが **[パラメーター]** ボックス内の正しい序数位置にない場合も、実行時に行われるパラメーター マッピングには、パラメーター名ではなく、パラメーターの序数位置が使用されます。  
  
 通常、EXEC コマンドでは、プロシージャのパラメーター値を指定する変数の名前をパラメーター名として使用する必要があります。  
  
### <a name="specifying-parameters-by-using-names"></a>名前を使用したパラメーターの指定  
 実際のパラメーター名が RDBMS から返される場合、SELECT ステートメントと EXEC ステートメントで使用されるパラメーターは名前によってマップされます。 このパラメーター名は、SELECT ステートメントまたは EXEC ステートメントによって実行されるストアド プロシージャで必要な名前と一致する必要があります。  
  
 次の SQL ステートメントは、 **データベースで利用できる** uspGetWhereUsedProductID [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] ストアド プロシージャを実行します。  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 このストアド プロシージャでは、パラメーター値を指定するために変数 `@StartProductID` と `@CheckDate`を必要としています。 パラメーターが **[マッピング]** ボックスの一覧に表示される順序は関係ありません。 ここで必要となるのは、パラメーター名が、\@ 記号を含めて、ストアド プロシージャの変数名と一致することのみです。  
  
### <a name="mapping-parameters-to-variables"></a>パラメーターの変数へのマッピング  
 パラメーターは、実行時にパラメーター値を提供する変数にマップされます。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] に用意されているシステム変数を使用することもできますが、通常はユーザー定義変数を使用します。 ユーザー定義変数を使用する場合、この変数に設定するデータ型は、パラメーター参照がマップされている列のデータ型との互換性があることを確認してください。 詳細については、「 [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)」を参照してください。  
  
## <a name="troubleshooting-the-ole-db-source"></a>OLE DB ソースのトラブルシューティング  
 OLE DB ソースによる外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、OLE DB ソースによる外部データ ソースからのデータ読み込みに関するトラブルシューティングを行うことができます。 OLE DB ソースによる外部データ プロバイダーの呼び出しのログを記録するには、パッケージ ログ記録を有効にして、パッケージ レベルで **Diagnostic** イベントを選択します。 詳細については、「 [パッケージ実行のトラブルシューティング ツール](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)」を参照してください。  
  
## <a name="configuring-the-ole-db-source"></a>OLE DB ソースの構成  
 プロパティはプログラムによって設定するか、または [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから設定できます。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが反映されます。 **[詳細エディター]** ダイアログ ボックスまたはプログラムで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [OLE DB カスタム プロパティ](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [OLE DB ソースを使用してデータを抽出する](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)  
  
-   [クエリ パラメーターをデータ フロー コンポーネントの変数にマップする](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [データ フロー コンポーネントのプロパティを設定する](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [マージ変換およびマージ結合変換用にデータを並べ替える](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 social.technet.microsoft.com の Wiki の記事「 [SSIS with Oracle Connectors](https://go.microsoft.com/fwlink/?LinkId=220670)(SSIS から Oracle への接続)」  
  
## <a name="ole-db-source-editor-connection-manager-page"></a>[OLE DB ソース エディター] ([接続マネージャー] ページ)
  **[OLE DB ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、ソースの OLE DB 接続マネージャーを選択できます。 さらにこのページを使用して、データベースのテーブルやビューを選択できます。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007 を使用するデータ ソースからデータを読み込むには、OLE DB ソースを使用します。 Excel ソースを使用して Excel 2007 データ ソースからデータを読み込むことはできません。 詳細については、「 [Configure OLE DB Connection Manager](../../integration-services/connection-manager/configure-ole-db-connection-manager.md)」 (OLE DB 接続マネージャーの構成) を参照してください。  
>   
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 以前のバージョンを使用するデータ ソースからデータを読み込むには、Excel ソースを使用します。 詳細については、「[[Excel ソース エディター] ([接続マネージャー] ページ)](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md)」を参照してください。  
  
> [!NOTE]  
>  OLE DB ソースの **CommandTimeout** プロパティは、 **[OLE DB ソース エディター]** ではアクセスできませんが、 **[詳細エディター]** を使用して設定できます。 このプロパティの詳細については、「 [OLE DB Custom Properties](../../integration-services/data-flow/ole-db-custom-properties.md)」(OLE DB のカスタム プロパティ) の Excel ソースのセクションを参照してください。  
  
### <a name="open-the-ole-db-source-editor-connection-manager-page"></a>OLE DB ソース エディターを開く ([接続マネージャー] ページ)  
  
1.  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] で、OLE DB ソースを [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]パッケージに追加します。  
  
2.  ソース コンポーネントを右クリックし、 **[編集]** をクリックします。  
  
3.  **[接続マネージャー]** をクリックします。  
  
### <a name="static-options"></a>静的オプション  
 **[キャッシュなし]**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。  
  
 **[新規作成]**  
 **[OLE DB 接続マネージャーの構成]** ダイアログ ボックスを使用して、新しい接続マネージャーを作成します。  
  
 **[データ アクセス モード]**  
 ソースからデータを選択する方法を指定します。  
  
|オプション|[説明]|  
|------------|-----------------|  
|[テーブルまたはビュー]|OLE DB データベースのテーブルまたはビューからデータを取得します。|  
|[テーブル名またはビュー名の変数]|テーブル名またはビュー名を変数で指定します。<br /><br /> **関連情報:** [パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|[SQL コマンド]|SQL クエリを使用して、OLE DB データ ソースからデータを取得します。|  
|[変数からの SQL コマンド]|SQL クエリ テキストを変数で指定します。|  
  
 **プレビュー**  
 **[データ ビュー]** ダイアログ ボックスを使用して、結果をプレビューします。 **プレビュー** では、最大で 200 行を表示できます。  
  
> [!NOTE]  
>  データをプレビューするときに、CLR ユーザー定義型を含む列にはデータが表示されません。 その代わりに、\<値が大きすぎて表示できません> または System.Byte[] が値として表示されます。 前者は、SQL OLE DB プロバイダーを使用してデータ ソースにアクセスする場合に表示されます。後者は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client プロバイダーを使用している場合に表示されます。  
  
### <a name="data-access-mode-dynamic-options"></a>データ アクセス モードの動的オプション  
  
#### <a name="data-access-mode--table-or-view"></a>[データ アクセス モード] = [テーブルまたはビュー]  
 **[テーブル名またはビュー名]**  
 データ ソースで使用できるテーブルまたはビューの一覧から、テーブルまたはビューの名前を選択します。  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>[データ アクセス モード] = [テーブル名またはビュー名の変数]  
 **[変数名]**  
 テーブル名またはビュー名を含む変数を選択します。  
  
#### <a name="data-access-mode--sql-command"></a>[データ アクセス モード] = [SQL コマンド]  
 **[SQL コマンド テキスト]**  
 SQL クエリのテキストを入力し、 **[クエリの作成]** をクリックしてクエリを作成するか、 **[参照]** をクリックしてクエリ テキストを含むファイルを指定します。  
  
 **パラメーター**  
 クエリ テキスト内でパラメーターのプレースホルダーとして "?" を使用することにより、 パラメーター化クエリを入力した場合は、 **[クエリ パラメーターの設定]** ダイアログ ボックスを使用して、クエリ入力パラメーターをパッケージ変数にマップします。  
  
 **Build query**  
 SQL クエリを視覚的に作成するには、 **[クエリ ビルダー]** ダイアログ ボックスを使用します。  
  
 **[参照]**  
 **[開く]** ダイアログ ボックスを使用して、SQL クエリのテキストが含まれているファイルを指定します。  
  
 **[クエリの解析]**  
 クエリ テキストの構文を検査します。  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>データ アクセス モードが [変数からの SQL コマンド] の場合  
 **[変数名]**  
 SQL クエリのテキストを含む変数を選択します。  
  
## <a name="ole-db-source-editor-columns-page"></a>[OLE DB ソース エディター] ([列] ページ)
  **[OLE DB ソース エディター]** ダイアログ ボックスの **[列]** ページを使用すると、出力列をそれぞれの外部 (変換元) 列にマップできます。  
  
### <a name="options"></a>オプション  
 **使用できる外部列**  
 データ ソース内の使用できる外部列の一覧を表示します。 このテーブルを使用して列を追加または削除することはできません。  
  
 **[外部列]**  
 ここで表示される外部 (変換元) 列の順序は、この変換元のデータを使用するコンポーネントを構成するときの列の表示順に反映されます。 この順序を変更するには、テーブルで選択した列を消去してから、別の順序で一覧から外部列を選択します。  
  
 **出力列**  
 各出力列の一意な名前を表示します。 既定では選択された外部 (変換元) 列の名前になりますが、一意でわかりやすい名前を付けることもできます。 指定された名前は、SSIS デザイナーに表示されます。  
  
## <a name="ole-db-source-editor-error-output-page"></a>[OLE DB ソース エディター] ([エラー出力] ページ)
  **[OLE DB ソース エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを選択したり、エラー出力列のプロパティを設定したりできます。  
  
### <a name="options"></a>オプション  
 **[入力または出力]**  
 データ ソースの名前を表示します。  
  
 **列**  
 **[OLE DB ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページで選択されている外部 (ソース) 列を表示します。  
  
 **Error**  
 エラーが発生した場合に、障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **関連項目:** [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **切り捨て**  
 切り捨てが発生したときの処理方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を指定します。  
  
 **[説明]**  
 エラーの説明を表示します。  
  
 **[選択したセルに設定する値]**  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルに対して障害を無視するか、行をリダイレクトするか、コンポーネントを失敗させるかを指定します。  
  
 **[適用]**  
 選択したセルにエラー処理オプションを適用します。  
  
## <a name="see-also"></a>参照  
 [OLE DB 変換先](../../integration-services/data-flow/ole-db-destination.md)   
 [Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)   
 [データ フロー](../../integration-services/data-flow/data-flow.md)  
  
  
