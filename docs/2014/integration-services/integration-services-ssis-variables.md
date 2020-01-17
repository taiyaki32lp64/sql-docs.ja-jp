---
title: Integration Services (SSIS) の変数 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b824129d1687dce8471800f79d106328b9ee36f6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62892281"
---
# <a name="integration-services-ssis-variables"></a>Integration Services (SSIS) の変数
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
  
 変数 (システム変数とユーザー定義変数) はすべて、SQL 実行タスクが使用するパラメーター バインドで使用して、SQL ステートメントのパラメーターに変数をマップできます。 詳細については、「 [SQL 実行タスク](control-flow/execute-sql-task.md) 」と「 [SQL 実行タスクのパラメーターとリターン コード](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)」を参照してください。  
  
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
  
 コンテナーの種類ごとに、異なるセットのシステム変数を使用できます。 パッケージとパッケージ要素が使用するシステム変数の詳細については、「[システム変数](system-variables.md)」を参照してください。  
  
 変数の実際的な使用シナリオの詳細については、「[パッケージで変数を使用する](../../2014/integration-services/use-variables-in-packages.md)」を参照してください。  
  
## <a name="variable-properties"></a>変数のプロパティ  
 **[変数]** ウィンドウまたは **[プロパティ]** ウィンドウで、次のプロパティを設定してユーザー定義変数を構成できます。 一部のプロパティは [プロパティ] ウィンドウでのみ使用できます。  
  
> [!NOTE]  
>  システム変数で構成可能なオプションは、変数値が変更されたときにイベントを起動するかどうかを指定するオプションのみです。  
  
 説明  
 変数の説明を指定します。  
  
 EvaluateAsExpression  
 プロパティを設定すると`True`、指定された式を使用して変数の値を設定します。  
  
 式  
 変数に割り当てられる式を指定します。  
  
 名前  
 変数名を指定します。  
  
 Namespace  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] には、**User** および **System** という 2 つの名前空間が用意されています。 既定では、カスタム変数は **User** 名前空間に属し、システム変数は **System** 名前空間に属します。 ユーザー定義変数用に追加の名前空間を作成し、**User** 名前空間の名前を変更することはできますが、**System** 名前空間の名前を変更したり、変数を **System** 名前空間に追加したり、システム変数を別の名前空間に割り当てたりすることはできません。  
  
 RaiseChangedEvent  
 このプロパティを `True` に設定すると、変数の値が変更された場合に `OnVariableValueChanged` イベントが発生します。  
  
 ReadOnly  
 このプロパティを `False` に設定すると、変数は読み取り/書き込み用となります。  
  
 スコープ  
 > [!NOTE]  
>  **[変数]** ウィンドウの **[変数の移動]** をクリックすることによってしか、このプロパティの設定は変更できません。  
  
 変数は、パッケージのスコープ内、またはパッケージ内のコンテナー、タスク、またはイベント ハンドラーのスコープ内で作成されます。 パッケージ コンテナーは、コンテナー階層の最上層にあるため、パッケージ スコープを持つ変数はグローバル変数と同じように機能し、パッケージ内のすべてのコンテナーで使用できます。 同様に、For ループ コンテナーなどのコンテナーのスコープ内で定義された変数は、For ループ コンテナー内のすべてのタスクまたはコンテナーで使用できます。  
  
 パッケージでパッケージ実行タスクを使用して他のパッケージを実行する場合、呼び出し元のパッケージのスコープまたはパッケージ実行タスクで定義された変数は、構成の種類で親パッケージ変数を使用することにより、呼び出し先のパッケージで使用できます。 詳細については、「 [パッケージ構成](../../2014/integration-services/package-configurations.md)」を参照してください。  
  
 [IncludeInDebugDump]  
 変数値がデバッグ ダンプ ファイルに含まれるかどうかを示します。  
  
 ユーザー定義変数とシステム変数は、既定の値を **[inclueindebugdump]** オプションは`true`します。  
  
 ただし、ユーザー定義変数の場合、システムがリセットされ、 **IncludeInDebugDump**オプションを`false`次の条件が満たされたとき。  
  
-   場合、 **EvaluateAsExpression**変数のプロパティに設定されて`true`、リセット、 **IncludeInDebugDump**オプションを`false`。  
  
     変数の値として式のテキストをデバッグ ダンプ ファイルに含めるには、設定、 **IncludeInDebugDump**オプションを`true`します。  
  
-   変数のデータ型を文字列に変更する場合、システムがリセット、 **IncludeInDebugDump**オプションを`false`します。  
  
 システムをリセットすると、 **IncludeInDebugDump**オプションを`false`、このユーザーが選択した値をオーバーライドする可能性があります。  
  
 値  
 ユーザー定義変数の値には、リテラルまたは式を設定できます。 変数には、変数値および変数のデータ型を設定するオプションが含まれています。 この 2 つのプロパティには互換性が必要です。たとえば、文字列の値を整数データ型に使用することはできません。  
  
 変数を式として評価するように構成した場合は、式を指定する必要があります。 式は実行時に評価され、変数は評価結果に設定されます。 たとえば、変数が式 `DATEPART("month", GETDATE())` を使用している場合、変数の値は、現在の日付の月と等しい数値になります。 式は、 [!INCLUDE[ssIS](../includes/ssis-md.md)] 式の構文文法を使用する、有効な式である必要があります。 変数に式を使用する場合、リテラルおよび式文法が提供する演算子と関数も使用できますが、パッケージ内のデータ フローの列は参照できません。 式の最大長は 4,000 文字です。 詳細については、「 [Integration Services (SSIS) 式](expressions/integration-services-ssis-expressions.md)に評価されるまでそのワークフローを繰り返します。  
  
 ValueType  
 > [!NOTE]  
>  このプロパティの値は **[変数]** ウィンドウの **[データ型]** 列に表示されます。  
  
 変数の値のデータ型を指定します。  
  
## <a name="configuring-variables"></a>変数の構成  
 プロパティを設定するには [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、「 [[変数] ウィンドウ](../../2014/integration-services/variables-window.md)」を参照してください。  
  
 変数のプロパティ、およびプログラムによるこれらのプロパティの設定方法の詳細については、「<xref:Microsoft.SqlServer.Dts.Runtime.Variable>」を参照してください。  
  
## <a name="related-tasks"></a>Related Tasks  
 [パッケージ内のユーザー定義変数のスコープの追加、削除、変更](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
 [ユーザー定義変数のプロパティを設定する](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
 [子パッケージでの変数およびパラメーターの値の使用](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
 [クエリ パラメーターをデータ フロー コンポーネントの変数にマップする](data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
  
