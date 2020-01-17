---
title: CDC ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.cdcsource.f1
- sql13.ssis.designer.cdcsource.connection.f1
- sql13.ssis.designer.cdcsource.columns.f1
- sql13.ssis.designer.cdcsource.errorhandling.f1
ms.assetid: 99775608-e177-44ed-bb44-aaccb0f4f327
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 668b7343ae893d302a27c0a68aec58e536cffcc9
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293279"
---
# <a name="cdc-source"></a>CDC ソース

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  CDC ソースは [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 変更テーブルから変更データの範囲を読み取り、変更内容を下流の他の SSIS コンポーネントに伝えます。  
  
 CDC ソースによって読み取られた変更データの範囲は "CDC 処理範囲" と呼ばれ、現在のデータ フローの開始前に実行される CDC 制御タスクによって決定されます。 CDC 処理範囲は、テーブル グループの CDC 処理の状態を保持するパッケージ変数の値から導き出されます。  
  
 CDC ソースは、データベース テーブル、ビュー、または SQL ステートメントを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースからデータを抽出します。  
  
 CDC ソースは、次の構成を使用します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC データベースにアクセスするための、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ADO.NET 接続マネージャー。 CDC ソース接続を構成する方法の詳細については、「 [[CDC ソース エディター] &#40;[接続マネージャー] ページ&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)」を参照してください。  
  
-   CDC のために有効にされたテーブル。  
  
-   選択したテーブルのキャプチャ インスタンスの名前 (複数存在する場合)。  
  
-   変更処理モード。  
  
-   CDC 処理範囲が決定される基になる、CDC 状態パッケージ変数の名前。 CDC ソースによって、その変数が変更されることはありません。  
  
 CDC ソースによって返されるデータは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC 関数の **cdc.fn_cdc_get_all_changes_\<capture-instance-name>** または **cdc.fn_cdc_get_net_changes_\<capture-instance-name>** (使用できる場合) によって返されるデータと同じです。 唯一、必要に応じて追加できる列として **__$initial_processing** があります。この列は、現在の処理範囲がテーブルの初期読み込みの範囲と重複できるかどうかを示します。 初期処理の詳細については、「 [CDC 制御タスク](../../integration-services/control-flow/cdc-control-task.md)」を参照してください。  
  
 CDC ソースには、1 つの標準出力と 1 つのエラー出力があります。  
  
## <a name="error-handling"></a>エラー処理  
 CDC ソースにはエラー出力があります。 コンポーネントのエラー出力には、次の出力列があります。  
  
-   **エラー コード**: 値は常に -1 です。  
  
-   **エラー列**: (変換エラーの) エラーの原因となるソース列。  
  
-   **エラー行の列**: エラーの原因となったレコード データ。  
  
 CDC ソースは、エラー動作の設定に応じて、抽出処理中に発生したエラー (データ変換、切り捨て) をエラー出力に返します。  
  
## <a name="data-type-support"></a>データ型のサポート  
 Microsoft の CDC ソース コンポーネントはすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型をサポートし、SSIS データ型に正確にマッピングします。  
  
## <a name="troubleshooting-the-cdc-source"></a>CDC ソースのトラブルシューティング  
 以下に、CDC ソースのトラブルシューティング情報を示します。  
  
### <a name="use-this-script-to-isolate-problems-and-reproduce-them-in-sql-server-management-studio"></a>このスクリプトを使用して問題を特定し、SQL Server Management Studio で再現する  
 CDC ソース操作は、CDC ソースを呼び出す前に実行される CDC 制御タスク操作によって管理されます。 CDC 制御タスクは、開始 LSN と終了 LSN が保存されている CDC 状態パッケージ変数の値を比較します。 CDC 制御タスクは、次のスクリプトに相当する関数を実行します。  
  
```sql
use <cdc-enabled-database-name>  
               declare @start_lsn binary(10), @end_lsn binary(10)  
               set @start_lsn = sys.fn_cdc_increment_lsn(  
                       convert(binary(10),'0x' + '<value-from-state-cs>', 1))  
               set @end_lsn =   
                       convert(binary(10),'0x' + '<value-from-state-ce>', 1)  
               select * from cdc.fn_cdc_get_net_changes_dbo_Table1(@start_lsn,  
@end_lsn, '<mode>')  
```  
  
 それぞれの文字の説明は次のとおりです。  
  
-   \<cdc-enabled-database-name> は、変更テーブルが含まれている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースの名前です。  
  
-   \<value-from-state-cs> は、CDC 状態変数に、CS/\<value-from-state-cs>/ として示される値です (CS は Current-processing-range-Start (現在の処理範囲の開始) の略語です)。  
  
-   \<value-from-state-ce> は、CDC 状態変数に、CE/\<value-from-state-ce>/ として示される値です (CE は Current-processing-range-End (現在の処理範囲の終了) の略語です)。  
  
-   \<mode> は、CDC の処理モードです。 この処理モードは、 **[すべて]** 、 **[古い値を含むすべて]** 、 **[差分]** 、 **[更新マスクを含む差分]** 、 **[結合を含む差分]** のいずれかの値です。  
  
 このスクリプトを実行すると、エラーの再現と特定を簡単に行うことができる [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で問題を再現することによって、問題を特定できます。  
  
#### <a name="sql-server-error-message"></a>SQL Server エラー メッセージ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって、次のメッセージが返されることがあります。  
  
 **プロシージャまたは関数 cdc.fn_cdc_get_net_changes_\<..> に指定された引数が不足しています。**  
  
 このエラーは、引数が不足していることを示すものではありません。 CDC 状態変数の開始または終了 LSN 値が無効であることを示します。  
  
## <a name="configuring-the-cdc-source"></a>CDC ソースの構成  
 CDC ソースは、プログラムによって、または SSIS デザイナーを使用して構成できます。  
  
 詳細については、次のいずれかのトピックを参照してください。  
  
-   [[CDC ソース エディター] &#40;[接続マネージャー] ページ&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md)  
  
-   [[CDC ソース エディター] &#40;[列] ページ&#41;](../../integration-services/data-flow/cdc-source-editor-columns-page.md)  
  
-   [CDC ソース エディター &#40;[エラー出力] ページ&#41;](../../integration-services/data-flow/cdc-source-editor-error-output-page.md)  
  
 **[詳細エディター]** ダイアログ ボックスには、プログラムによって設定できるプロパティが表示されます。  
  
 **[詳細エディター]** ダイアログ ボックスを開くには、次の操作を実行します。  
  
-   **プロジェクトの** [データ フロー] [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 画面で、CDC ソースを右クリックし、 **[詳細エディターの表示]** をクリックします。  
  
 **[詳細エディター]** ダイアログ ボックスで設定できるプロパティの詳細については、「 [CDC ソースのカスタム プロパティ](../../integration-services/data-flow/cdc-source-custom-properties.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [CDC ソースのカスタム プロパティ](../../integration-services/data-flow/cdc-source-custom-properties.md)  
  
-   [CDC ソースを使用した変更データ抽出](../../integration-services/data-flow/extract-change-data-using-the-cdc-source.md)  
  
## <a name="cdc-source-editor-connection-manager-page"></a>[CDC ソース エディター] ([接続マネージャー] ページ)
  **[CDC ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページを使用すると、CDC ソースが変更行を読み取る [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] データベース (CDC データベース) の ADO.NET 接続マネージャーを選択できます。 CDC データベースを選択した後で、キャプチャされたテーブルをデータベースで選択する必要があります。  
  
 CDC ソースの詳細については、「 [CDC ソース](../../integration-services/data-flow/cdc-source.md)」を参照してください。  
  
### <a name="task-list"></a>タスク一覧  
 **[CDC ソース エディター] の [接続マネージャー] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、CDC ソースを含む [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、CDC ソースをダブルクリックします。  
  
3.  **[CDC ソース エディター]** で、 **[接続マネージャー]** をクリックします。  
  
### <a name="options"></a>オプション  
 **ADO.NET 接続マネージャー**  
 既存の接続マネージャーを一覧から選択するか、 **[新規作成]** をクリックして新しい接続を作成します。 選択した変更テーブルが存在する、CDC に対応した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへの接続である必要があります。  
  
 **[新規作成]**  
 **[新規作成]** をクリックします。 新しい接続マネージャーを作成できる **[ADO.NET 接続マネージャーの構成エディター]** ダイアログ ボックスが開きます。  
  
 **[CDC テーブル]**  
 読み取って、処理のために下流の SSIS コンポーネントに渡す、キャプチャされた変更の含まれる CDC ソース テーブルを選択します。  
  
 **[キャプチャ インスタンス]**  
 読み取る CDC テーブルの CDC キャプチャ インスタンスの名前を選択または入力します。  
  
 キャプチャされたソース テーブルには、スキーマの変更によりテーブル定義のシームレスな遷移を処理するためのキャプチャされたインスタンスが 1 ～ 2 個含まれることがあります。 キャプチャ対象のソース テーブルに複数のキャプチャ インスタンスが定義されている場合は、ここで使用するキャプチャ インスタンスを選択してください。 [スキーマ].[テーブル] という形式のテーブルの既定のキャプチャ インスタンス名は \<スキーマ>_\<テーブル> ですが、使用される実際のキャプチャ インスタンス名は異なる可能性があります。 読み取り元の実際のテーブルは、**cdc .\<キャプチャ インスタンス>_CT** という形式の CDC テーブルです。  
  
 **[CDC 処理モード]**  
 処理上のニーズに最も適した処理モードを選択します。 オプションは次のとおりです。  
  
-   **[すべて]** : **[更新前]** の値なしで、現在の CDC 範囲内の変更を返します。  
  
-   **[古い値を含むすべて]** : 古い値 ( **[更新前]** ) を含め、現在の CDC 処理範囲内の変更を返します。 更新操作ごとに、2 つの行 (更新前の値の行と更新後の値の行) が存在することになります。  
  
-   **[差分]** : 現在の CDC 処理範囲内で変更された、ソース行あたり 1 つの変更行のみを返します。 ソース行が複数回更新された場合は、変更が結合されたうえで生成されます (たとえば、挿入と更新が 1 回の更新として、または更新と削除が 1 回の削除として、結合されたうえで生成されることがあります)。 [差分] 変更処理モードで作業する場合は、1 つのソース行が複数の出力に出現するため、変更を削除、挿入、および更新の各出力に分割し、並行処理することができます。  
  
-   **[更新マスクを含む差分]** : このモードは通常の [差分] モードと似ていますが、 **__$\<column-name>\__Changed** という名前のパターンを持つブール型の列も追加されます。これは、現在の変更行の変更された列を示します。  
  
-   **[結合を含む差分]** : このモードは通常の [結合] モードと似ていますが、挿入操作と更新操作が 1 つの結合操作 (UPSERT) に結合されます。  
  
> [!NOTE]  
>  どの差分変更オプションを使用する場合も、ソース テーブルに主キーまたは一意のインデックスが必要です。 主キーまたは一意のインデックスがないテーブルに対しては、 **[すべて]** オプションを使用する必要があります。  
  
 **[CDC 状態を含む変数]**  
 現在の CDC コンテキストの CDC 状態を保持する SSIS 文字列パッケージ変数を選択します。 CDC 状態変数の詳細については、「 [状態変数の定義](../../integration-services/data-flow/define-a-state-variable.md)」を参照してください。  
  
 **[再処理インジケーター列を含める]**  
 **__$reprocessing**という特別な出力列を作成する場合は、このチェック ボックスをオンにします。  
  
 CDC 処理範囲が初期処理範囲 (初期読み込みの期間に対応する LSN の範囲) と重なる場合か、CDC 処理範囲が前の実行でのエラーの後に再処理される場合、この列の値は **true** になります。 このインジケーター列を使用すると、SSIS 開発者は変更を再処理するときに、エラーを別々に処理できます (たとえば、非既存行の削除やキーの重複により失敗した挿入などの操作を無視できます)。  
  
 詳細については、「 [CDC ソースのカスタム プロパティ](../../integration-services/data-flow/cdc-source-custom-properties.md)」を参照してください。  
  
## <a name="cdc-source-editor-columns-page"></a>[CDC ソース エディター] ([列] ページ)
  **[CDC ソース エディター]** ダイアログ ボックスの **[列]** ページを使用すると、出力列をそれぞれの外部 (ソース) 列にマップできます。  
  
### <a name="task-list"></a>タスク一覧  
 **[CDC ソース エディター] の [列] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、CDC ソースを含む [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、CDC ソースをダブルクリックします。  
  
3.  **[CDC ソース エディター]** で、 **[列]** をクリックします。  
  
### <a name="options"></a>オプション  
 **使用できる外部列**  
 データ ソース内の使用できる外部列の一覧です。 このテーブルを使用して列を追加または削除することはできません。 ソースで使用する列を選択します。 選択した列は、選択した順序で **[外部列]** の一覧に追加されます。  
  
 **[外部列]**  
 外部 (ソース) 列のビューです。CDC ソースのデータを使用するコンポーネントを構成するときの表示順になります。 この順序を変更するには、まず **[使用できる外部列]** の一覧で選択した列を消去してから、別の順序で一覧から外部列を選択します。 選択した列は、選択した順序で **[外部列]** の一覧に追加されます。  
  
 **出力列**  
 各出力列の一意の名前を入力します。 既定では選択された外部 (ソース) 列の名前になりますが、一意でわかりやすい名前を付けることもできます。 入力した名前は、SSIS デザイナーで表示されます。  
  
## <a name="cdc-source-editor-error-output-page"></a>[CDC ソース エディター] ([エラー出力] ページ)
  **[CDC ソース エディター]** ダイアログ ボックスの **[エラー出力]** ページを使用すると、エラー処理オプションを選択できます。  
  
### <a name="task-list"></a>タスク一覧  
 **[CDC ソース エディター] の [エラー出力] ページを開くには**  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]で、CDC ソースを含む [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] パッケージを開きます。  
  
2.  **[データ フロー]** タブで、CDC ソースをダブルクリックします。  
  
3.  **[CDC ソース エディター]** で、 **[エラー出力]** をクリックします。  
  
### <a name="options"></a>オプション  
 **[入力または出力]**  
 データ ソースの名前を表示します。  
  
 **列**  
 **[CDC ソース エディター]** ダイアログ ボックスの **[接続マネージャー]** ページで選択した外部 (ソース) 列を表示します。  
  
 **Error**  
 CDC ソースでフローのエラーを処理する方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。  
  
 **切り捨て**  
 CDC ソースでフローの切り捨てを処理する方法 (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。  
  
 **[説明]**  
 使用されていません。  
  
 **[選択したセルに設定する値]**  
 エラーまたは切り捨てが発生した場合に、選択したすべてのセルを CDC ソースでどのように処理するか (エラーを無視する、行をリダイレクトする、またはコンポーネントを失敗させる) を選択します。  
  
 **[適用]**  
 選択したセルにエラー処理オプションを適用します。  
  
### <a name="error-handling-options"></a>エラー処理オプション  
 CDC ソースでのエラーと切り捨ての処理方法を構成するには、次のオプションを使用します。  
  
 **エラー コンポーネント**  
 エラーまたは切り捨てが発生すると、データ フロー タスクは失敗します。 これは既定の動作です。  
  
 **エラーを無視する**  
 エラーまたは切り捨ては無視され、データ行は CDC ソース出力に送られます。  
  
 **[フローのリダイレクト]**  
 エラーまたは切り捨てのデータ行は、CDC ソースのエラー出力に送られます。 この場合は、CDC ソースのエラー処理が使用されます。 詳細については、「 [CDC ソース](../../integration-services/data-flow/cdc-source.md)」を参照してください。  
  
## <a name="related-content"></a>関連コンテンツ  
  
-   mattmasson.com のブログ「[CDC ソースの処理モード](https://www.mattmasson.com/2012/01/processing-modes-for-the-cdc-source/)」  
  
  
