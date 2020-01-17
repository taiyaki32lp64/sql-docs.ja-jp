---
title: スクリプト コンポーネントによる変換先の作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], destination components
- destinations [Integration Services], components
- input columns [Integration Services]
ms.assetid: 214e22e8-7e7d-4876-b690-c138e5721b81
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 946fc77d3bde2814176ebefce4102742a0288a91
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296488"
---
# <a name="creating-a-destination-with-the-script-component"></a>スクリプト コンポーネントによる変換先の作成

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのデータ フロー内では、変換先コンポーネントを使用して、上流の変換元や変換から受け取ったデータをデータ ソースに保存します。 通常、変換先コンポーネントをデータ ソースに接続するには、既存の接続マネージャーを使用します。  
  
 スクリプト コンポーネントの概要については、「[スクリプト コンポーネントによるデータ フローの拡張](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)」を参照してください。  
  
 スクリプト コンポーネントおよびそれによって生成されるインフラストラクチャ コードを活用すれば、カスタム データ フロー コンポーネントを開発するための手順を大幅に簡略化できます。 ただし、スクリプト コンポーネントのしくみを理解するため、「[カスタム データ フロー コンポーネントの開発](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」セクション、特に「[カスタム変換先コンポーネントの開発](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)」を参照して、カスタム データ フロー コンポーネント開発の手順に目を通しておくと役立つことがあります。  
  
## <a name="getting-started-with-a-destination-component"></a>変換先コンポーネントの概要  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの [データ フロー] タブにスクリプト コンポーネントを追加すると、 **[スクリプト コンポーネントの種類を選択]** ダイアログ ボックスが開き、 **[変換元]** 、 **[変換先]** 、または **[変換]** スクリプトのいずれかを選択するように求められます。 このダイアログ ボックスで、 **[変換先]** を選択します。  
  
 次に、[!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで、変換の出力を変換先コンポーネントに接続します。 テスト目的の場合、変換を介さずに変換元を直接変換先に接続することもできます。  
  
## <a name="configuring-a-destination-component-in-metadata-design-mode"></a>メタデータ デザイン モードでの変換先コンポーネントの構成  
 変換先コンポーネントを作成するオプションを選択したら、 **[スクリプト変換エディター]** を使用して、コンポーネントを構成します。 詳細については、「[スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)」を参照してください。  
  
 スクリプト変換先で使用するスクリプト言語を選択するには、 **[スクリプト変換エディター]** ダイアログ ボックスの **[スクリプト]** ページにある **[ScriptLanguage]** プロパティを設定します。  
  
> [!NOTE]  
>  スクリプト コンポーネントの既定のスクリプト言語を設定するには、 **[オプション]** ダイアログ ボックスの **[全般]** ページにある **[スクリプト言語]** オプションを使用します。 詳細については、「 [General Page](../general-page-of-integration-services-designers-options.md)」を参照してください。  
  
 データ フローの変換先コンポーネントには、1 つの入力があり、出力はありません。 コンポーネントの入力の設定は、メタデータ デザイン モードでカスタム スクリプトを記述する前に完了する必要のある作業の 1 つです。これを行うには、 **[スクリプト変換エディター]** を使用します。  
  
### <a name="adding-connection-managers"></a>接続マネージャーの追加  
 通常、変換先コンポーネントは既存の接続マネージャーを使用してデータ ソースに接続し、データ フローからのデータを保存します。 **[スクリプト変換エディター]** の **[接続マネージャー]** ページで **[追加]** をクリックして、適切な接続マネージャーを追加します。  
  
 ただし、接続マネージャーは、便宜上、特定の種類のデータ ソースに接続するために必要な情報をカプセル化して格納するユニットにすぎません。 データの読み込みや保存、場合によってはデータ ソースとの接続や切断を行うためには、独自のカスタム コードを記述する必要があります。  
  
 スクリプト コンポーネントで接続マネージャーを使用する方法の一般情報については、「[スクリプト コンポーネントでのデータ ソースへの接続](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)」を参照してください。  
  
 **[スクリプト変換エディター]** の **[接続マネージャー]** ページの詳細については、「[スクリプト変換エディター &#40;[接続マネージャー] ページ&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md)」を参照してください。  
  
### <a name="configuring-inputs-and-input-columns"></a>入力および入力列の設定  
 変換先コンポーネントには、1 つの入力があり、出力はありません。  
  
 **[スクリプト変換エディター]** の **[入力列]** ページには、データ フローの上流コンポーネントの出力で使用できる列が一覧表示されます。 保存する列を選択します。  
  
 **[スクリプト変換エディター]** の **[入力列]** ページの詳細については、「[[スクリプト変換エディター] &#40;[入力列] ページ&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)」を参照してください。  
  
 **[スクリプト変換エディター]** の **[入力および出力]** ページには入力が 1 つ表示されています。この入力の名前は変更できます。 スクリプト内ではこの名前で入力を参照しますが、参照には自動生成されたコードによって作成されたアクセサー プロパティが使用されます。  
  
 **[スクリプト変換エディター]** の **[入力および出力]** ページの詳細については、「[[スクリプト変換エディター] &#40;[入力および出力] ページ&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)」を参照してください。  
  
### <a name="adding-variables"></a>変数の追加  
 スクリプトで既存の変数を使用する場合は、 **[スクリプト変換エディター]** の **[スクリプト]** ページで、**ReadOnlyVariables** および **ReadWriteVariables** プロパティ フィールドに追加できます。  
  
 プロパティ フィールドに複数の変数を追加する場合は、各変数名をコンマで区切ります。 また、**ReadOnlyVariables** および **ReadWriteVariables** プロパティ フィールドの横にある省略記号 ( **[...]** ) ボタンをクリックしてから、 **[変数の選択]** ダイアログ ボックスで変数を選択することで、複数の変数を選択することもできます。  
  
 スクリプト コンポーネントで変数を使用する方法に関する一般情報については、「[スクリプト コンポーネントでの変数の使用](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)」を参照してください。  
  
 **[スクリプト変換エディター]** の **[スクリプト]** ページの詳細については、「[[スクリプト変換エディター] &#40;[スクリプト] ページ&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md)」を参照してください。  
  
## <a name="scripting-a-destination-component-in-code-design-mode"></a>コード デザイン モードでの変換先コンポーネントのスクリプト作成  
 コンポーネントのメタデータを構成した後、カスタム スクリプトを記述できます。 **[スクリプト変換エディター]** の **[スクリプト]** ページで **[スクリプトの編集]** をクリックし、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE を開いて、カスタム スクリプトを追加できます。 使用するスクリプト言語は、 **[スクリプト]** ページの **[ScriptLanguage]** プロパティで、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic と [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# のどちらをスクリプト言語として選択したかによって決まります。  
  
 スクリプト コンポーネントを使用して作成されたすべての種類のコンポーネントに適用される重要な情報については、「[スクリプト コンポーネントのコーディングおよびデバッグ](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)」を参照してください。  
  
### <a name="understanding-the-auto-generated-code"></a>自動生成されたコードについて  
 変換コンポーネントを作成して構成した後で VSTA IDE を開くと、コード エディターには編集可能な **ScriptMain** クラス表示され、**ProcessInputRow** メソッドのスタブが示されます。 **ScriptMain** クラスはカスタム コードを記述する場所であり、**ProcessInputRow** は変換コンポーネントの最重要メソッドです。  
  
 VSTA の **[プロジェクト エクスプローラー]** ウィンドウを開くと、スクリプト コンポーネントにより、**BufferWrapper** および **ComponentWrapper** というプロジェクト アイテムが、読み取り専用の状態で自動生成されていることもわかります。 **ScriptMain** クラスは、**ComponentWrapper** プロジェクト アイテム内の **UserComponent** クラスから継承されます。  
  
 実行時に、データ フロー エンジンが **UserComponent** クラスの **ProcessInput** メソッドを呼び出します。これにより、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 親クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> メソッドがオーバーライドされます。 **ProcessInput** メソッドは、入力バッファーの行を順にループし、各行で 1 回ずつ **ProcessInputRow** メソッドを呼び出します。  
  
### <a name="writing-your-custom-code"></a>カスタム コードの記述  
 カスタム変換先コンポーネントの作成を終了するには、必要に応じて **ScriptMain** クラスで使用できる次のメソッドにスクリプトを記述する場合があります。  
  
1.  外部データ ソースに接続する場合は、**AcquireConnections** メソッドをオーバーライドします。 接続マネージャーから、接続オブジェクトまたは必要な接続情報を抽出します。  
  
2.  データを保存する準備のため、**PreExecute** メソッドをオーバーライドします。 たとえば、このメソッド内で **SqlCommand** およびそのパラメーターを作成し、設定することができます。  
  
3.  各入力行を外部データ ソースにコピーするには、オーバーライドされた **ProcessInputRow** メソッドを使用します。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変換先の場合、列の値を **SqlCommand** のパラメーターにコピーし、各行で 1 回ずつコマンドを実行できます。 フラット ファイル変換先の場合、各列の値を列区切り記号で区切って **StreamWriter** に書き込むことができます。  
  
4.  必要に応じて外部データ ソースとの接続を切断し、その他の必要なクリーンアップ作業を実行するには、**PostExecute** メソッドをオーバーライドします。  
  
## <a name="examples"></a>使用例  
 次の例では、変換先コンポーネントを作成するために **ScriptMain** クラスで必要なコードを示します。  
  
> [!NOTE]
>  これらの例では、**AdventureWorks** サンプル データベースの **Person.Address** テーブルを使用して、その第 1 列および第 4 列、つまり、**int*AddressID*** 列および **nvarchar(30)City** 列をデータ フローにそのまま渡します。 このセクションの変換元、変換、および変換先の例でも、同じデータが使用されます。 他の前提条件および仮定条件については、それぞれの例で説明します。  
  
### <a name="adonet-destination-example"></a>ADO.NET 変換先の例  
 この例では、既存の [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを使用して、データ フローのデータを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルに保存する変換先コンポーネントを示します。  
  
 このサンプル コードを実行する場合は、パッケージやコンポーネントを次のように構成する必要があります。  
  
1.  **SqlClient** プロバイダーを使用する [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを作成して、**AdventureWorks** データベースに接続します。  
  
2.  **AdventureWorks** データベースで次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを実行して、変換先テーブルを作成します。  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
3.  新しいスクリプト コンポーネントを [データ フロー] デザイナー画面に追加し、変換先として構成します。  
  
4.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで、上流変換元の出力または変換の出力を変換先コンポーネントに接続します (変換なしで直接変換元を変換先に接続することもできます)。この出力には、サンプル データベース **AdventureWorks** の **Person.Address** テーブルから、少なくとも **AddressID** 列および **City** 列を含むデータが供給される必要があります。  
  
5.  **[スクリプト変換エディター]** を開きます。 **[入力列]** ページで、**AddressID** 入力列と **City** 入力列を選択します。  
  
6.  **[入力および出力]** ページで、入力を **MyAddressInput** などのわかりやすい名前に変更します。  
  
7.  **[接続マネージャー]** ページで、[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを追加または作成し、**MyADONETConnectionManager** などの名前を付けます。  
  
8.  **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックし、続きのスクリプトを入力します。 スクリプト開発環境を閉じます。  
  
9. **[スクリプト変換エディター]** を閉じ、サンプルを実行します。  
  
```vb  
Imports System.Data.SqlClient  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim connMgr As IDTSConnectionManager100  
    Dim sqlConn As SqlConnection  
    Dim sqlCmd As SqlCommand  
    Dim sqlParam As SqlParameter  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        connMgr = Me.Connections.MyADONETConnectionManager  
        sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        sqlCmd = New SqlCommand("INSERT INTO Person.Address2(AddressID, City) " & _  
            "VALUES(@addressid, @city)", sqlConn)  
        sqlParam = New SqlParameter("@addressid", SqlDbType.Int)  
        sqlCmd.Parameters.Add(sqlParam)  
        sqlParam = New SqlParameter("@city", SqlDbType.NVarChar, 30)  
        sqlCmd.Parameters.Add(sqlParam)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
        With sqlCmd  
            .Parameters("@addressid").Value = Row.AddressID  
            .Parameters("@city").Value = Row.City  
            .ExecuteNonQuery()  
        End With  
    End Sub  
  
    Public Overrides Sub ReleaseConnections()  
  
        connMgr.ReleaseConnection(sqlConn)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.Data.SqlClient;  
public class ScriptMain:  
    UserComponent  
  
{  
    IDTSConnectionManager100 connMgr;  
    SqlConnection sqlConn;  
    SqlCommand sqlCmd;  
    SqlParameter sqlParam;  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        connMgr = this.Connections.MyADONETConnectionManager;  
        sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        sqlCmd = new SqlCommand("INSERT INTO Person.Address2(AddressID, City) " +  
            "VALUES(@addressid, @city)", sqlConn);  
        sqlParam = new SqlParameter("@addressid", SqlDbType.Int);  
        sqlCmd.Parameters.Add(sqlParam);  
        sqlParam = new SqlParameter("@city", SqlDbType.NVarChar, 30);  
        sqlCmd.Parameters.Add(sqlParam);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
        {  
            sqlCmd.Parameters["@addressid"].Value = Row.AddressID;  
            sqlCmd.Parameters["@city"].Value = Row.City;  
            sqlCmd.ExecuteNonQuery();  
        }  
    }  
  
    public override void ReleaseConnections()  
    {  
  
        connMgr.ReleaseConnection(sqlConn);  
  
    }  
  
}  
```  
  
### <a name="flat-file-destination-example"></a>フラット ファイル変換先の例  
 この例では、既存のフラット ファイル接続マネージャーを使用して、データ フローのデータをフラット ファイルに保存する変換先コンポーネントを示します。  
  
 このサンプル コードを実行する場合は、パッケージやコンポーネントを次のように構成する必要があります。  
  
1.  変換先ファイルに接続するフラット ファイル接続マネージャーを作成します。 ファイルが存在しない場合は、変換先コンポーネントによって作成されます。 変換先ファイルを、**AddressID** 列および **City** 列を含む、コンマ区切りファイルとして構成します。  
  
2.  新しいスクリプト コンポーネントを [データ フロー] デザイナー画面に追加し、変換先として構成します。  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで、上流変換元の出力または変換の出力を変換先コンポーネントに接続します (変換なしで直接変換元を変換先に接続することもできます)。この出力には、サンプル データベース **AdventureWorks** サンプル データベースの **Person.Address** テーブルから、少なくとも **AddressID** 列および **City** 列を含むデータが渡される必要があります。  
  
4.  **[スクリプト変換エディター]** を開きます。 **[入力列]** ページで、**AddressID** 列と **City** 列を選択します。  
  
5.  **[入力および出力]** ページで、入力を **MyAddressInput** などのわかりやすい名前に変更します。  
  
6.  **[接続マネージャー]** ページで、フラット ファイル接続マネージャーを追加または作成し、**MyFlatFileDestConnectionManager** などのわかりやすい名前を付けます。  
  
7.  **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックし、続きのスクリプトを入力します。 スクリプト開発環境を閉じます。  
  
8.  **[スクリプト変換エディター]** を閉じ、サンプルを実行します。  
  
```vb  
Imports System.IO  
...  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Dim copiedAddressFile As String  
    Private textWriter As StreamWriter  
    Private columnDelimiter As String = ","  
  
    Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
        Dim connMgr As IDTSConnectionManager100 = _  
            Me.Connections.MyFlatFileDestConnectionManager  
        copiedAddressFile = CType(connMgr.AcquireConnection(Nothing), String)  
  
    End Sub  
  
    Public Overrides Sub PreExecute()  
  
        textWriter = New StreamWriter(copiedAddressFile, False)  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With textWriter  
            If Not Row.AddressID_IsNull Then  
                .Write(Row.AddressID)  
            End If  
            .Write(columnDelimiter)  
            If Not Row.City_IsNull Then  
                .Write(Row.City)  
            End If  
            .WriteLine()  
        End With  
  
    End Sub  
  
    Public Overrides Sub PostExecute()  
  
        textWriter.Close()  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System.IO;  
public class ScriptMain:  
    UserComponent  
  
{  
    string copiedAddressFile;  
    private StreamWriter textWriter;  
    private string columnDelimiter = ",";  
  
    public override void AcquireConnections(object Transaction)  
    {  
  
        IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileDestConnectionManager;  
        copiedAddressFile = (string) connMgr.AcquireConnection(null);  
  
    }  
  
    public override void PreExecute()  
    {  
  
        textWriter = new StreamWriter(copiedAddressFile, false);  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            if (!Row.AddressID_IsNull)  
            {  
                textWriter.Write(Row.AddressID);  
            }  
            textWriter.Write(columnDelimiter);  
            if (!Row.City_IsNull)  
            {  
                textWriter.Write(Row.City);  
            }  
            textWriter.WriteLine();  
        }  
  
    }  
  
    public override void PostExecute()  
    {  
  
        textWriter.Close();  
  
    }  
  
}  
```  
  
## <a name="see-also"></a>参照  
 [スクリプト コンポーネントによる変換元の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-source-with-the-script-component.md)   
 [カスタム変換先コンポーネントの開発](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)  
  
  
