---
title: 'チュートリアル: SQL Server のカスタムの静的コード分析ルール アセンブリを作成する | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: f7b6ed8c-a4e0-4e33-9858-a8aa40aef309
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6e2f103303a90837a899330952b6f69544b4c496
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659539"
---
# <a name="walkthrough-authoring-a-custom-static-code-analysis-rule-assembly-for-sql-server"></a>チュートリアル: SQL Server のカスタムの静的コード分析ルール アセンブリを作成する
このチュートリアルでは、SQL Server のコード分析ルールを作成する手順について説明します。 このチュートリアルで作成するルールは、ストアド プロシージャ、トリガー、および関数で WAITFOR DELAY ステートメントを回避する場合に使用します。  
  
このチュートリアルでは、次の手順を使用して、Transact\-SQL の静的コード分析のカスタム ルールを作成します。  
  
1.  クラス ライブラリを作成し、そのプロジェクトの署名を有効にして、必要な参照を追加します。  
  
2.  Visual C\# のカスタム ルール クラスを作成します。  
  
3.  2 つのヘルパー Visual C\# クラスを作成します。  
  
4.  作成した結果の DLL をインストールするには、Extensions ディレクトリにコピーします。  
  
5.  新しいコード分析ルールが設定されていることを確認します。  
  
**前提条件**  
  
このチュートリアルを実行するには、次のコンポーネントが必要です。  
  
-   Visual C\# または Visual Basic の開発をサポートする、SQL Server Data Tools を含む Visual Studio のバージョンがインストールされていること。  
  
-   SQL Server オブジェクトを含む SQL Server プロジェクト。  
  
-   データベース プロジェクトを配置できる SQL Server のインスタンス。  
  
> [!NOTE]  
> このチュートリアルは、既に SQL Server Data Tools の SQL Server 機能を使い慣れているユーザーを対象としています。 また、クラス ライブラリの作成方法、コード エディターを使用してクラスにコードを追加する方法など、Visual Studio の概念を理解している必要があります。  
  
## <a name="creating-a-custom-code-analysis-rule-for-sql-server"></a>SQL Server のカスタム コード分析ルールを作成する  
まずクラス ライブラリを作成します。 クラス ライブラリ プロジェクトを作成するには、次の操作を行います。  
  
1.  SampleRules という名前の Visual C\# または Visual Basic のクラス ライブラリ プロジェクトを作成します。  
  
2.  ファイル Class1.cs の名前を AvoidWaitForDelayRule.cs に変更します。  
  
3.  ソリューション エクスプローラーで、プロジェクト ノードを右クリックし、 **[参照の追加]** をクリックします。  
  
4.  [フレームワーク] タブで [System.ComponentModel.Composition] を選択します。  
  
5.  **[参照]** をクリックし、C:\Program Files (x86)\\MicrosoftSQL Server\120\SDK\Assemblies ディレクトリに移動して、Microsoft.SqlServer.TransactSql.ScriptDom.dll を選択します。次に、[OK] をクリックします。  
  
6.  次に、必要な DACFx 参照をインストールします。 **[参照]** をクリックし、<Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120 ディレクトリに移動します。 Microsoft.SqlServer.Dac.dll、Microsoft.SqlServer.Dac.Extensions.dll、および Microsoft.Data.Tools.Schema.Sql.dll の各エントリを選択し、 **[追加]** 、 **[OK]** の順にクリックします。  
  
    これで、DACFx バイナリが Visual Studio インストール ディレクトリ内にインストールされます。 Visual Studio 2012 の場合、通常、<Visual Studio Install Dir> は C:\Program Files (x86)\\MicrosoftVisual Studio 11.0 になります。 Visual Studio 2013 の場合、通常は C:\Program Files (x86)\\MicrosoftVisual Studio 12.0 です。  
  
次に、ルールに使用するサポート クラスを追加します。  
  
## <a name="creating-the-custom-code-analysis-rule-supporting-classes"></a>カスタム コード分析ルールのサポート クラスを作成する  
ルール用のクラスを作成する前に、ビジター クラスと属性クラスをプロジェクトに追加します。 これらのクラスは、追加のカスタム ルールを作成するときに便利なことがあります。  
  
最初に定義する必要があるクラスは、WaitForDelayVisitor クラスです。このクラスは、[TSqlConcreteFragmentVisitor](https://docs.microsoft.com/en-us/dotnet/api/microsoft.sqlserver.transactsql.scriptdom.tsqlconcretefragmentvisitor) から派生します。 このクラスを使用すると、モデル内の WAITFOR DELAY ステートメントにアクセスできます。 ビジター クラスは、SQL Server で提供される [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) API を利用します。 この API の Transact\-SQL コードは、抽象構文ツリー (AST) として表されます。ビジター クラスは、WAITFORDELAY ステートメントなど、特定の構文オブジェクトを探すときに便利です。 構文オブジェクトは、特定のオブジェクト プロパティや関係に関連付けられていないので、オブジェクト モデルを使用して見つけるのは難しいことがありますが、ビジター パターンと [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) API を使用すると、簡単に見つかります。  
  
### <a name="defining-the-waitfordelayvisitor-class"></a>WaitForDelayVisitor クラスを定義する  
  
1.  **ソリューション エクスプローラー**で、SampleRules プロジェクトを選択します。  
  
2.  **[プロジェクト]** メニューで、 **[クラスの追加]** を選択します。 **[新しい項目の追加]** ダイアログ ボックスが表示されます。  
  
3.  **[名前]** テキスト ボックスに「WaitForDelayVisitor.cs」と入力し、 **[追加]** ボタンをクリックします。 WaitForDelayVisitor.cs ファイルは、**ソリューション エクスプローラー**のプロジェクトに追加されます。  
  
4.  WaitForDelayVisitor.cs ファイルを開き、次のコードに合わせて内容を更新します。  
  
    ```  
    using System.Collections.Generic;  
    using Microsoft.SqlServer.TransactSql.ScriptDom;  
    namespace SampleRules {  
        class WaitForDelayVistor {}  
    }  
    ```  
  
5.  クラス宣言で、アクセス修飾子を internal に変更し、TSqlConcreteFragmentVisitor からクラスを派生させます。  
  
    ```  
    internal class WaitForDelayVisitor : TSqlConcreteFragmentVisitor {}  
    ```  
  
6.  次のコードを追加して、List メンバー変数を定義します。  
  
    ```  
    public IList<WaitForStatement> WaitForDelayStatements { get; private set; }  
    ```  
  
7.  次のコードを追加して、クラス コンストラクターを定義します。  
  
    ```  
    public WaitForDelayVisitor() {  
       WaitForDelayStatments = new List<WaitForStatement>();  
    }  
    ```  
  
8.  次のコードを追加して、ExplicitVisit メソッドをオーバーライドします。  
  
    ```  
    public override void ExplicitVisit(WaitForStatement node) {  
       // We are only interested in WAITFOR DELAY occurrences  
       if (node.WaitForOption == WaitForOption.Delay)  
          WaitForDelayStatments.Add(node);  
    }  
    ```  
  
    このメソッドは、モデル内の WAITFOR ステートメントにアクセスし、DELAY オプションを指定したステートメントを WAITFOR DELAY ステートメントの一覧に追加します。 ここで参照するキー クラスは、[WaitForStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.waitforstatement.aspx) です。  
  
9. **[ファイル]** メニューの **[保存]** をクリックします。  
  
2 つ目のクラスは、LocalizedExportCodeAnalysisRuleAttribute.cs です。 このクラスは、フレームワークに用意されている組み込みの Microsoft.SqlServer.Dac.CodeAnalysis.ExportCodeAnalysisRuleAttribute の拡張機能です。リソース ファイルのルールで使用される DisplayName と Description の読み取りをサポートしています。 このクラスは、複数の言語でルールを使用する予定がある場合に便利です。  
  
### <a name="defining-the-localizedexportcodeanalysisruleattribute-class"></a>LocalizedExportCodeAnalysisRuleAttribute クラスを定義する  
  
1.  **ソリューション エクスプローラー**で、SampleRules プロジェクトを選択します。  
  
2.  **[プロジェクト]** メニューで、 **[クラスの追加]** を選択します。 **[新しい項目の追加]** ダイアログ ボックスが表示されます。  
  
3.  **[名前]** テキスト ボックスに「LocalizedExportCodeAnalysisRuleAttribute.cs」と入力し、 **[追加]** ボタンをクリックします。 ファイルは、**ソリューション エクスプローラー**のプロジェクトに追加されます。  
  
4.  ファイルを開き、次のコードに合わせて内容を更新します。  
  
    ```  
    using Microsoft.SqlServer.Dac.CodeAnalysis;  
    using System;  
    using System.Globalization;  
    using System.Reflection;  
    using System.Resources;  
  
    namespace SampleRules  
    {  
  
        internal class LocalizedExportCodeAnalysisRuleAttribute : ExportCodeAnalysisRuleAttribute  
        {  
            private readonly string _resourceBaseName;  
            private readonly string _displayNameResourceId;  
            private readonly string _descriptionResourceId;  
  
            private ResourceManager _resourceManager;  
            private string _displayName;  
            private string _descriptionValue;  
  
            /// <summary>  
            /// Creates the attribute, with the specified rule ID, the fully qualified  
            /// name of the resource file that will be used for looking up display name  
            /// and description, and the Ids of those resources inside the resource file.  
            /// </summary>  
            public LocalizedExportCodeAnalysisRuleAttribute(  
                string id,  
                string resourceBaseName,  
                string displayNameResourceId,  
                string descriptionResourceId)  
                : base(id, null)  
            {  
                _resourceBaseName = resourceBaseName;  
                _displayNameResourceId = displayNameResourceId;  
                _descriptionResourceId = descriptionResourceId;  
            }  
  
            /// <summary>  
            /// Rules in a different assembly would need to overwrite this  
            /// </summary>  
            /// <returns></returns>  
            protected virtual Assembly GetAssembly()  
            {  
                return GetType().Assembly;  
            }  
  
            private void EnsureResourceManagerInitialized()  
            {  
                var resourceAssembly = GetAssembly();  
  
                try  
                {  
                    _resourceManager = new ResourceManager(_resourceBaseName, resourceAssembly);  
                }  
                catch (Exception ex)  
                {  
                    var msg = String.Format(CultureInfo.CurrentCulture, RuleResources.CannotCreateResourceManager, _resourceBaseName, resourceAssembly);  
                    throw new RuleException(msg, ex);  
                }  
            }  
  
            private string GetResourceString(string resourceId)  
            {  
                EnsureResourceManagerInitialized();  
                return _resourceManager.GetString(resourceId, CultureInfo.CurrentUICulture);  
            }  
  
            /// <summary>  
            /// Overrides the standard DisplayName and looks up its value inside a resources file  
            /// </summary>  
            public override string DisplayName  
            {  
                get  
                {  
                    if (_displayName == null)  
                    {  
                        _displayName = GetResourceString(_displayNameResourceId);  
                    }  
                    return _displayName;  
                }  
            }  
  
            /// <summary>  
            /// Overrides the standard Description and looks up its value inside a resources file  
            /// </summary>  
            public override string Description  
            {  
                get  
                {  
                    if (_descriptionValue == null)  
                    {   
                        _descriptionValue = GetResourceString(_descriptionResourceId);  
                    }  
                    return _descriptionValue;  
                }  
            }  
        }  
    }  
    ```  
  
次に、ルール名、ルールの説明、およびカテゴリを定義したリソース ファイルを追加します。このルールは、ルール構成インターフェイスに表示されます。  
  
### <a name="to-add-a-resource-file-and-three-resource-strings"></a>リソース ファイルと 3 つのリソース文字列を追加するには  
  
1.  **ソリューション エクスプローラー**で、SampleRules プロジェクトを選択します。  
  
2.  **[プロジェクト]** メニューで、 **[新しい項目の追加]** を選択します。 **[新しい項目の追加]** ダイアログ ボックスが表示されます。  
  
3.  **[インストールされたテンプレート]** の一覧で、 **[全般]** をクリックします。  
  
4.  詳細ウィンドウの **[リソース ファイル]** をクリックします。  
  
5.  **[名前]** に「RuleResources.resx」と入力します。 リソースが定義されていないリソース エディターが表示されます。  
  
6.  次のように、4 つのリソース文字列を定義します。  
  
    |[オブジェクト名]|[値]|  
    |--------|---------|  
    |AvoidWaitForDelay_ProblemDescription|WAITFOR DELAY ステートメントは {0} にありました。|  
    |AvoidWaitForDelay_RuleName|ストアド プロシージャ、関数、およびトリガーで WaitFor Delay ステートメントの使用を回避します。|  
    |CategorySamples|SamplesCategory|  
    |CannotCreateResourceManager|{1} から {0} の ResourceManager は作成できません。|  
  
7.  **[ファイル]** メニューで、 **[RuleResources.resx の保存]** をクリックします。  
  
次に、ユーザー インターフェイスにルールに関する情報を表示するときに Visual Studio で使用されるリソース ファイル内のリソースを参照するクラスを定義します。  
  
### <a name="defining-the-sampleconstants-class"></a>SampleConstants クラスを定義する  
  
1.  **ソリューション エクスプローラー**で、SampleRules プロジェクトを選択します。  
  
2.  **[プロジェクト]** メニューで、 **[クラスの追加]** を選択します。 **[新しい項目の追加]** ダイアログ ボックスが表示されます。  
  
3.  **[名前]** テキスト ボックスに「SampleRuleConstants.cs」と入力し、 **[追加]** ボタンをクリックします。 SampleRuleConstants.cs ファイルは、**ソリューション エクスプローラー**のプロジェクトに追加されます。  
  
4.  SampleRuleConstants.cs ファイルを開き、次の using ステートメントをファイルに追加します。  
  
    ```  
    namespace SampleRules  
    {   
        internal static class RuleConstants  
        {  
            /// <summary>  
            /// The name of the resources file to use when looking up rule resources  
            /// </summary>  
            public const string ResourceBaseName = "Public.Dac.Samples.Rules.RuleResources";  
  
            /// <summary>  
            /// Lookup name inside the resources file for the select asterisk rule name  
            /// </summary>  
            public const string AvoidWaitForDelay_RuleName = "AvoidWaitForDelay_RuleName";  
            /// <summary>  
            /// Lookup ID inside the resources file for the select asterisk description  
            /// </summary>  
            public const string AvoidWaitForDelay_ProblemDescription = "AvoidWaitForDelay_ProblemDescription";  
  
            /// <summary>  
            /// The design category (should not be localized)  
            /// </summary>  
            public const string CategoryDesign = "Design";  
  
            /// <summary>  
            /// The performance category (should not be localized)  
            /// </summary>  
            public const string CategoryPerformance = "Design";  
        }  
    }  
    ```  
  
5.  **[ファイル]**  >  **[保存]** をクリックします。  
  
## <a name="creating-the-custom-code-analysis-rule-class"></a>カスタム コード分析ルール クラスを作成する  
以上の手順で、カスタム コード分析ルールで使用するヘルパー クラスを追加したら、カスタム ルール クラスを作成し、AvoidWaitForDelayRule という名前を付けます。 データベースの開発時に、AvoidWaitForDelayRule カスタム ルールを使用すると、ストアド プロシージャ、トリガー、および関数で WAITFOR DELAY ステートメントを回避できます。  
  
### <a name="creating-the-avoidwaitfordelayrule-class"></a>AvoidWaitForDelayRule クラスを作成する  
  
1.  **ソリューション エクスプローラー**で、SampleRules プロジェクトを選択します。  
  
2.  **[プロジェクト]** メニューで、 **[クラスの追加]** を選択します。 **[新しい項目の追加]** ダイアログ ボックスが表示されます。  
  
3.  **[名前]** テキスト ボックスに「AvoidWaitForDelayRule.cs」と入力し、 **[追加]** をクリックします。 AvoidWaitForDelayRule.cs ファイルは、**ソリューション エクスプローラー**のプロジェクトに追加されます。  
  
4.  AvoidWaitForDelayRule.cs ファイルを開き、次の using ステートメントをファイルに追加します。  
  
    ```  
    using Microsoft.SqlServer.Dac.CodeAnalysis;  
    using Microsoft.SqlServer.Dac.Model;  
    using Microsoft.SqlServer.TransactSql.ScriptDom;  
    using System;  
    using System.Collections.Generic;  
    using System.Globalization;   
    namespace SampleRules {  
        class AvoidWaitForDelayRule {}  
    }  
    ```  
  
5.  AvoidWaitForDelayRule クラス宣言で、アクセス修飾子を public に変更します。  
  
    ```  
    /// <summary>  
    /// This is a rule that returns a warning message   
    /// whenever there is a WAITFOR DELAY statement appears inside a subroutine body.  
    /// This rule only applies to stored procedures, functions and triggers.  
    /// </summary>  
    public sealed class AvoidWaitForDelayRule  
    ```  
  
6.  Microsoft.SqlServer.Dac.CodeAnalysis.SqlCodeAnalysisRule 基本クラスから AvoidWaitForDelayRule クラスを派生させます。  
  
    ```  
    public sealed class AvoidWaitForDelayRule : SqlCodeAnalysisRule  
    ```  
  
7.  LocalizedExportCodeAnalysisRuleAttribute をクラスに追加します。  
  
    LocalizedExportCodeAnalysisRuleAttribute を使用すると、コード分析サービスでカスタム コード分析ルールを検出できます。 コード分析では、ExportCodeAnalysisRuleAttribute (またはこの属性から継承している属性) でマークしたクラスのみを使用できます。  
  
    LocalizedExportCodeAnalysisRuleAttribute には、サービスに使用する必要があるメタデータがいくつか用意されています。 たとえば、このルールの一意の ID、Visual Studio ユーザー インターフェイスに表示される表示名、問題を特定するときにルールに使用できる説明などです。  
  
    ```  
    [LocalizedExportCodeAnalysisRule(AvoidWaitForDelayRule.RuleId,  
        RuleConstants.ResourceBaseName,  
        RuleConstants.AvoidWaitForDelay_RuleName,   
        RuleConstants.AvoidWaitForDelay_ProblemDescription  
        Category = RuleConstants.CategoryPerformance,   
        RuleScope = SqlRuleScope.Element)]   
    public sealed class AvoidWaitForDelayRule : SqlCodeAnalysisRule  
    {  
       /// <summary>  
       /// The Rule ID should resemble a fully-qualified class name. In the Visual Studio UI  
       /// rules are grouped by "Namespace + Category", and each rule is shown using "Short ID: DisplayName".  
       /// For this rule, that means the grouping will be "Public.Dac.Samples.Performance", with the rule  
       /// shown as "SR1004: Avoid using WaitFor Delay statements in stored procedures, functions and triggers."  
       /// </summary>  
       public const string RuleId = "RuleSamples.SR1004";  
    }  
    ```  
  
    このルールでは特定の要素を分析するため、RuleScope プロパティを Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleScope.Element にする必要があります。 このルールは、モデル内の一致する要素ごとに 1 回呼び出されます。 モデル全体を分析する場合は、Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleScope.Model を代わりに使用できます。  
  
8.  Microsoft.SqlServer.Dac.CodeAnalysis.SqlAnalysisRule.SupportedElementTypes を設定するコンストラクターを追加します。 要素がスコープのルールの場合は必須です。 このルールを適用する要素の種類を定義します。 この場合、ルールはストアド プロシージャ、トリガー、および関数に適用されます。 Microsoft.SqlServer.Dac.Model.ModelSchema クラスでは、分析に使用できるすべての要素の種類が一覧表示されることに注意してください。  
  
    ```  
    public AvoidWaitForDelayRule()  
    {  
       // This rule supports Procedures, Functions and Triggers. Only those objects will be passed to the Analyze method  
       SupportedElementTypes = new[]  
       {  
          // Note: can use the ModelSchema definitions, or access the TypeClass for any of these types  
          ModelSchema.ExtendedProcedure,  
          ModelSchema.Procedure,  
          ModelSchema.TableValuedFunction,  
          ModelSchema.ScalarFunction,  
  
          ModelSchema.DatabaseDdlTrigger,  
          ModelSchema.DmlTrigger,  
          ModelSchema.ServerDdlTrigger  
       };  
    }  
    ```  
  
9. 入力パラメーターとして Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleExecutionContext を使用する、Microsoft.SqlServer.Dac.CodeAnalysis.SqlAnalysisRule.Analyze(Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleExecutionContext) メソッドのオーバーライドを追加します。 このメソッドは、可能性のある問題の一覧を返します。  
  
    また、コンテキスト パラメーターから Microsoft.SqlServer.Dac.Model.TSqlModel、Microsoft.SqlServer.Dac.Model.TSqlObject、および [TSqlFragment](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.tsqlfragment.aspx) を取得します。 次に、モデル内のすべての WAITFOR DELAY ステートメントの一覧を取得するために、WaitForDelayVisitor クラスが使用されます。  
  
    その一覧の [WaitForStatement](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.waitforstatement.aspx) ごとに、Microsoft.SqlServer.Dac.CodeAnalysis.SqlRuleProblem が作成されます。  
  
    ```  
    /// <summary>  
    /// For element-scoped rules the Analyze method is executed once for every matching   
    /// object in the model.   
    /// </summary>  
    /// <param name="ruleExecutionContext">The context object contains the TSqlObject being   
    /// analyzed, a TSqlFragment  
    /// that's the AST representation of the object, the current rule's descriptor, and a   
    /// reference to the model being  
    /// analyzed.  
    /// </param>  
    /// <returns>A list of problems should be returned. These will be displayed in the Visual   
    /// Studio error list</returns>  
    public override IList<SqlRuleProblem> Analyze(  
        SqlRuleExecutionContext ruleExecutionContext)  
    {  
         IList<SqlRuleProblem> problems = new List<SqlRuleProblem>();  
  
         TSqlObject modelElement = ruleExecutionContext.ModelElement;  
  
         // this rule does not apply to inline table-valued function  
         // we simply do not return any problem in that case.  
         if (IsInlineTableValuedFunction(modelElement))  
         {  
             return problems;  
         }  
  
         string elementName = GetElementName(ruleExecutionContext, modelElement);  
  
         // The rule execution context has all the objects we'll need, including the   
         // fragment representing the object,  
         // and a descriptor that lets us access rule metadata  
         TSqlFragment fragment = ruleExecutionContext.ScriptFragment;  
         RuleDescriptor ruleDescriptor = ruleExecutionContext.RuleDescriptor;  
  
         // To process the fragment and identify WAITFOR DELAY statements we will use a   
         // visitor   
         WaitForDelayVisitor visitor = new WaitForDelayVisitor();  
         fragment.Accept(visitor);  
         IList<WaitForStatement> waitforDelayStatements = visitor.WaitForDelayStatements;  
  
         // Create problems for each WAITFOR DELAY statement found   
         // When creating a rule problem, always include the TSqlObject being analyzed. This   
         // is used to determine  
         // the name of the source this problem was found in and a best guess as to the   
         // line/column the problem was found at.  
         //  
         // In addition if you have a specific TSqlFragment that is related to the problem   
         //also include this  
         // since the most accurate source position information (start line and column) will   
         // be read from the fragment  
         foreach (WaitForStatement waitForStatement in waitforDelayStatements)  
         {  
            SqlRuleProblem problem = new SqlRuleProblem(  
                String.Format(CultureInfo.CurrentCulture,   
                    ruleDescriptor.DisplayDescription, elementName),  
                modelElement,  
                waitForStatement);  
            problems.Add(problem);  
        }  
        return problems;  
    }  
  
    private static string GetElementName(  
        SqlRuleExecutionContext ruleExecutionContext,   
        TSqlObject modelElement)  
    {  
        // Get the element name using the built in DisplayServices. This provides a number of   
        // useful formatting options to  
        // make a name user-readable  
        var displayServices = ruleExecutionContext.SchemaModel.DisplayServices;  
        string elementName = displayServices.GetElementName(  
            modelElement, ElementNameStyle.EscapedFullyQualifiedName);  
        return elementName;  
    }  
  
    private static bool IsInlineTableValuedFunction(TSqlObject modelElement)  
    {  
        return TableValuedFunction.TypeClass.Equals(modelElement.ObjectType)  
                       && FunctionType.InlineTableValuedFunction ==   
            modelElement.GetMetadata<FunctionType>(TableValuedFunction.FunctionType);  
    }  
    ```  
  
10. **[ファイル]**  >  **[保存]** をクリックします。  
  
### <a name="building-the-class-library"></a>クラス ライブラリをビルドする  
  
1.  **[プロジェクト]** メニューの **[SampleRules のプロパティ]** をクリックします。  
  
2.  **[署名]** タブをクリックします。  
  
3.  **[アセンブリの署名]** をクリックします。  
  
4.  **[厳密な名前のキー ファイルを選択してください]** で **[<New>]** をクリックします。  
  
5.  **[厳密な名前キーの作成]** ダイアログ ボックスで、 **[キー ファイル]** に「MyRefKey」と入力します。  
  
6.  (省略可能) 厳密な名前のキー ファイルにパスワードを指定できます。  
  
7.  **[OK]** をクリックします。  
  
8.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
9. **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  
  
次に、アセンブリをインストールし、SQL Server プロジェクトをビルドして配置するときに読み込まれるようにします。  
  
## <a name="install-a-static-code-analysis-rule"></a>静的コード分析ルールのインストール  
ルールをインストールするには、アセンブリおよび関連付けられた .pdb ファイルを Extensions フォルダーにコピーする必要があります。  
  
### <a name="to-install-the-samplerules-assembly"></a>SampleRules アセンブリをインストールするには  
次に、アセンブリ情報を Extensions ディレクトリにコピーします。 Visual Studio が起動すると、<Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120\Extensions ディレクトリとサブディレクトリの機能拡張が特定され、使用できるようになります。  
  
Visual Studio 2012 の場合、通常、<Visual Studio Install Dir> は C:\Program Files (x86)\\MicrosoftVisual Studio 11.0 になります。 Visual Studio 2013 の場合、通常は C:\Program Files (x86)\\MicrosoftVisual Studio 12.0 です。  
  
出力ディレクトリの SampleRules.dll アセンブリ ファイルを <Visual Studio Install Dir>\Common7\IDE\Extensions\\Microsoft\SQLDB\DAC\120\Extensions ディレクトリにコピーします。 既定では、コンパイル済みの .dll ファイルのパスは YourSolutionPath\YourProjectPath\bin\Debug または YourSolutionPath\YourProjectPath\bin\Release です。  
  
以上でルールのインストールは完了です。Visual Studio を再起動すると、ルールが表示されます。 次に、Visual Studio の新しいセッションを開始して、データベース プロジェクトを作成します。  
  
### <a name="starting-a-new-visual-studio-session-and-creating-a-database-project"></a>新しい Visual Studio セッションの開始とデータベース プロジェクトの作成  
  
1.  Visual Studio の 2 つ目のセッションを開始します。  
  
2.  **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順にクリックします。  
  
3.  **[新しいプロジェクト]** ダイアログ ボックスの **[インストールされたテンプレート]** の一覧で、 **[SQL Server]** ノードを展開し、 **[SQL Server データベース プロジェクト]** をクリックします。  
  
4.  **[名前]** テキスト ボックスに「SampleRulesDB」と入力し、 **[OK]** をクリックします。  
  
最後に、SQL Server プロジェクトに新しいルールが表示されます。 新しい AvoidWaitForRule コード分析ルールを表示するには:  
  
1.  **ソリューション エクスプローラー**で、SampleRulesDB プロジェクトを選択します。  
  
2.  **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 [SampleRulesDB のプロパティ] ページが表示されます。  
  
3.  **[コード分析]** をクリックします。 RuleSamples.CategorySamples という新しいカテゴリが表示されます。  
  
4.  RuleSamples .CategorySamples を展開します。 "SR1004:Avoid WAITFOR DELAY statement in stored procedures, triggers, and functions" (SR1004: ストアド プロシージャ、関数、トリガーで WaitFor Delay ステートメントを使用しないでください) と表示されます。  
  
## <a name="see-also"></a>参照  
[データベース コード分析ルールの機能拡張の概要](../ssdt/overview-of-extensibility-for-database-code-analysis-rules.md)  
  
