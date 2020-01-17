---
title: パッケージでプロパティ式を使用する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], expressions
- Integration Services packages, expressions
- SQL Server Integration Services packages, expressions
- dynamic properties
- updating package properties
- SSIS packages, expressions
- expressions [Integration Services], property expressions
- property expressions [Integration Services]
ms.assetid: a4bfc925-3ef6-431e-b1dd-7e0023d3a92d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dd78d7fb5f80b766dc7c51ae077d2a241c34d59c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768855"
---
# <a name="use-property-expressions-in-packages"></a>パッケージでプロパティ式を使用する
  プロパティ式とは、実行時にプロパティの動的更新を可能にするためにプロパティに割り当てられた式のことです。 たとえば、プロパティ式を使用して、変数に格納された電子メール アドレスを挿入して、メール送信タスクで使用される [宛先] 行を更新できます。  
  
 式は、パッケージ、タスク、Foreach ループ、For ループ、シーケンス、Foreach 列挙子、イベント ハンドラー、パッケージまたはプロジェクト レベルの接続マネージャー、またはログ プロバイダーに追加できます。 これらのオブジェクトの読み取り/書き込みプロパティはすべて、プロパティ式を実装できます。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] では、データ フロー コンポーネントの一部のカスタム プロパティでプロパティ式を使用することもできます。 変数と優先順位制約では、プロパティ式がサポートされていませんが、式を使用できる特殊なプロパティが使用されています。  
  
 プロパティ式は、いろいろな方法で更新できます。  
  
-   ユーザー定義変数をパッケージ構成に含め、パッケージを配置するときに更新できます。 実行時には、プロパティ式は更新された変数値を使用して評価されます。  
  
-   式に含まれるシステム変数は実行時に更新されます。これにより、プロパティの評価結果が変わります。  
  
-   日付と時刻の関数は実行時に評価され、更新された値をプロパティ式に提供します。  
  
-   式内の変数は、スクリプト タスクおよびスクリプト コンポーネントが実行するスクリプトによって更新できます。  
  
 式は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 式言語を使用して作成します。 式では、式言語で提供される演算子、関数、および型キャストと組み合わせて、システム変数またはユーザー定義変数を使用できます。  
  
> [!NOTE]  
>  ユーザー定義変数およびシステム変数の名前では、大文字と小文字が区別されます。  
  
 詳細については、「 [Integration Services (SSIS) 式](integration-services-ssis-expressions.md)に評価されるまでそのワークフローを繰り返します。  
  
 プロパティ式の重要な使い方として、パッケージを配置するインスタンスごとに構成をカスタマイズできます。 これにより、異なる環境に合わせてパッケージのプロパティを動的に更新できます。 たとえば、接続マネージャーの接続文字列に変数を割り当てるプロパティ式を作成し、パッケージが配置されたときに変数が更新されるようにしておくと、実行時に適切な接続文字列が使用されます。 パッケージの構成は、プロパティ式が評価される前に読み込まれます。  
  
 1 つのプロパティで使用できるプロパティ式は 1 つだけであり、1 つのプロパティ式は 1 つのプロパティだけに適用できます。 ただし、同じプロパティ式を複数個作成し、それらを異なるプロパティに割り当てることができます。  
  
 プロパティによっては、列挙子の値を使用して設定するものもあります。 プロパティ式で列挙子メンバーを参照するときは、その列挙子メンバーの表示名に相当する数値を使用する必要があります。 たとえば、プロパティ式で `LoggingMode` 列挙からの値を使用する `DTSLoggingMode` プロパティを設定する場合、プロパティ式では表示名 `Enabled`、`Disabled`、または `UseParentSetting` ではなく 0、1、または 2 を使用する必要があります。 詳細については、「 [Enumerated Constants in Property Expressions](enumerated-constants-in-property-expressions.md)」(プロパティ式における列挙定数) を参照してください。  
  
## <a name="property-expression-user-interface"></a>プロパティ式のユーザー インターフェイス  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] には、プロパティ式を作成および管理するためのツール セットが用意されています。  
  
-   タスク、For ループ コンテナー、および Foreach コンテナーのカスタム エディターにある **[式]** ページ。 **[式]** ページでは、式を編集したり、タスク、Foreach ループ、または For ループで使用されるプロパティ式のリストを表示できます。  
  
-   **[プロパティ]** ウィンドウ。式を編集したり、パッケージまたはパッケージ オブジェクトで使用されるプロパティ式のリストを表示できます。  
  
-   **[プロパティ式エディター]** ダイアログ ボックス。プロパティ式を作成、更新、および削除できます。  
  
-   **[式ビルダー]** ダイアログ ボックス。グラフィカルなツールを使用して式を作成できます。 **[式ビルダー]** ダイアログ ボックスでは、評価結果をプロパティに割り当てることなく、式の評価を確認できます。  
  
 次の図は、プロパティ式を追加、変更、および削除するために使用するユーザー インターフェイスを示しています。  
  
 ![プロパティ式のユーザー インターフェイス](../media/ssis-propertyexpressionui.gif "プロパティ式のユーザー インターフェイス")  
  
 **[プロパティ]** ウィンドウおよび **[式]** ページでは、 **[式]** コレクション レベルの参照ボタン **[...]** をクリックして **[プロパティ式エディター]** ダイアログ ボックスを開きます。 プロパティ式エディターでは、プロパティを式にマップし、プロパティ式を入力できます。 グラフィカルな式ツールを使用して式を作成してから検証する場合は、式レベルの参照ボタン **[...]** をクリックして **[式ビルダー]** ダイアログ ボックスを開き、式を作成または変更します。その後、必要に応じて式を検証します。  
  
 **[式ビルダー]** ダイアログ ボックスは、 **[プロパティ式エディター]** ダイアログ ボックスから開くこともできます。  
  
#### <a name="to-work-with-property-expressions"></a>プロパティ式を操作するには  
  
-   [プロパティ式を追加または変更する](add-or-change-a-property-expression.md)  
  
### <a name="setting-property-expressions-of-data-flow-components"></a>データ フロー コンポーネントのプロパティ式の設定  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]でパッケージを構築すると、プロパティ式をサポートするデータ フロー コンポーネントのプロパティが、そのデータ フロー コンポーネントが属するデータ フロー タスクに表示されます。 データ フロー コンポーネントのプロパティ式を追加、変更、および削除するには、データ フロー コンポーネントが属するデータ フローのデータ フロー タスクを右クリックし、 **[プロパティ]** をクリックします。 [プロパティ] ウィンドウに、プロパティ式を使用できるデータ フロー コンポーネントのプロパティが一覧表示されます。 たとえば、SampleCustomer という名前のデータ フローで行サンプリング変換の SamplingValue プロパティのプロパティ式を作成または変更するには、行サンプリング変換が属するデータ フローのデータ フロー タスクを右クリックし、 **[プロパティ]** をクリックします。 [プロパティ] ウィンドウに、SamplingValue プロパティが [SampleCustomer].[SamplingValue] の形式で一覧表示されます。  
  
 [プロパティ] ウィンドウで、データ フロー コンポーネントのプロパティ式を他の種類の [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] オブジェクトのプロパティ式と同じ方法で追加、変更、および削除します。 また、[プロパティ] ウィンドウから、データ フロー コンポーネントのプロパティ式を追加、変更、または削除するために使用するさまざまなダイアログ ボックスやビルダーにアクセスすることもできます。 プロパティ式で更新できるデータ フロー コンポーネントのプロパティの詳細については、「 [Transformation Custom Properties](../data-flow/transformations/transformation-custom-properties.md)」(変換のカスタム プロパティ) を参照してください。  
  
## <a name="loading-property-expressions"></a>プロパティ式の読み込み  
 プロパティ式が読み込まれるタイミングは、指定したり制御することができません。 プロパティ式は、パッケージとパッケージ オブジェクトの検証時に評価され読み込まれます。 パッケージを保存し、 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーでパッケージを開いて、パッケージを実行すると、検証が行われます。  
  
 そのため、プロパティ式の追加後にパッケージを保存するか、パッケージを実行するか、パッケージを再度開かない限り、プロパティ式を使用するパッケージ オブジェクトのプロパティの更新値は [!INCLUDE[ssIS](../../../includes/ssis-md.md)] デザイナーに表示されません。  
  
 各種のオブジェクト (接続マネージャー、ログ プロバイダー、列挙子) に関連付けられているプロパティ式は、その種類のオブジェクトに固有のメソッドを呼び出したときにも読み込まれます。 たとえば、接続マネージャーのプロパティは、 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] が接続のインスタンスを作成する前に読み込まれます。  
  
 プロパティ式は、パッケージ構成が読み込まれた後に読み込まれます。 たとえば変数は、対応する構成でまず更新されてから、その変数を使用するプロパティ式が評価され読み込まれます。 つまり、プロパティ式が使用する変数の値は常に、構成によって設定された値です。  
  
> [!NOTE]  
>  使用することはできません、`Set`のオプション、 **dtexec**プロパティ式を設定するためのユーティリティ。  
  
 次の表に、 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] のプロパティ式が評価され読み込まれるタイミングをまとめます。  
  
|オブジェクトの種類|読み込みと評価|  
|-----------------|-----------------------|  
|パッケージ、Foreach ループ、For ループ、シーケンス、タスク、データ フロー コンポーネント|構成の読み込み後<br /><br /> 検証前<br /><br /> 実行前|  
|接続マネージャー|構成の読み込み後<br /><br /> 検証前<br /><br /> 実行前<br /><br /> 接続インスタンスの作成前|  
|ログ プロバイダー|構成の読み込み後<br /><br /> 検証前<br /><br /> 実行前<br /><br /> ログを開く前|  
|Foreach 列挙子|構成の読み込み後<br /><br /> 検証前<br /><br /> 実行前<br /><br /> ループの各列挙前|  
  
## <a name="using-property-expressions-in-the-foreach-loop"></a>Foreach ループでのプロパティ式の使用  
 多くの場合、Foreach ループ コンテナー内部で使用される接続マネージャーの `ConnectionString` プロパティ値を設定するには、プロパティ式の実装が役立ちます。 ループの各反復処理で列挙子の現在値が変数にマップされた後、プロパティ式でこの変数の値を使用して `ConnectionString` プロパティの値を動的に更新できます。  
  
 Foreach ループで使用されるファイル、複数のファイル、フラット ファイル、および複数フラット ファイル接続マネージャーの `ConnectionString` プロパティでプロパティ式を使用する場合は、いくつかの点について考慮する必要があります。 `MaxConcurrentExecutables` プロパティを 1 より大きな値または -1 に設定することにより、複数の実行可能ファイルが同時に実行されるようにパッケージを構成できます。 値が -1 の場合は、同時に実行できる実行可能ファイルの最大数が、プロセッサの総数に 2 を加えた数と等しいことを意味します。 実行可能ファイルを並列実行することに起因する不適切な結果を回避するには、値 `MaxConcurrentExecutables` を 1 に設定することをお勧めします。 `MaxConcurrentExecutables` を 1 に設定しないと、`ConnectionString` プロパティの値を保証できず、結果を予測できません。  
  
 たとえば、フォルダー内のファイルを列挙し、ファイル名を取得し、SQL 実行タスクを使用してテーブルに各ファイル名を挿入する Foreach ループを考えます。 `MaxConcurrentExecutables` を 1 に設定しないと、SQL 実行タスクの 2 つのインスタンスが同時にテーブルへの書き込みを行う場合、書き込みが競合する可能性があります。  
  
## <a name="sample-property-expressions"></a>サンプルのプロパティ式  
 プロパティ式でのシステム変数、演算子、関数、および文字列リテラルの使い方を次のサンプル式に示します。  
  
### <a name="property-expression-for-the-loggingmode-property-of-a-package"></a>パッケージの LoggingMode プロパティ用のプロパティ式  
 次のプロパティ式を使用すると、パッケージの LoggingMode プロパティを設定できます。 この式では、DAY 関数と GETDATE 関数を使用して、ある日付の日要素を表す整数を取得します。 日要素が 1 日または 15 日の場合、ログ記録が有効です。それ以外の場合は、ログ記録が無効です。 値 1 は、整数 LoggingMode 列挙子メンバーの同等`Enabled`、値 2 は、整数とメンバーの同等`Disabled`します。 式では、列挙子のメンバー名ではなく、数値を使用する必要があります。  
  
 `DAY((DT_DBTIMESTAMP)GETDATE())==1||DAY((DT_DBTIMESTAMP)GETDATE())==15?1:2`  
  
### <a name="property-expression-for-the-subject-of-an-e-mail-message"></a>電子メール メッセージの件名用のプロパティ式  
 次のプロパティ式を使用すると、メール送信タスクの Subject プロパティを設定して、適切な電子メールの件名を入力できます。 この式では、文字列リテラル、システム変数、連結演算子 (+)、キャスト演算子、DATEDIFF 関数、および GETDATE 関数の組み合わせを使用しています。 システム変数は `PackageName` 変数と `StartTime` 変数です。  
  
 `"PExpression-->Package: (" + @[System::PackageName] + ") Started:"+  (DT_WSTR, 30) @[System::StartTime] + " Duration:"  +  (DT_WSTR,10) (DATEDIFF( "ss", @[System::StartTime] , GETDATE()  )) + " seconds"`  
  
 パッケージの名前が EmailRowCountPP であり、3/4/2005 に実行され、実行された期間が 9 秒間であった場合、この式は次の文字列に評価されます。  
  
 PExpression-->Package: (EmailRowCountPP) Started:3/4/2005 11:06:18 AM Duration:9 seconds.  
  
### <a name="property-expression-for-the-message-of-an-e-mail-message"></a>電子メール メッセージのメッセージ用のプロパティ式  
 次のプロパティ式を使用すると、メール送信タスクの MessageSource プロパティを設定できます。 この式では、文字列リテラル、ユーザー定義変数、および連結演算子 (+) の組み合わせを使用しています。 ユーザー定義変数の名前は、 `nasdaqrawrows`、 `nyserawrows`、および `amexrawrows`です。 文字列 "\n" は、復帰を示します。  
  
 `"Rows Processed: "  +   "\n" +"   NASDAQ: "  +   (dt_wstr,9)@[nasdaqrawrows]   + "\n" + "   NYSE: "  +  (dt_wstr,9)@[nyserawrows]  + "\n" + "   Amex: "  +  (dt_wstr,9)@[amexrawrows]`  
  
 `nasdaqrawrows` が 7058、 `nyserawrows` が 3528、 `amexrawrows` が 1102 である場合、式は次の文字列に評価されます。  
  
 Rows Processed:  
  
 NASDAQ:7058  
  
 NYSE:3528  
  
 AMEX:1102  
  
### <a name="property-expression-for-the-executable-property-of-an-execute-process-task"></a>プロセス実行タスクの Executable プロパティ用のプロパティ式  
 次のプロパティ式を使用すると、プロセス実行タスクの Executable プロパティを設定できます。 この式では、文字列リテラル、演算子、および関数の組み合わせを使用しています。 この式では、DATEPART 関数、GETDATE 関数、および条件演算子を使用しています。  
  
 `DATEPART("weekday", GETDATE()) ==2?"notepad.exe":"mspaint.exe"`  
  
 プロセス実行タスクは週の 2 日目に notepad.exe を実行し、それ以外の日には mspaint.exe を実行します。  
  
### <a name="property-expression-for-the-connectionstring-property-of-a-flat-file-connection-manager"></a>フラット ファイル接続マネージャーの ConnectionString プロパティ用のプロパティ式  
 次のプロパティ式を使用すると、フラット ファイル接続マネージャーの ConnectionString プロパティを設定できます。 この式では、テキスト ファイルへのパスを格納するユーザー定義変数 `myfilenamefull`を 1 つだけ使用しています。  
  
 `@[User::myfilenamefull]`  
  
> [!NOTE]  
>  接続マネージャー用のプロパティ式には、[プロパティ] ウィンドウからのみアクセスできます。 接続マネージャーのプロパティを表示するには、[プロパティ] ウィンドウが開いているときに **デザイナーの** [接続マネージャー] [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 領域で接続マネージャーを選択するか、接続マネージャーを右クリックして **[プロパティ]** を選択する必要があります。  
  
### <a name="property-expression-for-the-configstring-property-of-a-text-file-log-provider"></a>テキスト ファイル ログ プロバイダーの ConfigString プロパティ用のプロパティ式  
 次のプロパティ式を使用すると、テキスト ファイル ログ プロバイダーの ConfigString プロパティを設定できます。 この式では、使用するファイル接続マネージャーの名前を格納するユーザー定義変数 `varConfigString`を 1 つだけ使用しています。 ファイル接続マネージャーにより、ログ エントリの書き込み先のテキスト ファイルのパスが指定されます。  
  
 `@[User::varConfigString]`  
  
> [!NOTE]  
>  ログ プロバイダー用のプロパティ式には、[プロパティ] ウィンドウからのみアクセスできます。 ログ プロバイダーのプロパティを表示するには、[プロパティ] ウィンドウが開いているときに **デザイナーの** [パッケージ エクスプローラー] [!INCLUDE[ssIS](../../../includes/ssis-md.md)] タブでログ プロバイダーを選択するか、パッケージ エクスプローラーでログ プロバイダーを右クリックし、 **[プロパティ]** をクリックする必要があります。  
  
## <a name="external-resources"></a>外部リソース  
  
-   [式/構成マーカー (CodePlex プロジェクト)](https://go.microsoft.com/fwlink/?LinkId=146625)  
  
-   social.technet.microsoft.com の技術記事「 [SSIS 式の例](https://go.microsoft.com/fwlink/?LinkId=220761)」  
  
## <a name="see-also"></a>参照  
 [パッケージで変数を使用する](../use-variables-in-packages.md)  
  
  
