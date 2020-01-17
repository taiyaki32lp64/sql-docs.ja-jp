---
title: ODBC 入力元 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.odbcsource.f1
- sql13.ssis.designer.odbcsource.connection.f1
- sql13.ssis.designer.odbcsource.columns.f1
- sql13.ssis.designer.odbcsource.errorhandling.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 19a234b8c2939730a6c5a815885606dac15d0a0a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298165"
---
# <a name="odbc-source"></a>ODBC 入力元

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ODBC 入力元は、データベース テーブル、ビュー、または SQL ステートメントを使用して、ODBC でサポートされているデータベースからデータを抽出します。  
  
 ODBC 入力元には、データを抽出するために、次のデータ アクセス モードがあります。  
  
-   テーブルまたはビュー。  
  
-   SQL ステートメントの結果。  
  
 入力元は、使用するプロバイダーを指定する、ODBC 接続マネージャーを使用します。  
  
 ODBC 入力元には、ソース データ出力列があります。 出力列が ODBC 入力先で入力先列にマッピングされている場合に、入力先列にマッピングされている入力列がないときにはエラーが発生することがあります。 さまざまな種類の列をマッピングできますが、出力列と入力先との間に互換性がない場合は、実行時にエラーが発生します。 エラー動作設定に応じて、エラーが無視されるか、エラーが発生するか、エラー出力に行が送信されます。  
  
 ODBC 入力元には、1 つの標準出力と 1 つのエラー出力があります。  
  
## <a name="error-handling"></a>エラー処理  
 ODBC 入力元にはエラー出力があります。 コンポーネントのエラー出力には、次の出力列があります。  
  
-   **エラー コード**: 現在のエラーに対応する数字です。 エラーの一覧については、使用している ODBC でサポートされているデータベースのドキュメントを参照してください。 SSIS エラー コードの一覧については、「SSIS のエラー コードおよびメッセージ リファレンス」を参照してください。  
  
-   **エラー列**: (変換エラーの) エラーの原因となるソース列。  
  
-   標準出力データ列。  
  
 ODBC 入力元は、エラー動作の設定に応じて、抽出処理中に発生したエラー (データ変換、切り捨て) をエラー出力に返します。 詳細については、「[ODBC 変換先エディター &#40;[接続マネージャー] ページ&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)」を参照してください。  
  
## <a name="data-type-support"></a>データ型のサポート  
 ODBC 入力元でサポートされるデータ型については、「Connector for Open Database Connectivity (ODBC)」を参照してください。  
  
## <a name="extract-options"></a>抽出オプション  
 ODBC 入力元は、 **バッチ** または **行ごと** のどちらかのモードで動作します。 使用するモードは、 **FetchMethod** プロパティによって決まります。 以下に、モードの説明を示します。  
  
-   **バッチ**: コンポーネントは、把握した ODBC プロバイダーの機能に基づいて、最も効率的なフェッチ方法を使用します。 最新の ODBC プロバイダーの場合、これは配列バインドを使用する SQLFetchScroll です (このとき、配列のサイズは **BatchSize** プロパティによって決定します)。 **[バッチ]** を選択したが、この方法がプロバイダーでサポートされていない場合、ODBC 入力先は自動的に **[行ごと]** モードに切り替わります。  
  
-   **行ごと**: コンポーネントは SQLFetch を使用して、一度に 1 行ずつ取得します。  
  
 **FetchMethod** プロパティの詳細については、「 [ODBC 入力元のカスタム プロパティ](../../integration-services/data-flow/odbc-source-custom-properties.md)」を参照してください。  
  
## <a name="parallelism"></a>Parallelism  
 並列実行できる ODBC 入力元コンポーネントの数に制限はありません。これは、同一テーブル上にある場合または異なるテーブル上にある場合、同一コンピューター上で実行する場合または異なるコンピューター上で実行する場合のいずれにも該当します (ただし、通常のグローバルなセッション制限を除きます)。  
  
 ただし、使用する ODBC プロバイダーの制限によって、プロバイダーを介するコンカレント接続数が制限される場合があります。 これらの制限によって、ODBC 入力元で使用できる並列インスタンス数のサポートが制限されます。 SSIS プロバイダーは、使用される ODBC プロバイダーの制限を把握し、SSIS パッケージを作成する際に考慮する必要があります。  
  
## <a name="troubleshooting-the-odbc-source"></a>ODBC 入力元のトラブルシューティング  
 ODBC 入力元による外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、ODBC 入力元による外部データ ソースからのデータ読み込みに関するトラブルシューティングを行うことができます。 ODBC 入力元による外部データ プロバイダーの呼び出しをログに記録するには、ODBC ドライバー マネージャーによるトレースを有効にします。 詳細については、「 *ODBC で ODBC トレースを生成する方法 (データ ソース管理者向け)* 」の Microsoft のドキュメントを参照してください。  
  
## <a name="configuring-the-odbc-source"></a>ODBC 入力元の構成  
 ODBC 入力元は、プログラムによって、または SSIS デザイナーを使用して構成できます。  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが表示されます。  
  
 **[詳細エディター]** ダイアログ ボックスを開くには、次の操作を実行します。  
  
-   **プロジェクトの** [データ フロー] [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 画面で、ODBC 入力元を右クリックし、 **[詳細エディターの表示]** をクリックします。  
  
 [詳細エディター] ダイアログ ボックスで設定できるプロパティの詳細については、「 [ODBC 入力元のカスタム プロパティ](../../integration-services/data-flow/odbc-source-custom-properties.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [ODBC 変換元を使用したデータ抽出](../../integration-services/data-flow/extract-data-by-using-the-odbc-source.md)  
  
-   [ODBC 変換元のカスタム プロパティ](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
## <a name="odbc-source-editor-connection-manager-page"></a>[ODBC ソース エディター] ([接続マネージャー] ページ)
  **[ODBC 入力元エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、入力元の ODBC 接続マネージャーを選択できます。 さらにこのページを使用して、データベースのテーブルやビューを選択できます。  
  
### <a name="task-list"></a>タスク一覧  
 **[ODBC 入力元エディター] の [接続マネージャー] ページを開くには**  
  
-   [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、ODBC 入力元を含む [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
-   **[データ フロー]** タブで、ODBC 入力元をダブルクリックします。  
  
### <a name="options"></a>オプション  
  
#### <a name="connection-manager"></a>[ODBC 入力元エディター]  
 既存の ODBC 接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。 ODBC でサポートされているデータベースへの接続を選択または入力できます。  
  
#### <a name="new"></a>ボタンを使用して新しい  
 **[新規作成]** をクリックします。 新しい ODBC 接続マネージャーを作成できる **[ODBC 接続マネージャーの構成エディター]** ダイアログ ボックスが開きます。  
  
#### <a name="data-access-mode"></a>[データ アクセス モード]  
 入力元のデータを選択する方法を選択します。 次の表に示すオプションがあります。  
  
|オプション|[説明]|  
|------------|-----------------|  
|テーブル名|ODBC データ ソースのテーブルまたはビューからデータを取得します。 このオプションを選択する場合は、以下の一覧から値を選択します。|  
||**[テーブル名またはビュー名]** : 使用できるテーブルまたはビューを一覧から選択するか、正規表現を入力してテーブルを特定します。|  
||この一覧には、最初の 1,000 個のテーブルのみが含まれます。 データベースに 1,000 を超えるテーブルがある場合、テーブル名の最初の文字を入力するか、名前の一部の入力にワイルドカード (*) を使用すると、目的のテーブルが表示されます。|  
|[SQL コマンド]|SQL クエリを使用して、ODBC データ ソースからデータを取得します。 使用しているソース データベースの構文でクエリを記述してください。 このオプションを選択する場合は、以下のいずれかの方法でクエリを入力します。|  
||**[SQL コマンド テキスト]** フィールドに SQL クエリのテキストを入力します。|  
||**[参照]** をクリックして、テキスト ファイルから SQL クエリを読み込みます。|  
||**[クエリの解析]** をクリックして、クエリ テキストの構文を検証します。|  
  
#### <a name="preview"></a>プレビュー  
 **[プレビュー]** をクリックすると、選択したテーブルまたはビューから抽出されたデータを先頭から最大で 200 行表示できます。  
  
## <a name="odbc-source-editor-columns-page"></a>[ODBC ソース エディター] ([列] ページ)
  **[ODBC ソース エディター]** ダイアログ ボックスの **[列]** ページを使用すると、出力列をそれぞれの外部 (入力元) 列にマップできます。  
  
### <a name="task-list"></a>タスク一覧  
 **[ODBC 入力元エディター] の [列] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、ODBC 入力元を含む [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、ODBC 入力元をダブルクリックします。  
  
3.  **[ODBC 入力元エディター]** で、 **[列]** をクリックします。  
  
### <a name="options"></a>オプション  
  
#### <a name="available-external-columns"></a>使用できる外部列  
 データ ソース内の使用できる外部列の一覧です。 このテーブルを使用して列を追加または削除することはできません。 入力元から使用する列を選択します。 選択した列は、選択した順序で **[外部列]** の一覧に追加されます。  
  
 **[すべて選択]** チェック ボックスをオンにすると、すべての列が選択されます。  
  
#### <a name="external-column"></a>外部列  
 外部 (入力元) 列のビューです。ODBC 入力元のデータを使用するコンポーネントを構成するときの表示順になります。  
  
#### <a name="output-column"></a>出力列  
 各出力列の一意の名前を入力します。 既定では選択された外部 (変換元) 列の名前になりますが、一意でわかりやすい名前を付けることもできます。 入力した名前は、SSIS デザイナーで表示されます。  
  
## <a name="odbc-source-editor-error-output-page"></a>[ODBC ソース エディター] ([エラー出力] ページ)
  **[ODBC 入力元エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを選択できます。  
  
### <a name="task-list"></a>タスク一覧  
 **[ODBC 入力元エディター] の [エラー出力] ページを開くには**  
  
-   [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、ODBC 入力元を含む [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
-   **[データ フロー]** タブで、ODBC 入力元をダブルクリックします。  
  
-   **[ODBC 入力元エディター]** で、 **[エラー出力]** をクリックします。  
  
### <a name="options"></a>オプション  
  
#### <a name="inputoutput"></a>[入力または出力]  
 データ ソースの名前を表示します。  
  
#### <a name="column"></a>[列]  
 使用されていません。  
  
#### <a name="error"></a>エラー  
 ODBC 入力元でフローのエラーを処理する方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。  
  
#### <a name="truncation"></a>切り捨て  
 ODBC 入力元でフローの切り捨てを処理する方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。  
  
#### <a name="description"></a>[説明]  
 使用されていません。  
  
#### <a name="set-this-value-to-selected-cells"></a>[選択したセルに設定する値]  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルを ODBC 入力元でどのように処理するか (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。  
  
#### <a name="apply"></a>[適用]  
 選択したセルにエラー処理オプションを適用します。  
  
### <a name="error-handling-options"></a>エラー処理オプション  
 ODBC 入力元でのエラーと切り捨ての処理方法を構成するには、次のオプションを使用します。  
  
#### <a name="fail-component"></a>エラー コンポーネント  
 エラーまたは切り捨てが発生すると、データ フロー タスクは失敗します。 これは既定の動作です。  
  
#### <a name="ignore-failure"></a>エラーを無視する  
 エラーまたは切り捨ては無視されます。  
  
#### <a name="redirect-flow"></a>[フローのリダイレクト]  
 エラーまたは切り捨てが ODBC 入力元のエラー出力に送られる原因となった行。  
  
  
