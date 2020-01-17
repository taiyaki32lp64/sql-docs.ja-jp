---
title: チュートリアル:配置計画を変更するためのデータベース プロジェクトの配置の拡張 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 22b077b1-fa25-49ff-94f6-6d0d196d870a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d683bc743fe621b35cdc59588ce04f6ee96c5bbe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068976"
---
# <a name="walkthrough-extend-database-project-deployment-to-modify-the-deployment-plan"></a>チュートリアル:配置計画を変更するためにデータベース プロジェクトの配置を拡張する
配置コントリビューターを作成して、SQL プロジェクトの配置時にカスタム アクションを実行できます。 [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) または [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) を作成できます。 計画の実行前に計画を変更する場合は [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) を使用し、計画の実行中に操作を実行する場合は [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) を使用します。 このチュートリアルでは、SqlRestartableScriptContributor という名前の [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) を作成して、配置スクリプトのバッチに IF ステートメントを追加し、実行中にエラーが発生した場合は完了するまでスクリプトを再実行できるようにします。  
  
このチュートリアルでは、次の主なタスクを行います。  
  
-   [DeploymentPlanModifier 型の配置コントリビューターを作成する](#CreateDeploymentContributor)  
  
-   [配置コントリビューターをインストールする](#InstallDeploymentContributor)  
  
-   [配置コントリビューターを実行またはテストする](#TestDeploymentContributor)  
  
## <a name="prerequisites"></a>Prerequisites  
このチュートリアルを実行するには、次のコンポーネントが必要です。  
  
-   C# または VB の開発をサポートする、SQL Server Data Tools を含む Visual Studio のバージョンがインストールされていること。  
  
-   SQL オブジェクトを含む SQL プロジェクト。  
  
-   データベース プロジェクトを配置できる SQL Server のインスタンス。  
  
> [!NOTE]  
> このチュートリアルは、既に SQL Server Data Tools の SQL 機能を使い慣れているユーザーを対象としています。 また、クラス ライブラリの作成方法、コード エディターを使用してクラスにコードを追加する方法など、Visual Studio の基本的な概念を理解している必要があります。  
  
## <a name="CreateDeploymentContributor"></a>配置コントリビューターの作成  
配置コントリビューターを作成するには、次のタスクを実行する必要があります。  
  
-   クラス ライブラリ プロジェクトを作成し、必要な参照を追加する。  
  
-   [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) から継承する SqlRestartableScriptContributor という名前のクラスを定義する。  
  
-   [OnExecute](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributor.onexecute.aspx) メソッドをオーバーライドする。  
  
-   プライベート ヘルパー メソッドを追加する。  
  
-   結果として得られるアセンブリをビルドする。  
  
#### <a name="to-create-a-class-library-project"></a>クラス ライブラリ プロジェクトを作成するには  
  
1.  MyOtherDeploymentContributor という名前の Visual C# または Visual Basic クラス ライブラリ プロジェクトを作成します。  
  
2.  "Class1.cs" ファイルの名前を "SqlRestartableScriptContributor.cs" に変更します。  
  
3.  ソリューション エクスプローラーで、プロジェクト ノードを右クリックし、 **[参照の追加]** をクリックします。  
  
4.  [フレームワーク] タブで **System.ComponentModel.Composition** を選択します。  
  
5.  **[参照]** をクリックし、**C:\Program Files (x86)\Microsoft SQL Server\110\SDK\Assemblies** ディレクトリに移動して、**Microsoft.SqlServer.TransactSql.ScriptDom.dll** を選択します。次に、 **[OK]** をクリックします。  
  
6.  必要な SQL 参照を追加します。この操作を行うには、プロジェクト ノードを右クリックし、 **[参照の追加]** をクリックします。 **[参照]** をクリックし、**C:\Program Files (x86)\Microsoft SQL Server\110\DAC\Bin** フォルダーに移動します。 **Microsoft.SqlServer.Dac.dll**、**Microsoft.SqlServer.Dac.Extensions.dll**、および **Microsoft.Data.Tools.Schema.Sql.dll** の各エントリを選択し、 **[追加]** 、 **[OK]** の順にクリックします。  
  
次に、コードをクラスに追加します。  
  
#### <a name="to-define-the-sqlrestartablescriptcontributor-class"></a>SqlRestartableScriptContributor クラスを定義するには  
  
1.  コード エディターで、次の **using** ステートメントに一致するように、class1.cs ファイルを更新します。  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.Globalization;  
    using System.Text;  
    using Microsoft.SqlServer.Dac.Deployment;  
    using Microsoft.SqlServer.Dac.Model;  
    using Microsoft.SqlServer.TransactSql.ScriptDom;  
    ```  
  
2.  クラス定義を次の例に一致するように更新します。  
  
    ```csharp  
        /// <summary>  
    /// This deployment contributor modifies a deployment plan by adding if statements  
    /// to the existing batches in order to make a deployment script able to be rerun to completion  
    /// if an error is encountered during execution  
    /// </summary>  
    [ExportDeploymentPlanModifier("MyOtherDeploymentContributor.RestartableScriptContributor", "1.0.0.0")]  
    public class SqlRestartableScriptContributor : DeploymentPlanModifier  
    {  
    }  
  
    ```  
  
    これで、[DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) から継承する配置コントリビューターの定義が完了しました。 ビルドおよび配置プロセス中に、カスタム コントリビューターは標準の拡張機能ディレクトリから読み込まれます。 配置計画を変更するコントリビューターは、[ExportDeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.exportdeploymentplanmodifierattribute.aspx) 属性によって識別されます。 コントリビューターを検出できるようにするためにこの属性は必須です。 この属性は次のようになります。  
  
    ```csharp  
    [ExportDeploymentPlanModifier("MyOtherDeploymentContributor.RestartableScriptContributor", "1.0.0.0")]  
  
    ```  
  
3.  次のメンバー宣言を追加します。  
  
    ```vb  
         private const string BatchIdColumnName = "BatchId";  
            private const string DescriptionColumnName = "Description";  
  
            private const string CompletedBatchesVariableName = "CompletedBatches";  
            private const string CompletedBatchesVariable = "$(CompletedBatches)";  
            private const string CompletedBatchesSqlCmd = @":setvar " + CompletedBatchesVariableName + " __completedBatches_{0}_{1}";  
            private const string TotalBatchCountSqlCmd = @":setvar TotalBatchCount {0}";  
            private const string CreateCompletedBatchesTable = @"  
    if OBJECT_ID(N'tempdb.dbo." + CompletedBatchesVariable + @"', N'U') is null  
    begin  
    use tempdb  
    create table [dbo].[$(CompletedBatches)]  
    (  
    BatchId int primary key,  
    Description nvarchar(300)  
    )  
    use [$(DatabaseName)]  
    end  
    ";  
  
    ```  
  
    次に、OnExecute メソッドをオーバーライドして、データベース プロジェクトの配置時に実行するコードを追加します。  
  
#### <a name="to-override-onexecute"></a>OnExecute をオーバーライドするには  
  
1.  SqlRestartableScriptContributor クラスに次のメソッドを追加します。  
  
    ```csharp  
    /// <summary>  
    /// You override the OnExecute method to do the real work of the contributor.  
    /// </summary>  
    /// <param name="context"></param>  
    protected override void OnExecute(DeploymentPlanContributorContext context)  
    {  
         // Replace this with the method body  
    }  
  
    ```  
  
    [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) と [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) 両方の基本クラスである [DeploymentPlanContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributor.aspx) から [OnExecute](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributor.onexecute.aspx) メソッドをオーバーライドします。 この OnExecute メソッドに、[DeploymentPlanContributorContext](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributorcontext.aspx) オブジェクトが渡され、指定されたすべての引数、ソースとターゲットのデータベース モデル、配置計画、および配置オプションにアクセスできるようになります。 この例では、配置計画とターゲット データベース名を取得します。  
  
2.  次に、OnExecute メソッドに本体の最初の部分を追加します。  
  
    ```vb  
    // Obtain the first step in the Plan from the provided context  
    DeploymentStep nextStep = context.PlanHandle.Head;  
    int batchId = 0;  
    BeginPreDeploymentScriptStep beforePreDeploy = null;  
  
    // Loop through all steps in the deployment plan  
    while (nextStep != null)  
    {  
        // Increment the step pointer, saving both the current and next steps  
        DeploymentStep currentStep = nextStep;  
        nextStep = currentStep.Next;  
  
        // Add additional step processing here  
    }  
  
    // if we found steps that required processing, set up a temporary table to track the work that you are doing  
    if (beforePreDeploy != null)  
    {  
        // Add additional post-processing here  
    }  
  
    // Cleanup and drop the table   
    DeploymentScriptStep dropStep = new DeploymentScriptStep(DropCompletedBatchesTable);  
    base.AddAfter(context.PlanHandle, context.PlanHandle.Tail, dropStep);  
  
    ```  
  
    このコードでは、いくつかのローカル変数を定義し、配置計画のすべてのステップの処理を実行するループを設定します。 ループの完了後、後処理を実行する必要があります。その後、計画実行の進行状況を追跡するために配置中に作成した一時テーブルを削除します。 ここで重要な型は、[DeploymentStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentstep.aspx) と [DeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptstep.aspx) です。 重要なメソッドは AddAfter です。  
  
3.  次に、"Add additional step processing here" というコメントを次のコードで置き換えて、ステップ処理を追加します。  
  
    ```csharp  
    // Look for steps that mark the pre/post deployment scripts  
    // These steps will always be in the deployment plan even if the  
    // user's project does not have a pre/post deployment script  
    if (currentStep is BeginPreDeploymentScriptStep)  
    {  
        // This step marks the beginning of the predeployment script.  
        // Save the step and move on.  
        beforePreDeploy = (BeginPreDeploymentScriptStep)currentStep;  
        continue;  
    }  
    if (currentStep is BeginPostDeploymentScriptStep)  
    {  
        // This is the step that marks the beginning of the post deployment script.    
        // We do not continue processing after this point.  
        break;  
    }  
    if (currentStep is SqlPrintStep)  
    {  
        // We do not need to put if statements around these  
        continue;  
    }  
  
    // if we have not yet found the beginning of the pre-deployment script steps,   
    // skip to the next step.  
    if (beforePreDeploy == null)  
    {  
        // We only surround the "main" statement block with conditional  
        // statements  
        continue;  
    }  
  
    // Determine if this is a step that we need to surround with a conditional statement  
    DeploymentScriptDomStep domStep = currentStep as DeploymentScriptDomStep;  
    if (domStep == null)  
    {  
        // This step is not a step that we know how to modify,  
        // so skip to the next step.  
        continue;  
    }  
  
    TSqlScript script = domStep.Script as TSqlScript;  
    if (script == null)  
    {  
        // The script dom step does not have a script with batches - skip  
        continue;  
    }  
  
        // Loop through all the batches in the script for this step.  All the statements  
        // in the batch will be enclosed in an if statement that will check the  
        // table to ensure that the batch has not already been executed  
        TSqlObject sqlObject;  
        string stepDescription;  
        GetStepInfo(domStep, out stepDescription, out sqlObject);  
        int batchCount = script.Batches.Count;  
  
    for (int batchIndex = 0; batchIndex < batchCount; batchIndex++)  
    {  
        // Add batch processing here  
    }  
  
    ```  
  
    コードのコメントは処理の説明です。 簡単に説明すると、このコードは、目的のステップを検索するため、他のステップをスキップして、配置後のステップの先頭に到達すると停止します。 条件付きで囲む必要があるステートメントがステップに含まれている場合は、追加の処理を実行します。 重要な型、メソッド、プロパティには次のようなものがあります。[BeginPreDeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.beginpredeploymentscriptstep.aspx)、[BeginPostDeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.beginpostdeploymentscriptstep.aspx)、[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)、[TSqlScript](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlscript.aspx)、Script、[DeploymentScriptDomStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptdomstep.aspx)、[SqlPrintStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqlprintstep.aspx)。  
  
4.  次に、"Add batch processing here" というコメントを次のように置き換えて、バッチ処理コードを追加します。  
  
    ```csharp  
        // Create the if statement that will contain the batch's contents  
        IfStatement ifBatchNotExecutedStatement = CreateIfNotExecutedStatement(batchId);  
        BeginEndBlockStatement statementBlock = new BeginEndBlockStatement();  
        ifBatchNotExecutedStatement.ThenStatement = statementBlock;  
        statementBlock.StatementList = new StatementList();  
  
        TSqlBatch batch = script.Batches[batchIndex];  
        int statementCount = batch.Statements.Count;  
  
        // Loop through all statements in the batch, embedding those in an sp_execsql  
        // statement that must be handled this way (schemas, stored procedures,   
        // views, functions, and triggers).  
        for (int statementIndex = 0; statementIndex < statementCount; statementIndex++)  
        {  
            // Add additional statement processing here  
        }  
  
        // Add an insert statement to track that all the statements in this  
        // batch were executed.  Turn on nocount to improve performance by  
        // avoiding row inserted messages from the server  
        string batchDescription = string.Format(CultureInfo.InvariantCulture,  
            "{0} batch {1}", stepDescription, batchIndex);  
  
        PredicateSetStatement noCountOff = new PredicateSetStatement();  
        noCountOff.IsOn = false;  
        noCountOff.Options = SetOptions.NoCount;  
  
        PredicateSetStatement noCountOn = new PredicateSetStatement();  
        noCountOn.IsOn = true;  
        noCountOn.Options = SetOptions.NoCount;   
        InsertStatement batchCompleteInsert = CreateBatchCompleteInsert(batchId, batchDescription);  
        statementBlock.StatementList.Statements.Add(noCountOn);  
    statementBlock.StatementList.Statements.Add(batchCompleteInsert);  
        statementBlock.StatementList.Statements.Add(noCountOff);  
  
        // Remove all the statements from the batch (they are now in the if block) and add the if statement  
        // as the sole statement in the batch  
        batch.Statements.Clear();  
        batch.Statements.Add(ifBatchNotExecutedStatement);  
  
        // Next batch  
        batchId++;  
  
    ```  
  
    このコードによって、IF ステートメントが BEGIN/END ブロックと共に作成されます。 次に、バッチ内のステートメントに対して追加の処理を実行します。 この処理が終わったら、INSERT ステートメントを追加して、スクリプト実行の進行状況を追跡する一時テーブルに情報を追加します。 最後に、バッチを更新し、バッチ内のステートメントを、そのステートメントを含む新しい IF ステートメントに置き換えます。重要な型、メソッド、プロパティは、[IfStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.ifstatement.aspx)、[BeginEndBlockStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.beginendblockstatement.aspx)、[StatementList](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.statementlist.aspx)、[TSqlBatch](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlbatch.aspx)、[PredicateSetStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.predicatesetstatement.aspx)、[SetOptions](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.setoptions.aspx)、[InsertStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.insertstatement.aspx) です。  
  
5.  ステートメント処理ループの本体を追加します。 "Add additional statement processing here" というコメントを次のコードで置き換えます。  
  
    ```csharp  
    TSqlStatement smnt = batch.Statements[statementIndex];  
  
    if (IsStatementEscaped(sqlObject))  
    {  
        // "escape" this statement by embedding it in a sp_executesql statement  
        string statementScript;  
        domStep.ScriptGenerator.GenerateScript(smnt, out statementScript);  
        ExecuteStatement spExecuteSql = CreateExecuteSql(statementScript);  
        smnt = spExecuteSql;  
    }  
  
    statementBlock.StatementList.Statements.Add(smnt);  
  
    ```  
  
    バッチ内の各ステートメントについて、そのステートメントの型を sp_executesql ステートメントでラップする必要がある場合は、ステートメントを適宜変更します。 その後、コードによって、作成した BEGIN/END ブロックのステートメント リストにそのステートメントが追加されます。 重要な型、メソッド、およびプロパティは、[TSqlStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlstatement.aspx) および [ExecuteStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executestatement.aspx) です。  
  
6.  最後に、"Add additional post-processing here" というコメントを次のコードで置き換えて、後処理セクションを追加します。  
  
    ```csharp  
    // Declare a SqlCmd variables.  
    //  
    // CompletedBatches variable - defines the name of the table in tempdb that will track  
    // all the completed batches.  The temporary table's name has the target database name and  
    // a guid embedded in it so that:  
    // * Multiple deployment scripts targeting different DBs on the same server  
    // * Failed deployments with old tables do not conflict with more recent deployments  
    //  
    // TotalBatchCount variable - the total number of batches surrounded by if statements.  Using this  
    // variable pre/post deployment scripts can also use the CompletedBatches table to make their  
    // script rerunnable if there is an error during execution  
    StringBuilder sqlcmdVars = new StringBuilder();  
    sqlcmdVars.AppendFormat(CultureInfo.InvariantCulture, CompletedBatchesSqlCmd,  
        context.Options.TargetDatabaseName, Guid.NewGuid().ToString("D"));  
    sqlcmdVars.AppendLine();  
    sqlcmdVars.AppendFormat(CultureInfo.InvariantCulture, TotalBatchCountSqlCmd, batchId);  
  
    DeploymentScriptStep completedBatchesSetVarStep = new DeploymentScriptStep(sqlcmdVars.ToString());  
    base.AddBefore(context.PlanHandle, beforePreDeploy, completedBatchesSetVarStep);  
  
    // Create the temporary table we will use to track the work that we are doing  
    DeploymentScriptStep createStatusTableStep = new DeploymentScriptStep(CreateCompletedBatchesTable);  
    base.AddBefore(context.PlanHandle, beforePreDeploy, createStatusTableStep);  
  
    ```  
  
    条件付きステートメントで囲んだステップが 1 つ以上見つかった場合は、配置スクリプトにステートメントを追加して SQLCMD 変数を定義する必要があります。 最初の CompletedBatches 変数には、スクリプト実行時に正常に完了したバッチを追跡するために配置スクリプトで使用する一時テーブルの一意の名前が格納されます。 2 番目の TotalBatchCount 変数には、配置スクリプト内のバッチの総数が格納されます。  
  
    その他の重要な型、プロパティ、およびメソッドは次のとおりです。  
  
    StringBuilder、[DeploymentScriptStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptstep.aspx)、AddBefore。  
  
    次に、このメソッドによって呼び出されるヘルパー メソッドを定義します。  
  
#### <a name="to-add-the-helper-methods"></a>ヘルパー メソッドを追加するには  
  
-   多数のヘルパー メソッドを定義する必要があります。 重要なメソッドを次に示します。  
  
    |**方法**|**[説明]**|  
    |--------------|-------------------|  
    |CreateExecuteSQL|提供されたステートメントを EXEC sp_executesql ステートメントで囲むように CreateExecuteSQL メソッドを定義します。 重要な型、メソッド、プロパティには次のようなものがあります。[ExecuteStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executestatement.aspx)、[ExecutableProcedureReference](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executableprocedurereference.aspx)、[SchemaObjectName](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.schemaobjectname.aspx)、[ProcedureReference](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.procedurereference.aspx)、[ExecuteParameter](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.executeparameter.aspx)。|  
    |CreateCompletedBatchesName|CreateCompletedBatchesName メソッドを定義します。 このメソッドによって、バッチの一時テーブルに挿入される名前が作成されます。重要な型、メソッド、プロパティには次のようなものがあります。[SchemaObjectName](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.schemaobjectname.aspx)。|  
    |IsStatementEscaped|IsStatementEscaped メソッドを定義します。 このメソッドは、モデル要素の型のステートメントを IF ステートメントで囲む前に EXEC sp_executesql ステートメントでラップする必要があるかどうかを判断します。 重要な型、メソッド、プロパティには次のようなものがあります。次のモデルの種類の TSqlObject.ObjectType、ModelTypeClass、TypeClass プロパティ。Schema、Procedure、View、TableValuedFunction、ScalarFunction、DatabaseDdlTrigger、DmlTrigger、ServerDdlTrigger。|  
    |CreateBatchCompleteInsert|CreateBatchCompleteInsert メソッドを定義します。 このメソッドは、スクリプト実行の進行状況を追跡するために配置スクリプトに追加される INSERT ステートメントを作成します。 重要な型、メソッド、プロパティには次のようなものがあります。InsertStatement、NamedTableReference、ColumnReferenceExpression、ValuesInsertSource、RowValue。|  
    |CreateIfNotExecutedStatement|CreateIfNotExecutedStatement メソッドを定義します。 このメソッドは、現在のバッチが既に実行されているかどうかを調べるために一時的なバッチ実行テーブルを確認する IF ステートメントを生成します。 重要な型、メソッド、プロパティには次のようなものがあります。IfStatement、ExistsPredicate、ScalarSubquery、NamedTableReference、WhereClause、ColumnReferenceExpression、IntegerLiteral、BooleanComparisonExpression、BooleanNotExpression。|  
    |GetStepInfo|GetStepInfo メソッドを定義します。 このメソッドは、ステップ名に加え、ステップのスクリプトを作成するために使用されたモデル要素に関する情報を抽出します。 重要な型およびメソッドには、次のようなものがあります。[DeploymentPlanContributorContext](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributorcontext.aspx)、[DeploymentScriptDomStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentscriptdomstep.aspx)、[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)、[CreateElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.createelementstep.aspx)、[AlterElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.alterelementstep.aspx)、[DropElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.dropelementstep.aspx)。|  
    |GetElementName|TSqlObject の書式設定された名前を作成します。|  
  
1.  次のコードを追加して、ヘルパー メソッドを定義します。  
  
    ```csharp  
  
    /// <summary>  
    /// The CreateExecuteSql method "wraps" the provided statement script in an "sp_executesql" statement  
    /// Examples of statements that must be so wrapped include: stored procedures, views, and functions  
    /// </summary>  
    private static ExecuteStatement CreateExecuteSql(string statementScript)  
    {  
        // define a new Exec statement  
        ExecuteStatement executeSp = new ExecuteStatement();  
        ExecutableProcedureReference spExecute = new ExecutableProcedureReference();  
        executeSp.ExecuteSpecification = new ExecuteSpecification { ExecutableEntity = spExecute };  
  
        // define the name of the procedure that you want to execute, in this case sp_executesql  
        SchemaObjectName procName = new SchemaObjectName();  
        procName.Identifiers.Add(CreateIdentifier("sp_executesql", QuoteType.NotQuoted));  
        ProcedureReference procRef = new ProcedureReference { Name = procName };  
  
        spExecute.ProcedureReference = new ProcedureReferenceName { ProcedureReference = procRef };  
  
        // add the script parameter, constructed from the provided statement script  
        ExecuteParameter scriptParam = new ExecuteParameter();  
        spExecute.Parameters.Add(scriptParam);  
        scriptParam.ParameterValue = new StringLiteral { Value = statementScript };  
        scriptParam.Variable = new VariableReference { Name = "@stmt" };  
        return executeSp;  
    }  
  
    /// <summary>  
    /// The CreateIdentifier method returns a Identifier with the specified value and quoting type  
    /// </summary>  
    private static Identifier CreateIdentifier(string value, QuoteType quoteType)  
    {  
        return new Identifier { Value = value, QuoteType = quoteType };  
    }  
  
    /// <summary>  
    /// The CreateCompletedBatchesName method creates the name that will be inserted  
    /// into the temporary table for a batch.  
    /// </summary>  
    private static SchemaObjectName CreateCompletedBatchesName()  
    {  
        SchemaObjectName name = new SchemaObjectName();  
        name.Identifiers.Add(CreateIdentifier("tempdb", QuoteType.SquareBracket));  
        name.Identifiers.Add(CreateIdentifier("dbo", QuoteType.SquareBracket));  
        name.Identifiers.Add(CreateIdentifier(CompletedBatchesVariable, QuoteType.SquareBracket));  
        return name;  
    }  
  
    /// <summary>  
    /// Helper method that determins whether the specified statement needs to  
    /// be escaped  
    /// </summary>  
    /// <param name="sqlObject"></param>  
    /// <returns></returns>  
    private static bool IsStatementEscaped(TSqlObject sqlObject)  
    {  
        HashSet<ModelTypeClass> escapedTypes = new HashSet<ModelTypeClass>  
        {  
            Schema.TypeClass,  
            Procedure.TypeClass,  
            View.TypeClass,  
            TableValuedFunction.TypeClass,  
            ScalarFunction.TypeClass,  
            DatabaseDdlTrigger.TypeClass,  
            DmlTrigger.TypeClass,  
            ServerDdlTrigger.TypeClass  
        };  
        return escapedTypes.Contains(sqlObject.ObjectType);  
    }  
  
    /// <summary>  
    /// Helper method that creates an INSERT statement to track a batch being completed  
    /// </summary>  
    /// <param name="batchId"></param>  
    /// <param name="batchDescription"></param>  
    /// <returns></returns>  
    private static InsertStatement CreateBatchCompleteInsert(int batchId, string batchDescription)  
    {  
        InsertStatement insert = new InsertStatement();  
        NamedTableReference batchesCompleted = new NamedTableReference();  
        insert.InsertSpecification = new InsertSpecification();  
        insert.InsertSpecification.Target = batchesCompleted;  
        batchesCompleted.SchemaObject = CreateCompletedBatchesName();  
  
        // Build the columns inserted into  
        ColumnReferenceExpression batchIdColumn = new ColumnReferenceExpression();  
        batchIdColumn.MultiPartIdentifier = new MultiPartIdentifier();  
        batchIdColumn.MultiPartIdentifier.Identifiers.Add(CreateIdentifier(BatchIdColumnName, QuoteType.NotQuoted));  
  
        ColumnReferenceExpression descriptionColumn = new ColumnReferenceExpression();  
        descriptionColumn.MultiPartIdentifier = new MultiPartIdentifier();  
        descriptionColumn.MultiPartIdentifier.Identifiers.Add(CreateIdentifier(DescriptionColumnName, QuoteType.NotQuoted));  
  
        insert.InsertSpecification.Columns.Add(batchIdColumn);  
        insert.InsertSpecification.Columns.Add(descriptionColumn);  
  
        // Build the values inserted  
        ValuesInsertSource valueSource = new ValuesInsertSource();  
        insert.InsertSpecification.InsertSource = valueSource;  
  
        RowValue values = new RowValue();  
        values.ColumnValues.Add(new IntegerLiteral { Value = batchId.ToString() });  
        values.ColumnValues.Add(new StringLiteral { Value = batchDescription });  
        valueSource.RowValues.Add(values);  
  
        return insert;  
    }  
  
    /// <summary>  
    /// This is a helper method that generates an if statement that checks the batches executed  
    /// table to see if the current batch has been executed.  The if statement will look like this  
    ///   
    /// if not exists(select 1 from [tempdb].[dbo].[$(CompletedBatches)]   
    ///                where BatchId = batchId)  
    /// begin  
    /// end  
    /// </summary>  
    /// <param name="batchId"></param>  
    /// <returns></returns>  
    private static IfStatement CreateIfNotExecutedStatement(int batchId)  
    {  
        // Create the exists/select statement  
        ExistsPredicate existsExp = new ExistsPredicate();  
        ScalarSubquery subQuery = new ScalarSubquery();  
        existsExp.Subquery = subQuery;  
  
        subQuery.QueryExpression = new QuerySpecification  
        {  
            SelectElements =  
            {  
                new SelectScalarExpression  { Expression = new IntegerLiteral { Value ="1" } }  
            },  
            FromClause = new FromClause  
            {  
                TableReferences =  
                    {  
                        new NamedTableReference() { SchemaObject = CreateCompletedBatchesName() }  
                    }  
            },  
            WhereClause = new WhereClause  
            {  
                SearchCondition = new BooleanComparisonExpression  
                {  
                    ComparisonType = BooleanComparisonType.Equals,  
                    FirstExpression = new ColumnReferenceExpression  
                    {  
                        MultiPartIdentifier = new MultiPartIdentifier  
                        {  
                            Identifiers = { CreateIdentifier(BatchIdColumnName, QuoteType.SquareBracket) }  
                        }  
                    },  
                    SecondExpression = new IntegerLiteral { Value = batchId.ToString() }  
                }  
            }  
        };  
  
        // Put together the rest of the statement  
        IfStatement ifNotExists = new IfStatement  
        {  
            Predicate = new BooleanNotExpression  
            {  
                Expression = existsExp  
            }  
        };  
  
        return ifNotExists;  
    }  
  
    /// <summary>  
    /// Helper method that generates a useful description of the step.  
    /// </summary>  
    private static void GetStepInfo(  
        DeploymentScriptDomStep domStep,  
        out string stepDescription,  
        out TSqlObject element)  
    {  
        element = null;  
  
        // figure out what type of step we've got, and retrieve  
        // either the source or target element.  
        if (domStep is CreateElementStep)  
        {  
            element = ((CreateElementStep)domStep).SourceElement;  
        }  
        else if (domStep is AlterElementStep)  
        {  
            element = ((AlterElementStep)domStep).SourceElement;  
        }  
        else if (domStep is DropElementStep)  
        {  
            element = ((DropElementStep)domStep).TargetElement;  
        }  
  
        // construct the step description by concatenating the type and the fully qualified  
        // name of the associated element.  
        string stepTypeName = domStep.GetType().Name;  
        if (element != null)  
        {  
            string elementName = GetElementName(element);  
  
            stepDescription = string.Format(CultureInfo.InvariantCulture, "{0} {1}",  
                stepTypeName, elementName);  
        }  
        else  
        {  
            // if the step has no associated element, just use the step type as the description  
            stepDescription = stepTypeName;  
        }  
    }  
  
    private static string GetElementName(TSqlObject element)  
    {  
        StringBuilder name = new StringBuilder();  
        if (element.Name.HasExternalParts)  
        {  
            foreach (string part in element.Name.ExternalParts)  
            {  
                if (name.Length > 0)  
                {  
                    name.Append('.');  
                }  
                name.AppendFormat("[{0}]", part);  
            }  
        }  
  
        foreach (string part in element.Name.Parts)  
        {  
            if (name.Length > 0)  
            {  
                name.Append('.');  
            }  
            name.AppendFormat("[{0}]", part);  
        }  
  
        return name.ToString();  
    }  
  
    ```  
  
2.  変更内容を SqlRestartableScriptContributor.cs に保存します。  
  
次に、クラス ライブラリをビルドします。  
  
#### <a name="to-sign-and-build-the-assembly"></a>アセンブリの署名とビルドを行うには  
  
1.  **[プロジェクト]** メニューの **[MyOtherDeploymentContributor のプロパティ]** をクリックします。  
  
2.  **[署名]** タブをクリックします。  
  
3.  **[アセンブリの署名]** をクリックします。  
  
4.  **[厳密な名前のキー ファイルを選択してください]** で **[<New>]** をクリックします。  
  
5.  **[厳密な名前キーの作成]** ダイアログ ボックスで、 **[キー ファイル]** に「 **MyRefKey**」と入力します。  
  
6.  (省略可能) 厳密な名前のキー ファイルにパスワードを指定できます。  
  
7.  **[OK]** をクリックします。  
  
8.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
9. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  
  
    次に、アセンブリをインストールし、SQL プロジェクトの配置時に読み込まれるようにします。  
  
## <a name="InstallDeploymentContributor"></a>配置コントリビューターのインストール  
配置コントリビューターをインストールするには、アセンブリおよび関連付けられた .pdb ファイルを Extensions フォルダーにコピーする必要があります。  
  
#### <a name="to-install-the-myotherdeploymentcontributor-assembly"></a>MyOtherDeploymentContributor アセンブリをインストールするには  
  
1.  次に、アセンブリ情報を Extensions ディレクトリにコピーします。 Visual Studio の起動時に、%Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions ディレクトリとサブディレクトリ内のすべての拡張機能が認識され、使用できるようになります。  
  
2.  **MyOtherDeploymentContributor.dll** アセンブリ ファイルを出力ディレクトリから %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions ディレクトリにコピーします。 既定では、コンパイル済みの .dll ファイルのパスは YourSolutionPath\YourProjectPath\bin\Debug または YourSolutionPath\YourProjectPath\bin\Release です。  
  
## <a name="TestDeploymentContributor"></a>配置コントリビューターの実行またはテスト  
配置コントリビューターを実行またはテストするには、次のタスクを実行する必要があります。  
  
-   ビルドする予定の .sqlproj ファイルにプロパティを追加する。  
  
-   MSBuild を使用し、適切なパラメーターを指定して、データベース プロジェクトを配置する。  
  
### <a name="add-properties-to-the-sql-project-sqlproj-file"></a>SQL プロジェクト (.sqlproj) ファイルにプロパティを追加するには  
実行するコントリビューターの ID を指定するには、必ず SQL プロジェクト ファイルを更新する必要があります。 これは、次の 2 つの方法のいずれかで行うことができます。  
  
1.  .sqlproj ファイルを手動で変更して、必要な引数を追加できます。 この方法を選択できるのは、コントリビューターで構成に必要なコントリビューター引数がない場合、または多数のプロジェクト間でビルド コントリビューターを再利用しない場合です。 このオプションを選択した場合は、.sqlproj ファイル内の最初の Import ノードの後に次のステートメントを追加します。  
  
    ```  
    <PropertyGroup>  
      <DeploymentContributors>  
        $(DeploymentContributors); MyOtherDeploymentContributor.RestartableScriptContributor  
      </DeploymentContributors>  
    </PropertyGroup>  
    ```  
  
2.  もう 1 つの方法では、必要なコントリビューター引数を含むターゲット ファイルを作成します。 この方法は、既定値が含まれるため、複数のプロジェクトに同じコントリビューターを使用していて、必要なコントリビューター引数がある場合に役立ちます。 この場合は、MSBuild 拡張機能のパスにターゲット ファイルを作成します。  
  
    1.  %Program Files%\MSBuild に移動します。  
  
    2.  ターゲット ファイルの保存先となる新しいフォルダー "MyContributors" を作成します。  
  
    3.  このディレクトリ内に新しいファイル "MyContributors.targets" を作成し、次のテキストを追加して、ファイルを保存します。  
  
        ```  
        <?xml version="1.0" encoding="utf-8"?>  
  
        <Project xmlns="https://schemas.microsoft.com/developer/msbuild/2003">  
          <PropertyGroup>  
            <DeploymentContributors>$(DeploymentContributors);MyOtherDeploymentContributor.RestartableScriptContributor</DeploymentContributors>  
          </PropertyGroup>  
        </Project>  
  
        ```  
  
    4.  コントリビューターを実行するプロジェクトの .sqlproj ファイル内で、\<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets" \/> ノードの後に次のステートメントを追加してターゲット ファイルをインポートします。  
  
        ```  
        <Import Project="$(MSBuildExtensionsPath)\MyContributors\MyContributors.targets " />  
  
        ```  
  
上記の方法のいずれかを実行すると、MSBuild を使用して、コマンド ライン ビルドのパラメーターを渡すことができます。  
  
> [!NOTE]  
> コントリビューター ID を指定するには、必ず "DeploymentContributors" プロパティを更新する必要があります。 この ID は、コントリビューター ソース ファイル内の "ExportDeploymentPlanModifier" 属性で使用されているのと同じ ID です。 これを指定しないと、プロジェクトのビルド時にコントリビューターが実行されません。 "ContributorArguments" プロパティは、コントリビューターの実行に必要な引数がある場合にのみ更新する必要があります。  
  
## <a name="deploy-the-database-project"></a>データベース プロジェクトの配置  
  
#### <a name="to-deploy-your-sql-project-and-generate-a-deployment-report"></a>SQL プロジェクトを配置して配置レポートを生成するには  
  
-   プロジェクトは、通常どおり Visual Studio 内で発行または配置できます。 SQL プロジェクトが含まれているソリューションを開き、プロジェクトの右クリックのショートカット メニューで [発行...] をクリックするか、LocalDB へのデバッグ配置を行うために F5 キーを使用するだけです。 この例では、[発行...] ダイアログを使用して配置スクリプトを生成します。  
  
    1.  Visual Studio を起動し、SQL プロジェクトが含まれているソリューションを開きます。  
  
    2.  ソリューション エクスプローラーでプロジェクトを右クリックし、 **[発行...]** をクリックします。  
  
    3.  発行先のサーバー名とデータベース名を設定します。  
  
    4.  ダイアログの下部にあるオプションから **[スクリプトの生成]** を選択します。 これにより、配置に使用できるスクリプトが生成されます。 このスクリプトを調べて、スクリプトを再開できるように IF ステートメントが追加されていることを確認します。  
  
    5.  結果として生成された配置スクリプトを調べます。 "配置前スクリプト テンプレート" というラベルの付いたセクションの直前に、次のような Transact-SQL 構文があります。  
  
        ```  
        :setvar CompletedBatches __completedBatches_CompareProjectDB_cd1e348a-8f92-44e0-9a96-d25d65900fca  
        :setvar TotalBatchCount 17  
        GO  
  
        if OBJECT_ID(N'tempdb.dbo.$(CompletedBatches)', N'U') is null  
        begin  
        use tempdb  
        create table [dbo].[$(CompletedBatches)]  
        (  
        BatchId int primary key,  
        Description nvarchar(300)  
        )  
        use [$(DatabaseName)]  
        end  
  
        ```  
  
        配置スクリプトの後半部分では、各バッチの周囲に、元のステートメントを囲む IF ステートメントがあります。 たとえば、CREATE SCHEMA ステートメントの場合は次のようなコードになります。  
  
        ```  
        IF NOT EXISTS (SELECT 1  
                       FROM   [tempdb].[dbo].[$(CompletedBatches)]  
                       WHERE  [BatchId] = 0)  
            BEGIN  
                EXECUTE sp_executesql @stmt = N'CREATE SCHEMA [Sales]  
            AUTHORIZATION [dbo]';  
                SET NOCOUNT ON;  
                INSERT  [tempdb].[dbo].[$(CompletedBatches)] (BatchId, Description)  
                VALUES                                      (0, N'CreateElementStep Sales batch 0');  
                SET NOCOUNT OFF;  
            END  
  
        ```  
  
        CREATE SCHEMA は、IF ステートメント内の EXECUTE sp_executesql ステートメントで囲む必要があるステートメントの 1 つです。 CREATE TABLE などのステートメントは、EXECUTE sp_executesql ステートメントを必要とせず、次のコード例のようになります。  
  
        ```  
        IF NOT EXISTS (SELECT 1  
                       FROM   [tempdb].[dbo].[$(CompletedBatches)]  
                       WHERE  [BatchId] = 1)  
            BEGIN  
                CREATE TABLE [Sales].[Customer] (  
                    [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
                    [CustomerName] NVARCHAR (40) NOT NULL,  
                    [YTDOrders]    INT           NOT NULL,  
                    [YTDSales]     INT           NOT NULL  
                );  
                SET NOCOUNT ON;  
                INSERT  [tempdb].[dbo].[$(CompletedBatches)] (BatchId, Description)  
                VALUES                                      (1, N'CreateElementStep Sales.Customer batch 0');  
                SET NOCOUNT OFF;  
            END  
  
        ```  
  
        > [!NOTE]  
        > ターゲット データベースと同一のデータベース プロジェクトを配置した場合、生成されるレポートにはあまり意味がありません。 意味のある結果を得るには、データベースに対する変更を配置するか、新しいデータベースを配置します。  
  
## <a name="command-line-deployment-using-generated-dacpac-file"></a>生成された dacpac ファイルを使用したコマンド ライン配置  
SQL プロジェクトのビルドが完了すると、コマンド ラインからスキーマを配置するために使用できる dacpac ファイルが作成されます。これにより、ビルド コンピューターなどの別のコンピューターから配置することができます。 SqlPackage は、さまざまなオプションを使用して dacpacs を配置できるコマンド ライン ユーティリティです。これらのオプションにより、ユーザーは、特に dacpac の配置や配置スクリプトの生成を実行できます。 詳しくは、「[SqlPackage.exe](https://msdn.microsoft.com/library/hh550080(v=VS.103).aspx)」をご覧ください。  
  
> [!NOTE]  
> DeploymentContributors プロパティが定義されているプロジェクトからビルドされた dacpacs を正常に配置するには、配置コントリビューターを含む DLL を、使用中のコンピューターにインストールする必要があります。 これは、配置を正常に完了するためにこれらの DLL が必須とマークされているためです。  
>   
> この要件を回避するには、.sqlproj ファイルから配置コントリビューターを除外します。 代わりに、**AdditionalDeploymentContributors** パラメーターを指定した SqlPackage を使用して、配置中にコントリビューターを実行するように指定します。 これは、特殊な状況 (特定のサーバーへの配置など) でコントリビューターを使用する場合にのみ役立ちます。  
  
## <a name="next-steps"></a>Next Steps  
配置計画に対するその他の種類の変更については、実行する前に試すことができます。 適用する可能性のあるその他の変更の種類には、次のようなものがあります。  
  
-   バージョン番号を関連付けるすべてのデータベース オブジェクトに拡張プロパティを追加する。  
  
-   配置スクリプトで追加の診断用 PRINT ステートメントまたはコメントを追加または削除する。  
  
## <a name="see-also"></a>参照  
[ビルド コントリビューターと配置コントリビューターを使用してデータベースのビルドと配置をカスタマイズする](../ssdt/use-deployment-contributors-to-customize-database-build-and-deployment.md)  
[チュートリアル:モデルの統計を生成するためのデータベース プロジェクトのビルドの拡張](../ssdt/walkthrough-extend-database-project-build-to-generate-model-statistics.md)  
[チュートリアル:配置計画を分析するためのデータベース プロジェクトの配置の拡張](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)  
  
