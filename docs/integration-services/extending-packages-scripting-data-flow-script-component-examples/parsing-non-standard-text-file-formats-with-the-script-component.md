---
title: スクリプト コンポーネントを使用した標準以外のテキスト ファイル形式の解析 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- text file reading [Integration Services]
- Script component [Integration Services], non-standard text file formats
- transformations [Integration Services], components
- Script component [Integration Services], examples
ms.assetid: 1fda034d-09e4-4647-9a9f-e8d508c2cc8f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 733c3a909629514b55042d21f02cfca563d3c531
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297064"
---
# <a name="parsing-non-standard-text-file-formats-with-the-script-component"></a>スクリプト コンポーネントを使用した標準以外のテキスト ファイル形式の解析

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ソース データが標準以外の形式の場合、複数の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 変換を連結するより、すべての解析ロジックを単一のスクリプトに統合する方がより便利で、同じ結果が得られる場合があります。  
  
 [例 1: 行区切りのレコードの解析](#example1)  
  
 [例 2: 親レコードと子レコードの分割](#example2)  
  
> [!NOTE]  
>  複数のデータ フロー タスクおよび複数のパッケージでより簡単に再利用できるコンポーネントを作成する場合は、このスクリプト コンポーネント サンプルのコードを基にした、カスタム データ フロー コンポーネントの作成を検討してください。 詳細については、「 [カスタム データ フロー コンポーネントの開発](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」を参照してください。  
  
##  <a name="example1"></a> 例 1: 行区切りのレコードの解析  
 この例では、データの各列が個別の行に表示されるテキスト ファイルを取得し、スクリプト コンポーネントを使用して解析し、変換先テーブルに入れる方法を示します。  
  
 スクリプト コンポーネントをデータ フローで変換として使用するための構成方法の詳細については、「[スクリプト コンポーネントによる同期変換の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)」および「[スクリプト コンポーネントによる非同期変換の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)」を参照してください。  
  
#### <a name="to-configure-this-script-component-example"></a>このスクリプト コンポーネントの例を構成するには  
  
1.  次のソース データを含む、**rowdelimiteddata.txt** という名前のテキスト ファイルを作成して保存します。  
  
    ```  
    FirstName: Nancy  
    LastName: Davolio  
    Title: Sales Representative  
    City: Seattle  
    StateProvince: WA  
  
    FirstName: Andrew  
    LastName: Fuller  
    Title: Vice President, Sales  
    City: Tacoma  
    StateProvince: WA  
  
    FirstName: Steven  
    LastName: Buchanan  
    Title: Sales Manager  
    City: London  
    StateProvince:  
  
    ```  
  
2.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を開き、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続します。  
  
3.  変換先データベースを選択し、新しいクエリ ウィンドウを開きます。 クエリ ウィンドウで、次のスクリプトを実行して変換先テーブルを作成します。  
  
    ```sql
    create table RowDelimitedData  
    (  
    FirstName varchar(32),  
    LastName varchar(32),  
    Title varchar(32),  
    City varchar(32),  
    StateProvince varchar(32)  
    )  
  
    ```  
  
4.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] を開き、ParseRowDelim.dtsx という名前の新しい [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを作成します。  
  
5.  フラット ファイル接続マネージャーをパッケージに追加し、RowDelimitedData という名前を付け、前の手順で作成した rowdelimiteddata.txt ファイルに接続するように構成します。  
  
6.  OLE DB 接続マネージャーをパッケージに追加し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスと、変換先テーブルを作成したデータベースに接続するように構成します。  
  
7.  データ フロー タスクをパッケージに追加し、SSIS デザイナーの **[データ フロー]** タブをクリックします。  
  
8.  フラット ファイル ソースをデータ フローに追加し、RowDelimitedData 接続マネージャーを使用するように構成します。 **[フラット ファイル ソース エディター]** の **[列]** ページで、単一の使用可能な外部列を選択します。  
  
9. スクリプト コンポーネントをデータ フローに追加し、変換として構成します。 フラット ファイル ソースの出力をスクリプト コンポーネントに接続します。  
  
10. スクリプト コンポーネントをダブルクリックし、 **[スクリプト変換エディター]** を表示します。  
  
11. **[スクリプト変換エディター]** の **[入力列]** ページで、単一の使用可能な入力列を選択します。  
  
12. **[スクリプト変換エディター]** の **[入力および出力]** ページで、出力 0 を選択し、**SynchronousInputID** を None に設定します。 次の 5 つの出力列を、すべて文字列型 [DT_STR]、長さ 32 で作成します。  
  
    -   FirstName  
  
    -   LastName  
  
    -   [タイトル]  
  
    -   City  
  
    -   StateProvince  
  
13. **[スクリプト変換エディター]** の **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックし、例の **ScriptMain** クラスに示すコードを入力します。 スクリプト開発環境と **[スクリプト変換エディター]** を閉じます。  
  
14. SQL Server 変換先をデータ フローに追加します。 OLE DB 接続マネージャーと RowDelimitedData テーブルを使用するように構成します。 スクリプト コンポーネントの出力をこの変換先に接続します。  
  
15. パッケージを実行します。 パッケージが完成したら、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換先テーブル内のレコードを確認します。  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
    Dim columnName As String  
    Dim columnValue As String  
  
    ' Check for an empty row.  
    If Row.Column0.Trim.Length > 0 Then  
        columnName = Row.Column0.Substring(0, Row.Column0.IndexOf(":"))  
        ' Check for an empty value after the colon.  
        If Row.Column0.Substring(Row.Column0.IndexOf(":")).TrimEnd.Length > 1 Then  
            ' Extract the column value from after the colon and space.  
            columnValue = Row.Column0.Substring(Row.Column0.IndexOf(":") + 2)  
            Select Case columnName  
                Case "FirstName"  
                    ' The FirstName value indicates a new record.  
                    Me.Output0Buffer.AddRow()  
                    Me.Output0Buffer.FirstName = columnValue  
                Case "LastName"  
                    Me.Output0Buffer.LastName = columnValue  
                Case "Title"  
                    Me.Output0Buffer.Title = columnValue  
                Case "City"  
                    Me.Output0Buffer.City = columnValue  
                Case "StateProvince"  
                    Me.Output0Buffer.StateProvince = columnValue  
            End Select  
        End If  
    End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
        string columnName;  
        string columnValue;  
  
        // Check for an empty row.  
        if (Row.Column0.Trim().Length > 0)  
        {  
            columnName = Row.Column0.Substring(0, Row.Column0.IndexOf(":"));  
            // Check for an empty value after the colon.  
            if (Row.Column0.Substring(Row.Column0.IndexOf(":")).TrimEnd().Length > 1)  
            // Extract the column value from after the colon and space.  
            {  
                columnValue = Row.Column0.Substring(Row.Column0.IndexOf(":") + 2);  
                switch (columnName)  
                {  
                    case "FirstName":  
                        // The FirstName value indicates a new record.  
                        this.Output0Buffer.AddRow();  
                        this.Output0Buffer.FirstName = columnValue;  
                        break;  
                    case "LastName":  
                        this.Output0Buffer.LastName = columnValue;  
                        break;  
                    case "Title":  
                        this.Output0Buffer.Title = columnValue;  
                        break;  
                    case "City":  
                        this.Output0Buffer.City = columnValue;  
                        break;  
                    case "StateProvince":  
                        this.Output0Buffer.StateProvince = columnValue;  
                        break;  
                }  
            }  
        }  
  
    }  
```  
  
##  <a name="example2"></a> 例 2: 親レコードと子レコードの分割  
 この例では、親レコードの前に区切り行があり、親レコードの後に行数不定の子レコード行が続くテキスト ファイルを取得し、スクリプト コンポーネントを使用して解析し、適切に正規化された親変換先テーブルと子変換先テーブルに入れる方法を示します。 この簡単な例は、なんらかの方法で各レコードの先頭と末尾を識別できれば、各親レコードおよび子レコードで複数の行または列を使用するソース ファイルに容易に適用できます。  
  
> [!CAUTION]  
>  このサンプルは、デモンストレーションのみを目的としています。 サンプルを複数回実行すると、重複したキーの値が変換先テーブルに挿入されます。  
  
 スクリプト コンポーネントをデータ フローで変換として使用するための構成方法の詳細については、「[スクリプト コンポーネントによる同期変換の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)」および「[スクリプト コンポーネントによる非同期変換の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)」を参照してください。  
  
#### <a name="to-configure-this-script-component-example"></a>このスクリプト コンポーネントの例を構成するには  
  
1.  次のソース データを含む、**parentchilddata.txt** という名前のテキスト ファイルを作成して保存します。  
  
    ```  
    **********  
    PARENT 1 DATA  
    child 1 data  
    child 2 data  
    child 3 data  
    child 4 data  
    **********  
    PARENT 2 DATA  
    child 5 data  
    child 6 data  
    child 7 data  
    child 8 data  
    **********  
  
    ```  
  
2.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開き、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに接続します。  
  
3.  変換先データベースを選択し、新しいクエリ ウィンドウを開きます。 クエリ ウィンドウで、次のスクリプトを実行して変換先テーブルを作成します。  
  
    ```sql
    CREATE TABLE [dbo].[Parents]([ParentID] [int] NOT NULL,  
    [ParentRecord] [varchar](32) NOT NULL,  
     CONSTRAINT [PK_Parents] PRIMARY KEY CLUSTERED   
    ([ParentID] ASC))  
    GO  
    CREATE TABLE [dbo].[Children]([ChildID] [int] NOT NULL,  
    [ParentID] [int] NOT NULL,  
    [ChildRecord] [varchar](32) NOT NULL,  
     CONSTRAINT [PK_Children] PRIMARY KEY CLUSTERED   
    ([ChildID] ASC))  
    GO  
    ALTER TABLE [dbo].[Children] ADD CONSTRAINT [FK_Children_Parents] FOREIGN KEY([ParentID])  
    REFERENCES [dbo].[Parents] ([ParentID])  
  
    ```  
  
4.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] を開き、SplitParentChild.dtsx という名前の新しい [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを作成します。  
  
5.  フラット ファイル接続マネージャーをパッケージに追加し、ParentChildData という名前を付け、前の手順で作成した parentchilddata.txt ファイルに接続するように構成します。  
  
6.  OLE DB 接続マネージャーをパッケージに追加し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスと、変換先テーブルを作成したデータベースに接続するように構成します。  
  
7.  データ フロー タスクをパッケージに追加し、SSIS デザイナーの **[データ フロー]** タブをクリックします。  
  
8.  フラット ファイル ソースをデータ フローに追加し、ParentChildData 接続マネージャーを使用するように構成します。 **[フラット ファイル ソース エディター]** の **[列]** ページで、単一の使用可能な外部列を選択します。  
  
9. スクリプト コンポーネントをデータ フローに追加し、変換として構成します。 フラット ファイル ソースの出力をスクリプト コンポーネントに接続します。  
  
10. スクリプト コンポーネントをダブルクリックし、 **[スクリプト変換エディター]** を表示します。  
  
11. **[スクリプト変換エディター]** の **[入力列]** ページで、単一の使用可能な入力列を選択します。  
  
12. **[スクリプト変換エディター]** の **[入力および出力]** ページで、出力 0 を選択し、ParentRecords に名前を変更してから、**SynchronousInputID** を None に設定します。 次の 2 つの出力列を作成します。  
  
    -   ParentID (主キー)、4 バイト符号付き整数型 [DT_I4]  
  
    -   ParentRecord、文字列型 [DT_STR]、長さ 32  
  
13. 2 つ目の出力を作成し、ChildRecords という名前を付けます。 新しい出力の **SynchronousInputID** は既に None に設定されています。 次の 3 つの出力列を作成します。  
  
    -   ChildID (主キー)、4 バイト符号付き整数型 [DT_I4]  
  
    -   ParentID (外部キー)、4 バイト符号付き整数型 [DT_I4]  
  
    -   ChildRecord、文字列型 [DT_STR]、長さ 50  
  
14. **[スクリプト変換エディター]** の **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックします。 **ScriptMain** クラスに、例に示すコードを入力します。 スクリプト開発環境と **[スクリプト変換エディター]** を閉じます。  
  
15. SQL Server 変換先をデータ フローに追加します。 スクリプト コンポーネントの ParentRecords 出力をこの変換先に接続します。OLE DB 接続マネージャーと Parents テーブルを使用するように構成します。  
  
16. 別の SQL Server 変換先をデータ フローに追加します。 スクリプト コンポーネントの ChildRecords 出力をこの変換先に接続します。 OLE DB 接続マネージャーと Children テーブルを使用するように構成します。  
  
17. パッケージを実行します。 パッケージが完成したら、2 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換先テーブル内の親レコードと子レコードを確認します。  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
    Static nextRowIsParent As Boolean = False  
    Static parentCounter As Integer = 0  
    Static childCounter As Integer = 0  
  
    ' If current row starts with separator characters,  
    '  then following row contains new parent record.  
    If Row.Column0.StartsWith("***") Then  
        nextRowIsParent = True  
    Else  
        If nextRowIsParent Then  
            ' Current row contains parent record.  
            parentCounter += 1  
            Me.ParentRecordsBuffer.AddRow()  
            Me.ParentRecordsBuffer.ParentID = parentCounter  
            Me.ParentRecordsBuffer.ParentRecord = Row.Column0  
            nextRowIsParent = False  
        Else  
            ' Current row contains child record.  
            childCounter += 1  
            Me.ChildRecordsBuffer.AddRow()  
            Me.ChildRecordsBuffer.ChildID = childCounter  
            Me.ChildRecordsBuffer.ParentID = parentCounter  
            Me.ChildRecordsBuffer.ChildRecord = Row.Column0  
        End If  
    End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
    int static_Input0_ProcessInputRow_childCounter = 0;  
    int static_Input0_ProcessInputRow_parentCounter = 0;  
    bool static_Input0_ProcessInputRow_nextRowIsParent = false;  
  
        // If current row starts with separator characters,   
        // then following row contains new parent record.   
        if (Row.Column0.StartsWith("***"))  
        {  
            static_Input0_ProcessInputRow_nextRowIsParent = true;  
        }  
        else  
        {  
            if (static_Input0_ProcessInputRow_nextRowIsParent)  
            {  
                // Current row contains parent record.   
                static_Input0_ProcessInputRow_parentCounter += 1;  
                this.ParentRecordsBuffer.AddRow();  
                this.ParentRecordsBuffer.ParentID = static_Input0_ProcessInputRow_parentCounter;  
                this.ParentRecordsBuffer.ParentRecord = Row.Column0;  
                static_Input0_ProcessInputRow_nextRowIsParent = false;  
            }  
            else  
            {  
                // Current row contains child record.   
                static_Input0_ProcessInputRow_childCounter += 1;  
                this.ChildRecordsBuffer.AddRow();  
                this.ChildRecordsBuffer.ChildID = static_Input0_ProcessInputRow_childCounter;  
                this.ChildRecordsBuffer.ParentID = static_Input0_ProcessInputRow_parentCounter;  
                this.ChildRecordsBuffer.ChildRecord = Row.Column0;  
            }  
        }  
  
    }  
```  
  
## <a name="see-also"></a>参照  
 [スクリプト コンポーネントによる同期変換の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [スクリプト コンポーネントによる非同期変換の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
  
  
