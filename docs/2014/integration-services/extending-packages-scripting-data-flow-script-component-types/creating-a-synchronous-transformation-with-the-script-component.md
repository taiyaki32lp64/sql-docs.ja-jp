---
title: スクリプト コンポーネントによる同期変換の作成 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: aa1bee1a-ab06-44d8-9944-4bff03d73016
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7e2fc735cd4834fcb6e59550604b831b5d8790fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768592"
---
# <a name="creating-a-synchronous-transformation-with-the-script-component"></a>スクリプト コンポーネントによる同期変換の作成
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのデータ フロー内で変換コンポーネントを使用することにより、変換元から変換先にデータが受け渡される過程で、データを修正または分析できます。 同期出力型の変換では、各入力列はコンポーネントを通過するたびに処理されます。 非同期出力型の変換では、処理を完了するための入力列をすべて受け取ってから、処理が行われます。 このトピックでは、同期変換について説明します。 非同期変換については、「[スクリプト コンポーネントによる非同期変換の作成](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)」を参照してください。 同期コンポーネントと非同期コンポーネントの相違点の詳細については、「[同期変換と非同期変換について](../understanding-synchronous-and-asynchronous-transformations.md)」を参照してください。  
  
 スクリプト コンポーネントの概要については、「[スクリプト コンポーネントによるデータ フローの拡張](../extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)」を参照してください。  
  
 スクリプト コンポーネントおよびそれによって生成されるインフラストラクチャ コードを活用すれば、カスタム データ フロー コンポーネントを開発するための手順を大幅に簡略化できます。 ただし、スクリプト コンポーネントのしくみを理解するため、「[カスタム データ フロー コンポーネントの開発](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」のセクション、特に「[同期出力型のカスタム変換コンポーネントの開発](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)」を参照して、カスタム データ フロー コンポーネントを開発する場合に従う必要がある手順に目を通しておくと役立つことがあります。  
  
## <a name="getting-started-with-a-synchronous-transformation-component"></a>同期変換コンポーネントの概要  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの [データ フロー] ペインにスクリプト コンポーネントを追加すると、 **[スクリプト コンポーネントの種類を選択]** ダイアログ ボックスが開き、[変換元]、[変換先]、[変換] コンポーネントの種類のいずれかを選択するように求められます。 このダイアログ ボックスで、 **[変換]** を選択します。  
  
## <a name="configuring-a-synchronous-transformation-component-in-metadata-design-mode"></a>メタデータ デザイン モードでの同期変換コンポーネントの構成  
 変換コンポーネントを作成するオプションを選択したら、 **[スクリプト変換エディター]** を使用して、コンポーネントを構成します。 詳細については、「[スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](../extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)」を参照してください。  
  
 スクリプト コンポーネントのスクリプト言語を設定するには、 **[スクリプト変換エディター]** の **[スクリプト]** ページにある **[ScriptLanguage]** プロパティを設定します。  
  
> [!NOTE]  
>  スクリプト コンポーネントの既定のスクリプト言語を設定するには、 **[オプション]** ダイアログ ボックスの **[全般]** ページにある **[スクリプト言語]** オプションを使用します。 詳細については、「 [General Page](../general-page-of-integration-services-designers-options.md)」を参照してください。  
  
 データ フロー変換コンポーネントには 1 つの入力があり、1 つ以上の出力がサポートされます。 コンポーネントの入力および出力の設定は、メタデータ デザイン モードでカスタム スクリプトを記述する前に完了する必要のある手順の 1 つです。これを行うには、 **[スクリプト変換エディター]** を使用します。  
  
### <a name="configuring-input-columns"></a>入力列の設定  
 変換コンポーネントには 1 つの入力があります。  
  
 **[スクリプト変換エディター]** の **[入力列]** ページには、データ フローの上流コンポーネントの出力で使用できる列が一覧表示されます。 変換する列、またはそのまま出力する列を選択します。 変換するすべての列の適切な場所に、読み取り/書き込みのマークを付けます。  
  
 **[スクリプト変換エディター]** の **[入力列]** ページの詳細については、「[[スクリプト変換エディター] &#40;[入力列] ページ&#41;](../script-transformation-editor-input-columns-page.md)」を参照してください。  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>入力、出力、および出力列の設定  
 変換コンポーネントには、1 つ以上の出力を設定できます。  
  
 **[スクリプト変換エディター]** の **[入力および出力]** ページには、1 つの出力が作成されていますが、その出力に列はありません。 エディターのこのページで、必要に応じて以下の項目を設定します。  
  
-   予期しない値を含む行に対するシミュレートされたエラー出力など、1 つ以上の出力を追加して作成する場合は、 **[出力の追加]** および **[出力の削除]** ボタンを使用して、同期変換コンポーネントの出力を管理します。 すべての入力行は、使用できるすべての出力に送信されます。ただし、各行を出力のうちいずれか 1 つにリダイレクトするように指定した場合を除きます。 行をリダイレクトするように指定するには、出力の `ExclusionGroup` プロパティに 0 以外の整数値を指定します。 出力を識別するために `ExclusionGroup` に入力した整数値に特別の意味はありませんが、指定した出力のグループでは一貫して同じ整数を使用する必要があります。  
  
    > [!NOTE]  
    >  すべての行を出力しない場合は、0 以外の `ExclusionGroup` プロパティ値を単一の出力で使用することもできます。 ただし、この場合は、出力に送信する各行について、**DirectRowTo\<outputbuffer>** メソッドを明示的に呼び出す必要があります。  
  
-   入力および出力に、わかりやすい名前を割り当てます。 スクリプト コンポーネントはこの名前を使用して、型指定されたアクセサー プロパティを生成します。これは、スクリプト内で入力や出力を参照するために使用できます。  
  
-   同期変換の列は現状のままにしておきます。 通常、同期変換はデータ フローに列を追加しません。 データはバッファーの所定の位置で変更され、バッファーがデータ フロー内の次のコンポーネントに渡されます。 このような場合、変換の出力に対して明示的に出力列を追加したり構成する必要はありません。 出力がエディターに表示される際、明示的に定義された列は含まれません。  
  
-   行レベルのエラー用のシミュレートされたエラー出力に新しい列を追加します。 通常、同じ `ExclusionGroup` 内の複数の出力には、同じ出力列のセットが含まれます。 ただし、シミュレートされたエラー出力を作成するには、エラー情報を格納するために列の追加が必要となる場合があります。 データ フロー エンジンがエラー行を処理する方法については、「[データ フロー コンポーネントでのエラー出力の使用](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)」を参照してください。 スクリプト コンポーネントでは、独自のコードを記述して、追加した列に該当するエラー情報を格納する必要があるので注意してください。 詳細については、「[スクリプト コンポーネントに対するエラー出力のシミュレート](../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)」を参照してください。  
  
 **[スクリプト変換エディター]** の **[入力および出力]** ページの詳細については、「[[スクリプト変換エディター] &#40;[入力および出力] ページ&#41;](../script-transformation-editor-inputs-and-outputs-page.md)」を参照してください。  
  
### <a name="adding-variables"></a>変数の追加  
 スクリプトで既存の変数を使用する場合を追加、`ReadOnlyVariables`と`ReadWriteVariables`プロパティ フィールドに、**スクリプト**のページ、**スクリプト変換エディター**します。  
  
 プロパティ フィールドに複数の変数を追加する場合は、各変数名をコンマで区切ります。 省略記号をクリックして、複数の変数を選択することもできます ( **.** ) ボタンの横に、`ReadOnlyVariables`と`ReadWriteVariables`プロパティ フィールドでは、および内の変数を選択し、**変数の選択** ダイアログ ボックス。  
  
 スクリプト コンポーネントで変数を使用する方法に関する一般情報については、「[スクリプト コンポーネントでの変数の使用](../extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)」を参照してください。  
  
 **[スクリプト変換エディター]** の **[スクリプト]** ページの詳細については、「[[スクリプト変換エディター] &#40;[スクリプト] ページ&#41;](../script-transformation-editor-script-page.md)」を参照してください。  
  
## <a name="scripting-a-synchronous-transformation-component-in-code-design-mode"></a>コード デザイン モードでの同期変換コンポーネントのスクリプト作成  
 コンポーネントのメタデータを構成した後、カスタム スクリプトを記述できます。 **[スクリプト変換エディター]** の **[スクリプト]** ページで **[スクリプトの編集]** をクリックし、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE を開いて、カスタム スクリプトを追加できます。 使用するスクリプト言語は、 **[スクリプト]** ページの **[ScriptLanguage]** プロパティで、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic と [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# のどちらをスクリプト言語として選択したかによって決まります。  
  
 スクリプト コンポーネントを使用して作成されたすべての種類のコンポーネントに適用される重要な情報については、「[スクリプト コンポーネントのコーディングおよびデバッグ](../extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)」を参照してください。  
  
### <a name="understanding-the-auto-generated-code"></a>自動生成されたコードについて  
 変換コンポーネントを作成して構成した後で VSTA IDE を開くと、コード エディターには `ScriptMain` クラスが編集可能な状態で表示されます。また、`ProcessInputRow` メソッドがスタブとして表示されます。 カスタム コードは `ScriptMain` クラスに記述します。また、`ProcessInputRow` は変換コンポーネントの最重要メソッドです。  
  
 開く場合、**プロジェクト エクスプ ローラー** VSTA のウィンドウに、スクリプト コンポーネントが読み取り専用に生成も表示できる`BufferWrapper`と`ComponentWrapper`プロジェクト項目。 `ScriptMain`クラスから継承、`UserComponent`クラス、`ComponentWrapper`プロジェクト アイテム。  
  
 実行時には、データ フロー エンジンが `ProcessInput` クラスの `UserComponent` メソッドを呼び出します。これは親クラスである <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> の <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> メソッドをオーバーライドします。 `ProcessInput` メソッドは、入力バッファーに格納された行を順にループし、各行で 1 回ずつ `ProcessInputRow` メソッドを呼び出します。  
  
### <a name="writing-your-custom-code"></a>カスタム コードの記述  
 同期出力型の変換コンポーネントは、記述するすべてのデータ フロー コンポーネントの中で最も単純です。 たとえば、このトピックの単一出力の例は、次のカスタム コードで構成されています。  
  
```vb  
Row.City = UCase(Row.City)  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
```  
  
 同期型のカスタム変換コンポーネントの作成を完了するには、オーバーライドされた `ProcessInputRow` メソッドを使用して、入力バッファーにある各行のデータを変換します。 データ フロー エンジンは、バッファーがいっぱいになると、データ フロー内の次のコンポーネントにこのバッファーを渡します。  
  
 必要に応じて、`PreExecute` クラスで使用できる `PostExecute` メソッドや `ScriptMain` メソッドにもスクリプトを記述して、準備処理や終了後の処理を行う場合もあります。  
  
### <a name="working-with-multiple-outputs"></a>複数の出力の処理  
 使用できる 2 つ以上の出力のいずれかに入力行を送信する場合でも、前述した単一出力の例と比べて、必要なカスタム コードはそれほど多くありません。 たとえば、このトピックの 2 つの出力の例は、次のカスタム コードで構成されています。  
  
```vb  
Row.City = UCase(Row.City)  
If Row.City = "REDMOND" Then  
    Row.DirectRowToMyRedmondAddresses()  
Else  
    Row.DirectRowToMyOtherAddresses()  
End If  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
if (Row.City=="REDMOND")  
{  
    Row.DirectRowToMyRedmondAddresses();  
}  
else  
{  
    Row.DirectRowToMyOtherAddresses();  
}  
```  
  
 この例では、ユーザーが設定した出力の名前に基づき、スクリプト コンポーネントが **DirectRowTo\<OutputBufferX>** メソッドを生成します。 同様のコードを使用して、シミュレートされたエラー出力にエラー行を送信することもできます。  
  
## <a name="examples"></a>使用例  
 この例では、同期変換コンポーネントを作成するために、`ScriptMain` クラスで必要なカスタム コードを示します。  
  
> [!NOTE]  
>  これらの例を使用して、 **Person.Address**テーブルに、`AdventureWorks`サンプル データベースとの最初と 4 番目の列を渡す、 **intAddressID**と**nvarchar (30) City**列をデータ フローです。 このセクションの変換元、変換、および変換先の例でも、同じデータが使用されます。 他の前提条件および仮定条件については、それぞれの例で説明します。  
  
### <a name="single-output-synchronous-transformation-example"></a>単一出力の同期変換の例  
 この例では、単一の出力が含まれる同期変換コンポーネントを示します。 この変換では **AddressID** 列をパススルーして、**City** 列を大文字に変換します。  
  
 このサンプル コードを実行する場合は、パッケージやコンポーネントを次のように構成する必要があります。  
  
1.  新しいスクリプト コンポーネントを [データ フロー] デザイナー画面に追加し、変換として構成します。  
  
2.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで、変換元または他の変換の出力を、新しい変換コンポーネントに接続します。 この出力からデータを提供する必要があります、 **Person.Address**のテーブル、`AdventureWorks`サンプル データベースを含む、 **AddressID**と**市区町村**列。  
  
3.  **[スクリプト変換エディター]** を開きます。 **[入力列]** ページで、**AddressID** 列と **City** 列を選択します。 **City** 列を、読み取り/書き込み可能としてマークします。  
  
4.  **[入力および出力]** ページで、入力と出力を **MyAddressInput** と **MyAddressOutput** などのわかりやすい名前に変更します。 出力の `SynchronousInputID` は、入力の `ID` に対応していることに注意してください。 したがって、出力列を追加して設定する必要はありません。  
  
5.  **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックし、続きのスクリプトを入力します。 その後、スクリプト開発環境と **[スクリプト変換エディター]** を閉じます。  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の変換先、または「[スクリプト コンポーネントによる変換先の作成](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)」で説明されている変換先コンポーネントの例など、**AddressID** および **City** 列が予期される変換先コンポーネントを作成して構成します。 変換の出力を変換先コンポーネントに接続します。 `AdventureWorks` データベースで次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを実行して、変換先テーブルを作成できます。  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  サンプルを実行します。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
    }  
  
}  
```  
  
### <a name="two-output-synchronous-transformation-example"></a>2 つの出力の同期変換の例  
 この例では、2 つの出力を持つ同期変換コンポーネントを示します。 この変換では **AddressID** 列をパススルーして、**City** 列を大文字に変換します。 都市名が Redmond の場合、変換はその行を 1 つの出力に送信し、他のすべての行をもう 1 つの出力に送信します。  
  
 このサンプル コードを実行する場合は、パッケージやコンポーネントを次のように構成する必要があります。  
  
1.  新しいスクリプト コンポーネントを [データ フロー] デザイナー画面に追加し、変換として構成します。  
  
2.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで、変換元または他の変換の出力を、新しい変換コンポーネントに接続します。 この出力からデータを提供する必要があります、 **Person.Address**のテーブル、`AdventureWorks`サンプル データベースを含む、少なくとも**AddressID**と**市区町村**列。  
  
3.  **[スクリプト変換エディター]** を開きます。 **[入力列]** ページで、**AddressID** 列と **City** 列を選択します。 **City** 列を、読み取り/書き込み可能としてマークします。  
  
4.  **[入力および出力]** ページで、2 番目の出力を作成します。 新しい出力を追加したら、`SynchronousInputID` が入力の `ID` に設定されていることを確認します。 このプロパティは、既定として作成された最初の出力で既に設定されています。 各出力で、`ExclusionGroup` プロパティを 0 以外の同じ値に設定し、入力行を 2 つの相互排他的な出力に分割することを指定します。 出力列を出力に追加する必要はありません。  
  
5.  入力と出力を、**MyAddressInput**、**MyRedmondAddresses**、**MyOtherAddresses** などのわかりやすい名前に変更します。  
  
6.  **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックし、続きのスクリプトを入力します。 その後、スクリプト開発環境と **[スクリプト変換エディター]** を閉じます。  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の変換先、フラット ファイル変換先、または「[スクリプト コンポーネントによる変換先の作成](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)」で説明されている変換先コンポーネントの例など、**AddressID** および **City** 列が予期される 2 つの変換先コンポーネントを作成して構成します。 変換の各出力をいずれかの変換先コンポーネントに接続します。 変換先テーブルを作成するには、`AdventureWorks` データベースで次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドと同様のコマンド (一意のテーブル名を使用) を実行します。  
  
    ```  
    CREATE TABLE [Person].[Address2](  
        [AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL  
    ```  
  
8.  サンプルを実行します。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
        If Row.City = "REDMOND" Then  
            Row.DirectRowToMyRedmondAddresses()  
        Else  
            Row.DirectRowToMyOtherAddresses()  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
        if (Row.City == "REDMOND")  
        {  
            Row.DirectRowToMyRedmondAddresses();  
        }  
        else  
        {  
            Row.DirectRowToMyOtherAddresses();  
        }  
  
    }  
}  
```  
  
|![](./media/creating-a-synchronous-transformation-with-the-script-component/dts-16.gif)  **常に最新の Integration Services**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/msconame-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [同期および非同期変換の変換について](../understanding-synchronous-and-asynchronous-transformations.md)[スクリプト コンポーネントによる非同期変換の作成](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)[同期型のカスタム変換コンポーネントの開発出力](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
  
  
