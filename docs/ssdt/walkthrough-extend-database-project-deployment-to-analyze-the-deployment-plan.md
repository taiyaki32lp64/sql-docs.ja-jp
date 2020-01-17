---
title: チュートリアル:配置計画を分析するためのデータベース プロジェクトの配置の拡張 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 9ead8470-93ba-44e3-8848-b59322e37621
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 167667590df0b2172e05674c462cfa9833d45acd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912782"
---
# <a name="walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan"></a>チュートリアル:配置計画を分析するためにデータベース プロジェクトの配置を拡張する
配置コントリビューターを作成して、SQL プロジェクトの配置時にカスタム アクションを実行できます。 DeploymentPlanModifier または DeploymentPlanExecutor を作成できます。 計画の実行前に計画を変更する場合は DeploymentPlanModifier を使用し、計画の実行中に操作を実行する場合は DeploymentPlanExecutor を使用します。 このチュートリアルでは、データベース プロジェクトの配置時に実行されるアクションに関するレポートを作成する、DeploymentUpdateReportContributor という名前の DeploymentPlanExecutor を作成します。 このビルド コントリビューターはレポートを生成するかどうかを制御するパラメーターを受け取るため、追加のステップを実行する必要があります。  
  
このチュートリアルでは、次の主なタスクを行います。  
  
-   [DeploymentPlanExecutor 型の配置コントリビューターを作成する](#CreateDeploymentContributor)  
  
-   [配置コントリビューターをインストールする](#InstallDeploymentContributor)  
  
-   [配置コントリビューターのテスト](#TestDeploymentContributor)  
  
## <a name="prerequisites"></a>Prerequisites  
このチュートリアルを実行するには、次のコンポーネントが必要です。  
  
-   C# または VB の開発をサポートする、SQL Server Data Tools (SSDT) を含む Visual Studio のバージョンがインストールされていること。  
  
-   SQL オブジェクトを含む SQL プロジェクト。  
  
-   データベース プロジェクトを配置できる SQL Server のインスタンス。  
  
> [!NOTE]  
> このチュートリアルは、既に SSDT の SQL 機能を使い慣れているユーザーを対象としています。 また、クラス ライブラリの作成方法、コード エディターを使用してクラスにコードを追加する方法など、Visual Studio の基本的な概念を理解している必要があります。  
  
## <a name="CreateDeploymentContributor"></a>配置コントリビューターの作成  
配置コントリビューターを作成するには、次のタスクを実行する必要があります。  
  
-   クラス ライブラリ プロジェクトを作成し、必要な参照を追加する。  
  
-   [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) から継承する、DeploymentUpdateReportContributor という名前のクラスを定義する。  
  
-   OnExecute メソッドをオーバーライドする。  
  
-   プライベート ヘルパー クラスを追加する。  
  
-   結果として得られるアセンブリをビルドする。  
  
#### <a name="to-create-a-class-library-project"></a>クラス ライブラリ プロジェクトを作成するには  
  
1.  MyDeploymentContributor という名前の Visual Basic または Visual C# のクラス ライブラリ プロジェクトを作成します。  
  
2.  "Class1.cs" ファイルの名前を "DeploymentUpdateReportContributor.cs" に変更します。  
  
3.  ソリューション エクスプローラーで、プロジェクト ノードを右クリックし、 **[参照の追加]** をクリックします。  
  
4.  [フレームワーク] タブで **System.ComponentModel.Composition** を選択します。  
  
5.  必要な SQL 参照を追加します。この操作を行うには、プロジェクト ノードを右クリックし、 **[参照の追加]** をクリックします。 **[参照]** をクリックし、**C:\Program Files (x86)\Microsoft SQL Server\110\DAC\Bin** フォルダーに移動します。 **Microsoft.SqlServer.Dac.dll**、**Microsoft.SqlServer.Dac.Extensions.dll**、および **Microsoft.Data.Tools.Schema.Sql.dll** の各エントリを選択し、 **[追加]** 、 **[OK]** の順にクリックします。  
  
    次に、コードをクラスに追加します。  
  
#### <a name="to-define-the-deploymentupdatereportcontributor-class"></a>DeploymentUpdateReportContributor クラスを定義するには  
  
1.  コード エディターで、次の **using** ステートメントに一致するように、DeploymentUpdateReportContributor.cs ファイルを更新します。  
  
    ```csharp  
    using System;  
    using System.IO;  
    using System.Text;  
    using System.Xml;  
    using Microsoft.SqlServer.Dac.Deployment;  
    using Microsoft.SqlServer.Dac.Extensibility;  
    using Microsoft.SqlServer.Dac.Model;  
  
    ```  
  
2.  クラス定義を次のように更新します。  
  
    ```csharp  
    /// <summary>  
        /// An executor that generates a report detailing the steps in the deployment plan. Will only run  
        /// if a "GenerateUpdateReport=true" contributor argument is set in the project file, in a targets file or  
        /// passed as an additional argument to the DacServices API. To set in a project file, add the following:  
        ///   
        /// <PropertyGroup>  
        ///     <ContributorArguments Condition="'$(Configuration)' == 'Debug'">  
        /// $(ContributorArguments);DeploymentUpdateReportContributor.GenerateUpdateReport=true;  
        ///     </ContributorArguments>  
        /// <PropertyGroup>  
        ///   
        /// </summary>  
        [ExportDeploymentPlanExecutor("MyDeploymentContributor.DeploymentUpdateReportContributor", "1.0.0.0")]  
        public class DeploymentUpdateReportContributor : DeploymentPlanExecutor  
        {  
        }  
  
    ```  
  
    これで、DeploymentPlanExecutor から継承する配置コントリビューターの定義が完了しました。 ビルドおよび配置プロセス中に、カスタム コントリビューターは標準の拡張機能ディレクトリから読み込まれます。 配置計画を実行するコントリビューターは、[ExportDeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.exportdeploymentplanexecutorattribute.aspx) 属性によって識別されます。  
  
    コントリビューターを検出できるようにするためにこの属性は必須です。 これは次のようになります。  
  
    ```csharp  
    [ExportDeploymentPlanExecutor("MyDeploymentContributor.DeploymentUpdateReportContributor", "1.0.0.0")]  
  
    ```  
  
    この場合、属性の最初のパラメーターは一意の識別子である必要があります。この識別子は、プロジェクト ファイル内でコントリビューターを識別するために使用されます。 ベスト プラクティスとして、ご利用のライブラリの名前空間 (このチュートリアルでは MyDeploymentContributor) とクラス名 (このチュートリアルでは DeploymentUpdateReportContributor) を組み合わせて識別子を作成することをお勧めします。  
  
3.  次に、このプロバイダーでコマンド ライン パラメーターを受け取ることができるように次のメンバーを追加します。  
  
    ```csharp  
    public const string GenerateUpdateReport = "DeploymentUpdateReportContributor.GenerateUpdateReport";  
    ```  
  
    このメンバーにより、ユーザーは、GenerateUpdateReport オプションを使用してレポートを生成するかどうかを指定できます。  
  
    次に、OnExecute メソッドをオーバーライドして、データベース プロジェクトの配置時に実行するコードを追加します。  
  
#### <a name="to-override-onexecute"></a>OnExecute をオーバーライドするには  
  
-   DeploymentUpdateReportContributor クラスに次のメソッドを追加します。  
  
    ```csharp  
    /// <summary>  
            /// Override the OnExecute method to perform actions when you execute the deployment plan for  
            /// a database project.  
            /// </summary>  
            protected override void OnExecute(DeploymentPlanContributorContext context)  
            {  
                // determine whether the user specified a report is to be generated  
                bool generateReport = false;  
                string generateReportValue;  
                if (context.Arguments.TryGetValue(GenerateUpdateReport, out generateReportValue) == false)  
                {  
                    // couldn't find the GenerateUpdateReport argument, so do not generate  
                    generateReport = false;  
                }  
                else  
                {  
                    // GenerateUpdateReport argument was specified, try to parse the value  
                    if (bool.TryParse(generateReportValue, out generateReport))  
                    {  
                        // if we end up here, the value for the argument was not valid.  
                        // default is false, so do nothing.  
                    }  
                }  
  
                if (generateReport == false)  
                {  
                    // if user does not want to generate a report, we are done  
                    return;  
                }  
  
                // We will output to the same directory where the deployment script  
                // is output or to the current directory  
                string reportPrefix = context.Options.TargetDatabaseName;  
                string reportPath;  
                if (string.IsNullOrEmpty(context.DeploymentScriptPath))  
                {  
                    reportPath = Environment.CurrentDirectory;  
                }  
                else  
                {  
                    reportPath = Path.GetDirectoryName(context.DeploymentScriptPath);  
                }  
                FileInfo summaryReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".summary.xml"));  
                FileInfo detailsReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".details.xml"));  
  
                // Generate the reports by using the helper class DeploymentReportWriter  
                DeploymentReportWriter writer = new DeploymentReportWriter(context);  
                writer.WriteReport(summaryReportFile);  
                writer.IncludeScripts = true;  
                writer.WriteReport(detailsReportFile);  
  
                string msg = "Deployment reports ->"  
                    + Environment.NewLine + summaryReportFile.FullName  
                    + Environment.NewLine + detailsReportFile.FullName;  
  
                ExtensibilityError reportMsg = new ExtensibilityError(msg, Severity.Message);  
                base.PublishMessage(reportMsg);  
            }  
        /// <summary>  
        /// Override the OnExecute method to perform actions when you execute the deployment plan for  
        /// a database project.  
        /// </summary>  
            protected override void OnExecute(DeploymentPlanContributorContext context)  
            {  
                // determine whether the user specified a report is to be generated  
                bool generateReport = false;  
                string generateReportValue;  
                if (context.Arguments.TryGetValue(GenerateUpdateReport, out generateReportValue) == false)  
                {  
                    // couldn't find the GenerateUpdateReport argument, so do not generate  
                    generateReport = false;  
                }  
                else  
                {  
                    // GenerateUpdateReport argument was specified, try to parse the value  
                    if (bool.TryParse(generateReportValue, out generateReport))  
                    {  
                        // if we end up here, the value for the argument was not valid.  
                        // default is false, so do nothing.  
                    }  
                }  
  
                if (generateReport == false)  
                {  
                    // if user does not want to generate a report, we are done  
                    return;  
                }  
  
                // We will output to the same directory where the deployment script  
                // is output or to the current directory  
                string reportPrefix = context.Options.TargetDatabaseName;  
                string reportPath;  
                if (string.IsNullOrEmpty(context.DeploymentScriptPath))  
                {  
                    reportPath = Environment.CurrentDirectory;  
                }  
                else  
                {  
                    reportPath = Path.GetDirectoryName(context.DeploymentScriptPath);  
                }  
                FileInfo summaryReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".summary.xml"));  
                FileInfo detailsReportFile = new FileInfo(Path.Combine(reportPath, reportPrefix + ".details.xml"));  
  
                // Generate the reports by using the helper class DeploymentReportWriter  
                DeploymentReportWriter writer = new DeploymentReportWriter(context);  
                writer.WriteReport(summaryReportFile);  
                writer.IncludeScripts = true;  
                writer.WriteReport(detailsReportFile);  
  
                string msg = "Deployment reports ->"  
                    + Environment.NewLine + summaryReportFile.FullName  
                    + Environment.NewLine + detailsReportFile.FullName;  
  
                DataSchemaError reportMsg = new DataSchemaError(msg, ErrorSeverity.Message);  
                base.PublishMessage(reportMsg);  
            }  
    ```  
  
    この OnExecute メソッドに、[DeploymentPlanContributorContext](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplancontributorcontext.aspx) オブジェクトが渡され、指定されたすべての引数、ソースとターゲットのデータベース モデル、ビルド プロパティ、および拡張ファイルにアクセスできるようになります。 この例では、モデルを取得し、そのモデルに関する情報を出力するヘルパー関数を呼び出します。 ここでは、発生したエラーを報告するために、基本クラスで PublishMessage ヘルパー メソッドを使用します。  
  
    その他の重要な型およびメソッドは、[TSqlModel](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlmodel.aspx)、[ModelComparisonResult](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.modelcomparisonresult.aspx)、[DeploymentPlanHandle](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanhandle.aspx)、[SqlDeploymentOptions](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqldeploymentoptions.aspx) です。  
  
    次に、配置計画の詳細を調査するヘルパー クラスを定義します。  
  
#### <a name="to-add-the-helper-class-that-generates-the-report-body"></a>レポート本文を生成するヘルパー クラスを追加するには  
  
-   次のコードを追加して、ヘルパー クラスとそのメソッドを追加します。  
  
    ```csharp  
    /// <summary>  
            /// This class is used to generate a deployment  
            /// report.   
            /// </summary>  
            private class DeploymentReportWriter  
            {  
                readonly TSqlModel _sourceModel;  
                readonly ModelComparisonResult _diff;  
                readonly DeploymentStep _planHead;  
  
                /// <summary>  
                /// The constructor accepts the same context info  
                /// that was passed to the OnExecute method of the  
                /// deployment contributor.  
                /// </summary>  
                public DeploymentReportWriter(DeploymentPlanContributorContext context)  
                {  
                    if (context == null)  
                    {  
                        throw new ArgumentNullException("context");  
                    }  
  
                    // save the source model, source/target differences,  
                    // and the beginning of the deployment plan.  
                    _sourceModel = context.Source;  
                    _diff = context.ComparisonResult;  
                    _planHead = context.PlanHandle.Head;  
                }  
                /// <summary>  
                /// Property indicating whether script bodies  
                /// should be included in the report.  
                /// </summary>  
                public bool IncludeScripts { get; set; }  
  
                /// <summary>  
                /// Drives the report generation, opening files,   
                /// writing the beginning and ending report elements,  
                /// and calling helper methods to report on the  
                /// plan operations.  
                /// </summary>  
                internal void WriteReport(FileInfo reportFile)  
                {// Assumes that we have a valid report file  
                    if (reportFile == null)  
                    {  
                        throw new ArgumentNullException("reportFile");  
                    }  
  
                    // set up the XML writer  
                    XmlWriterSettings xmlws = new XmlWriterSettings();  
                    // Indentation makes it a bit more readable  
                    xmlws.Indent = true;  
                    FileStream fs = new FileStream(reportFile.FullName, FileMode.Create, FileAccess.Write, FileShare.ReadWrite);  
                    XmlWriter xmlw = XmlWriter.Create(fs, xmlws);  
  
                    try  
                    {  
                        xmlw.WriteStartDocument(true);  
                        xmlw.WriteStartElement("DeploymentReport");  
  
                        // Summary report of the operations that  
                        // are contained in the plan.  
                        ReportPlanOperations(xmlw);  
  
                        // You could add a method call here  
                        // to produce a detailed listing of the   
                        // differences between the source and  
                        // target model.  
                        xmlw.WriteEndElement();  
                        xmlw.WriteEndDocument();  
                        xmlw.Flush();  
                        fs.Flush();  
                    }  
                    finally  
                    {  
                        xmlw.Close();  
                        fs.Dispose();  
                    }  
                }  
  
                /// <summary>  
                /// Writes details for the various operation types  
                /// that could be contained in the deployment plan.  
                /// Optionally writes script bodies, depending on  
                /// the value of the IncludeScripts property.  
                /// </summary>  
                private void ReportPlanOperations(XmlWriter xmlw)  
                {// write the node to indicate the start  
                    // of the list of operations.  
                    xmlw.WriteStartElement("Operations");  
  
                    // Loop through the steps in the plan,  
                    // starting at the beginning.  
                    DeploymentStep currentStep = _planHead;  
                    while (currentStep != null)  
                    {  
                        // Report the type of step  
                        xmlw.WriteStartElement(currentStep.GetType().Name);  
  
                        // based on the type of step, report  
                        // the relevant information.  
                        // Note that this procedure only handles   
                        // a subset of all step types.  
                        if (currentStep is SqlRenameStep)  
                        {  
                            SqlRenameStep renameStep = (SqlRenameStep)currentStep;  
                            xmlw.WriteAttributeString("OriginalName", renameStep.OldName);  
                            xmlw.WriteAttributeString("NewName", renameStep.NewName);  
                            xmlw.WriteAttributeString("Category", GetElementCategory(renameStep.RenamedElement));  
                        }  
                        else if (currentStep is SqlMoveSchemaStep)  
                        {  
                            SqlMoveSchemaStep moveStep = (SqlMoveSchemaStep)currentStep;  
                            xmlw.WriteAttributeString("OrignalName", moveStep.PreviousName);  
                            xmlw.WriteAttributeString("NewSchema", moveStep.NewSchema);  
                            xmlw.WriteAttributeString("Category", GetElementCategory(moveStep.MovedElement));  
                        }  
                        else if (currentStep is SqlTableMigrationStep)  
                        {  
                            SqlTableMigrationStep dmStep = (SqlTableMigrationStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(dmStep.SourceTable));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(dmStep.SourceElement));  
                        }  
                        else if (currentStep is CreateElementStep)  
                        {  
                            CreateElementStep createStep = (CreateElementStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(createStep.SourceElement));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(createStep.SourceElement));  
                        }  
                        else if (currentStep is AlterElementStep)  
                        {  
                            AlterElementStep alterStep = (AlterElementStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(alterStep.SourceElement));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(alterStep.SourceElement));  
                        }  
                        else if (currentStep is DropElementStep)  
                        {  
                            DropElementStep dropStep = (DropElementStep)currentStep;  
                            xmlw.WriteAttributeString("Name", GetElementName(dropStep.TargetElement));  
                            xmlw.WriteAttributeString("Category", GetElementCategory(dropStep.TargetElement));  
                        }  
  
                        // If the script bodies are to be included,  
                        // add them to the report.  
                        if (this.IncludeScripts)  
                        {  
                            using (StringWriter sw = new StringWriter())  
                            {  
                                currentStep.GenerateBatchScript(sw);  
                                string tsqlBody = sw.ToString();  
                                if (string.IsNullOrEmpty(tsqlBody) == false)  
                                {  
                                    xmlw.WriteCData(tsqlBody);  
                                }  
                            }  
                        }  
  
                        // close off the current step  
                        xmlw.WriteEndElement();  
                        currentStep = currentStep.Next;  
                    }  
                    xmlw.WriteEndElement();  
                }  
  
                /// <summary>  
                /// Returns the category of the specified element  
                /// in the source model  
                /// </summary>  
                private string GetElementCategory(TSqlObject element)  
                {  
                    return element.ObjectType.Name;  
                }  
  
                /// <summary>  
                /// Returns the name of the specified element  
                /// in the source model  
                /// </summary>  
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
            }        /// <summary>  
            /// This class is used to generate a deployment  
            /// report.   
            /// </summary>  
            private class DeploymentReportWriter  
            {  
                /// <summary>  
                /// The constructor accepts the same context info  
                /// that was passed to the OnExecute method of the  
                /// deployment contributor.  
                /// </summary>  
                public DeploymentReportWriter(DeploymentPlanContributorContext context)  
                {  
               }  
                /// <summary>  
                /// Property indicating whether script bodies  
                /// should be included in the report.  
                /// </summary>  
                public bool IncludeScripts { get; set; }  
  
                /// <summary>  
                /// Drives the report generation, opening files,   
                /// writing the beginning and ending report elements,  
                /// and calling helper methods to report on the  
                /// plan operations.  
                /// </summary>  
                internal void WriteReport(FileInfo reportFile)  
                {  
                }  
  
                /// <summary>  
                /// Writes details for the various operation types  
                /// that could be contained in the deployment plan.  
                /// Optionally writes script bodies, depending on  
                /// the value of the IncludeScripts property.  
                /// </summary>  
                private void ReportPlanOperations(XmlWriter xmlw)  
                {  
                }  
  
                /// <summary>  
                /// Returns the category of the specified element  
                /// in the source model  
                /// </summary>  
                private string GetElementCategory(IModelElement element)  
                {  
                }  
  
                /// <summary>  
                /// Returns the name of the specified element  
                /// in the source model  
                /// </summary>  
                private string GetElementName(IModelElement element)  
                {  
                }  
            }  
    ```  
  
-   変更内容をクラス ファイルに保存します。 ヘルパー クラスでは、多くの有用な型を参照しています。  
  
    |**コード領域**|**有用な型**|  
    |-----------------|--------------------|  
    |クラス メンバー|[TSqlModel](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlmodel.aspx)、[ModelComparisonResult](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.modelcomparisonresult.aspx)、[DeploymentStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentstep.aspx)|  
    |WriteReport メソッド|XmlWriter と XmlWriterSettings|  
    |ReportPlanOperations メソッド|重要な型には次のようなものがあります。[DeploymentStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentstep.aspx)、[SqlRenameStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqlrenamestep.aspx)、[SqlMoveSchemaStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqlmoveschemastep.aspx)、[SqlTableMigrationStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.sqltablemigrationstep.aspx)、[CreateElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.createelementstep.aspx)、[AlterElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.alterelementstep.aspx)、[DropElementStep](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.dropelementstep.aspx)。<br /><br />他にも多くのステップがあります。ステップの完全な一覧については、API のドキュメントを参照してください。|  
    |GetElementCategory|[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)|  
    |GetElementName|[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)|  
  
    次に、クラス ライブラリをビルドします。  
  
#### <a name="to-sign-and-build-the-assembly"></a>アセンブリの署名とビルドを行うには  
  
1.  **[プロジェクト]** メニューの **[MyDeploymentContributor のプロパティ]** をクリックします。  
  
2.  **[署名]** タブをクリックします。  
  
3.  **[アセンブリの署名]** をクリックします。  
  
4.  **[厳密な名前のキー ファイルを選択してください]** で **[<New>]** をクリックします。  
  
5.  **[厳密な名前キーの作成]** ダイアログ ボックスで、 **[キー ファイル]** に「 **MyRefKey**」と入力します。  
  
6.  (省略可能) 厳密な名前のキー ファイルにパスワードを指定できます。  
  
7.  **[OK]** をクリックします。  
  
8.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
9. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  
  
次に、アセンブリをインストールし、SQL プロジェクトをビルドして配置するときに読み込まれるようにします。  
  
## <a name="InstallDeploymentContributor"></a>配置コントリビューターのインストール  
配置コントリビューターをインストールするには、アセンブリおよび関連付けられた .pdb ファイルを Extensions フォルダーにコピーする必要があります。  
  
#### <a name="to-install-the-mydeploymentcontributor-assembly"></a>MyDeploymentContributor アセンブリをインストールするには  
  
-   次に、アセンブリ情報を Extensions ディレクトリにコピーします。 Visual Studio の起動時に、%Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions ディレクトリとサブディレクトリ内のすべての拡張機能が認識され、使用できるようになります。  
  
-   **MyDeploymentContributor.dll** アセンブリ ファイルを出力ディレクトリから %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions ディレクトリにコピーします。 既定では、コンパイル済みの .dll ファイルのパスは YourSolutionPath\YourProjectPath\bin\Debug または YourSolutionPath\YourProjectPath\bin\Release です。  
  
## <a name="TestDeploymentContributor"></a>配置コントリビューターのテスト  
配置コントリビューターをテストするには、次のタスクを実行する必要があります。  
  
-   配置する予定の .sqlproj ファイルにプロパティを追加する。  
  
-   MSBuild を使用し、適切なパラメーターを指定して、プロジェクトを配置する。  
  
### <a name="add-properties-to-the-sql-project-sqlproj-file"></a>SQL プロジェクト (.sqlproj) ファイルにプロパティを追加するには  
実行するコントリビューターの ID を指定するには、必ず SQL プロジェクト ファイルを更新する必要があります。 また、このコントリビューターには "GenerateUpdateReport" 引数が必要なため、これをコントリビューター引数として指定する必要があります。  
  
2 つの方法のいずれかでこれを行うことができます。 .sqlproj ファイルを手動で変更して、必要な引数を追加できます。 この方法を選択できるのは、コントリビューターで構成に必要なコントリビューター引数がない場合、または多数のプロジェクト間でコントリビューターを再利用しない場合です。 このオプションを選択した場合は、.sqlproj ファイル内の最初の Import ノードの後に次のステートメントを追加します。  
  
```  
<PropertyGroup>  
    <DeploymentContributors>$(DeploymentContributors); MyDeploymentContributor.DeploymentUpdateReportContributor</DeploymentContributors>  
<ContributorArguments Condition="'$(Configuration)' == 'Debug'">$(ContributorArguments);DeploymentUpdateReportContributor.GenerateUpdateReport=true;</ContributorArguments>  
  </PropertyGroup>  
```  
  
もう 1 つの方法では、必要なコントリビューター引数を含むターゲット ファイルを作成します。 この方法は、既定値が含まれるため、複数のプロジェクトに同じコントリビューターを使用していて、必要なコントリビューター引数がある場合に役立ちます。 この場合は、MSBuild 拡張機能のパスにターゲット ファイルを作成します。  
  
1.  %Program Files%\MSBuild に移動します。  
  
2.  ターゲット ファイルの保存先となる新しいフォルダー "MyContributors" を作成します。  
  
3.  このディレクトリ内に新しいファイル "MyContributors.targets" を作成し、次のテキストを追加して、ファイルを保存します。  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
  
    <Project xmlns="https://schemas.microsoft.com/developer/msbuild/2003">  
      <PropertyGroup>  
    <DeploymentContributors>$(DeploymentContributors);MyDeploymentContributor.DeploymentUpdateReportContributor</DeploymentContributors>  
    <ContributorArguments Condition="'$(Configuration)' == 'Debug'">$(ContributorArguments); DeploymentUpdateReportContributor.GenerateUpdateReport=true;</ContributorArguments>  
      </PropertyGroup>  
    </Project>  
    ```  
  
4.  コントリビューターを実行するプロジェクトの .sqlproj ファイル内で、\<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets" \/> ノードの後に次のステートメントを追加してターゲット ファイルをインポートします。  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath)\MyContributors\MyContributors.targets " />  
    ```  
  
上記の方法のいずれかを実行すると、MSBuild を使用して、コマンド ライン ビルドのパラメーターを渡すことができます。  
  
> [!NOTE]  
> コントリビューター ID を指定するには、必ず "DeploymentContributors" プロパティを更新する必要があります。 これは、コントリビューター ソース ファイル内の "ExportDeploymentPlanExecutor" 属性で使用されているのと同じ ID です。 これを指定しないと、プロジェクトのビルド時にコントリビューターが実行されません。 "ContributorArguments" プロパティは、コントリビューターの実行に必要な引数がある場合にのみ更新する必要があります。  
  
### <a name="deploy-the-database-project"></a>データベース プロジェクトの配置  
プロジェクトは、通常どおり Visual Studio 内で発行または配置できます。 ご利用の SQL プロジェクトが含まれているソリューションを開き、プロジェクトの右クリックのショートカット メニューで [発行] をクリックするか、LocalDB へのデバッグ配置を行うために F5 キーを使用するだけです。 この例では、[発行...] ダイアログを使用して配置スクリプトを生成します。  
  
##### <a name="to-deploy-your-sql-project-and-generate-a-deployment-report"></a>SQL プロジェクトを配置して配置レポートを生成するには  
  
1.  Visual Studio を起動し、SQL プロジェクトが含まれているソリューションを開きます。  
  
2.  ご利用のプロジェクトを選択し、F5 キーを押してデバッグ配置を実行します。 注: ContributorArguments 要素は、構成が "デバッグ" の場合のみに含まれるよう設定されているため、この時点では、デバッグ配置の配置レポートのみが作成されます。 これを変更するには、ContributorArguments の定義から Condition="'$(Configuration)' == 'Debug'" ステートメントを削除します。  
  
3.  出力ウィンドウには、次のような出力が表示されます。  
  
    ```  
    ------ Deploy started: Project: Database1, Configuration: Debug Any CPU ------  
    Finished verifying cached model in 00:00:00  
    Deployment reports ->  
  
      C:\Users\UserName\Documents\Visual Studio 2012\Projects\MyDatabaseProject\MyDatabaseProject\sql\debug\MyTargetDatabase.summary.xml  
      C:\Users\UserName\Documents\Visual Studio 2012\Projects\MyDatabaseProject\MyDatabaseProject\sql\debug\MyTargetDatabase.details.xml  
  
      Deployment script generated to:  
      C:\Users\UserName\Documents\Visual Studio 2012\Projects\MyDatabaseProject\MyDatabaseProject\sql\debug\MyDatabaseProject.sql  
  
    ```  
  
4.  MyTargetDatabase.summary.xml を開き、内容を確認します。 このファイルは、新しいデータベースの配置を示す次の例に似ています。  
  
    ```  
    <?xml version="1.0" encoding="utf-8" standalone="yes"?>  
    <DeploymentReport>  
      <Operations>  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <BeginPreDeploymentScriptStep />  
        <DeploymentScriptStep />  
        <EndPreDeploymentScriptStep />  
        <SqlBeginPreservationStep />  
        <SqlEndPreservationStep />  
        <SqlBeginDropsStep />  
        <SqlEndDropsStep />  
        <SqlBeginAltersStep />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales" Category="Schema" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Customer" Category="Table" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.PK_Customer_CustID" Category="Primary Key" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Orders" Category="Table" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.PK_Orders_OrderID" Category="Primary Key" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Customer_YTDOrders" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Customer_YTDSales" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Orders_OrderDate" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.Def_Orders_Status" Category="Default Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.FK_Orders_Customer_CustID" Category="Foreign Key" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.CK_Orders_FilledDate" Category="Check Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.CK_Orders_OrderDate" Category="Check Constraint" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspCancelOrder" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspFillOrder" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspNewCustomer" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspPlaceNewOrder" Category="Procedure" />  
        <SqlPrintStep />  
        <CreateElementStep Name="Sales.uspShowOrderDetails" Category="Procedure" />  
        <SqlEndAltersStep />  
        <DeploymentScriptStep />  
        <BeginPostDeploymentScriptStep />  
        <DeploymentScriptStep />  
        <EndPostDeploymentScriptStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
        <DeploymentScriptDomStep />  
      </Operations>  
    </DeploymentReport>  
  
    ```  
  
    > [!NOTE]  
    > ターゲット データベースと同一のデータベース プロジェクトを配置した場合、生成されるレポートにはあまり意味がありません。 意味のある結果を得るには、データベースに対する変更を配置するか、新しいデータベースを配置します。  
  
5.  MyTargetDatabase.details.xml を開き、内容を確認します。 詳細ファイルの小さいセクションに示されるエントリおよびスクリプトでは、Sales スキーマの作成、テーブルの作成に関するメッセージの出力、およびテーブルの作成を実行します。  
  
    ```  
    <CreateElementStep Name="Sales" Category="Schema"><![CDATA[CREATE SCHEMA [Sales]  
        AUTHORIZATION [dbo];  
  
    ]]></CreateElementStep>  
        <SqlPrintStep><![CDATA[PRINT N'Creating [Sales].[Customer]...';  
  
    ]]></SqlPrintStep>  
        <CreateElementStep Name="Sales.Customer" Category="Table"><![CDATA[CREATE TABLE [Sales].[Customer] (  
        [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
        [CustomerName] NVARCHAR (40) NOT NULL,  
        [YTDOrders]    INT           NOT NULL,  
        [YTDSales]     INT           NOT NULL  
    );  
  
    ]]></CreateElementStep>  
  
    ```  
  
    実行時に配置計画を分析することにより、配置に含まれるすべての情報について報告することも、その計画のステップに基づいた追加のアクションを実行することもできます。  
  
## <a name="next-steps"></a>Next Steps  
出力 XML ファイルの処理を実行するには、追加のツールを作成できます。 これは、[DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) の一例にすぎません。 また、[DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) を作成し、実行前に配置プランを変更することもできます。  
  
## <a name="see-also"></a>参照  
[チュートリアル:モデルの統計を生成するためのデータベース プロジェクトのビルドの拡張](https://msdn.microsoft.com/library/ee461508(v=vs.100).aspx)  
[チュートリアル:配置計画を変更するためにデータベース プロジェクトの配置を拡張する](https://msdn.microsoft.com/library/ee461507(v=vs.100).aspx)  
[ビルド コントリビューターと配置コントリビューターを使用してデータベースのビルドと配置をカスタマイズする](https://msdn.microsoft.com/library/ee461505(v=vs.100).aspx)  
  
