---
title: パッケージで変数を使用する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined variables [Integration Services]
- variables [Integration Services], use scenarios
- system variables [Integration Services]
ms.assetid: 7742e92d-46c5-4cc4-b9a3-45b688ddb787
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96bfbf87789aa1d683b6368f210539a191f7ee95
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054689"
---
# <a name="use-variables-in-packages"></a>パッケージで変数を使用する
  変数は、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージに追加できる便利で柔軟な機能です。変数を使用すると、パッケージのオブジェクト間、および親パッケージと子パッケージとの間で情報を交換できます。 また、変数は式やスクリプトでも使用できます。  
  
## <a name="user-defined-variables-and-system-variables"></a>ユーザー定義変数とシステム変数  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ではシステム変数が用意されているほか、ユーザー定義変数をサポートします。 新しいパッケージを作成した場合、コンテナーやタスクをパッケージに追加した場合、またはイベント ハンドラーを作成した場合、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] によってコンテナーに一連のシステム変数が追加されます。 システム変数には、パッケージ、コンテナー、タスク、またはイベント ハンドラーに関する有益な情報が含まれています。 たとえば、パッケージの実行時に、 **MachineName** システム変数にはパッケージを実行しているコンピューターの名前が含まれ、 **StartTime** にはパッケージの実行が開始された時刻が含まれます。 システム変数は読み取り専用です。 詳細については、「 [システム変数](system-variables.md)」を参照してください。  
  
 ユーザー定義変数を作成して、パッケージで使用できます。 ユーザー定義変数は、 [!INCLUDE[ssIS](../includes/ssis-md.md)]の優先順位制約、For ループ コンテナー、派生列変換、および条件分割変換で使用される式、スクリプト、およびプロパティの値を更新するプロパティ式など、多くの方法で使用できます。  
  
 たとえば、For ループ コンテナーの評価条件でユーザー定義変数を使用できます。 また、Foreach ループ コンテナーの列挙子コレクション値を変数にマップしたり、SQL 実行タスクがパラメーター化された SQL ステートメントを使用する場合にステートメントのパラメーターを変数にマップしたりできます。 詳細については、「 [Integration Services &#40;SSIS&#41; の変数](integration-services-ssis-variables.md)」を参照してください。  
  
## <a name="variables-usage-scenarios"></a>変数の使用法のシナリオ  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージでは、変数をさまざまな方法で使用します。 パッケージにユーザー定義変数を追加して、ソリューションに必要な柔軟性と管理性を実装しないと、パッケージ開発があまり進まない場合もあります。 シナリオによっては、システム変数もよく使用します。  
  
 **プロパティの式** パッケージおよびパッケージ オブジェクトのプロパティを設定するプロパティ式に値を提供するために、変数を使用します。 たとえば、式 `SELECT * FROM @varTableName` に含まれている変数 `varTableName` は、SQL 実行タスクによって実行される SQL ステートメントを更新します。 式 `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`では、 `varPackageFirst` 変数で指定されたパッケージを月の最初の日に実行し、 `varPackageOther` 変数で指定されたパッケージを別の日に実行することにより、[パッケージの実行] タスクで実行されるパッケージを更新しています。 詳細については、「 [パッケージでプロパティ式を使用する](expressions/use-property-expressions-in-packages.md)」を参照してください。  
  
 **データ フロー式** 変数を使用して、派生列変換と条件分割変換で列に値を設定するための式や、データ行を各種の変換出力に送るための式に値を提供します。 たとえば、式 `@varSalutation + LastName`は、 `VarSalutation` 変数の値と `LastName` 列を連結します。 式 `Income < @HighIncome` は、`Income` 列の値が `HighIncome` 変数の値よりも小さいデータ行を出力に送信します。 詳細については、「[派生列変換](data-flow/transformations/derived-column-transformation.md)」、「[条件分割変換](data-flow/transformations/conditional-split-transformation.md)」、および「[Integration Services (SSIS) の式](expressions/integration-services-ssis-expressions.md)」を参照してください。  
  
 **優先順位制約の式** 優先順位制約で制約付き実行可能ファイルを実行するかどうかを決定するために使用する値を提供します。 これらの式は、実行結果 (成功、失敗、完了) と組み合わせて使用することも、実行結果の代わりに使用することもできます。 たとえば、式 `@varMax > @varMin` が `true` に評価される場合、実行可能ファイルは実行されます。 詳細については、「 [優先順位制約に式を追加する](control-flow/precedence-constraints.md)」を参照してください。  
  
 **パラメーターおよびリターン コード** 入力パラメーターに値を提供したり、出力パラメーターおよびリターン コードの値を格納したりします。 そのためには、変数をパラメーターおよび戻り値にマップします。 たとえば、変数 `varProductId` を 23 に設定して SQL ステートメント `SELECT * from Production.Product WHERE ProductID = ?`を実行すると、 `ProductID` が 23 である製品が取得されます。 詳細については、「 [SQL 実行タスク](control-flow/execute-sql-task.md) 」と「 [SQL 実行タスクのパラメーターとリターン コード](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)」を参照してください。  
  
 **For ループ式** For ループの初期化式、評価式、および代入式で使用する値を提供します。 たとえば、変数 `varCount` が 2、変数 `varMaxCount` が 10、初期化式が `@varCount`、評価式が  `@varCount < @varMaxCount`、代入式が `@varCount =@varCount +1`の場合、ループは 8 回繰り返されます。 詳細については、「 [For ループ コンテナー](control-flow/for-loop-container.md)」を参照してください。  
  
 **親パッケージ変数の構成** 親パッケージから子パッケージに値を渡します。 子パッケージは、親パッケージ変数の構成を使用することにより、親パッケージの変数にアクセスできます。 たとえば、子パッケージが親パッケージと同じ日付を使用する必要がある場合、子パッケージは親パッケージの GETDATE 関数によって設定される変数を指定する親パッケージ変数の構成を定義できます。 詳細については、「 [パッケージ実行タスク](control-flow/execute-package-task.md) 」と「 [パッケージ構成](../../2014/integration-services/package-configurations.md)」を参照してください。  
  
 **スクリプト タスクおよびスクリプト コンポーネント** 読み取り専用変数および読み取り/書き込み変数の一覧をスクリプト タスクまたはスクリプト コンポーネントに提供し、スクリプト内の読み取り/書き込み変数を更新して、更新された値をスクリプトの内外で使用します。 たとえば、コード `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`では、スクリプト変数 `numberOfCars` が変数 `NumberOfCars`の値によって更新されます。 詳細については、「 [スクリプト タスクでの変数の使用](control-flow/script-task.md)」を参照してください。  
  
## <a name="configurations-and-variables"></a>構成と変数  
 変数を動的に更新するために、変数の構成を作成し、パッケージと共に構成を配置して、パッケージの配置時に構成ファイルの変数の値を更新できます。 実行時に、パッケージは更新された変数の値を使用します。 詳細については、「 [パッケージ構成を作成する](../../2014/integration-services/create-package-configurations.md)」を参照してください。  
  
### <a name="to-add-modify-and-delete-user-defined-variables"></a>ユーザー定義変数を追加、修正、および削除するには  
  
-   [パッケージ内のユーザー定義変数のスコープの追加、削除、変更](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
-   [ユーザー定義変数のプロパティを設定する](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
  
