---
title: 方法:SQL Server 単体テスト デザイナーのテスト条件を作成する | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 48076062-1ef5-419a-8a55-3c7b4234cc35
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6406c2e2ff709e163057163424719169cb2b9787
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911790"
---
# <a name="how-to-create-test-conditions-for-the-sql-server-unit-test-designer"></a>方法:SQL Server 単体テスト デザイナーのテスト条件を作成する
新しいテスト条件の作成には、拡張可能な [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) クラスを利用できます。 たとえば、列数や結果セットの値を検証するテスト条件を作成することができます。  
  
## <a name="to-create-a-test-condition"></a>テスト条件を作成するには  
この手順では、SQL Server 単体テスト デザイナーに表示されるテスト条件を作成する方法について説明します。  
  
1.  Visual Studio でクラス ライブラリ プロジェクトを作成します。  
  
2.  **[プロジェクト]** メニューの **[参照の追加]** をクリックします。  
  
3.  **[.NET]** タブをクリックします。  
  
4.  **[コンポーネント名]** の一覧で **System.ComponentModel.Composition** を選択し、 **[OK]** をクリックします。  
  
5.  必要なアセンブリ参照を追加します。 プロジェクト ノードを右クリックし、 **[参照の追加]** をクリックします。 **[参照]** をクリックし、C:\Program Files (x86)\\MicrosoftSQL Server\110\DAC\Bin フォルダーに移動します。 Microsoft.Data.Tools.Schema.Sql.dll を選択し、[追加] をクリックして、[OK] をクリックします。  
  
6.  **[プロジェクト]** メニューの **[プロジェクトのアンロード]** をクリックします。  
  
7.  **ソリューション エクスプローラー**でプロジェクトを右クリックして、 **[<project name>.csproj の編集]** を選択します。  
  
8.  Microsoft.CSharp.targets をインポートした後、次の Import ステートメントを追加します。  
  
    ```  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' == ''" />  
    <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.Sql.UnitTesting.targets" Condition="'$(VisualStudioVersion)' != ''" />  
    ```  
  
9. ファイルを保存して閉じます。 **ソリューション エクスプローラー**でプロジェクトを右クリックして、 **[プロジェクトの再読み込み]** をクリックします。  
  
10. [TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) クラスから、独自のクラスを派生します。  
  
11. アセンブリに厳密な名前で署名します。 詳細については、「[ソフト NUMA を使用するように厳密な名前でアセンブリに署名する](https://msdn.microsoft.com/library/xc31ft41.aspx)」を参照してください。  
  
12. クラス ライブラリをビルドします。  
  
13. 新しいテスト条件を使用できるようにするには、署名したアセンブリを %Program Files%\Microsoft Visual Studio <Version>\Common7\IDE\Extensions\Microsoft\SQLDB\TestConditions フォルダーにコピーする必要があります。 このフォルダーが存在しない場合は作成します。 このディレクトリにコピーするには、コンピューターの管理特権が必要です。  
  
14. テスト条件をインストールします。 詳しくは、「[SQL Server の単体テストのカスタム テスト条件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)」をご覧ください。  
  
15. 新しい SQL Server の単体テストをプロジェクトに追加し、プロジェクトに追加されるテスト条件への参照を作成します。 プロジェクトのテスト条件アセンブリに手動で参照を追加することができます。 この手順を実行した後は、デザイナーを読み込み直します。  
  
    > [!NOTE]  
    > 参照を作成するには、テスト クラスの追加が必要です。 参照を追加したら、このテスト クラスは削除してかまいません。  
  
次の例では、ResultSet に返される列数を検証する簡単なテスト条件を作成します。 この簡単なテスト条件は、ストアド プロシージャのコントラクトに誤りがないことを確認するために使用できます。  
  
```  
using System;  
using System.ComponentModel;  
using System.Data;  
using System.Data.Common;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting;  
using Microsoft.Data.Tools.Schema.Sql.UnitTesting.Conditions;  
  
namespace Ssdt.Samples.SqlUnitTesting  
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
  
        // method you need to override  
        // to perform the condition verification  
        public override void Assert(DbConnection validationConnection, SqlExecutionResult[] results)  
        {  
            // call base for parameter validation  
            base.Assert(validationConnection, results);  
  
            // verify batch exists  
            if (results.Length < _batch)  
                throw new DataException(String.Format("Batch {0} does not exist", _batch));  
  
            SqlExecutionResult result = results[_batch - 1];  
  
            // verify resultset exists  
            if (result.DataSet.Tables.Count < ResultSet)  
                throw new DataException(String.Format("ResultSet {0} does not exist", ResultSet));  
  
            DataTable table = result.DataSet.Tables[ResultSet - 1];  
  
            // actual condition verification  
            // verify resultset column count matches expected  
            if (table.Columns.Count != Count)  
                throw new DataException(String.Format(  
                    "ResultSet {0}: {1} columns did not match the {2} columns expected",  
                    ResultSet, table.Columns.Count, Count));  
        }  
  
        // this method is called to provide the string shown in the  
        // test conditions panel grid describing what the condition tests  
        public override string ToString()  
        {  
            return String.Format(  
                "Condition fails if ResultSet {0} does not contain {1} columns",  
                ResultSet, Count);  
        }  
  
        // below are the test condition properties  
        // that are exposed to the user in the property browser  
        #region Properties  
  
        // property specifying the resultset for which  
        // you want to check the column count  
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
  
        // property specifying  
        // expected column count  
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
  
カスタムのテスト条件のクラスは、[TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) 基本クラスから継承します。 カスタムのテスト条件のインストール後は、条件の追加プロパティを使用して、[プロパティ] ウィンドウから条件を構成できます。  
  
[TestCondition](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.testcondition(v=vs.103).aspx) を拡張したクラスに [ExportTestConditionAttribute](https://msdn.microsoft.com/library/microsoft.data.tools.schema.sql.unittesting.conditions.exporttestconditionattribute(v=vs.103).aspx) を追加する必要があります。 この属性により、このクラスは SQL Server Data Tools で探索可能になり、単体テストの設計および実行中に使用できるようになります。 この属性は、次の 2 つのパラメーターを受け取ります。  
  
|属性パラメーター|[位置]|[説明]|  
|-----------------------|------------|---------------|  
|DisplayName|1|[テスト条件] ボックスの文字列を識別します。 この名前は一意である必要があります。 2 つの条件に同じ表示名が付いている場合、ユーザーには最初に検出された条件が表示され、Visual Studio エラー マネージャーに警告が表示されます。|  
|ImplementingType|2|拡張型を一意に識別するために使用されます。 属性を配置する型に一致するように、このパラメーターを変更する必要があります。 この例では、**ResultSetColumnCountCondition** 型を使用しているため、**typeof(ResultSetColumnCountCondition)** を使用します。 型が **NewTestCondition** である場合は、**typeof(NewTestCondition)** を使用します。|  
  
この例では、2 つのプロパティを追加します。 カスタムのテスト条件では、ResultSet プロパティで、列数の検証に使用する結果セットを指定できます。 さらに、Count プロパティで、予期される列数を指定できます。  
  
プロパティごとに 3 つの属性が追加されます。  
  
-   プロパティの整理に使用するカテゴリ名。  
  
-   プロパティの表示名。  
  
-   プロパティの説明。  
  
プロパティの検証が実行され、ResultSet プロパティの値が 1 以上かどうか、および Count プロパティの値が 0 以上かどうかが検証されます。  
  
Assert メソッドで、テスト条件の主要なタスクを実行します。 Assert メソッドをオーバーライドして、予期される条件が満たされているかどうかを検証します。 このメソッドは、次の 2 つのパラメーターを渡します。  
  
-   1 つ目のパラメーターは、データベース接続で、テスト条件の検証に使用されます。  
  
-   2 つ目は、より重要なパラメーターの結果配列で、実行されたバッチごとに 1 つ配列要素を返します。  
  
テスト スクリプトごとにサポートされるバッチは 1 つのみです。 そのため、テスト条件では、常に最初の配列要素を調べます。 この配列要素には、DataSet が含まれており、DataSet はテスト スクリプトに返された結果セットを含んでいます。 この例では、このコードで DataSet のデータ テーブルに適切な列数があるかどうかを検証します。 詳細については、DataSet を参照してください。  
  
署名するテスト条件を含むクラス ライブラリを設定する必要があります。署名は、プロジェクトのプロパティの [署名] タブで行います。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストのカスタム テスト条件](../ssdt/custom-test-conditions-for-sql-server-unit-tests.md)  
  
