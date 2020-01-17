---
title: Integration Services (SSIS) の変数 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- user-defined variables [Integration Services]
- scope [Integration Services]
- system variables [Integration Services]
- variables [Integration Services]
- variables [Integration Services], about variables
- values [Integration Services]
ms.assetid: c1e81ad6-628b-46d4-9b09-d2866517b6ca
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 973e5e1449205d5e72abfa03068db3c8c3e98f87
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296161"
---
# <a name="integration-services-ssis-variables"></a>Integration Services (SSIS) の変数

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  変数には、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージと、パッケージに含まれるコンテナー、タスク、およびイベント ハンドラーで、実行時に使用できる値が格納されます。 スクリプト タスクおよびスクリプト コンポーネント内のスクリプトも、変数を使用できます。 タスクとコンテナーにワークフロー内での順位を付ける優先順位制約では、制約の定義に式を含める場合に変数を使用できます。  
  
 変数は、次の目的で [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージ内で使用できます。  
  
-   実行時に、パッケージ要素のプロパティを更新します。 たとえば、1 つの Foreach ループ コンテナーで許可できる実行可能ファイルの数を動的に設定できます。  
  
-   メモリ内に参照テーブルを組み込みます。 たとえば、パッケージは、データ値を持つ変数を読み込む SQL 実行タスクを実行できます。  
  
-   データ値を持つ変数を読み込み、それらを使用して WHERE 句の検索条件を指定します。 たとえば、SQL 実行タスク内の Transact-SQL ステートメントによって使用される変数の値をスクリプト タスク内のスクリプトで更新できます。  
  
-   整数値を持つ変数を読み込み、その値を使用してパッケージ制御フロー内のループを制御します。 たとえば、For ループ コンテナーの評価式内の変数を使用して繰り返しを制御できます。  
  
-   実行時に Transact-SQL ステートメントのパラメーター値を作成します。 たとえば、パッケージは SQL 実行タスクを実行し、変数を使用して Transact-SQL ステートメント内のパラメーターを動的に設定できます。  
  
-   変数値が含まれる式を構築します。 たとえば、派生列の変換は、変数値に列の値を乗算することによって取得した結果を使用して、列の値を設定できます。  
  
## <a name="system-and-user-defined-variables"></a>システム変数とユーザー定義変数  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、ユーザー定義変数とシステム変数の、2 種類の変数がサポートされています。 ユーザー定義変数とはパッケージの開発者によって定義された変数で、システム変数とは [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]によって定義された変数です。 ユーザー定義変数は、パッケージで必要な数だけ作成できますが、システム変数は追加作成できません。  
  
 変数 (システム変数とユーザー定義変数) はすべて、SQL 実行タスクが使用するパラメーター バインドで使用して、SQL ステートメントのパラメーターに変数をマップできます。 詳細については、「 [SQL 実行タスク](../integration-services/control-flow/execute-sql-task.md) 」と「 [SQL 実行タスクのパラメーターとリターン コード](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)」を参照してください。  
  
> [!NOTE]  
>  ユーザー定義変数とシステム変数の名前では、大文字と小文字が区別されます。  
  
 パッケージ、Foreach ループ コンテナー、For ループ コンテナー、シーケンス コンテナー、タスク、およびイベント ハンドラーの、すべての種類の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] コンテナーに対してユーザー定義変数を作成できます。 ユーザー定義変数は、コンテナーの変数のコレクションのメンバーです。  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーを使用してパッケージを作成すると、変数のコレクションのメンバーは、 **デザイナーの** [パッケージ エクスプローラー] **タブ上の** [変数] [!INCLUDE[ssIS](../includes/ssis-md.md)] フォルダー内に表示されます。 このフォルダーには、ユーザー定義変数とシステム変数が一覧表示されます。  
  
 ユーザー定義変数は、次の方法で構成できます。  
  
-   変数の名前と説明を指定します。  
  
-   変数の名前空間を指定します。  
  
-   変数値が変更されたときに、変数がイベントを起動するかどうかを示します。  
  
-   変数は読み取り専用か、読み取り/書き込み可能かを示します。  
  
-   式の評価結果を使用して、変数値を設定します。  
  
-   パッケージ、またはタスクなどのパッケージ オブジェクトのスコープ内に、変数を作成します。  
  
-   変数の値とデータ型を指定します。  
  
 システム変数で構成可能なオプションは、変数値が変更されたときにイベントを起動するかどうかを指定するオプションのみです。  
  
 コンテナーの種類ごとに、異なるセットのシステム変数を使用できます。 パッケージとパッケージ要素が使用するシステム変数の詳細については、「 [システム変数](../integration-services/system-variables.md)」を参照してください。  
  
 変数の実際的な使用シナリオの詳細については、「 [パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)」を参照してください。  
  
## <a name="properties-of-variables"></a>変数のプロパティ  
 **[変数]** ウィンドウまたは **[プロパティ]** ウィンドウで、次のプロパティを設定してユーザー定義変数を構成できます。 一部のプロパティは [プロパティ] ウィンドウでのみ使用できます。  
  
> [!NOTE]  
>  システム変数で構成可能なオプションは、変数値が変更されたときにイベントを起動するかどうかを指定するオプションのみです。  
  
 **Description**    
 変数の説明を指定します。  
  
 **EvaluateAsExpression**    
 このプロパティを **True**に設定すると、指定された式を使用して変数の値が設定されます。  
  
 **式**    
 変数に割り当てられる式を指定します。  
  
 **名前**    
 変数名を指定します。  
  
 **名前空間**  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] では、 **User** および **System**という 2 つの名前空間が用意されています。 既定では、カスタム変数は **User** 名前空間に属し、システム変数は **System** 名前空間に属します。 ユーザー定義変数用に追加の名前空間を作成し、 **User** 名前空間の名前を変更することはできますが、 **System** 名前空間の名前を変更したり、変数を **System** 名前空間に追加したり、システム変数を別の名前空間に割り当てたりすることはできません。  
  
**RaiseChangedEvent**  
 このプロパティを **True**に設定すると、変数の値が変更された場合に **OnVariableValueChanged** イベントが発生します。  
  
 **ReadOnly**  
 このプロパティを **False**に設定すると、変数は読み取り/書き込み用となります。  
  
**スコープ**    
 > [!NOTE]  
>  **[変数]** ウィンドウの **[変数の移動]** をクリックすることによってしか、このプロパティの設定は変更できません。  
  
 変数は、パッケージのスコープ内、またはパッケージ内のコンテナー、タスク、またはイベント ハンドラーのスコープ内で作成されます。 パッケージ コンテナーは、コンテナー階層の最上層にあるため、パッケージ スコープを持つ変数はグローバル変数と同じように機能し、パッケージ内のすべてのコンテナーで使用できます。 同様に、For ループ コンテナーなどのコンテナーのスコープ内で定義された変数は、For ループ コンテナー内のすべてのタスクまたはコンテナーで使用できます。  
  
 パッケージでパッケージ実行タスクを使用して他のパッケージを実行する場合、呼び出し元のパッケージのスコープまたはパッケージ実行タスクで定義された変数は、構成の種類で親パッケージ変数を使用することにより、呼び出し先のパッケージで使用できます。 詳細については、「 [パッケージ構成](../integration-services/packages/package-configurations.md)」を参照してください。  
  
**[IncludeInDebugDump]**  
 変数値がデバッグ ダンプ ファイルに含まれるかどうかを示します。  
  
 ユーザー定義変数およびシステム変数の場合、 **[InclueInDebugDump]** オプションの既定値は **true**です。  
  
 ただし、ユーザー定義変数に関しては、次の条件に該当する場合、システムによって **[IncludeInDebugDump]** オプションが **false** にリセットされます。  
  
-   **EvaluateAsExpression** 変数のプロパティが **true**に設定されている場合は、 **IncludeInDebugDump** オプションが **false**にリセットされます。  
  
     式のテキストを変数値としてデバッグ ダンプ ファイルに含めるには、 **[IncludeInDebugDump]** オプションを **true**に設定します。  
  
-   変数のデータ型が文字列に変更された場合は、 **[IncludeInDebugDump]** オプションが **false**にリセットされます。  
  
 **[IncludeInDebugDump]** オプションが **false** にリセットされると、ユーザーが選択した値をオーバーライドする場合があります。  
  
**値**    
ユーザー定義変数の値には、リテラルまたは式を設定できます。 変数の値を null にすることはできません。 変数の既定値は次のようになります。

| データ型 | 既定値 |
|---|---|
| Boolean | False |
| 数値データ型とバイナリ データ型 | 0 (ゼロ) |
| Char データ型と文字列データ型 | (空の文字列) |
| Object | System.Object |
| | |

変数には、変数値と変数のデータ型を設定するオプションが含まれています。 この 2 つのプロパティには互換性が必要です。たとえば、文字列の値を整数データ型に使用することはできません。  
  
 変数を式として評価するように構成した場合は、式を指定する必要があります。 式は実行時に評価され、変数は評価結果に設定されます。 たとえば、変数が式 `DATEPART("month", GETDATE())` を使用している場合、変数の値は、現在の日付の月と等しい数値になります。 式は、 [!INCLUDE[ssIS](../includes/ssis-md.md)] 式の構文文法を使用する、有効な式である必要があります。 変数に式を使用する場合、リテラルおよび式文法が提供する演算子と関数も使用できますが、パッケージ内のデータ フローの列は参照できません。 式の最大長は 4,000 文字です。 詳細については、「 [Integration Services (SSIS) 式](../integration-services/expressions/integration-services-ssis-expressions.md)に評価されるまでそのワークフローを繰り返します。  
  
**ValueType**    
 > [!NOTE]  
>  このプロパティの値は **[変数]** ウィンドウの **[データ型]** 列に表示されます。  
  
 変数の値のデータ型を指定します。  

## <a name="scenarios-for-using-variables"></a>変数の使用に関するシナリオ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージでは、変数をさまざまな方法で使用します。 パッケージにユーザー定義変数を追加して、ソリューションに必要な柔軟性と管理性を実装しないと、パッケージ開発があまり進まない場合もあります。 シナリオによっては、システム変数もよく使用します。  
  
 **プロパティの式** パッケージおよびパッケージ オブジェクトのプロパティを設定するプロパティ式に値を提供するために、変数を使用します。 たとえば、式 `SELECT * FROM @varTableName` に含まれている変数 `varTableName` は、SQL 実行タスクによって実行される SQL ステートメントを更新します。 式 `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`では、 `varPackageFirst` 変数で指定されたパッケージを月の最初の日に実行し、 `varPackageOther` 変数で指定されたパッケージを別の日に実行することにより、[パッケージの実行] タスクで実行されるパッケージを更新しています。 詳細については、「 [パッケージでプロパティ式を使用する](../integration-services/expressions/use-property-expressions-in-packages.md)」を参照してください。  
  
 **データ フロー式** 変数を使用して、派生列変換と条件分割変換で列に値を設定するための式や、データ行を各種の変換出力に送るための式に値を提供します。 たとえば、式 `@varSalutation + LastName`は、 `VarSalutation` 変数の値と `LastName` 列を連結します。 式 `Income < @HighIncome` は、`Income` 列の値が `HighIncome` 変数の値よりも小さいデータ行を出力に送信します。 詳細については、「[派生列変換](../integration-services/data-flow/transformations/derived-column-transformation.md)」、「[条件分割変換](../integration-services/data-flow/transformations/conditional-split-transformation.md)」、および「[Integration Services (SSIS) の式](../integration-services/expressions/integration-services-ssis-expressions.md)」を参照してください。  
  
 **優先順位制約の式** 優先順位制約で制約付き実行可能ファイルを実行するかどうかを決定するために使用する値を提供します。 これらの式は、実行結果 (成功、失敗、完了) と組み合わせて使用することも、実行結果の代わりに使用することもできます。 たとえば、式 `@varMax > @varMin`が **true**に評価される場合、実行可能ファイルは実行されます。 詳細については、「[優先順位制約に式を追加する](https://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1)」を参照してください。  
  
 **パラメーターおよびリターン コード** 入力パラメーターに値を提供したり、出力パラメーターおよびリターン コードの値を格納したりします。 そのためには、変数をパラメーターおよび戻り値にマップします。 たとえば、変数 `varProductId` を 23 に設定して SQL ステートメント `SELECT * from Production.Product WHERE ProductID = ?`を実行すると、 `ProductID` が 23 である製品が取得されます。 詳細については、「 [SQL 実行タスク](../integration-services/control-flow/execute-sql-task.md) 」と「 [SQL 実行タスクのパラメーターとリターン コード](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)」を参照してください。  
  
 **For ループ式** For ループの初期化式、評価式、および代入式で使用する値を提供します。 たとえば、変数 `varCount` が 2、変数 `varMaxCount` が 10、初期化式が `@varCount`、評価式が  `@varCount < @varMaxCount`、代入式が `@varCount =@varCount +1`の場合、ループは 8 回繰り返されます。 詳細については、「 [For ループ コンテナー](../integration-services/control-flow/for-loop-container.md)」を参照してください。  
  
 **親パッケージ変数の構成** 親パッケージから子パッケージに値を渡します。 子パッケージは、親パッケージ変数の構成を使用することにより、親パッケージの変数にアクセスできます。 たとえば、子パッケージが親パッケージと同じ日付を使用する必要がある場合、子パッケージは親パッケージの GETDATE 関数によって設定される変数を指定する親パッケージ変数の構成を定義できます。 詳細については、「 [パッケージ実行タスク](../integration-services/control-flow/execute-package-task.md) 」と「 [パッケージ構成](../integration-services/packages/package-configurations.md)」を参照してください。  
  
 **スクリプト タスクおよびスクリプト コンポーネント** 読み取り専用変数および読み取り/書き込み変数の一覧をスクリプト タスクまたはスクリプト コンポーネントに提供し、スクリプト内の読み取り/書き込み変数を更新して、更新された値をスクリプトの内外で使用します。 たとえば、コード `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`では、スクリプト変数 `numberOfCars` が変数 `NumberOfCars`の値によって更新されます。 詳細については、「 [スクリプト タスクでの変数の使用](../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)」を参照してください。  

## <a name="add-a-variable"></a>変数の追加  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、操作する [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージをダブルクリックして開きます。  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、変数のスコープを定義するには、次のいずれかの操作を行います。  
  
    -   スコープをパッケージに設定するには、 **[制御フロー]** タブのデザイン画面上の任意の場所をクリックします。  
  
    -   スコープをイベント ハンドラーに設定するには、 **[イベント ハンドラー]** タブのデザイン画面で、実行可能ファイルおよびイベント ハンドラーを選択します。  
  
    -   スコープをタスクまたはコンテナーに設定するには、 **[制御フロー]** タブまたは **[イベント ハンドラー]** タブのデザイン画面で、タスクまたはコンテナーをクリックします。  
  
4.  **SSIS** メニューの **[変数]** をクリックします。 必要に応じて、View.Variables コマンドを **[オプション]** ダイアログ ボックスの **[キーボード]** ページで選択したキーの組み合わせにマップすることによって、 **[変数]** ウィンドウを表示することもできます。  
  
5.  **[変数]** ウィンドウで、 **[変数の追加]** アイコンをクリックします。 新しい変数が一覧に追加されます。  
  
6.  必要に応じて、 **[グリッドのオプション]** アイコンをクリックし、 **[可変グリッドのオプション]** ダイアログ ボックスに表示する追加の列を選択して、 **[OK]** をクリックします。  
  
7.  必要に応じて、変数のプロパティを設定します。 詳細については、「 [ユーザー定義変数のプロパティを設定する](https://msdn.microsoft.com/library/f98ddbec-f668-4dba-a768-44ac3ae0536f)」を参照してください。  
  
8.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  

### <a name="add-variable-dialog-box"></a>[変数の追加] ダイアログ ボックス
**[変数の追加]** ダイアログ ボックスを使用すると、新しい変数のプロパティを指定できます。  
  
#### <a name="options"></a>オプション  
 **コンテナー**  
 一覧からコンテナーを選択します。 コンテナーにより、変数の有効範囲が定義されます。 パッケージまたはパッケージ内の実行可能ファイルがコンテナーになります。  
  
 **[名前]**  
 変数名を入力します。  
  
 **Namespace**  
 変数の名前空間を指定します。 既定で、ユーザー定義の変数は **User** 名前空間に置かれます。  
  
 **[値の型]**  
 データ型を選択します。  
  
 **Value**  
 値を入力します。 **[値の型]** オプションで指定したデータ型に適合する値を入力する必要があります。  
  
 **読み取り専用です。**  
 変数を読み取り専用にします。  
   
## <a name="delete-a-variable"></a>変数の削除  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージを右クリックして開きます。  
  
3.  **SSIS** メニューの **[変数]** をクリックします。 必要に応じて、View.Variables コマンドを **[オプション]** ダイアログ ボックスの **[キーボード]** ページで選択したキーの組み合わせにマップすることによって、 **[変数]** ウィンドウを表示することもできます。  
  
4.  削除する変数を選択し、 **[変数の削除]** をクリックします。  
  
     [変数] ウィンドウに変数が表示されない場合は、 **[グリッドのオプション]** をクリックし、 **[すべてのスコープの変数を表示する]** を選択します。  
  
5.  **[変数の削除の確認]** ダイアログ ボックスが開いた場合は、 **[はい]** をクリックして確定します。  
  
6.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="change-the-scope-of-a-variable"></a>変数のスコープの変更  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージを右クリックして開きます。  
  
3.  **SSIS** メニューの **[変数]** をクリックします。 必要に応じて、View.Variables コマンドを **[オプション]** ダイアログ ボックスの **[キーボード]** ページで選択したキーの組み合わせにマップすることによって、 **[変数]** ウィンドウを表示することもできます。  
  
4.  変数を選択して、 **[変数の移動]** をクリックします。  
  
     [変数] ウィンドウに変数が表示されない場合は、 **[グリッドのオプション]** をクリックし、 **[すべてのスコープの変数を表示する]** を選択します。  
  
5.  **[新しいスコープの選択]** ダイアログ ボックスで、パッケージまたはパッケージ内のコンテナー、タスク、またはイベント ハンドラーを選択して、変数のスコープを変更します。  
  
6.  更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  

## <a name="set-the-properties-of-a-user-defined-variable"></a>ユーザー定義変数のプロパティを設定する
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]でユーザー定義変数のプロパティを設定するには、次の機能のいずれかを使用します。  
  
-   [変数] ウィンドウ。  
  
-   [プロパティ] ウィンドウ。 **[プロパティ]** ウィンドウには、 **[変数]** ウィンドウでは使用できない変数を構成するための次のプロパティが一覧表示されています: Description、EvaluateAsExpression、Expression、ReadOnly、ValueType、IncludeInDebugDump。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、RaiseChangedEvent プロパティを除き、更新できないプロパティを持つ一連のシステム変数もあります。  
  
### <a name="set-expressions-on-variables"></a>変数への式の設定  
  
 **[プロパティ]** ウィンドウを使用してユーザー定義変数に式を設定する場合:  
  
-   変数の値は、Value プロパティまたは Expression プロパティによって設定できます。 既定では、EvaluateAsExpression プロパティが **False** に設定されており、Value プロパティによって変数の値が設定されます。 式を使用して値を設定するには、EvaluateAsExpression を **True**に設定してから、Expression プロパティで式を指定します。 Value プロパティには、自動的に式の評価結果が設定されます。  
  
-   ValueType プロパティには、Value プロパティの値のデータ型が含まれます。 Value が式によって設定される場合、ValueType は、式の評価結果と互換性があるデータ型に自動的に更新されます。 たとえば、Value に 0 が含まれ、ValueType プロパティに **Int32** が含まれる場合に Expression を GETDATE() に設定すると、Value には現在の日付と時間が含まれ、ValueType は **DateTime**に設定されます。  
  
-   変数の **[プロパティ]** ウィンドウからは **[式ビルダー]** ダイアログ ボックスを開くことができます。 このツールを使用すると、式の作成、検証、および評価を行うことができます。 詳しくは、「[式ビルダー](../integration-services/expressions/expression-builder.md)」と「[Integration Services &#40;SSIS&#41; の式](../integration-services/expressions/integration-services-ssis-expressions.md)」をご覧ください。  
  
 **[変数]** ウィンドウを使用してユーザー定義変数に式を設定する場合:  
  
-   式を使用して変数値を設定するには、最初に変数のデータ型が式の評価結果と互換性があることを確認してから、 **[変数]** ウィンドウの **[式]** 列に式を指定します。 **[プロパティ]** ウィンドウの EvaluateAsExpression プロパティが自動的に **True**に設定されます。  
  
-   変数に式を割り当てると、変数の横に特別なアイコン マーカーが表示されます。 この特別なアイコン マーカーは、式が設定されている接続マネージャーおよびタスクの横にも表示されます。  
  
-   変数の **[変数]** ウィンドウからは **[式ビルダー]** ダイアログ ボックスを開くことができます。 このツールを使用すると、式の作成、検証、および評価を行うことができます。 詳しくは、「[式ビルダー](../integration-services/expressions/expression-builder.md)」と「[Integration Services &#40;SSIS&#41; の式](../integration-services/expressions/integration-services-ssis-expressions.md)」をご覧ください。  
  
 **[変数]** ウィンドウおよび **[プロパティ]** ウィンドウでは、変数に式を割り当てて、**EvaluateAsExpression** を **True** に設定した場合、変数のデータ型は変更できません。  
  
### <a name="set-the-namespace-and-name-properties"></a>Namespace プロパティと Name プロパティの設定
  
 **Name** プロパティと **Namespace** プロパティの値の最初の文字は、Unicode Standard 2.0 に定義されているアルファベット文字か、アンダースコア (_) にする必要があります。 2 番目以降の文字では、Unicode Standard 2.0 に定義されている文字または数字と、アンダースコア (\_) を使用できます。  
  
### <a name="set-variable-properties-in-the-variables-window"></a>[変数] ウィンドウでの変数プロパティの設定   
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージを右クリックして開きます。  
  
3.  **SSIS** メニューの **[変数]** をクリックします。  
  
     必要に応じて、View.Variables コマンドを **[オプション]** ダイアログ ボックスの **[キーボード]** ページで選択したキーの組み合わせにマップすることによって、 **[変数]** ウィンドウを表示することもできます。  
  
4.  必要に応じて、 **[変数]** ウィンドウで **[グリッドのオプション]** をクリックして、 **[変数]** ウィンドウに表示する列を選択したり、変数の一覧に適用するフィルターを選択したりします。  
  
5.  一覧から変数を選択し、 **[名前]** 、 **[データ型]** 、 **[値]** 、 **[名前空間]** 、 **[Raise Change Event (変更イベントの発生)]** 、 **[説明]** 、 **[式]** の各列の値を更新します。  
  
6.  一覧で変数を選択し、 **[変数の移動]** をクリックしてスコープを変更します。  
  
7.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
### <a name="set-variable-properties-in-the-properties-window"></a>[プロパティ] ウィンドウでの変数プロパティの設定  

1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  ソリューション エクスプローラーで、パッケージを右クリックして開きます。  
  
3.  **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックします。  
  
4.  [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで、 **[パッケージ エクスプローラー]** タブをクリックし、[パッケージ] ノードを展開します。  
  
5.  パッケージの適用範囲の変数を変更するには、[変数] ノードを展開します。それ以外の場合は、変更する変数が含まれている [変数] ノードが表示されるまで、[イベント ハンドラー] または [実行可能ファイル] ノードを展開します。  
  
6.  変更するプロパティの変数をクリックします。  
  
7.  **[プロパティ]** ウィンドウで、読み取り/書き込みの変数プロパティを更新します。 ユーザー定義変数の場合は読み取り/読み取りのみのプロパティもあります。  
  
     プロパティの詳細については、「[Integration Services &#40;SSIS&#41; の変数](../integration-services/integration-services-ssis-variables.md)」を参照してください。  
  
8.  更新されたパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  

## <a name="update-a-variable-dynamically-with-configurations"></a>構成での変数の動的更新  
 変数を動的に更新するために、変数の構成を作成し、パッケージと共に構成を配置して、パッケージの配置時に構成ファイルの変数の値を更新できます。 実行時に、パッケージは更新された変数の値を使用します。 詳細については、「 [パッケージ構成を作成する](../integration-services/packages/create-package-configurations.md)」を参照してください。  

## <a name="related-tasks"></a>Related Tasks  
 [子パッケージでの変数およびパラメーターの値の使用](../integration-services/packages/legacy-package-deployment-ssis.md#child)  
  
 [クエリ パラメーターをデータ フロー コンポーネントの変数にマップする](../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
