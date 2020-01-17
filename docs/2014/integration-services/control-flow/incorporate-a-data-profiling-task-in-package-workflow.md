---
title: パッケージ ワークフローでデータ プロファイル タスクを使用する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Data Profiling task [Integration Services], using output in workflow
ms.assetid: 39a51586-6977-4c45-b80b-0157a54ad510
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5d8096ee89a9c0b63c89849a02317dc23b2b130e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62831632"
---
# <a name="incorporate-a-data-profiling-task-in-package-workflow"></a>パッケージ ワークフローでデータ プロファイル タスクを使用する
  データ プロファイルとクリーンアップは、初期段階で自動化されるプロセスの対象にはなりません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]では、データ プロファイル タスクを出力する場合、通常、視覚的な分析とユーザーの判断によって、報告された違反が意味のあるものか過剰であるかを判断する必要があります。 データ品質の問題を認識した後でも、クリーンアップに最適な方法に取り組む綿密な計画が必要です。  
  
 ただし、データ品質の基準が確立された後に、データ ソースの定期的な分析とクリーンアップを自動化することが必要になる場合があります。 次のシナリオを考えてみます。  
  
-   **増分読み込みの前にデータ品質を確認する**。 データ プロファイル タスクを使用して、Customers テーブルの CustomerName 列のために、新しいデータの列の NULL 比プロファイルを計算します。 NULL 値の比率が 20% を超える場合は、プロファイル出力を含む電子メールをオペレーターに送信します。 それ以外の場合は、増分読み込みを続行します。  
  
-   **指定した条件が満たされる場合にクリーンアップを自動化する**。 データ プロファイル タスクを使用し、州の参照テーブルに対して State 列、および郵便番号の参照テーブルに対して ZIP Code/Postal Code 列の値包含プロファイルを計算します。 州の値の包含の強さが 80% 未満でも、郵便番号の値の包含の強さが 99% を超える場合は、2 つのことを示しています。 1 つは州のデータが適切ではないこと、 もう 1 つは郵便番号のデータは適切であることです。 現在の郵便番号の値から正しい州の値の参照を実行することで州のデータをクリーンアップするデータ フロー タスクを起動します。  
  
 データ フロー タスクを組み込むことのできるワークフローを用意したら、このタスクを追加するために必要な手順を理解する必要があります。 次のセクションでは、データ フロー タスクを組み込む一般的な手順について説明します。 最後の 2 つのセクションでは、データ フロー タスクを直接データ ソースに接続する方法、またはデータ フローから変換されたデータに接続する方法について説明します。  
  
## <a name="defining-a-general-workflow-for-the-data-flow-task"></a>データ フロー タスクの一般的なワークフローの定義  
 パッケージのワークフローでデータ プロファイル タスクの出力を使用するための一般的な方法の概要を次に示します。  
  
#### <a name="to-use-the-output-of-the-data-profiling-task-programmatically-in-a-package"></a>データ プロファイル タスクの出力をパッケージ内でプログラムによって使用するには  
  
1.  パッケージにデータ プロファイル タスクを追加して構成します。  
  
2.  プロファイルの結果から取得する値を保持するようにパッケージ変数を構成します。  
  
3.  スクリプト タスクを追加して構成します。 スクリプト タスクをデータ プロファイル タスクに接続します。 スクリプト タスクで、必要な値をデータ プロファイル タスクの出力ファイルから読み取り、パッケージ変数を設定するコードを作成します。  
  
4.  スクリプト タスクをワークフロー内の下流の分岐に接続する優先順位制約では、変数の値を使用してワークフローを分ける式を作成します。  
  
 データ プロファイル タスクをパッケージのワークフローに組み込む場合は、このタスクの次の 2 つの機能に注意してください。  
  
-   **タスクの出力**。 データ プロファイル タスクは、DataProfile.xsd スキーマに従って、その出力をファイルまたはパッケージ変数に XML 形式で書き込みます。 そのため、パッケージの条件ワークフローでプロファイルの結果を使用する場合は、XML 出力に対してクエリを実行する必要があります。 Xpath クエリ言語を使用すると、この XML 出力に対して簡単にクエリを実行できます。 この XML 出力の構造を調べるために、サンプルの出力ファイル、またはスキーマ自体を開くことができます。 出力ファイルまたはスキーマを開くには、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]やその他の XML エディター、またはメモ帳などのテキスト エディターを使用できます。  
  
    > [!NOTE]  
    >  Data Profile Viewer に表示されるプロファイルの結果には、出力で直接見つからない、計算された値もあります。 たとえば、列の NULL 比プロファイルの出力には、行の総数と、NULL 値を含む行の総数が含まれます。 列の NULL 比を取得するには、この 2 つの値に対してクエリを実行してから、NULL 値を含む行の比率を計算します。  
  
-   **タスクの入力**。 データ プロファイル タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルからその入力を読み取ります。 そのため、既にデータ フローに読み込まれて変換されたデータをプロファイルする場合は、メモリ内のデータをステージング テーブルに保存する必要があります。  
  
 ここでは、外部データ ソースから直接送信されるデータ、またはデータ フロー タスクから変換されるデータのプロファイルを実行する、この一般的なワークフローを適用します。 また、データ フロー タスクの入出力の要件を扱う方法についても説明します。  
  
## <a name="connecting-the-data-profiling-task-directly-to-an-external-data-source"></a>外部データ ソースへの直接的なデータ プロファイル タスクの接続  
 データ プロファイル タスクでは、データ ソースから直接送信されるデータをプロファイルできます。  この機能を説明するために、次の例では、データ プロファイル タスクを使用して、 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの Person.Address テーブルの列で列の NULL 比プロファイルを計算します。 その後、この例では、スクリプト タスクを使用して出力ファイルから結果を取得し、ワークフローを分けるために使用できるパッケージ変数を設定します。  
  
> [!NOTE]  
>  この簡単な例では、AddressLine2 列を選択しました。この列では NULL 値の比率が高くなっています。  
  
 この例は、次の手順で構成されます。  
  
-   外部データ ソース、およびプロファイルの結果を格納する出力ファイルに接続する接続マネージャーを構成します。  
  
-   データ プロファイル タスクで必要な値を保持するパッケージ変数を構成します。  
  
-   列の NULL 比プロファイルを計算するようにデータ プロファイル タスクを構成します。  
  
-   データ プロファイル タスクからの XML 出力を処理するスクリプト タスクを構成します。  
  
-   データ プロファイル タスクの結果に基づいて実行する、ワークフロー内の下流の分岐を制御する優先順位制約を構成します。  
  
### <a name="configure-the-connection-managers"></a>接続マネージャーの構成  
 この例では、次の 2 つの接続マネージャーがあります。  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] データベースに接続する [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 接続マネージャー。  
  
-   データ プロファイル タスクの結果を格納する出力ファイルを作成するファイル接続マネージャー。  
  
##### <a name="to-configure-the-connection-managers"></a>接続マネージャーを構成するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、新しい [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを作成します。  
  
2.  [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーをパッケージに追加します。 この接続マネージャーを、.NET Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) を使用して、 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] データベースの使用可能なインスタンスに接続するように構成します。  
  
     既定では、接続マネージャーの名前は \<server name>.AdventureWorks1 となります。  
  
3.  ファイル接続マネージャーをパッケージに追加します。 この接続マネージャーを、データ プロファイル タスクの出力ファイルを作成するように構成します。  
  
     この例では、ファイル名 DataProfile1.xml を使用します。 既定では、接続マネージャーの名前はファイルと同じになります。  
  
### <a name="configure-the-package-variables"></a>パッケージ変数の構成  
 この例では、2 つのパッケージ変数を使用します。  
  
-   ProfileConnectionName 変数は、ファイル接続マネージャーの名前をスクリプト タスクに渡します。  
  
-   AddressLine2NullRatio 変数は、この列の計算された NULL 比をスクリプト タスクからパッケージに渡します。  
  
##### <a name="to-configure-the-package-variables-that-will-hold-profile-results"></a>プロファイルの結果を保持するパッケージ変数を構成するには  
  
-   **[変数]** ウィンドウで、次の 2 つのパッケージ変数を追加して構成します。  
  
    -   名前を入力します`ProfileConnectionName`、変数のいずれかの設定には、この変数の型と**文字列**。  
  
    -   名前を入力します`AddressLine2NullRatio`、その他の変数および設定するには、この変数の型**二重**。  
  
### <a name="configure-the-data-profiling-task"></a>データ プロファイル タスクの構成  
 データ プロファイル タスクは、次のように構成する必要があります。  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーが提供するデータを入力として使用します。  
  
-   入力データに対して列の NULL 比プロファイルを実行します。  
  
-   ファイル接続マネージャーに関連付けられているファイルにプロファイルの結果を保存します。  
  
##### <a name="to-configure-the-data-profiling-task"></a>データ プロファイル タスクを構成するには  
  
1.  制御フローにデータ プロファイル タスクを追加します。  
  
2.  **[データ プロファイル タスク エディター]** を開き、タスクを構成します。  
  
3.  エディターの **[全般]** ページの **[変換先]** で、既に構成済みのファイル接続マネージャーの名前を選択します。  
  
4.  エディターの **[プロファイル要求]** ページで、列の NULL 比プロファイルを新しく作成します。  
  
5.  **[要求プロパティ]** ペインの **[接続マネージャー]** で、既に構成済みの [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを選択します。 次に、 **[TableOrView]** で Person.Address を選択します。  
  
6.  データ プロファイル タスク エディターを閉じます。  
  
### <a name="configure-the-script-task"></a>スクリプト タスクの構成  
 スクリプト タスクは、出力ファイルから結果を取得し、既に構成済みのパッケージ変数を設定するように構成する必要があります。  
  
##### <a name="to-configure-the-script-task"></a>スクリプト タスクを構成するには  
  
1.  制御フローにスクリプト タスクを追加します。  
  
2.  スクリプト タスクをデータ プロファイル タスクに接続します。  
  
3.  **スクリプト タスク エディター** を開いて、タスクを構成します。  
  
4.  **[スクリプト]** ページで、使用するプログラミング言語を選択します。 次に、2 つのパッケージ変数をスクリプトで使用できるようにします。  
  
    1.  `ReadOnlyVariables`、`ProfileConnectionName`します。  
  
    2.  **ReadWriteVariables**、`AddressLine2NullRatio`します。  
  
5.  **[スクリプトの編集]** を選択して、スクリプト開発環境を開きます。  
  
6.  System.Xml 名前空間への参照を追加します。  
  
7.  プログラミング言語に対応するサンプル コードを入力します。  
  
    ```vb  
    Imports System  
    Imports Microsoft.SqlServer.Dts.Runtime  
    Imports System.Xml  
  
    Public Class ScriptMain  
  
      Private FILENAME As String = "C:\ TEMP\DataProfile1.xml"  
      Private PROFILE_NAMESPACE_URI As String = "https://schemas.microsoft.com/DataDebugger/"  
      Private NULLCOUNT_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()"  
      Private TABLE_XPATH As String = _  
        "/default:DataProfile/default:DataProfileOutput/default:Profiles" & _  
        "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table"  
  
      Public Sub Main()  
  
        Dim profileConnectionName As String  
        Dim profilePath As String  
        Dim profileOutput As New XmlDocument  
        Dim profileNSM As XmlNamespaceManager  
        Dim nullCountNode As XmlNode  
        Dim nullCount As Integer  
        Dim tableNode As XmlNode  
        Dim rowCount As Integer  
        Dim nullRatio As Double  
  
        ' Open output file.  
        profileConnectionName = Dts.Variables("ProfileConnectionName").Value.ToString()  
        profilePath = Dts.Connections(profileConnectionName).ConnectionString  
        profileOutput.Load(profilePath)  
        profileNSM = New XmlNamespaceManager(profileOutput.NameTable)  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI)  
  
        ' Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM)  
        nullCount = CType(nullCountNode.Value, Integer)  
  
        ' Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM)  
        rowCount = CType(tableNode.Attributes("RowCount").Value, Integer)  
  
        ' Compute and return null ratio.  
        nullRatio = nullCount / rowCount  
        Dts.Variables("AddressLine2NullRatio").Value = nullRatio  
  
        Dts.TaskResult = Dts.Results.Success  
  
      End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System;  
    using Microsoft.SqlServer.Dts.Runtime;  
    using System.Xml;  
  
    public class ScriptMain  
    {  
  
      private string FILENAME = "C:\\ TEMP\\DataProfile1.xml";  
      private string PROFILE_NAMESPACE_URI = "https://schemas.microsoft.com/DataDebugger/";  
      private string NULLCOUNT_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:NullCount/text()";  
      private string TABLE_XPATH = "/default:DataProfile/default:DataProfileOutput/default:Profiles" + "/default:ColumnNullRatioProfile[default:Column[@Name='AddressLine2']]/default:Table";  
  
      public void Main()  
      {  
  
        string profileConnectionName;  
        string profilePath;  
        XmlDocument profileOutput = new XmlDocument();  
        XmlNamespaceManager profileNSM;  
        XmlNode nullCountNode;  
        int nullCount;  
        XmlNode tableNode;  
        int rowCount;  
        double nullRatio;  
  
        // Open output file.  
        profileConnectionName = Dts.Variables["ProfileConnectionName"].Value.ToString();  
        profilePath = Dts.Connections[profileConnectionName].ConnectionString;  
        profileOutput.Load(profilePath);  
        profileNSM = new XmlNamespaceManager(profileOutput.NameTable);  
        profileNSM.AddNamespace("default", PROFILE_NAMESPACE_URI);  
  
        // Get null count for column.  
        nullCountNode = profileOutput.SelectSingleNode(NULLCOUNT_XPATH, profileNSM);  
        nullCount = (int)nullCountNode.Value;  
  
        // Get row count for table.  
        tableNode = profileOutput.SelectSingleNode(TABLE_XPATH, profileNSM);  
        rowCount = (int)tableNode.Attributes["RowCount"].Value;  
  
        // Compute and return null ratio.  
        nullRatio = nullCount / rowCount;  
        Dts.Variables["AddressLine2NullRatio"].Value = nullRatio;  
  
        Dts.TaskResult = Dts.Results.Success;  
  
      }  
  
    }  
    ```  
  
    > [!NOTE]  
    >  この手順で示すサンプル コードでは、データ プロファイル タスクの出力をファイルから読み込む方法を示しています。 パッケージ変数からデータ プロファイル タスクの出力を読み込むには、この手順の後に示す他のサンプル コードを参照してください。  
  
8.  スクリプト開発環境を閉じてから、スクリプト タスク エディターを閉じます。  
  
#### <a name="alternative-code-reading-the-profile-output-from-a-variable"></a>変数からプロファイル出力を読み込むコード  
 上記の手順は、データ プロファイル タスクの出力をファイルから読み込む方法を示していますが、 この出力をパッケージ変数から読み込む方法もあります。 出力を変数から読み込むには、サンプル コードを次のように変更する必要があります。  
  
-   `LoadXml` メソッドではなく、`XmlDocument` クラスの `Load` メソッドを呼び出します。  
  
-   スクリプト タスク エディターで、プロファイル出力を格納するパッケージ変数の名前を、タスクの `ReadOnlyVariables` リストに追加します。  
  
-   次のコード例で示すように、変数の文字列値を `LoadXML` メソッドに渡します (この例では、プロファイル出力を格納するパッケージ変数の名前として "ProfileOutput" を使用しています)。  
  
    ```vb  
    Dim outputString As String  
    outputString = Dts.Variables("ProfileOutput").Value.ToString()  
    ...  
    profileOutput.LoadXml(outputString)  
    ```  
  
    ```csharp  
    string outputString;  
    outputString = Dts.Variables["ProfileOutput"].Value.ToString();  
    ...  
    profileOutput.LoadXml(outputString);  
    ```  
  
### <a name="configure-the-precedence-constraints"></a>優先順位制約の構成  
 優先順位制約は、データ プロファイル タスクの結果に基づいて実行する、ワークフロー内の下流の分岐を制御するように構成する必要があります。  
  
##### <a name="to-configure-the-precedence-constraints"></a>優先順位制約を構成するには  
  
-   スクリプト タスクをワークフロー内の下流の分岐に接続する優先順位制約では、変数の値を使用してワークフローを分ける式を作成します。  
  
     たとえば、 **[式と制約]** で、優先順位制約の **[評価操作]** を設定するとします。 次に、式の値として `@AddressLine2NullRatio < .90` を使用します。 これにより、ワークフローは、直前のタスクが成功した場合、および選択した列の NULL 値の比率が 90% 未満の場合に、選択したパスに沿って進みます。  
  
## <a name="connecting-the-data-profiling-task-to-transformed-data-from-the-data-flow"></a>データ フローから変換されたデータへのデータ プロファイル タスクの接続  
 データ ソースから直接データをプロファイルするのではなく、既にデータ フローに読み込まれて変換されたデータをプロファイルできます。 ただし、データ プロファイル タスクは、メモリ内のデータではなく、持続データに対してしか動作しません。 したがって、変換されたデータをステージング テーブルに保存するには、最初に、変換先コンポーネントを使用する必要があります。  
  
> [!NOTE]  
>  データ プロファイル タスクを構成する場合は、既存のテーブルと列を選択する必要があります。 そのため、タスクを構成するには、デザイン時にステージング テーブルを作成しておく必要があります。 つまり、このシナリオでは、実行時に作成した一時テーブルを使用することはできません。  
  
 データをステージング テーブルに保存すると、次の操作を行うことができます。  
  
-   データ プロファイル タスクを使用してデータをプロファイルする。  
  
-   このトピックの前半で説明したように、スクリプト タスクを使用して結果を読み込む。  
  
-   この結果を使用してパッケージの後続のワークフローを進む。  
  
 次の手順では、データ プロファイル タスクの出力を使用して、データ フローによって変換されたデータをプロファイルするための一般的な方法を示します。 この手順の多くは、外部データ ソースから直接送信されるデータをプロファイルするための既に説明した手順と似ています。 さまざまなコンポーネントを構成する方法の詳細については、上記の手順を確認してください。  
  
#### <a name="to-use-the-data-profiling-task-in-the-data-flow"></a>データ フローでデータ プロファイル タスクを使用するには  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]で、パッケージを作成します。  
  
2.  データ フローで、適切な変換元と変換を追加、構成、および接続します。  
  
3.  データ フローで、変換したデータをステージング テーブルに保存する変換先コンポーネントを追加、構成、および接続します。  
  
4.  制御フローで、ステージング テーブル内の変換したデータに対して必要なプロファイルを計算するデータ プロファイル タスクを追加して構成します。 データ プロファイル タスクをデータ フロー タスクに接続します。  
  
5.  プロファイルの結果から取得する値を保持するようにパッケージ変数を構成します。  
  
6.  スクリプト タスクを追加して構成します。 スクリプト タスクをデータ プロファイル タスクに接続します。 スクリプト タスクで、必要な値をデータ プロファイル タスクの出力から読み取り、パッケージ変数を設定するコードを作成します。  
  
7.  スクリプト タスクをワークフロー内の下流の分岐に接続する優先順位制約では、変数の値を使用してワークフローを分ける式を作成します。  
  
## <a name="see-also"></a>参照  
 [データ プロファイル タスクのセットアップ](data-profiling-task.md)   
 [Data Profile Viewer (Data Profile Viewer)](data-profile-viewer.md)  
  
  
