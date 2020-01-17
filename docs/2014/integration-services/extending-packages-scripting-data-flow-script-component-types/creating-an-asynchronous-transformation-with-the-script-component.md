---
title: スクリプト コンポーネントによる非同期変換の作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1940405c6bde86364024e10694f9aaf1da24b06d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768618"
---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>スクリプト コンポーネントによる非同期変換の作成
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージのデータ フロー内で変換コンポーネントを使用することにより、変換元から変換先にデータが受け渡される過程で、データを修正または分析できます。 同期出力型の変換では、各入力列はコンポーネントを通過するたびに処理されます。 非同期出力型の変換では、変換が入力行をすべて受け取るまで処理の実行を待機する場合と、変換が入力行をすべて受け取る前に一部の行を出力する場合があります。 このトピックでは、非同期変換について説明します。 処理で同期変換が必要な場合は、「[スクリプト コンポーネントによる同期変換の作成](../data-flow/transformations/script-component.md)」を参照してください。 同期コンポーネントと非同期コンポーネントの相違点の詳細については、「[同期変換と非同期変換について](../understanding-synchronous-and-asynchronous-transformations.md)」を参照してください。  
  
 スクリプト コンポーネントの概要については、「[スクリプト コンポーネントによるデータ フローの拡張](../extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)」を参照してください。  
  
 スクリプト コンポーネントおよびそれによって生成されるインフラストラクチャ コードを活用すれば、カスタム データ フロー コンポーネントを開発するための手順を簡略化できます。 ただし、スクリプト コンポーネントのしくみを理解するため、「[カスタム データ フロー コンポーネントの開発](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」セクション、特に「[同期出力型のカスタム変換コンポーネントの開発](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)」を参照して、カスタム データ フロー コンポーネントを開発する場合に従う必要がある手順に目を通しておくと役立つことがあります。  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>非同期変換コンポーネントの概要  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーの [データ フロー] タブにスクリプト コンポーネントを追加すると、 **[スクリプト コンポーネントの種類を選択]** ダイアログ ボックスが表示され、変換元、変換、または変換先としてあらかじめ設定するコンポーネントの入力を求めるメッセージが表示されます。 このダイアログ ボックスで、 **[変換]** を選択します。  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>メタデータ デザイン モードでの非同期変換コンポーネントの構成  
 変換コンポーネントを作成するオプションを選択したら、 **[スクリプト変換エディター]** を使用して、コンポーネントを構成します。 詳細については、「[スクリプト コンポーネント エディターでのスクリプト コンポーネントの構成](../extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)」を参照してください。  
  
 スクリプト コンポーネントで使用するスクリプト言語を選択するには、 **[スクリプト変換エディター]** ダイアログ ボックスの **[スクリプト]** ページにある **[ScriptLanguage]** プロパティを設定します。  
  
> [!NOTE]  
>  スクリプト コンポーネントの既定のスクリプト言語を設定するには、 **[オプション]** ダイアログ ボックスの **[全般]** ページにある **[スクリプト言語]** オプションを使用します。 詳細については、「 [General Page](../general-page-of-integration-services-designers-options.md)」を参照してください。  
  
 データ フロー変換コンポーネントには 1 つの入力があり、1 つ以上の出力を設定できます。 コンポーネントの入力および出力の設定は、メタデータ デザイン モードでカスタム スクリプトを記述する前に完了する必要のある手順の 1 つです。これを行うには、 **[スクリプト変換エディター]** を使用します。  
  
### <a name="configuring-input-columns"></a>入力列の設定  
 スクリプト コンポーネントを使用して作成した変換コンポーネントには、1 つの入力があります。  
  
 **[スクリプト変換エディター]** の **[入力列]** ページには、データ フローの上流コンポーネントの出力で使用できる列が一覧表示されます。 変換する列、またはそのまま出力する列を選択します。 変換するすべての列の適切な場所に、読み取り/書き込みのマークを付けます。  
  
 **[スクリプト変換エディター]** の **[入力列]** ページの詳細については、「[[スクリプト変換エディター] &#40;[入力列] ページ&#41;](../script-transformation-editor-input-columns-page.md)」を参照してください。  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>入力、出力、および出力列の設定  
 変換コンポーネントには、1 つ以上の出力を設定できます。  
  
 通常、非同期出力型の変換には、2 つの出力を設定します。 たとえば、特定の市内にある住所を数えたい場合、1 つの出力に住所データをそのまま送り、もう 1 つの出力に集計結果を送信します。 集計結果を出力するには、新しい出力列も 1 つ必要です。  
  
 **[スクリプト変換エディター]** の **[入力および出力]** ページには、既定で 1 つの出力が作成されていますが、出力列は作成されていません。 エディターのこのページでは、次の項目を設定できます。  
  
-   集計結果の出力など、1 つ以上の出力を追加して作成する場合は、 **[出力の追加]** および **[出力の削除]** ボタンを使用して、非同期変換コンポーネントの出力を管理します。 各出力の `SynchronousInputID` プロパティを 0 に設定すると、上流コンポーネントからのデータをそのまま出力するのではなく、変換を実行して、既存の行や列の適切な位置に出力することを示します。 この設定によって、出力が入力に対して非同期になります。  
  
-   入力や出力にはわかりやすい名前を付けておくことができます。 スクリプト コンポーネントはこの名前を使用して、型指定されたアクセサー プロパティを生成します。これは、スクリプト内で入力や出力を参照するために使用できます。  
  
-   通常、非同期変換は列をデータ フローに追加します。 出力の `SynchronousInputID` プロパティが 0 の場合、上流コンポーネントからのデータはそのまま出力されず、変換を実行して、既存の行や列の適切な位置に出力されることを示します。この場合、出力に対して出力列を明示的に追加して設定する必要があります。 出力列の名前は、マップ先の入力列と同じ名前にする必要はありません。  
  
-   追加情報を格納するために列を追加する場合があります。 その場合、追加した列にデータを格納するには、独自のコードを記述する必要があります。 標準エラー出力の動作の再現については、「[スクリプト コンポーネントに対するエラー出力のシミュレート](../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)」を参照してください。  
  
 **[スクリプト変換エディター]** の **[入力および出力]** ページの詳細については、「[[スクリプト変換エディター] &#40;[入力および出力] ページ&#41;](../script-transformation-editor-inputs-and-outputs-page.md)」を参照してください。  
  
### <a name="adding-variables"></a>変数の追加  
 値をスクリプト内で使用する既存の変数がある場合は、 **[スクリプト変換エディター]** の **[スクリプト]** ページで、ReadOnlyVariables および ReadWriteVariables プロパティ フィールドに追加できます。  
  
 プロパティ フィールドに複数の変数を追加する場合は、各変数名をコンマで区切ります。 省略記号をクリックして、複数の変数を選択することもできます ( **.** ) ボタンの横に、`ReadOnlyVariables`と`ReadWriteVariables`プロパティ フィールドでは、および内の変数を選択し、**変数の選択** ダイアログ ボックス。  
  
 スクリプト コンポーネントで変数を使用する方法に関する一般情報については、「[スクリプト コンポーネントでの変数の使用](../extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)」を参照してください。  
  
 **[スクリプト変換エディター]** の **[スクリプト]** ページの詳細については、「[[スクリプト変換エディター] &#40;[スクリプト] ページ&#41;](../script-transformation-editor-script-page.md)」を参照してください。  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>コード デザイン モードでの非同期変換コンポーネントのスクリプト作成  
 コンポーネントのメタデータをすべて構成した後、カスタム スクリプトを記述できます。 **[スクリプト変換エディター]** の **[スクリプト]** ページで **[スクリプトの編集]** をクリックし、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE を開いて、カスタム スクリプトを追加できます。 使用するスクリプト言語は、 **[スクリプト]** ページの **[ScriptLanguage]** プロパティで、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic と [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# のどちらをスクリプト言語として選択したかによって決まります。  
  
 スクリプト コンポーネントを使用して作成されたすべての種類のコンポーネントに適用される重要な情報については、「[スクリプト コンポーネントのコーディングおよびデバッグ](../extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)」を参照してください。  
  
### <a name="understanding-the-auto-generated-code"></a>自動生成されたコードについて  
 作成し、編集可能な変換コンポーネントを構成した後で VSTA IDE を開くと`ScriptMain`クラスは、ProcessInputRow および CreateNewOutputRows メソッド スタブのコード エディターで表示されます。 ScriptMain クラスはカスタム コードを記述する場所であり、ProcessInputRow は変換コンポーネントの最重要メソッドです。 `CreateNewOutputRows` メソッドは変換元コンポーネントで一般的に使用され、両方のコンポーネントが独自の出力行を作成する必要のある、非同期変換と似ています。  
  
 VSTA を開く場合**プロジェクト エクスプ ローラー**ウィンドウに、スクリプト コンポーネントが読み取り専用に生成も表示できる`BufferWrapper`と`ComponentWrapper`プロジェクト項目。 ScriptMain クラス内の UserComponent クラスから継承、`ComponentWrapper`プロジェクト アイテム。  
  
 実行時に、データ フロー エンジンはで PrimeOutput メソッドを呼び出す、`UserComponent`クラスでオーバーライドされます、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost.PrimeOutput%2A>のメソッド、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>クラスの親。 その後、PrimeOutput メソッドは CreateNewOutputRows メソッドを呼び出します。  
  
 次に、データ フロー エンジンが UserComponent クラスの ProcessInput メソッドを呼び出します。これにより、<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 親クラスの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> メソッドがオーバーライドされます。 ProcessInput メソッドは、入力バッファーの行を順にループし、各行で 1 回ずつ ProcessInputRow メソッドを呼び出します。  
  
### <a name="writing-your-custom-code"></a>カスタム コードの記述  
 非同期型のカスタム変換コンポーネントの作成を完了するには、オーバーライドされた ProcessInputRow メソッドを使用して、入力バッファーの各行のデータを処理する必要があります。 出力は入力に同期しないため、データの行を明示的に出力に書き込む必要があります。  
  
 非同期変換では、AddRow メソッドを使用して、ProcessInputRow または ProcessInput メソッド内から必要に応じて行を出力に追加できます。 CreateNewOutputRows メソッドを使用する必要はありません。 集計結果などの結果の単一行を特定の出力に書き込んでいる場合は、CreateNewOutputRows メソッドを使用してあらかじめ出力行を作成し、その値をすべての入力行を処理した後に入力できます。 ただし、スクリプト コンポーネントでは入力または出力で現在の行のみを使用できるため、CreateNewOutputRows メソッドで複数の行を作成しても役に立ちません。 CreateNewOutputRows メソッドは、処理する入力行のない変換元コンポーネントでより重要になります。  
  
 また、ProcessInput メソッド自体をオーバーライドし、入力バッファー内をループして各行で ProcessInputRow を呼び出す前後に、準備処理や終了処理を追加することもできます。 ProcessInputRow 各行をループとしての特定の都市の住所の数をカウントする ProcessInput をオーバーライド コード例では、このトピックのいずれかなど、`.`例がすべての行が追加されました後に、2 番目の出力に集計値を書き込む処理されます。 この例で出力の終了処理が ProcessInput で行われているのは、PostExecute が呼び出される時点では、出力バッファーが既に使用できなくなっているためです。  
  
 必要に応じて、ScriptMain クラスで使用できる PreExecute メソッドや PostExecute メソッドにもスクリプトを記述して、準備処理や終了処理を行う場合もあります。  
  
> [!NOTE]  
>  カスタム データ フロー コンポーネントを最初から開発した場合、PrimeOutput メソッドをオーバーライドして、出力バッファーに対する参照をキャッシュに保存し、後でデータの行をバッファーに追加できるようにする必要があります。 スクリプト コンポーネントを使用する場合は、オーバーライドする必要はありません。`BufferWrapper` プロジェクト アイテム内に、各出力バッファーを表すクラスが自動生成されるためです。  
  
## <a name="example"></a>例  
 この例では、非同期変換コンポーネントを作成するために ScriptMain クラスで必要なカスタム コードを示します。  
  
> [!NOTE]  
>  これらの例では、**AdventureWorks** サンプル データベースの **Person.Address** テーブルを使用して、その第 1 列および第 4 列、つまり、**intAddressID** 列および **nvarchar(30)City** 列をデータ フローにそのまま渡します。 このセクションの変換元、変換、および変換先の例でも、同じデータが使用されます。 他の前提条件および仮定条件については、それぞれの例で説明します。  
  
 次の例では、2 つの出力を持つ非同期変換コンポーネントを示します。 この変換では、**AddressID** 列および **City** 列のデータを 1 つの出力にそのまま渡し、特定の都市 (Redmond, Washington, U.S.A.) 内にある住所の数をカウントし、その結果の値を 2 番目の出力に送ります。  
  
 このサンプル コードを実行する場合は、パッケージやコンポーネントを次のように構成する必要があります。  
  
1.  新しいスクリプト コンポーネントを [データ フロー] デザイナー画面に追加し、変換として構成します。  
  
2.  デザイナーで、変換元または他の変換の出力を、新しい変換コンポーネントに接続します。 この出力には、サンプル データベース **AdventureWorks** の **Person.Address** テーブルから、少なくとも **AddressID** 列および **City** 列を含むデータが供給される必要があります。  
  
3.  **[スクリプト変換エディター]** を開きます。 **[入力列]** ページで、**AddressID** 列と **City** 列を選択します。  
  
4.  **[入力および出力]** ページで、最初の出力の **AddressID** 出力列と **City** 出力列を追加および構成します。 2 番目の出力を追加し、集計値を格納する出力列をその出力に追加します。 この例により各入力行が最初の出力に明示的にコピーされるため、最初の出力の SynchronousInputID プロパティを 0 に設定します。 新しく作成された出力の SynchronousInputID プロパティは既に 0 に設定されています。  
  
5.  入力、出力、および新しい出力列をわかりやすい名前に変更します。 この例では、入力の名前として **MyAddressInput**、出力には **MyAddressOutput** および **MySummaryOutput** を使用し、2 番目の出力の出力列には **MyRedmondCount** を使用します。  
  
6.  **[スクリプト]** ページで、 **[スクリプトの編集]** をクリックし、続きのスクリプトを入力します。 その後、スクリプト開発環境と **[スクリプト変換エディター]** を閉じます。  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の変換先、または「[スクリプト コンポーネントによる変換先の作成](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)」で説明されている変換先コンポーネントの例など、**AddressID** および **City** 列が予期される最初の出力の変換先コンポーネントを作成して構成します。 次に、変換の最初の出力である **MyAddressOutput** を変換先コンポーネントに接続します。 **AdventureWorks** データベースで次の [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを実行して、変換先テーブルを作成できます。  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  2 番目の出力に接続する別の変換先コンポーネントを作成して構成します。 次に、変換の 2 番目の出力である **MySummaryOutput** を変換先コンポーネントに接続します。 2 番目の出力からは 1 つの値を格納した行が 1 つ出力されるだけなので、フラット ファイル接続マネージャーを使用して、1 つの列を含む新しいファイルに接続する設定を簡単に行うことができます。 この例では、この変換先の列に **MyRedmondCount** という名前を付けます。  
  
9. サンプルを実行します。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Private myRedmondAddressCount As Integer  
  
    Public Overrides Sub CreateNewOutputRows()  
  
        MySummaryOutputBuffer.AddRow()  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInput(ByVal Buffer As MyAddressInputBuffer)  
  
        While Buffer.NextRow()  
            MyAddressInput_ProcessInputRow(Buffer)  
        End While  
  
        If Buffer.EndOfRowset Then  
            MyAddressOutputBuffer.SetEndOfRowset()  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount  
            MySummaryOutputBuffer.SetEndOfRowset()  
        End If  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With MyAddressOutputBuffer  
            .AddRow()  
            .AddressID = Row.AddressID  
            .City = Row.City  
        End With  
  
        If Row.City.ToUpper = "REDMOND" Then  
            myRedmondAddressCount += 1  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    private int myRedmondAddressCount;  
  
    public override void CreateNewOutputRows()  
    {  
  
        MySummaryOutputBuffer.AddRow();  
  
    }  
  
    public override void MyAddressInput_ProcessInput(MyAddressInputBuffer Buffer)  
    {  
  
        while (Buffer.NextRow())  
        {  
            MyAddressInput_ProcessInputRow(Buffer);  
        }  
  
        if (Buffer.EndOfRowset())  
        {  
            MyAddressOutputBuffer.SetEndOfRowset();  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount;  
            MySummaryOutputBuffer.SetEndOfRowset();  
        }  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            MyAddressOutputBuffer.AddRow();  
            MyAddressOutputBuffer.AddressID = Row.AddressID;  
            MyAddressOutputBuffer.City = Row.City;  
        }  
  
        if (Row.City.ToUpper() == "REDMOND")  
        {  
            myRedmondAddressCount += 1;  
        }  
  
    }  
  
}  
  
```  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [同期変換と非同期変換について](../understanding-synchronous-and-asynchronous-transformations.md)   
 [スクリプト コンポーネントによる同期変換の作成](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
 [非同期出力型のカスタム変換コンポーネントの開発](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  
