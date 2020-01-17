---
title: ODBC 入力先 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.odbcdest.f1
- sql13.ssis.designer.odbcdest.connection.f1
- sql13.ssis.designer.odbcdest.columns.f1
- sql13.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 153cbd447fa84087b50501005d0ea457f47d1eda
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298213"
---
# <a name="odbc-destination"></a>ODBC 入力先

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ODBC 入力先は、ODBC でサポートされているデータベース テーブルにデータを一括で読み込みます。 ODBC 入力先は ODBC 接続マネージャーを使用してデータ ソースに接続します。  
  
 ODBC 入力先には、入力列と入力先データ ソースの列との間のマッピングが含まれています。 入力列をすべての入力先列にマップする必要はありませんが、入力先列のプロパティによっては、入力先列にマップされる入力列がない場合、エラーが発生することがあります。 たとえば、入力先列で NULL 値が許容されていない場合は、入力列をその列にマップする必要があります。 また、さまざまな種類の列をマッピングできますが、入力データと入力先の列の型との間に互換性がない場合は、実行時にエラーが発生します。 エラー動作設定に応じて、エラーが無視されるか、エラーが発生するか、エラー出力に行が送信されます。  
  
 ODBC 入力先には、1 つの標準出力と 1 つのエラー出力があります。  
  
##  <a name="BKMK_odbcdestination_loadoptions"></a> 読み込みオプション  
 ODBC 入力先先は、2 つのアクセス読み込みモジュールのうちどちらかを使用できます。 [ODBC ソース エディター &#40;[接続マネージャー] ページ&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)。 次の 2 つのモードがあります。  
  
-   **バッチ**: このモードでは、ODBC 入力先は、把握した ODBC プロバイダーの機能に基づいて、最も効率的な挿入方法を使用します。 最新の ODBC プロバイダーの場合、これは、パラメーターを設定した INSERT ステートメントを準備し、行方向の配列パラメーター バインドを使用する方法です (このとき、配列のサイズは **BatchSize** プロパティによって制御します)。 **[バッチ]** を選択したが、この方法がプロバイダーでサポートされていない場合、ODBC 入力先は自動的に **[行ごと]** モードに切り替わります。  
  
-   **行ごと**: このモードでは、ODBC 入力先はパラメーターを設定した INSERT ステートメントを準備し、**SQL の Execute** を使用して一度に 1 行ずつ行を挿入します。  
  
## <a name="error-handling"></a>エラー処理  
 ODBC 入力先にはエラー出力があります。 コンポーネントのエラー出力には、次の出力列があります。  
  
-   **エラー コード**: 現在のエラーに対応する数字です。 エラーの一覧については、ソース データベースのドキュメントを参照してください。 SSIS エラー コードの一覧については、「SSIS のエラー コードおよびメッセージ リファレンス」を参照してください。  
  
-   **エラー列**: (変換エラーの) エラーの原因となるソース列。  
  
-   標準出力データ列。  
  
 ODBC 入力先は、エラー動作の設定に応じて、抽出処理中に発生したエラー (データ変換、切り捨て) をエラー出力に返します。 詳細については、「[CDC ソース エディター &#40;[エラー出力] ページ&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)」を参照してください。  
  
## <a name="parallelism"></a>並列処理  
 並列実行できる ODBC 入力先コンポーネントの数に制限はありません。これは、同一テーブル上にある場合または異なるテーブル上にある場合、同一コンピューター上で実行する場合または異なるコンピューター上で実行する場合のいずれにも該当します (ただし、通常のグローバルなセッション制限を除きます)。  
  
 ただし、使用する ODBC プロバイダーの制限によって、プロバイダーを介するコンカレント接続数が制限される場合があります。 これらの制限によって、ODBC 入力先で使用できる並列インスタンス数のサポートが制限されます。 SSIS プロバイダーは、使用される ODBC プロバイダーの制限を把握し、SSIS パッケージを作成する際に考慮する必要があります。  
  
 また、同一テーブルへの同時読み込みの場合、標準のレコード ロックのためにパフォーマンスが低下することがある点についても理解しておく必要があります。 これは、読み込まれているデータとテーブルの編成によって異なります。  
  
## <a name="troubleshooting-the-odbc-destination"></a>ODBC 入力先のトラブルシューティング  
 ODBC 入力元による外部データ プロバイダーの呼び出しをログに記録できます。 このログ機能を使用すると、ODBC 入力先による外部データ ソースへのデータ保存に関するトラブルシューティングを行うことができます。 ODBC 入力先による外部データ プロバイダーの呼び出しをログに記録するには、ODBC ドライバー マネージャーによるトレースを有効にします。 詳細については、「 *ODBC で ODBC トレースを生成する方法 (データ ソース管理者向け)* 」 の Microsoft のドキュメントを参照してください。  
  
## <a name="configuring-the-odbc-destination"></a>ODBC 入力先の構成  
 ODBC 入力先は、プログラムによって、または SSIS デザイナーを使用して構成できます。  
  
 詳細については、次のいずれかのトピックを参照してください。  
  
-   [ODBC 変換先エディター &#40;[接続マネージャー] ページ&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)  
  
-   [ODBC 変換先エディター &#40;[マッピング] ページ&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
-   [ODBC 変換先エディター &#40;[エラー出力] ページ&#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが表示されます。  
  
 **[詳細エディター]** ダイアログ ボックスを開くには、次の操作を実行します。  
  
-   **プロジェクトの** [データ フロー] [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 画面で、ODBC 入力先を右クリックし、 **[詳細エディターの表示]** をクリックします。  
  
 [詳細エディター] ダイアログ ボックスで設定できるプロパティの詳細については、「 [ODBC 入力先のカスタム プロパティ](../../integration-services/data-flow/odbc-destination-custom-properties.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [ODBC 変換先を使用したデータ読み込み](../../integration-services/data-flow/load-data-by-using-the-odbc-destination.md)  
  
-   [ODBC 変換先のカスタム プロパティ](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
## <a name="odbc-destination-editor-connection-manager-page"></a>[ODBC 変換先エディター]\([接続マネージャー] ページ)
  **[ODBC 入力先エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、入力先の ODBC 接続マネージャーを選択できます。 さらにこのページを使用して、データベースのテーブルやビューを選択できます。  
  
 **[ODBC 入力先エディター] の [接続マネージャー] ページを開くには**  
  
### <a name="task-list"></a>タスク一覧  
  
-   [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、ODBC 入力先を含む [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
-   **[データ フロー]** タブで、ODBC 入力先をダブルクリックします。  
  
-   **[ODBC 入力先エディター]** で、 **[接続マネージャー]** をクリックします。  
  
### <a name="options"></a>オプション  
  
#### <a name="connection-manager"></a>[ODBC 入力元エディター]  
 既存の ODBC 接続マネージャーを一覧から選択するか、[新規作成] をクリックして新しい接続を作成します。 ODBC でサポートされているデータベースへの接続を選択または入力できます。  
  
#### <a name="new"></a>ボタンを使用して新しい  
 **[新規作成]** をクリックします。 新しい接続マネージャーを作成できる **[ODBC 接続マネージャーの構成エディター]** ダイアログ ボックスが開きます。  
  
#### <a name="data-access-mode"></a>[データ アクセス モード]  
 データを入力先に読み込む方法を選択します。 次の表に示すオプションがあります。  
  
|オプション|[説明]|  
|------------|-----------------|  
|[テーブル名 - バッチ]|バッチ モードで動作する ODBC 入力先を構成するには、このオプションを選択します。 このオプションを選択した場合は、次のオプションを指定できます。|  
||**[テーブル名またはビュー名]** : 使用できるテーブルまたはビューを一覧から選択します。<br /><br /> この一覧には、最初の 1,000 個のテーブルのみが含まれます。 データベースに 1,000 を超えるテーブルがある場合、テーブル名の最初の文字を入力するか、名前の一部の入力にワイルドカード (\*) を使用すると、目的のテーブルが表示されます。<br /><br /> **[バッチ サイズ]** : 一括読み込みのバッチのサイズを入力します。 これは、バッチとして読み込まれる行数です。|  
|[テーブル名 - 行ごと]|一度に 1 行ずつ、入力先テーブルに各行を挿入するように ODBC 入力先を構成するには、このオプションを選択します。 このオプションを選択した場合は、次のオプションを指定できます。|  
||**[テーブル名またはビュー名]** : 使用できるテーブルまたはビューを一覧のデータベースから選択します。<br /><br /> この一覧には、最初の 1,000 個のテーブルのみが含まれます。 データベースに 1,000 を超えるテーブルがある場合、テーブル名の最初の文字を入力するか、名前の一部の入力にワイルドカード (*) を使用すると、目的のテーブルが表示されます。|  
  
#### <a name="preview"></a>プレビュー  
 **[プレビュー]** をクリックすると、選択したテーブルのデータが最大で 200 行表示されます。  
  
## <a name="odbc-destination-editor-mappings-page"></a>[ODBC 変換先エディター]\([マッピング] ページ)
  **[ODBC 入力先エディター]** ダイアログ ボックスの **[マッピング]** ページを使用すると、入力列を変換先列にマップできます。  
  
### <a name="options"></a>オプション  
  
#### <a name="available-input-columns"></a>[使用できる入力列]  
 使用できる入力列の一覧です。 使用できる変換先列に入力列をドラッグ アンド ドロップして、列をマップできます。  
  
#### <a name="available-destination-columns"></a>使用できる変換先列  
 使用できる変換先列の一覧です。 使用できる入力列に変換先列をドラッグ アンド ドロップして、列をマップできます。  
  
#### <a name="input-column"></a>入力列  
 選択した入力列を表示します。 出力から列を除外するために **\<無視>** を選択することで、マッピングを削除できます。  
  
#### <a name="destination-column"></a>変換先列  
 使用できるすべての変換先列を表示します (マップ済みの列とマップされていない列を両方とも含む)。  
  
## <a name="odbc-destination-editor-error-output-page"></a>ODBC 変換先エディター ([エラー出力] ページ)
  **[ODBC 入力先エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを選択できます。  
  
 **[ODBC 入力先エディター] の [エラー出力] ページを開くには**  
  
### <a name="task-list"></a>タスク一覧  
  
-   [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、ODBC 入力先を含む [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
-   **[データ フロー]** タブで、ODBC 入力先をダブルクリックします。  
  
-   **[ODBC 入力先エディター]** で、 **[エラー出力]** をクリックします。  
  
### <a name="options"></a>オプション  
  
#### <a name="inputoutput"></a>[入力または出力]  
 データ ソースの名前を表示します。  
  
#### <a name="column"></a>[列]  
 使用されていません。  
  
#### <a name="error"></a>エラー  
 ODBC 入力先でフローのエラーを処理する方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。  
  
#### <a name="truncation"></a>切り捨て  
 ODBC 入力先でフローの切り捨てを処理する方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。  
  
#### <a name="description"></a>[説明]  
 エラーの説明を表示します。  
  
#### <a name="set-this-value-to-selected-cells"></a>[選択したセルに設定する値]  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルを ODBC 入力先でどのように処理するか (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。  
  
#### <a name="apply"></a>[適用]  
 選択したセルにエラー処理オプションを適用します。  
  
### <a name="error-handling-options"></a>エラー処理オプション  
 ODBC 入力先でのエラーと切り捨ての処理方法を構成するには、次のオプションを使用します。  
  
#### <a name="fail-component"></a>エラー コンポーネント  
 エラーまたは切り捨てが発生すると、データ フロー タスクは失敗します。 これは既定の動作です。  
  
#### <a name="ignore-failure"></a>エラーを無視する  
 エラーまたは切り捨ては無視されます。  
  
#### <a name="redirect-flow"></a>[フローのリダイレクト]  
 エラーまたは切り捨てが ODBC 入力先のエラー出力に送られる原因となった行。 詳細については、「ODBC 入力先」を参照してください。  
  
