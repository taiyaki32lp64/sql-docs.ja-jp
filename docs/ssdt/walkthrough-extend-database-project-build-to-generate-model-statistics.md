---
title: 'チュートリアル: モデルの統計を生成するためのデータベース プロジェクトのビルドの拡張 | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d44935ce-63bf-46df-976a-5a54866c8119
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5e1844ae19de96b13b36fad59f5032fe68caaf19
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069010"
---
# <a name="walkthrough-extend-database-project-build-to-generate-model-statistics"></a>チュートリアル:モデルの統計を生成するためのデータベース プロジェクトのビルドの拡張
ビルド コントリビューターを作成して、データベース プロジェクトのビルド時にカスタム アクションを実行できます。 このチュートリアルでは、データベース プロジェクトのビルド時に SQL データベース モデルから統計を出力する ModelStatistics という名前のビルド コントリビューターを作成します。 このビルド コントリビューターはビルド時にパラメーターを受け取るため、追加のステップが必要となります。  
  
このチュートリアルでは、次の主なタスクを行います。  
  
-   [ビルド コントリビューターを作成する](#CreateBuildContributor)  
  
-   [ビルド コントリビューターをインストールする](#InstallBuildContributor)  
  
-   [ビルド コントリビューターをテストする](#TestBuildContributor)  
  
## <a name="prerequisites"></a>Prerequisites  
このチュートリアルを実行するには、次のコンポーネントが必要です。  
  
-   C# または VB の開発をサポートする、SQL Server Data Tools (SSDT) を含む Visual Studio のバージョンがインストールされていること。  
  
-   SQL オブジェクトを含む SQL プロジェクト。  
  
> [!NOTE]  
> このチュートリアルは、既に SSDT の SQL 機能を使い慣れているユーザーを対象としています。 また、クラス ライブラリの作成方法、コード エディターを使用してクラスにコードを追加する方法など、Visual Studio の基本的な概念を理解している必要があります。  
  
## <a name="build-contributor-background"></a>ビルド コントリビューターの背景情報  
ビルド コントリビューターは、プロジェクトのビルド中に、プロジェクトを表すモデルが生成されてからプロジェクトがディスクに保存されるまでの間に実行されます。 ビルド コントリビューターは、次のような多数のシナリオで使用できます。  
  
-   モデルのコンテンツを検証し、検証エラーを呼び出し元に報告する。 これを行うには、OnExecute メソッドにパラメーターとして渡されるリストにエラーを追加します。  
  
-   モデルの統計を生成してユーザーに報告する。 これは、次に例を示します。  
  
ビルド コントリビューターのメイン エントリ ポイントは OnExecute メソッドです。 BuildContributor から継承するすべてのクラスには、このメソッドを実装する必要があります。 このメソッドには BuildContributorContext オブジェクトが渡されます。このオブジェクトには、データベースのモデル、ビルド プロパティ、ビルド コントリビューターで使用される引数やファイルなど、ビルドに関連するすべてのデータが含まれます。  
  
**TSqlModel とデータベース モデル API**  
  
最も役に立つオブジェクトは、TSqlModel オブジェクトで表されるデータベース モデルです。 これは、テーブル、ビューなどのすべての要素とそれらの要素間のリレーションシップを含め、データベースを論理的に表したものです。 特定の種類の要素に対してクエリを実行し、関心のあるリレーションシップを走査するために使用できる厳密に型指定されたスキーマがあります。 このスキーマの使用方法の例については、このチュートリアルのコードを参照してください。  
  
このチュートリアルのコントリビューターの例で使用されているコマンドは次のとおりです。  
  
|**クラス**|**メソッド/プロパティ**|**[説明]**|  
|-------------|------------------------|-------------------|  
|[TSqlModel](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlmodel.aspx)|GetObjects()|モデルに対してクエリを実行してオブジェクトを取得します。これは、モデル API に対するメイン エントリ ポイントです。 Table や View などの最上位レベルの型のみに対してクエリを実行できます。Columns などの型は、モデルの走査によってのみ検出できます。 ModelTypeClass フィルターが指定されていない場合は、最上位レベルのすべての型が返されます。|  
|[TSqlObject](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.model.tsqlobject.aspx)|GetReferencedRelationshipInstances()|現在の TSqlObject によって参照される要素に対するリレーションシップを検出します。 たとえば、テーブルの場合、テーブルの列などのオブジェクトが返されます。 この場合、ModelRelationshipClass フィルターを使用すると、クエリの実行対象となる正確なリレーションシップを指定できます (たとえば、"Table.Columns" フィルターを使用した場合は列のみが返されます)。<br /><br />GetReferencingRelationshipInstances、GetChildren、GetParent など、類似するメソッドが多数あります。 詳細については、API のドキュメントを参照してください。|  
  
**コントリビューターを一意に識別する**  
  
ビルド プロセス中に、カスタム コントリビューターは標準の拡張機能ディレクトリから読み込まれます。 ビルド コントリビューターは、 [ExportBuildContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.exportbuildcontributorattribute.aspx) 属性によって識別されます。 コントリビューターを検出できるようにするためにこの属性は必須です。 この属性は次のようになります。  
  
```  
[ExportBuildContributor("ExampleContributors.ModelStatistics", "1.0.0.0")]  
  
```  
  
この場合、属性の最初のパラメーターは一意の識別子である必要があります。この識別子は、プロジェクト ファイル内でコントリビューターを識別するために使用されます。 ライブラリの名前空間 (このチュートリアルでは "ExampleContributors") とクラス名 (このチュートリアルでは "ModelStatistics") を組み合わせて識別子を生成することをお勧めします。 このチュートリアルの後半では、この名前空間を使用してコントリビューターの実行を指定する方法について説明します。  
  
## <a name="CreateBuildContributor"></a>ビルド コントリビューターを作成する  
ビルド コントリビューターを作成するには、次のタスクを実行する必要があります。  
  
-   クラス ライブラリ プロジェクトを作成し、必要な参照を追加する。  
  
-   [BuildContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx)から継承する ModelStatistics という名前のクラスを定義する。  
  
-   OnExecute メソッドをオーバーライドする。  
  
-   プライベート ヘルパー メソッドを追加する。  
  
-   結果として得られるアセンブリをビルドする。  
  
#### <a name="to-create-a-class-library-project"></a>クラス ライブラリ プロジェクトを作成するには  
  
1.  MyBuildContributor という名前の Visual Basic または Visual C# のクラス ライブラリ プロジェクトを作成します。  
  
2.  "Class1.cs" ファイルの名前を "ModelStatistics.cs" に変更します。  
  
3.  ソリューション エクスプローラーで、プロジェクト ノードを右クリックし、 **[参照の追加]** をクリックします。  
  
4.  **System.ComponentModel.Composition** エントリを選択し、 **[OK]** をクリックします。  
  
5.  必要な SQL 参照を追加します。この操作を行うには、プロジェクト ノードを右クリックし、 **[参照の追加]** をクリックします。 **[参照]** をクリックし、 **C:\Program Files (x86)\Microsoft SQL Server\110\DAC\Bin** フォルダーに移動します。 **Microsoft.SqlServer.Dac.dll**、 **Microsoft.SqlServer.Dac.Extensions.dll**、および **Microsoft.Data.Tools.Schema.Sql.dll** の各エントリを選択し、 **[OK]** をクリックします。  
  
    次に、コードをクラスに追加します。  
  
#### <a name="to-define-the-modelstatistics-class"></a>ModelStatistics クラスを定義するには  
  
1.  ModelStatistics クラスは、OnExecute メソッドに渡されたデータベース モデルを処理し、モデルのコンテンツの詳細を示す XML レポートを生成します。  
  
    コード エディターで、次のコードに一致するように ModelStatistics.cs ファイルを更新します。  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.IO;  
    using System.Linq;  
    using System.Xml.Linq;  
    using Microsoft.Data.Schema;  
    using Microsoft.Data.Schema.Build;  
    using Microsoft.Data.Schema.Extensibility;  
    using Microsoft.Data.Schema.SchemaModel;  
    using Microsoft.Data.Schema.Sql;  
  
    namespace ExampleContributors  
    {  
    /// <summary>  
        /// A BuildContributor that generates statistics about a model and saves this to the output directory.  
        /// Will only run if a "GenerateModelStatistics=true" contributor argument is set in the project file, or a targets file.   
        /// Statistics can be sorted by "none, "name" or "value", with "none" being the default sort behavior.  
        ///   
        /// To set contributor arguments in a project file, add the following:  
        ///   
        /// <PropertyGroup>  
        ///     <ContributorArguments Condition="'$(Configuration)' == 'Debug'">  
        /// $(ContributorArguments);ModelStatistics.GenerateModelStatistics=true;ModelStatistics.SortModelStatisticsBy="name";  
        ///     </ContributorArguments>  
        /// <PropertyGroup>      
        ///   
        /// This will generate model statistics when building in Debug mode only - remove the condition to generate in all build modes.  
        /// </summary>  
        [ExportBuildContributor("ExampleContributors.ModelStatistics", "1.0.0.0")]  
        public class ModelStatistics : BuildContributor  
        {  
            public const string GenerateModelStatistics = "ModelStatistics.GenerateModelStatistics";  
            public const string SortModelStatisticsBy = "ModelStatistics.SortModelStatisticsBy";  
            public const string OutDir = "ModelStatistics.OutDir";  
            public const string ModelStatisticsFilename = "ModelStatistics.xml";  
            private enum SortBy { None, Name, Value };  
            private static Dictionary<string, SortBy> SortByMap = new Dictionary<string, SortBy>(StringComparer.OrdinalIgnoreCase)  
            {  
                { "none", SortBy.None },  
                { "name", SortBy.Name },  
                { "value", SortBy.Value },  
            };  
  
            private SortBy _sortBy = SortBy.None;  
  
            /// <summary>  
            /// Override the OnExecute method to perform actions when you build a database project.  
            /// </summary>  
            protected override void OnExecute(BuildContributorContext context, IList<ExtensibilityError> errors)  
            {  
                // handle related arguments, passed in as part of  
                // the context information.  
                bool generateModelStatistics;  
                ParseArguments(context.Arguments, errors, out generateModelStatistics);  
  
                // Only generate statistics if requested to do so  
                if (generateModelStatistics)  
                {  
                    // First, output model-wide information, such  
                    // as the type of database schema provider (DSP)  
                    // and the collation.  
                    StringBuilder statisticsMsg = new StringBuilder();  
                    statisticsMsg.AppendLine(" ")  
                                 .AppendLine("Model Statistics:")  
                                 .AppendLine("===")  
                                 .AppendLine(" ");  
                    errors.Add(new ExtensibilityError(statisticsMsg.ToString(), Severity.Message));  
  
                    var model = context.Model;  
  
                    // Start building up the XML that will later  
                    // be serialized.  
                    var xRoot = new XElement("ModelStatistics");  
  
                    SummarizeModelInfo(model, xRoot, errors);  
  
                    // First, count the elements that are contained   
                    // in this model.  
                    IList<TSqlObject> elements = model.GetObjects(DacQueryScopes.UserDefined).ToList();  
                    Summarize(elements, element => element.ObjectType.Name, "UserDefinedElements", xRoot, errors);  
  
                    // Now, count the elements that are defined in  
                    // another model. Examples include built-in types,  
                    // roles, filegroups, assemblies, and any   
                    // referenced objects from another database.  
                    elements = model.GetObjects(DacQueryScopes.BuiltIn | DacQueryScopes.SameDatabase | DacQueryScopes.System).ToList();  
                    Summarize(elements, element => element.ObjectType.Name, "OtherElements", xRoot, errors);  
  
                    // Now, count the number of each type  
                    // of relationship in the model.  
                    SurveyRelationships(model, xRoot, errors);  
  
                    // Determine where the user wants to save  
                    // the serialized XML file.  
                    string outDir;  
                    if (context.Arguments.TryGetValue(OutDir, out outDir) == false)  
                    {  
                        outDir = ".";  
                    }  
                    string filePath = Path.Combine(outDir, ModelStatisticsFilename);  
                    // Save the XML file and tell the user  
                    // where it was saved.  
                    xRoot.Save(filePath);  
                    ExtensibilityError resultArg = new ExtensibilityError("Result was saved to " + filePath, Severity.Message);  
                    errors.Add(resultArg);  
                }  
            }  
  
            /// <summary>  
            /// Examine the arguments provided by the user  
            /// to determine if model statistics should be generated  
            /// and, if so, how the results should be sorted.  
            /// </summary>  
            private void ParseArguments(IDictionary<string, string> arguments, IList<ExtensibilityError> errors, out bool generateModelStatistics)  
            {  
                // By default, we don't generate model statistics  
                generateModelStatistics = false;  
  
                // see if the user provided the GenerateModelStatistics   
                // option and if so, what value was it given.  
                string valueString;  
                arguments.TryGetValue(GenerateModelStatistics, out valueString);  
                if (string.IsNullOrWhiteSpace(valueString) == false)  
                {  
                    if (bool.TryParse(valueString, out generateModelStatistics) == false)  
                    {  
                        generateModelStatistics = false;  
  
                        // The value was not valid from the end user  
                        ExtensibilityError invalidArg = new ExtensibilityError(  
                            GenerateModelStatistics + "=" + valueString + " was not valid.  It can be true or false", Severity.Error);  
                        errors.Add(invalidArg);  
                        return;  
                    }  
                }  
  
                // Only worry about sort order if the user requested  
                // that we generate model statistics.  
                if (generateModelStatistics)  
                {  
                    // see if the user provided the sort option and  
                    // if so, what value was provided.  
                    arguments.TryGetValue(SortModelStatisticsBy, out valueString);  
                    if (string.IsNullOrWhiteSpace(valueString) == false)  
                    {  
                        SortBy sortBy;  
                        if (SortByMap.TryGetValue(valueString, out sortBy))  
                        {  
                            _sortBy = sortBy;  
                        }  
                        else  
                        {  
                            // The value was not valid from the end user  
                            ExtensibilityError invalidArg = new ExtensibilityError(  
                                SortModelStatisticsBy + "=" + valueString + " was not valid.  It can be none, name, or value", Severity.Error);  
                            errors.Add(invalidArg);  
                        }  
                    }  
                }  
            }  
  
            /// <summary>  
            /// Retrieve the database schema provider for the  
            /// model and the collation of that model.  
            /// Results are output to the console and added to the XML  
            /// being constructed.  
            /// </summary>  
            private static void SummarizeModelInfo(TSqlModel model, XElement xContainer, IList<ExtensibilityError> errors)  
            {  
                // use a Dictionary to accumulate the information  
                // that will later be output.  
                var info = new Dictionary<string, string>();  
  
                // Two things of interest: the database schema  
                // provider for the model, and the language id and  
                // case sensitivity of the collation of that  
                // model  
                info.Add("Version", model.Version.ToString());  
  
                TSqlObject options = model.GetObjects(DacQueryScopes.UserDefined, DatabaseOptions.TypeClass).FirstOrDefault();  
                if (options != null)  
                {  
                    info.Add("Collation", options.GetProperty<string>(DatabaseOptions.Collation));  
                }  
  
                // Output the accumulated information and add it to   
                // the XML.  
                OutputResult("Basic model info", info, xContainer, errors);  
            }  
  
            /// <summary>  
            /// For a provided list of model elements, count the number  
            /// of elements for each class name, sorted as specified  
            /// by the user.  
            /// Results are output to the console and added to the XML  
            /// being constructed.  
            /// </summary>  
            private void Summarize<T>(IList<T> set, Func<T, string> groupValue, string category, XElement xContainer, IList<ExtensibilityError> errors)  
            { // Use a Dictionary to keep all summarized information  
                var statistics = new Dictionary<string, int>();  
  
                // For each element in the provided list,  
                // count items based on the specified grouping  
                var groups =  
                    from item in set  
                    group item by groupValue(item) into g  
                    select new { g.Key, Count = g.Count() };  
  
                // order the groups as requested by the user  
                if (this._sortBy == SortBy.Name)  
                {  
                    groups = groups.OrderBy(group => group.Key);  
                }  
                else if (this._sortBy == SortBy.Value)  
                {  
                    groups = groups.OrderBy(group => group.Count);  
                }  
  
                // build the Dictionary of accumulated statistics  
                // that will be passed along to the OutputResult method.  
                foreach (var item in groups)  
                {  
                    statistics.Add(item.Key, item.Count);  
                }  
  
                statistics.Add("subtotal", set.Count);  
                statistics.Add("total items", groups.Count());  
  
                // output the results, and build up the XML  
                OutputResult(category, statistics, xContainer, errors);  
            }  
  
            /// <summary>  
            /// Iterate over all model elements, counting the  
            /// styles and types for relationships that reference each   
            /// element  
            /// Results are output to the console and added to the XML  
            /// being constructed.  
            /// </summary>  
            private static void SurveyRelationships(TSqlModel model, XElement xContainer, IList<ExtensibilityError> errors)  
            {  
                // get a list that contains all elements in the model  
                var elements = model.GetObjects(DacQueryScopes.All);  
                // We are interested in all relationships that  
                // reference each element.  
                var entries =  
                    from element in elements  
                    from entry in element.GetReferencedRelationshipInstances(DacExternalQueryScopes.All)  
                    select entry;  
  
                // initialize our counting buckets  
                var composing = 0;  
                var hierachical = 0;  
                var peer = 0;  
  
                // process each relationship, adding to the   
                // appropriate bucket for style and type.  
                foreach (var entry in entries)  
                {  
                    switch (entry.Relationship.Type)  
                    {  
                        case RelationshipType.Composing:  
                            ++composing;  
                            break;  
                        case RelationshipType.Hierarchical:  
                            ++hierachical;  
                            break;  
                        case RelationshipType.Peer:  
                            ++peer;  
                            break;  
                        default:  
                            break;  
                    }  
                }  
  
                // build a dictionary of data to pass along  
                // to the OutputResult method.  
                var stat = new Dictionary<string, int>  
                {  
                    {"Composing", composing},  
                    {"Hierarchical", hierachical},  
                    {"Peer", peer},  
                    {"subtotal", entries.Count()}  
                };  
  
                OutputResult("Relationships", stat, xContainer, errors);  
            }  
  
            /// <summary>  
            /// Performs the actual output for this contributor,  
            /// writing the specified set of statistics, and adding any   
            /// output information to the XML being constructed.  
            /// </summary>  
            private static void OutputResult<T>(string category, Dictionary<string, T> statistics, XElement xContainer, IList<ExtensibilityError> errors)  
            {  
                var maxLen = statistics.Max(stat => stat.Key.Length) + 2;  
                var format = string.Format("{{0, {0}}}: {{1}}", maxLen);  
  
                StringBuilder resultMessage = new StringBuilder();  
                //List<ExtensibilityError> args = new List<ExtensibilityError>();  
                resultMessage.AppendLine(category);  
                resultMessage.AppendLine("-----------------");  
  
                // Remove any blank spaces from the category name  
                var xCategory = new XElement(category.Replace(" ", ""));  
                xContainer.Add(xCategory);  
  
                foreach (var item in statistics)  
                {  
                    //Console.WriteLine(format, item.Key, item.Value);  
                    var entry = string.Format(format, item.Key, item.Value);  
                    resultMessage.AppendLine(entry);  
                    // Replace any blank spaces in the element key with  
                    // underscores.  
                    xCategory.Add(new XElement(item.Key.Replace(' ', '_'), item.Value));  
                }  
                resultMessage.AppendLine(" ");  
                errors.Add(new ExtensibilityError(resultMessage.ToString(), Severity.Message));  
            }  
        }  
    }  
  
    ```  
  
    次に、クラス ライブラリをビルドします。  
  
### <a name="to-sign-and-build-the-assembly"></a>アセンブリの署名とビルドを行うには  
  
1.  **[プロジェクト]** メニューの **[MyBuildContributor のプロパティ]** をクリックします。  
  
2.  **[署名]** タブをクリックします。  
  
3.  **[アセンブリの署名]** をクリックします。  
  
4.  **[厳密な名前のキー ファイルを選択してください]** で **[<New>]** をクリックします。  
  
5.  **[厳密な名前キーの作成]** ダイアログ ボックスで、 **[キー ファイル]** に「 **MyRefKey**」と入力します。  
  
6.  (省略可能) 厳密な名前のキー ファイルにパスワードを指定できます。  
  
7.  **[OK]** をクリックします。  
  
8.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
9. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  
  
    次に、アセンブリをインストールし、SQL プロジェクトのビルド時に読み込まれるようにします。  
  
## <a name="InstallBuildContributor"></a>ビルド コントリビューターのインストール  
ビルド コントリビューターをインストールするには、アセンブリおよび関連付けられた .pdb ファイルを Extensions フォルダーにコピーする必要があります。  
  
#### <a name="to-install-the-mybuildcontributor-assembly"></a>MyBuildContributor アセンブリをインストールするには  
  
1.  次に、アセンブリ情報を Extensions ディレクトリにコピーします。 Visual Studio の起動時に、%Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions ディレクトリとサブディレクトリ内のすべての拡張機能が認識され、使用できるようになります。  
  
2.  **MyBuildContributor.dll** アセンブリ ファイルを出力ディレクトリから %Program Files%\Microsoft SQL Server\110\DAC\Bin\Extensions ディレクトリにコピーします。  
  
    > [!NOTE]  
    > 既定では、コンパイル済みの .dll ファイルのパスは YourSolutionPath\YourProjectPath\bin\Debug または YourSolutionPath\YourProjectPath\bin\Release です。  
  
## <a name="TestBuildContributor"></a>ビルド コントリビューターの実行またはテスト  
ビルド コントリビューターを実行またはテストするには、次のタスクを実行する必要があります。  
  
-   ビルドする予定の .sqlproj ファイルにプロパティを追加する。  
  
-   MSBuild を使用し、適切なパラメーターを指定して、データベース プロジェクトをビルドする。  
  
### <a name="add-properties-to-the-sql-project-sqlproj-file"></a>SQL プロジェクト (.sqlproj) ファイルにプロパティを追加するには  
実行するコントリビューターの ID を指定するには、必ず SQL プロジェクト ファイルを更新する必要があります。 また、このビルド コントリビューターは MSBuild からコマンド ライン パラメーターを受け取るため、ユーザーが MSBuild を使用してこれらのパラメーターを渡すことができるように SQL プロジェクトを変更する必要があります。  
  
これは、次の 2 つの方法のいずれかで行うことができます。  
  
-   .sqlproj ファイルを手動で変更して、必要な引数を追加できます。 この方法は、多数のプロジェクト間でビルド コントリビューターを再利用しない場合に選択できます。 このオプションを選択した場合は、.sqlproj ファイル内の最初の Import ノードの後に次のステートメントを追加します。  
  
    ```  
    /// <PropertyGroup>  
    ///     <ContributorArguments Condition="'$(Configuration)' == 'Debug'">  
    ///         $(ContributorArguments);ModelStatistics.GenerateModelStatistics=true;ModelStatistics.SortModelStatisticsBy="name";  
    ///     </ContributorArguments>  
    /// <PropertyGroup>  
  
    ```  
  
-   もう 1 つの方法では、必要なコントリビューター引数を含むターゲット ファイルを作成します。 この方法は、既定値が含まれるため、複数のプロジェクトに同じコントリビューターを使用している場合に役立ちます。  
  
    この場合は、MSBuild 拡張機能のパスにターゲット ファイルを作成します。  
  
    1.  %Program Files%\MSBuild\\ に移動します。  
  
    2.  ターゲット ファイルの保存先となる新しいフォルダー "MyContributors" を作成します。  
  
    3.  このディレクトリ内に新しいファイル "MyContributors.targets" を作成し、次のテキストを追加して、ファイルを保存します。  
  
        ```  
        <?xml version="1.0" encoding="utf-8"?>  
  
        <Project xmlns="https://schemas.microsoft.com/developer/msbuild/2003">  
          <PropertyGroup>  
            <BuildContributors>$(BuildContributors);ExampleContributors.ModelStatistics</BuildContributors>  
            <ContributorArguments Condition="'$(Configuration)' == 'Debug'">$(ContributorArguments);ModelStatistics.GenerateModelStatistics=true;ModelStatistics.SortModelStatisticsBy=name;</ContributorArguments>  
          </PropertyGroup>  
        </Project>  
        ```  
  
    4.  コントリビューターを実行するプロジェクトの .sqlproj ファイル内で、\<Import Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets" \/> ノードの後に次のステートメントを追加してターゲット ファイルをインポートします。  
  
        ```  
        <Import Project="$(MSBuildExtensionsPath)\MyContributors\MyContributors.targets " />  
        ```  
  
上記の方法のいずれかを実行すると、MSBuild を使用して、コマンド ライン ビルドのパラメーターを渡すことができます。  
  
> [!NOTE]  
> コントリビューター ID を指定するには、必ず "BuildContributors" プロパティを更新する必要があります。 この ID は、コントリビューター ソース ファイル内の "ExportBuildContributor" 属性で使用されているのと同じ ID です。 これを指定しないと、プロジェクトのビルド時にコントリビューターが実行されません。 "ContributorArguments" プロパティは、コントリビューターの実行に必要な引数がある場合のみに更新する必要があります。  
  
### <a name="build-the-sql-project"></a>SQL プロジェクトのビルド  
  
##### <a name="to-rebuild-your-database-project-by-using-msbuild-and-generate-statistics"></a>MSBuild を使用してデータベース プロジェクトをビルドし直し、統計を生成するには  
  
1.  Visual Studio で、プロジェクトを右クリックし、[リビルド] をクリックします。 これにより、プロジェクトがビルドし直されます。生成されたモデルの統計が表示されると共に、出力はビルド出力に含まれ、ModelStatistics.xml に保存されます。 xml ファイルを表示するには、ソリューション エクスプローラーで [すべてのファイルを表示] を選択する必要があることに注意してください。  
  
2.  Visual Studio のコマンド プロンプトを開きます。これには、 **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft Visual Studio <Visual Studio Version>]** 、 **[Visual Studio Tools]** の順にクリックして、 **[Visual Studio コマンド プロンプト (<Visual Studio Version>)]** をクリックします。  
  
3.  コマンド プロンプトで、SQL プロジェクトが含まれているフォルダーに移動します。  
  
4.  コマンド プロンプトで、次のコマンドを入力します。  
  
    ```  
    MSBuild /t:Rebuild MyDatabaseProject.sqlproj /p:BuildContributors=$(BuildContributors);ExampleContributors.ModelStatistics /p:ContributorArguments=$(ContributorArguments);GenerateModelStatistics=true;SortModelStatisticsBy=name;OutDir=.\;  
    ```  
  
    *MyDatabaseProject* を、ビルドするデータベース プロジェクトの名前に置き換えます。 プロジェクトを最後にビルドした後に変更した場合は、/t:Rebuild ではなく /t:Build を使用できます。  
  
    出力では、次のようなビルド情報が表示されます。  
  
```  
Model Statistics:  
===  
  
Basic model info  
-----------------  
    Version: Sql110  
  Collation: SQL_Latin1_General_CP1_CI_AS  
  
UserDefinedElements  
-----------------  
  DatabaseOptions: 1  
         subtotal: 1  
      total items: 1  
  
OtherElements  
-----------------  
                Assembly: 1  
       BuiltInServerRole: 9  
           ClrTypeMethod: 218  
  ClrTypeMethodParameter: 197  
         ClrTypeProperty: 20  
                Contract: 6  
                DataType: 34  
                Endpoint: 5  
               Filegroup: 1  
             MessageType: 14  
                   Queue: 3  
                    Role: 10  
                  Schema: 13  
                 Service: 3  
                    User: 4  
         UserDefinedType: 3  
                subtotal: 541  
             total items: 16  
  
Relationships  
-----------------  
     Composing: 477  
  Hierarchical: 6  
          Peer: 19  
      subtotal: 502  
  
```  
  
1.  ModelStatistics.xml を開き、内容を確認します。  
  
    報告された結果は、XML ファイルにも保存されます。  
  
## <a name="next-steps"></a>Next Steps  
出力 XML ファイルの処理を実行するには、追加のツールを作成できます。 これは、ビルド コントリビューターの一例にすぎません。 たとえば、ビルドの一部としてデータ辞書ファイルを出力するビルド コントリビューターを作成できます。  
  
## <a name="see-also"></a>参照  
[ビルド コントリビューターと配置コントリビューターを使用してデータベースのビルドと配置をカスタマイズする](../ssdt/use-deployment-contributors-to-customize-database-build-and-deployment.md)  
[チュートリアル:配置計画を分析するためのデータベース プロジェクトの配置の拡張](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)  
  
