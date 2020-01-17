---
title: パッケージ実行のトラブルシューティング ツール| Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Integration Services packages, troubleshooting
- SSIS packages, troubleshooting
- Integration Services, troubleshooting
- errors [Integration Services], troubleshooting
- packages [Integration Services], troubleshooting
ms.assetid: f18d6ff6-e881-444c-a399-730b52130e7c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 660ac899b1cf649bcc431bf10e2f9b18ca12cbc4
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637945"
---
# <a name="troubleshooting-tools-for-package-execution"></a>パッケージ実行のトラブルシューティング ツール

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、パッケージを完成して配置した後、そのパッケージの実行時のトラブルシューティングに使用できる機能とツールが含まれています。  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] には、デザイン時に、パッケージの実行を一時的に停止するブレイクポイント、進行状況ウィンドウ、およびデータ フロー全体でのデータの流れが追えるデータ ビューアーが用意されています。 ただし、既に配置されているパッケージを実行するときは、これらの機能を使用できません。 配置済みのパッケージのトラブルシューティングを行うための主な技法は次のとおりです。  
  
-   イベント ハンドラーを使ってパッケージ エラーをキャッチおよび処理する。  
  
-   エラー出力を使って不適切なデータをキャプチャする。  
  
-   ログ記録を使ってパッケージの実行をステップ単位に追跡する。  
  
 次のヒントや技法を使用して、実行中のパッケージの問題を回避することもできます。  
  
-   **トランザクションを使ってデータの整合性の確認を支援する**。 詳細については、「 [Integration Services のトランザクション](../../integration-services/integration-services-transactions.md)」をご覧ください。  
  
-   **チェックポイントを使って、エラーが発生した時点からパッケージを再開する**。 詳細については、「 [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md)」を参照してください。  
  
## <a name="catch-and-handle-package-errors-by-using-event-handlers"></a>イベント ハンドラーを使用したパッケージ エラーのキャッチおよび処理  
 イベント ハンドラーを使用することにより、パッケージやパッケージ内のオブジェクトで発生する多くのイベントに対応できます。  
  
-   **OnError イベントのイベント ハンドラーを作成する**。 イベント ハンドラーでは、Send Mail タスクを使用した管理者へのエラー通知、スクリプト タスクやカスタム ロジックを使用したトラブルシューティング用のシステム情報の取得、リソースや不完全な出力の一時的なクリーンアップなどを実行できます。 詳細については、「[Integration Services &#40;SSIS&#41; のイベント ハンドラー](../../integration-services/integration-services-ssis-event-handlers.md)」を参照してください。  
  
## <a name="troubleshoot-bad-data-by-using-error-outputs"></a>エラー出力を使った不適切なデータのトラブルシューティング  
 多くのデータ フロー コンポーネントではエラー出力を使用して、エラーを含む行を後で分析できるように別の場所にリダイレクトできます。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。  
  
-   **エラー出力を使って不適切なデータをキャプチャする**。 エラーを含む行をエラー テーブルやテキスト ファイルなどの別の場所に送信します。 エラー出力では、行が拒否される原因となったエラーの番号を含む列と、エラーが発生した列の ID を含む列の 2 つの数値列が自動的に追加されます。  
  
-   **関連情報をエラー出力に追加する**。 エラー出力から提供される 2 列の数値識別子だけでなく、エラー メッセージと列名を追加すると、エラー出力の分析が容易になります。 これら 2 つの列を追加する方法の例については、「 [スクリプト コンポーネントによるエラー出力の強化](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/enhancing-an-error-output-with-the-script-component.md)」を参照してください。  
  
-   **または、DiagnosticEx イベントを記録して列名を取得します**。 このイベントは、データ フロー系列マップをログに書き込みます。 エラー出力でキャプチャされた列識別子を使用して、この系列マップの列名を調べることができます。  詳細については、「[データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。  
  
     **DiagnosticEx** のメッセージ列の値は XML テキストです。 パッケージ実行のメッセージ テキストを表示するには、[catalog.operation_messages &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md) ビューのクエリを実行します。 **DiagnosticEx** イベントでは XML 出力に含まれる空白が維持されないので、ログのサイズを軽減できます。 読みやすくするために、XML 書式と構文の強調表示をサポートする XML エディター (たとえば Visual Studio) にログをコピーします。  
  
## <a name="troubleshoot-package-execution-by-using-operations-reports"></a>操作レポートを使ったパッケージ実行のトラブルシューティング  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] カタログに配置された [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの監視に役立つ標準の操作レポートを使用できます。 これらのパッケージ レポートは、パッケージの状態と履歴を確認したり、必要に応じて失敗の原因を特定したりするのに役立ちます。  
  
 詳細については、「 [パッケージ実行のレポートのトラブルシューティング](../../integration-services/troubleshooting/troubleshooting-reports-for-package-execution.md)」を参照してください。  
  
## <a name="troubleshoot-package-execution-by-using-ssisdb-views"></a>SSISDB ビューを使ったパッケージ実行のトラブルシューティング  
 クエリを実行してパッケージ実行や操作に関するその他の情報を監視するための複数の SSISDB データベース ビューが用意されています。 詳細については、「 [パッケージとその他の操作を実行するモニター](../../integration-services/performance/monitor-running-packages-and-other-operations.md)」を参照してください。  
  
## <a name="troubleshoot-package-execution-by-using-logging"></a>ログ記録を使ったパッケージ実行のトラブルシューティング  
 ログ記録を有効にすることで、実行中のパッケージで発生する多くの現象を追跡できます。 ログ プロバイダーは、後で分析するために特定のイベントに関する情報をキャプチャし、その情報をデータベース テーブル、フラット ファイル、XML ファイルなどのサポートされている出力形式で保存します。  
  
-   **ログ記録を有効にする**。 イベントのみ、およびキャプチャする情報項目のみを選択することによって、ログの出力を微調整できます。 詳細については、「 [Integration Services (SSIS) のログ記録](../performance/integration-services-ssis-logging.md)」を参照してください。  
  
-   **パッケージの Diagnostic イベントを選択して、プロバイダーに関する問題のトラブルシューティングを行います。** パッケージと外部データ ソースとのやり取りに関するトラブルシューティングに役立つログ メッセージが用意されています。 詳細については、「[トラブルシューティング ツールのパッケージ接続](troubleshooting-tools-for-package-connectivity.md)」を参照してください。  
  
-   **既定のログ出力を拡張する**。 ログ記録は、通常、パッケージを実行するたびに、ログの記録先に行を追加します。 各行のログ出力では名前や一意識別子でパッケージを識別していますが、一意の ExecutionID で各パッケージの実行も識別しています。そのため、1 つの一覧に大量のログ記録が出力され、分析が難しくなります。  
  
     次のアプローチは、既定のログ出力を拡張してレポートの生成を容易にするための 1 つの考え方です。  
  
    1.  **パッケージを実行するたびにログを記録する親テーブルを作成する**。 この親テーブルにはパッケージを実行するたびに 1 行だけを記録し、ExecutionID を使用して、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ログ記録テーブルの子レコードにリンクします。 各パッケージの最初に SQL 実行タスクを使用して、この新しい行を作成し、開始時刻を記録します。 次に、パッケージの終了時に別の SQL 実行タスクを使用して、終了時刻、実行時間、状態でその行を更新します。  
  
    2.  **データ フローに監査情報を追加する**。 監査変換を使用して、各行を作成または変更したパッケージの実行に関する情報を、データ フロー内の行に追加できます。 監査変換は、PackageName や ExecutionInstanceGUID など、9 種類の情報を作成します。 詳細については、「 [Audit Transformation](../../integration-services/data-flow/transformations/audit-transformation.md)」を参照してください。 監査を目的として各行に含めるカスタム情報があれば、派生列変換を使用して、その情報をデータ フロー内の行に追加できます。 詳細については、「 [派生列変換](../../integration-services/data-flow/transformations/derived-column-transformation.md)」を参照してください。  
  
    3.  **行数データのキャプチャを検討する**。 行数情報用に別のテーブルを作成することを検討します。このテーブルでは、パッケージ実行の各インスタンスを ExecutionID で識別します。 行数変換を使用して、データ フロー内の重要な時点の行数を一連の変数に保存します。 データ フローの終了後、SQL 実行タスクを使用してこの一連の値をテーブルの行に挿入すると、後の分析やレポートに役立ちます。  
  
     この方法の詳細については、[!INCLUDE[msCoName](../../includes/msconame-md.md)] のホワイト ペーパー「[Project REAL: Business Intelligence ETL Design Practices (プロジェクト REAL: ビジネス インテリジェンス ETL のデザイン方法)](https://www.microsoft.com/download/details.aspx?id=14582)」の「ETL Auditing and Logging (ETL の監査とログ記録)」をご覧ください。  
  
## <a name="troubleshoot-package-execution-by-using-debug-dump-files"></a>デバッグ ダンプ ファイルを使ったパッケージ実行のトラブルシューティング  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]では、パッケージの実行に関する情報を提供するデバッグ ダンプ ファイルを作成できます。 詳細については、「[パッケージ実行用のダンプ ファイルを生成する](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)」を参照してください。  
  
## <a name="troubleshoot-run-time-validation-issues"></a>実行時検証問題のトラブルシューティング  
 パッケージ内の前のタスクの実行が完了するまで、データ ソースに接続できなかったり、パッケージの一部を検証できなかったりすることがあります。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、こうした状況が原因で発生する検証エラーを回避するための以下の機能が備わっています。  
  
-   **パッケージが読み込まれるときには無効になっているパッケージ要素の DelayValidation プロパティを構成する**。 構成が無効になっているパッケージ要素の **DelayValidation** を **True** に設定できます。これによってパッケージが読み込まれるときの検証エラーを防ぎます。 たとえば、SQL 実行タスクが実行時に作成するまで存在しないテーブルを、データ フロー タスクで使用する場合があります。 **DelayValidation** プロパティはパッケージ ベル、またはパッケージに含まれている個別のタスクやコンテナーのレベルで有効にできます。  
  
     **DelayValidation** プロパティはデータ フロー タスク上で設定できますが、個別のデータ フロー コンポーネントでは設定できません。 個別のデータ フロー コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> プロパティを **false**。 ただし、このプロパティの値が **false**の場合、コンポーネントは外部データ ソースのメタデータに変更が加えられても認識しません。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> プロパティを **true** に設定すると、特にパッケージでトランザクションを使用している場合、データベース内でのロックに起因するブロッキング問題を回避するのに役立ちます。  
  
## <a name="troubleshoot-run-time-permissions-issues"></a>実行時の権限の問題のトラブルシューティング  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを使用して配置済みパッケージの実行を試みたときにエラーが発生した場合は、エージェントが使用しているアカウントに必要な権限がない可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブから実行するパッケージのトラブルシューティング方法については、「[SQL Server エージェントのジョブ ステップから SSIS パッケージを呼び出すとき、SSIS パッケージが実行されません。](https://support.microsoft.com/kb/918760)」を参照してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントのジョブからパッケージを実行する方法の詳細については、「 [パッケージに対する SQL Server エージェント ジョブ](../../integration-services/packages/sql-server-agent-jobs-for-packages.md)」を参照してください。  
  
 Excel や Access のデータ ソースに接続するには、TEMP 環境変数および TMP 環境変数で指定されているフォルダー内の一時ファイルの読み取り、書き込み、作成、および削除を行う権限を持ったアカウントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントに必要です。  
  
## <a name="troubleshoot-64-bit-issues"></a>64 ビット問題のトラブルシューティング  
  
-   **一部のデータ プロバイダーは 64 ビット プラットフォームに対応していない**。 特に、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet OLE DB Provider は Excel や Access のデータ ソースへの接続に必要ですが、64 ビット バージョンはありません。  
  
## <a name="troubleshoot-errors-without-a-description"></a>説明のないエラーのトラブルシューティング  
 説明のない [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] エラーが発生した場合は、「 [Integration Services のエラーおよびメッセージのリファレンス](../../integration-services/integration-services-error-and-message-reference.md) 」でエラー番号を検索することで、エラーの説明を参照できます。 現時点では、この一覧にトラブルシューティング情報は含まれていません。  
  
## <a name="related-tasks"></a>Related Tasks  
 [データ フローのデバッグ](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 dougbert.com のブログ記事「 [Adding the error column name to an error output](https://go.microsoft.com/fwlink/?LinkId=261546)」(エラー出力にエラー列名を追加する)  
