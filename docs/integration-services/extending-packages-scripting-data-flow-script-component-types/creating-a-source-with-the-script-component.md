---
title: スクリプト コンポーネントによる変換元の作成 | Microsoft Docs
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
- Script component [Integration Services], source components
- output columns [Integration Services]
- sources [Integration Services], components
ms.assetid: 547c4179-ea82-4265-8c6f-04a2aa77a3c0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6b3362c4761d6ad17618a2c390ada247be9071f1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296446"
---
# <a name="creating-a-source-with-the-script-component"></a>スクリプト コンポーネントによる変換元の作成

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのデータ フロー内で変換元コンポーネントを使用すると、データ ソースからデータを読み込み、下流にある変換や変換先に渡すことができます。 通常、データ ソースへの接続には、既存の接続マネージャーを使用します。  
  
 スクリプト コンポーネントの概要については、「[スクリプト コンポーネントによるデータ フローの拡張](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)」を参照してください。  
  
 スクリプト コンポーネントおよびそれによって生成されるインフラストラクチャ コードを活用すれば、カスタム データ フロー コンポーネントを開発するための手順を大幅に簡略化できます。 スクリプト コンポーネントの動作のしくみを理解するため、カスタム データ フロー コンポーネントの開発手順を理解しておくと役立つ場合があります。 「[カスタム データ フロー コンポーネントの開発](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」セクション、特に「[カスタム変換元コンポーネントの開発](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)」トピックを参照してください。  
  
## <a name="getting-started-with-a-source-component"></a>変換元コンポーネントの概要  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの [データ フロー] ペインにスクリプト コンポーネントを追加すると、 **[スクリプト コンポーネントの種類を選択]** ダイアログ ボックスが開き、[変換元]、[変換先]、[変換] スクリプトのいずれかを選択するように求められます。 このダイアログ ボックスで、 **[変換元]** を選択します。  
  
## <a name="configuring-a-source-component-in-metadata-design-mode"></a>メタデータ デザイン モードでの変換元コンポーネントの構成  
 変換元コンポーネントの作成を選択したら、 **[スクリプト変換エディター]** を使用して、コンポーネントを構成します。 詳細については、「[スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)」を参照してください。  
  
 データ フロー変換元コンポーネントに入力はありませんが、1 つ以上の出力を設定できます。 コンポーネントの出力の設定は、メタデータ デザイン モードでカスタム スクリプトを記述する前に完了する必要のある手順の 1 つです。これを行うには、 **[スクリプト変換エディター]** を使用します。  
  
 **[スクリプト変換エディター]** の **[スクリプト]** ページにある **[ScriptLanguage]** プロパティを設定して、スクリプト言語を指定することもできます。  
  
> [!NOTE]  
>  スクリプト コンポーネントとスクリプト タスクの既定のスクリプト言語を設定するには、 **[オプション]** ダイアログ ボックスの **[全般]** ページにある **[スクリプト言語]** オプションを使用します。 詳細については、「 [General Page](~/integration-services/control-flow/script-task-editor-general-page.md)」を参照してください。  
  
### <a name="adding-connection-managers"></a>接続マネージャーの追加  
 通常、変換元コンポーネントは既存の接続マネージャーを使用してデータ ソースに接続し、データをデータ フローに読み込みます。 **[スクリプト変換エディター]** の **[接続マネージャー]** ページで **[追加]** をクリックして、適切な接続マネージャーを追加します。  
  
 ただし、接続マネージャーは、便宜上、特定の種類のデータ ソースに接続するために必要な情報をカプセル化して格納するユニットにすぎません。 データの読み込みや保存、場合によってはデータ ソースとの接続や切断を行うためには、独自のカスタム コードを記述する必要もあります。  
  
 スクリプト コンポーネントで接続マネージャーを使用する方法の一般情報については、「[スクリプト コンポーネントでのデータ ソースへの接続](../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)」を参照してください。  
  
 **[スクリプト変換エディター]** の **[接続マネージャー]** ページの詳細については、「[スクリプト変換エディター &#40;[接続マネージャー] ページ&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-connection-managers-page.md)」を参照してください。  
  
### <a name="configuring-outputs-and-output-columns"></a>出力および出力列の設定  
 変換元コンポーネントに入力はありませんが、1 つ以上の出力を設定できます。 **[スクリプト変換エディター]** の **[入力および出力]** ページには、既定で 1 つの出力が作成されていますが、出力列は作成されていません。 エディターのこのページで、必要に応じて以下の項目を設定します。  
  
-   各出力に対する出力列は、手動で追加して設定する必要があります。 各出力に対する [出力列] フォルダーを選択し、 **[列の追加]** および **[列の削除]** ボタンを使用して、変換元コンポーネントの各出力に対する出力列を管理します。 後でスクリプト内で出力列を参照する際には、ここで割り当てた名前、および自動生成されたコードによって作成された、型指定されたアクセサー プロパティを使用します。  
  
-   予期しない値を含む行に対するシミュレートされたエラー出力など、1 つ以上の出力を追加して作成できます。 **[出力の追加]** および **[出力の削除]** ボタンを使用して、変換元コンポーネントの出力を管理します。 すべての入力行は使用可能なすべての出力に送られます。ただし、出力の **ExclusionGroup** プロパティに 0 以外の同じ値を指定すると、各行を、同じ **ExclusionGroup** の値を共有する出力のうちいずれか 1 つにのみ送ることもできます。 **ExclusionGroup** を識別するために選択された整数値に、特別な意味はありません。  
  
    > [!NOTE]  
    >  すべての行を出力しない場合は、0 以外の **ExclusionGroup** プロパティ値を単一の出力で使用することもできます。 ただし、この場合は、出力に送信する各行について、**DirectRowTo\<outputbuffer>** メソッドを明示的に呼び出す必要があります。  
  
-   出力にはわかりやすい名前を付けておくことができます。 後で出力を参照する際には、スクリプト内での名前、および自動生成されたコードによって作成された、型指定されたアクセサー プロパティを使用します。  
  
-   通常、同じ **ExclusionGroup** 内の複数の出力には、同じ出力列が含まれます。 ただし、シミュレートされたエラー出力を作成するには、エラー情報を格納するために列の追加が必要になる場合があります。 データ フロー エンジンがエラー行を処理する方法については、「[データ フロー コンポーネントでのエラー出力の使用](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)」を参照してください。 ただし、スクリプト コンポーネントでは、独自のコードを記述して、追加した列に該当するエラー情報を格納する必要があります。 詳細については、「[スクリプト コンポーネントに対するエラー出力のシミュレート](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)」を参照してください。  
  
 **[スクリプト変換エディター]** の **[入力および出力]** ページの詳細については、「[[スクリプト変換エディター] &#40;[入力および出力] ページ&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)」を参照してください。  
  
### <a name="adding-variables"></a>変数の追加  
 値をスクリプト内で使用する既存の変数がある場合は、 **[スクリプト変換エディター]** の **[スクリプト]** ページで、**ReadOnlyVariables** および **ReadWriteVariables** プロパティ フィールドに追加できます。  
  
 プロパティ フィールドに複数の変数を入力する場合は、変数名をコンマで区切ります。 また、**ReadOnlyVariables** および **ReadWriteVariables** プロパティ フィールドの横にある省略記号 ( **[...]** ) ボタンをクリックして **[変数の選択]** ダイアログ ボックスで変数を選択することで、複数の変数を入力することもできます。  
  
 スクリプト コンポーネントで変数を使用する方法に関する一般情報については、「[スクリプト コンポーネントでの変数の使用](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)」を参照してください。  
  
 **[スクリプト変換エディター]** の **[スクリプト]** ページの詳細については、「[[スクリプト変換エディター] &#40;[スクリプト] ページ&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md)」を参照してください。  
  
## <a name="scripting-a-source-component-in-code-design-mode"></a>コード デザイン モードでの変換元コンポーネントのスクリプト作成  
 コンポーネントのメタデータを構成したら、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE を開き、カスタム スクリプトのコードを作成します。 VSTA を開くには、 **[スクリプト変換エディター]** の **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックします。 **[ScriptLanguage]** プロパティで選択したスクリプト言語に応じて [!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual Basic または [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# のいずれかを使用し、独自のスクリプトを記述できます。  
  
 スクリプト コンポーネントを使用して作成されたすべての種類のコンポーネントに適用される重要な情報については、「[スクリプト コンポーネントのコーディングおよびデバッグ](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)」を参照してください。  
  
### <a name="understanding-the-auto-generated-code"></a>自動生成されたコードについて  
 変換元コンポーネントを作成して構成した後で VSTA IDE を開くと、コード エディターには編集可能な **ScriptMain** クラスが表示されます。 この **ScriptMain** クラスにカスタム コードを記述します。  
  
 **ScriptMain** クラスには、**CreateNewOutputRows** メソッドのスタブが含まれています。 **CreateNewOutputRows** は、変換元コンポーネントの最重要メソッドです。  
  
 VSTA の **[プロジェクト エクスプローラー]** ウィンドウを開くと、スクリプト コンポーネントにより、**BufferWrapper** および **ComponentWrapper** というプロジェクト アイテムが、読み取り専用の状態で自動生成されていることもわかります。 **ScriptMain** クラスは、**ComponentWrapper** プロジェクト アイテム内の **UserComponent** クラスから継承されます。  
  
 実行時には、データ フロー エンジンが **UserComponent** クラスの **PrimeOutput** メソッドを呼び出します。これにより、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 親クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> メソッドがオーバーライドされます。 次に、**PrimeOutput** メソッドは以下のメソッドを呼び出します。  
  
1.  **CreateNewOutputRows** メソッド。これを **ScriptMain** でオーバーライドして、最初は空である出力バッファーに、データ ソースの行を追加します。  
  
2.  **FinishOutputs** メソッド。既定では空です。 このメソッドを **ScriptMain** でオーバーライドして、出力を完了するために必要な処理を実行します。  
  
3.  **MarkOutputsAsFinished** プライベート メソッド。これは、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 親クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.SetEndOfRowset%2A> メソッドを呼び出し、出力が完了したことをデータ フロー エンジンに示します。 独自のコードで明示的に **SetEndOfRowset** を呼び出す必要はありません。  
  
### <a name="writing-your-custom-code"></a>カスタム コードの記述  
 カスタム変換元コンポーネントの作成を終了するには、必要に応じて **ScriptMain** クラスで使用できる次のメソッドにスクリプトを記述する場合があります。  
  
1.  外部データ ソースに接続する場合は、**AcquireConnections** メソッドをオーバーライドします。 接続マネージャーから、接続オブジェクトまたは必要な接続情報を抽出します。  
  
2.  変換元データをすべて同時に読み込める場合は、**PreExecute** メソッドをオーバーライドしてデータを読み込みます。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへの [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続に対して **SqlCommand** を実行し、すべての変換元データを同時に **SqlDataReader** に読み込むことができます。 変換元データを 1 行ずつ読み込む必要がある場合 (たとえば、テキスト ファイルを読み取る場合)、は、**CreateNewOutputRows** で行をループする際にデータを読み込むことができます。  
  
3.  オーバーライドされた **CreateNewOutputRows** メソッドを使用して、空の出力バッファーに新しい行を追加し、新しい出力行に各列の値を入力します。 各出力バッファーの **AddRow** メソッドを使用して空の新しい行を追加し、各列の値を設定します。 通常は、外部ソースから読み込まれた列から値をコピーします。  
  
4.  **PostExecute** メソッドをオーバーライドして、データの処理を終了します。 たとえば、データを読み込むために使用した **SqlDataReader** を閉じることができます。  
  
5.  **ReleaseConnections** メソッドを必要に応じてオーバーライドして、外部データ ソースとの接続を切断します。  
  
## <a name="examples"></a>使用例  
 次の例では、変換元コンポーネントを作成するために、**ScriptMain** クラスで必要なカスタム コードを示します。  
  
> [!NOTE]  
>  これらの例では、**AdventureWorks** サンプル データベースの **Person.Address** テーブルを使用して、その第 1 列および第 4 列、つまり、**intAddressID** 列および **nvarchar(30)City** 列をデータ フローにそのまま渡します。 このセクションの変換元、変換、および変換先の例でも、同じデータが使用されます。 他の前提条件および仮定条件については、それぞれの例で説明します。  
  
### <a name="adonet-source-example"></a>ADO.NET ソースの例  
 この例では、既存の [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のテーブルからデータを読み込み、データ フローに送る変換元コンポーネントを示します。  
  
 このサンプル コードを実行する場合は、パッケージやコンポーネントを次のように構成する必要があります。  
  
1.  **SqlClient** プロバイダーを使用する [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを作成して、**AdventureWorks** データベースに接続します。  
  
2.  新しいスクリプト コンポーネントを [データ フロー] デザイナー画面に追加し、変換元として構成します。  
  
3.  **[スクリプト変換エディター]** を開きます。 **[入力および出力]** ページで、既定の出力を **MyAddressOutput** などのわかりやすい名前に変更し、**AddressID** と **City** という 2 つの出力列を追加して構成します。  
  
    > [!NOTE]  
    >  **City** 出力列のデータ型は必ず DT_WSTR に変更してください。  
  
4.  **[接続マネージャー]** ページで、[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 接続マネージャーを追加または作成し、**MyADONETConnection** などの名前を付けます。  
  
5.  **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックし、続きのスクリプトを入力します。 その後、スクリプト開発環境と **[スクリプト変換エディター]** を閉じます。  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の変換先、または「[スクリプト コンポーネントによる変換先の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)」で説明されている変換先コンポーネントの例など、**AddressID** および **City** 列が予期される変換先コンポーネントを作成して構成します。 変換元のコンポーネントを変換先に接続します (変換なしで直接変換元を変換先に接続することもできます)。**AdventureWorks** データベースで次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを実行して、変換先テーブルを作成できます。  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  サンプルを実行します。  
  
    ```vb  
    Imports System.Data.SqlClient  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Dim connMgr As IDTSConnectionManager100  
        Dim sqlConn As SqlConnection  
        Dim sqlReader As SqlDataReader  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            connMgr = Me.Connections.MyADONETConnection  
            sqlConn = CType(connMgr.AcquireConnection(Nothing), SqlConnection)  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            Dim cmd As New SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn)  
            sqlReader = cmd.ExecuteReader  
  
        End Sub  
  
        Public Overrides Sub CreateNewOutputRows()  
  
            Do While sqlReader.Read  
                With MyAddressOutputBuffer  
                    .AddRow()  
                    .AddressID = sqlReader.GetInt32(0)  
                    .City = sqlReader.GetString(1)  
                End With  
            Loop  
  
        End Sub  
  
        Public Overrides Sub PostExecute()  
  
            sqlReader.Close()  
  
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
        SqlDataReader sqlReader;  
  
        public override void AcquireConnections(object Transaction)  
        {  
            connMgr = this.Connections.MyADONETConnection;  
            sqlConn = (SqlConnection)connMgr.AcquireConnection(null);  
  
        }  
  
        public override void PreExecute()  
        {  
  
            SqlCommand cmd = new SqlCommand("SELECT AddressID, City, StateProvinceID FROM Person.Address", sqlConn);  
            sqlReader = cmd.ExecuteReader();  
  
        }  
  
        public override void CreateNewOutputRows()  
        {  
  
            while (sqlReader.Read())  
            {  
                {  
                    MyAddressOutputBuffer.AddRow();  
                    MyAddressOutputBuffer.AddressID = sqlReader.GetInt32(0);  
                    MyAddressOutputBuffer.City = sqlReader.GetString(1);  
                }  
            }  
  
        }  
  
        public override void PostExecute()  
        {  
  
            sqlReader.Close();  
  
        }  
  
        public override void ReleaseConnections()  
        {  
  
            connMgr.ReleaseConnection(sqlConn);  
  
        }  
  
    }  
    ```  
  
### <a name="flat-file-source-example"></a>フラット ファイル ソースの例  
 この例では、既存のフラット ファイル接続マネージャーを使用して、フラット ファイルからデータを読み込み、データ フローに送る変換元コンポーネントを示します。 フラット ファイル ソースのデータは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] からエクスポートすることにより作成されます。  
  
 このサンプル コードを実行する場合は、パッケージやコンポーネントを次のように構成する必要があります。  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードを使用して、**AdventureWorks** サンプル データベースから、**Person.Address** テーブルをコンマ区切りフラット ファイルにエクスポートします。 この例では、ファイル名を ExportedAddresses.txt とします。  
  
2.  エクスポートされたデータ ファイルに接続するフラット ファイル接続マネージャーを作成します。  
  
3.  新しいスクリプト コンポーネントを [データ フロー] デザイナー画面に追加し、変換元として構成します。  
  
4.  **[スクリプト変換エディター]** を開きます。 **[入力および出力]** ページで、既定の出力を **MyAddressOutput** などのわかりやすい名前に変更します。 **AddressID** と **City** という 2 つの出力列を追加して構成します。  
  
5.  **[接続マネージャー]** ページで、**MyFlatFileSrcConnectionManager** などのわかりやすい名前を使用して、フラット ファイル接続マネージャーを追加または作成します。  
  
6.  **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックし、続きのスクリプトを入力します。 その後、スクリプト開発環境と **[スクリプト変換エディター]** を閉じます。  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の変換先、または「[スクリプト コンポーネントによる変換先の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)」で説明されている変換先コンポーネントの例など、変換先コンポーネントを作成して構成します。 変換元のコンポーネントを変換先に接続します (変換なしで直接変換元を変換先に接続することもできます)。**AdventureWorks** データベースで次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを実行して、変換先テーブルを作成できます。  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  サンプルを実行します。  
  
    ```vb  
    Imports System.IO  
    ...  
    Public Class ScriptMain  
        Inherits UserComponent  
  
        Private textReader As StreamReader  
        Private exportedAddressFile As String  
  
        Public Overrides Sub AcquireConnections(ByVal Transaction As Object)  
  
            Dim connMgr As IDTSConnectionManager100 = _  
                Me.Connections.MyFlatFileSrcConnectionManager  
            exportedAddressFile = _  
                CType(connMgr.AcquireConnection(Nothing), String)  
  
        End Sub  
  
        Public Overrides Sub PreExecute()  
            MyBase.PreExecute()  
            textReader = New StreamReader(exportedAddressFile)  
        End Sub  
  
        Public Overrides Sub CreateNewOutputRows()  
  
            Dim nextLine As String  
            Dim columns As String()  
  
            Dim delimiters As Char()  
            delimiters = ",".ToCharArray  
  
            nextLine = textReader.ReadLine  
            Do While nextLine IsNot Nothing  
                columns = nextLine.Split(delimiters)  
                With MyAddressOutputBuffer  
                    .AddRow()  
                    .AddressID = columns(0)  
                    .City = columns(3)  
                End With  
                nextLine = textReader.ReadLine  
            Loop  
  
        End Sub  
  
        Public Overrides Sub PostExecute()  
            MyBase.PostExecute()  
            textReader.Close()  
  
        End Sub  
  
    End Class  
    ```  
  
    ```csharp  
    using System.IO;  
    public class ScriptMain:  
        UserComponent  
  
    {  
        private StreamReader textReader;  
        private string exportedAddressFile;  
  
        public override void AcquireConnections(object Transaction)  
        {  
  
            IDTSConnectionManager100 connMgr = this.Connections.MyFlatFileSrcConnectionManager;  
            exportedAddressFile = (string)connMgr.AcquireConnection(null);  
  
        }  
  
        public override void PreExecute()  
        {  
            base.PreExecute();  
            textReader = new StreamReader(exportedAddressFile);  
        }  
  
        public override void CreateNewOutputRows()  
        {  
  
            string nextLine;  
            string[] columns;  
  
            char[] delimiters;  
            delimiters = ",".ToCharArray();  
  
            nextLine = textReader.ReadLine();  
            while (nextLine != null)  
            {  
                columns = nextLine.Split(delimiters);  
                {  
                    MyAddressOutputBuffer.AddRow();  
                    MyAddressOutputBuffer.AddressID = columns[0];  
                    MyAddressOutputBuffer.City = columns[3];  
                }  
                nextLine = textReader.ReadLine();  
            }  
  
        }  
  
        public override void PostExecute()  
        {  
  
            base.PostExecute();  
            textReader.Close();  
  
        }  
  
    }  
    ```  
  
## <a name="see-also"></a>参照  
 [スクリプト コンポーネントによる変換先の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)   
 [カスタム変換元コンポーネントの開発](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)  
  
  
