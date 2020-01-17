---
title: チュートリアル:カスタム テスト条件を使用してストアド プロシージャの結果を検証する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 4c33b494-a85e-4dd2-97b6-c88ee858a99c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6ef888bf2cf4259ec904194a39aa74ed44040586
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068982"
---
# <a name="walkthrough-using-a-custom-test-condition-to-verify-the-results-of-a-stored-procedure"></a>チュートリアル:カスタム テスト条件を使用してストアド プロシージャの結果を検証する
機能の拡張に関するこのチュートリアルでは、テスト条件を作成し、SQL Server の単体テストを作成して機能を検証します。 これには、テスト条件のクラス ライブラリ プロジェクトの作成およびクラス ライブラリ プロジェクトの署名とインストールが含まれます。 更新するテスト条件が既にある場合は、「[Visual Studio 2010 のカスタム テスト条件を、以前のリリースから SQL Server Data Tools にアップグレードする方法](../ssdt/how-to-upgrade-visual-studio-2010-custom-test-condition-to-ssdt.md)」を参照してください。  
  
このチュートリアルでは、次の作業について説明します。  
  
-   テスト条件を作成する方法。  
  
-   アセンブリに厳密な名前で署名する方法。  
  
-   必要な参照をプロジェクトに追加する方法。  
  
-   テスト条件をビルドする方法。  
  
-   新しいテスト条件をインストールする方法。  
  
-   新しいテスト条件をテストする方法。  
  
このチュートリアルを最後まで行うには、Visual Studio 2010 または Visual Studio 2012 と最新バージョンの SQL Server Data Tools が必要です。 詳しくは、「[SQL Server Data Tools のインストール](../ssdt/install-sql-server-data-tools.md)」をご覧ください。  
  
## <a name="creating-a-custom-test-condition"></a>カスタムのテスト条件を作成する  
まず、クラス ライブラリを作成します。  
  
1.  **[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。  
  
2.  **[新しいプロジェクト]** ダイアログ ボックスの **[プロジェクトの種類]** で、[Visual C\#] をクリックします。  
  
3.  **[テンプレート]** で、 **[クラス ライブラリ]** をクリックします。  
  
4.  **[名前]** テキスト ボックスに「**ColumnCountCondition**」と入力して、 **[OK]** をクリックします。  
  
次に、プロジェクトに署名します。  
  
1.  **[プロジェクト]** メニューの **[ColumnCountCondition のプロパティ]** をクリックします。  
  
2.  **[署名]** タブの **[アセンブリの署名]** チェック ボックスをオンにします。  
  
3.  **[厳密な名前のキー ファイルを選択してください]** で、 **[\<新規作成...>]** をクリックします。  
  
    **[厳密な名前キーの作成]** ダイアログ ボックスが表示されます。  
  
4.  **[キー ファイル]** ボックスに「**SampleKey**」と入力します。  
  
5.  パスワードを入力および確認し、 **[OK]** をクリックします。 ソリューションをビルドすると、キー ファイルを使用してアセンブリに署名されます。  
  
6.  **[ファイル]** メニューの **[すべてを保存]** をクリックします。  
  
7.  **[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  
  
次に、必要な参照をプロジェクトに追加します。  
  
1.  **ソリューション エクスプローラー**で、**ColumnCountCondition** プロジェクトを選択します。  
  
2.  **[プロジェクト]** メニューの **[参照の追加]** をクリックし、 **[参照の追加]** ダイアログ ボックスを表示します。  
  
3.  **[.NET]** タブを選択します。  
  
4.  **[コンポーネント名]** 列で、**System.ComponentModel.Composition** コンポーネントを探して選択します。 コンポーネントを選択した後、 **[OK]** をクリックします。  
  
5.  必要なアセンブリ参照を追加します。 プロジェクト ノードを右クリックし、 **[参照の追加]** をクリックします。 **[参照]** をクリックし、C:\Program Files (x86)\\MicrosoftSQL Server\110\DAC\Bin フォルダーに移動します。 Microsoft.Data.Tools.Schema.Sql.dll を選択し、[追加] をクリックして、[OK] をクリックします。  
  
6.  **[プロジェクト]** メニューの **[プロジェクトのアンロード]** をクリックします。  
  
7.  **ソリューション エクスプローラー**でプロジェクトを右クリックして、 **[<project name>.csproj の編集]** を選択します。  
  
8.  **Microsoft.CSharp.targets** をインポートした後、次の Import ステートメントを追加します。  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' == ''" />  
  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' != ''" />  
    ```  
  
9. ファイルを保存して閉じます。 **ソリューション エクスプローラー**でプロジェクトを右クリックして、 **[プロジェクトの再読み込み]** をクリックします。  
  
    **ソリューション エクスプローラー**で、プロジェクトの **[参照設定]** ノードの下に必要な参照が表示されます。  
  
## <a name="creating-the-resultsetcolumncountcondition-class"></a>ResultSetColumnCountCondition クラスを作成する  
**Class1** の名前を **ResultSetColumnCountCondition** に変更し、[testcondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) から派生するようにします。 **ResultSetColumnCountCondition** クラスは、ResultSet に返される列数を検証する簡単なテスト条件です。 この条件は、ストアド プロシージャのコントラクトに誤りがないことを確認するために使用できます。  
  
1.  **ソリューション エクスプローラー**で、Class1.cs を右クリックし、 **[名前の変更]** をクリックして「**ResultSetColumnCountCondition.cs**」と入力します。  
  
2.  **[はい]** をクリックして、Class1 へのすべての参照名の変更を確定します。  
  
3.  **ResultSetColumnCountCondition.cs** ファイルを開き、次の using ステートメントをファイルに追加します。  
  
    ```  
    using System;  
    using System.ComponentModel;  
    using System.Data;  
    using System.Data.Common;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
    using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
  
    namespace ColumnCountCondition {  
        public class ResultSetColumnCountCondition  
    ```  
  
4.  [testcondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) からクラスを派生します。  
  
    ```  
    public class ResultSetColumnCountCondition : TestCondition  
    ```  
  
5.  [ExportTestConditionAttribute](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.exporttestconditionattribute(v=vs.103).aspx) を追加します。 UnitTesting.Conditions.ExportTestConditionAttribute について詳しくは、「[SQL Server 単体テスト デザイナーのテスト条件を作成する方法](../ssdt/how-to-create-test-conditions-for-the-sql-server-unit-test-designer.md)」をご覧ください。  
  
    ```  
    [ExportTestCondition("ResultSet Column Count", typeof(ResultSetColumnCountCondition))]  
        public class ResultSetColumnCountCondition : TestCondition  
    ```  
  
6.  メンバー変数とコンストラクターを作成します。  
  
    ```  
            private int _resultSet;  
            private int _count;  
            private int _batch;  
  
            public ResultSetColumnCountCondition() {  
                _resultSet = 1;  
                _count = 0;  
                _batch = 1;  
            }  
    ```  
  
7.  **Assert** メソッドをオーバーライドします。 このメソッドは、**IDbConnection** (データベースへの接続を表します) と **SqlExecutionResult** を引数として受け取ります。 このメソッドは、エラー処理に **DataSchemaException** を使います。  
  
    ```  
           //method you need to override  
            //to perform the condition verification  
            public override void Assert(DbConnection validationConnection, SqlExecutionResult[] results)  
            {  
                //call base for parameter validation  
                base.Assert(validationConnection, results);  
  
                //verify batch exists  
                if (results.Length < _batch)  
                    throw new DataException(String.Format("Batch {0} does not exist", _batch));  
  
                SqlExecutionResult result = results[_batch - 1];  
  
                //verify resultset exists  
                if (result.DataSet.Tables.Count < ResultSet)  
                    throw new DataException(String.Format("ResultSet {0} does not exist", ResultSet));  
  
                DataTable table = result.DataSet.Tables[ResultSet - 1];  
  
                //actual condition verification  
                //verify resultset column count matches expected  
                if (table.Columns.Count != Count)  
                    throw new DataException(String.Format(  
                        "ResultSet {0}: {1} columns did not match the {2} columns expected",  
                        ResultSet, table.Columns.Count, Count));  
            }  
  
    Add the following method, which overrides the ToString method:  
    C#  
            //this method is called to provide the string shown in the  
            //test conditions panel grid describing what the condition tests  
            public override string ToString()  
            {  
                return String.Format(  
                    "Condition fails if ResultSet {0} does not contain {1} columns",  
                    ResultSet, Count);  
            }  
    ```  
  
8.  **CategoryAttribute**、**DisplayNameAttribute**、**DescriptionAttribute** の各属性を使って、次のテスト条件プロパティを追加します。  
  
    ```  
            //below are the test condition properties  
            //that are exposed to the user in the property browser  
            #region Properties  
  
            //property specifying the resultset for which  
            //you want to check the column count  
            [Category("Test Condition")]  
            [DisplayName("ResultSet")]  
            [Description("ResultSet Number")]  
            public int ResultSet  
            {  
                get { return _resultSet; }  
  
                set  
                {  
                    //basic validation  
                    if (value < 1)  
                        throw new ArgumentException("ResultSet cannot be less than 1");  
  
                    _resultSet = value;  
                }  
            }  
  
            //property specifying  
            //expected column count  
            [Category("Test Condition")]  
            [DisplayName("Count")]  
            [Description("Column Count")]  
            public int Count  
            {  
                get { return _count; }  
  
                set  
                {  
                    //basic validation  
                    if (value < 0)  
                        throw new ArgumentException("Count cannot be less than 0");  
  
                    _count = value;  
                }  
            }  
             #endregion  
    ```  
  
最終のコード リストを以下に示します。  
  
```  
using System;  
using System.ComponentModel;  
using System.Data;  
using System.Data.Common;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
  
namespace ColumnCountCondition  
{  
  
    [ExportTestCondition("ResultSet Column Count", typeof(ResultSetColumnCountCondition))]  
    public class ResultSetColumnCountCondition : TestCondition  
    {  
        private int _resultSet;  
        private int _count;  
        private int _batch;  
  
        public ResultSetColumnCountCondition()  
        {  
            _resultSet = 1;  
            _count = 0;  
            _batch = 1;  
        }  
  
        //method you need to override  
        //to perform the condition verification  
        public override void Assert(DbConnection validationConnection, SqlExecutionResult[] results)  
        {  
            //call base for parameter validation  
            base.Assert(validationConnection, results);  
  
            //verify batch exists  
            if (results.Length < _batch)  
                throw new DataException(String.Format("Batch {0} does not exist", _batch));  
  
            SqlExecutionResult result = results[_batch - 1];  
  
            //verify resultset exists  
            if (result.DataSet.Tables.Count < ResultSet)  
                throw new DataException(String.Format("ResultSet {0} does not exist", ResultSet));  
  
            DataTable table = result.DataSet.Tables[ResultSet - 1];  
  
            //actual condition verification  
            //verify resultset column count matches expected  
            if (table.Columns.Count != Count)  
                throw new DataException(String.Format(  
                    "ResultSet {0}: {1} columns did not match the {2} columns expected",  
                    ResultSet, table.Columns.Count, Count));  
        }  
  
        //this method is called to provide the string shown in the  
        //test conditions panel grid describing what the condition tests  
        public override string ToString()  
        {  
            return String.Format(  
                "Condition fails if ResultSet {0} does not contain {1} columns",  
                ResultSet, Count);  
        }  
  
        //below are the test condition properties  
        //that are exposed to the user in the property browser  
        #region Properties  
  
        //property specifying the resultset for which  
        //you want to check the column count  
        [Category("Test Condition")]  
        [DisplayName("ResultSet")]  
        [Description("ResultSet Number")]  
        public int ResultSet  
        {  
            get { return _resultSet; }  
  
            set  
            {  
                //basic validation  
                if (value < 1)  
                    throw new ArgumentException("ResultSet cannot be less than 1");  
  
                _resultSet = value;  
            }  
        }  
  
        //property specifying  
        //expected column count  
        [Category("Test Condition")]  
        [DisplayName("Count")]  
        [Description("Column Count")]  
        public int Count  
        {  
            get { return _count; }  
  
            set  
            {  
                //basic validation  
                if (value < 0)  
                    throw new ArgumentException("Count cannot be less than 0");  
  
                _count = value;  
            }  
        }  
  
        #endregion  
    }  
}  
  
```  
  
次に、プロジェクトをビルドします。  
  
## <a name="xxx"></a>プロジェクトをコンパイルしてテスト条件をインストールする  
**[ビルド]** メニューの **[ソリューションのビルド]** をクリックします。  
  
次に、アセンブリ情報を Extensions ディレクトリにコピーします。 Visual Studio が起動すると、%Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions ディレクトリとサブディレクトリ内のすべての機能拡張を識別し、使用できる状態にします。  
  
**ColumnCountCondition.dll** アセンブリ ファイルを、出力ディレクトリから %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions ディレクトリにコピーします。  
  
既定では、コンパイル済みの .dll ファイルのパスは *YourSolutionPath*\\*YourProjectPath*\bin\Debug または *YourSolutionPath*\\*YourProjectPath*\bin\Release です。  
  
次に、Visual Studio の新しいセッションを開始して、データベース プロジェクトを作成します。 新しい Visual Studio セッションを開始してデータベース プロジェクトを作成するには:  
  
1.  Visual Studio の 2 つ目のセッションを開始します。  
  
2.  **[ファイル]** メニューの **[新規作成]** をクリックし、 **[プロジェクト]** をクリックします。  
  
3.  **[新しいプロジェクト]** ダイアログ ボックスのインストール済みテンプレートの一覧で、 **[SQL Server]** ノードを選択します。  
  
4.  詳細ウィンドウで、 **[SQL Server データベース プロジェクト]** をクリックします。  
  
5.  **[名前]** テキスト ボックスに「**SampleConditionDB**」と入力して、 **[OK]** をクリックします。  
  
次に、単体テストを作成します。 新しいテスト クラス内に SQL Server の単体テストを作成するには:  
  
1.  **[テスト]** メニューの **[新しいテスト]** をクリックし、 **[新しいテストの追加]** ダイアログ ボックスを表示します。  
  
    また、**ソリューション エクスプローラー**でテスト プロジェクトを右クリックし、 **[追加]** をポイントして、 **[新しいテスト]** をクリックすることもできます。  
  
2.  テンプレートの一覧で、 **[SQL Server 単体テスト]** をクリックします。  
  
3.  **[テスト名]** に「**SampleUnitTest**」と入力します。  
  
4.  **[テスト プロジェクトに追加]** で、 **[新しい Visual C\# テスト プロジェクトの作成]** をクリックします。 続いて、 **[OK]** をクリックして **[新しいテスト プロジェクト]** ダイアログ ボックスを表示します。  
  
5.  プロジェクト名に「**SampleUnitTest**」と入力します。  
  
6.  **[キャンセル]** をクリックして、データベース接続を使用するテスト プロジェクトを構成せずに単体テストを作成します。 SQL Server 単体テスト デザイナーに、空白のテストが表示されます。 テスト プロジェクトに Visual C\# のソース コード ファイルが追加されます。  
  
    データベース接続が関連付けられたデータベース単体テストの作成および構成の詳細については、「[空の SQL Server の単体テストを作成する方法](../ssdt/how-to-create-an-empty-sql-server-unit-test.md)」を参照してください。  
  
7.  **[作成するにはここをクリックしてください]** をクリックし、単体テストの作成を完了します。 SQL Server プロジェクトに新しいテスト条件が表示されます。  
  
> [!NOTE]  
> 既存の単体テスト プロジェクトでカスタムのテスト条件を使用するには、1 つ以上の新しい SQL Server の単体テスト クラスを作成する必要があります。 テスト条件アセンブリへの必要な参照は、テスト クラスの作成時にテスト プロジェクトに追加されます。  
  
新しいテスト条件を表示するには、次の手順を実行します。  
  
1.  **SQL Server 単体テスト デザイナー**で、 **[テスト条件]** の **[名前]** 列にある inconclusiveCondition1 テストをクリックします。  
  
2.  **[テスト条件を削除します]** ツール バー ボタンをクリックして、inconclusiveCondition1 テストを削除します。  
  
3.  **[テスト条件]** ボックスをクリックし、 **[ResultSet 列数]** を選択します。  
  
4.  **[テスト条件を追加します]** ツール バー ボタンをクリックして、カスタムのテスト条件を追加します。  
  
5.  **[プロパティ]** ウィンドウで、Count プロパティ、Enabled プロパティ、および ResultSet プロパティを構成します。  
  
    詳細については、「[ソフト NUMA を使用するようにSQL Server の単体テストにテスト条件を追加する方法](../ssdt/how-to-add-test-conditions-to-sql-server-unit-tests.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストのカスタム テスト条件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
  
