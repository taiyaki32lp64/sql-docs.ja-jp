---
title: スクリプト コンポーネントによるエラー出力の強化 | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ba095c6aa132a816dc63377d0b04f559df6a6853
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71297076"
---
# <a name="enhancing-an-error-output-with-the-script-component"></a>スクリプト コンポーネントによるエラー出力の強化

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  既定では、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のエラー出力の 2 つの追加列 (ErrorCode と ErrorColumn) には、エラー番号を表す数値コードと、エラーが発生した列の ID しか含まれていません。 これらの数値は、対応するエラーの説明と列の名前がないとあまり役に立ちません。  
  
 ここでは、スクリプト コンポーネントを使用して、データ フローの既存のエラー出力データにエラーの説明と列名を追加する方法を説明します。 この例では、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> インターフェイスの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> メソッドを使用して、事前定義された特定の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] エラー コードに対応するエラーの説明を追加します。これは、スクリプト コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> プロパティから使用できます。 次いで、この例では、同じインターフェイスの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData130.GetIdentificationStringByID%2A> メソッドを使用してキャプチャした系列 ID に対応する列名を追加します。  
  
> [!NOTE]  
>  複数のデータ フロー タスクおよび複数のパッケージでより簡単に再利用できるコンポーネントを作成する場合は、このスクリプト コンポーネント サンプルのコードを基にした、カスタム データ フロー コンポーネントの作成を検討してください。 詳細については、「 [カスタム データ フロー コンポーネントの開発](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」を参照してください。  
  
## <a name="example"></a>例  
 次に示す例では、変換として構成されたスクリプト コンポーネントを使用して、データ フローの既存のエラー出力データにエラー説明と列名を追加します。  
  
 スクリプト コンポーネントをデータ フローで変換として使用するための構成方法の詳細については、「[スクリプト コンポーネントによる同期変換の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)」および「[スクリプト コンポーネントによる非同期変換の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)」を参照してください。  
  
#### <a name="to-configure-this-script-component-example"></a>このスクリプト コンポーネントの例を構成するには  
  
1.  新しいスクリプト コンポーネントを作成する前に、データ フローの上流コンポーネントを構成して、エラーや切り捨てが発生した場合に行をエラー出力にリダイレクトするようにします。 テスト目的の場合、たとえば、参照が失敗するような 2 つのテーブル間の参照変換を構成するなどして、エラーが発生するような形でコンポーネントを構成します。  
  
2.  新しいスクリプト コンポーネントを [データ フロー] デザイナー画面に追加し、変換として構成します。  
  
3.  上流コンポーネントからのエラー出力を新しいスクリプト コンポーネントに接続します。  
  
4.  **[スクリプト変換エディター]** を開き、 **[スクリプト]** ページの **[ScriptLanguage]** プロパティでスクリプト言語を選択します。  
  
5.  **[スクリプトの編集]** をクリックして [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE を開き、以下に示すサンプル コードを追加します。  
  
6.  VSTA を閉じます。  
  
7.  スクリプト変換エディターの **[入力列]** ページで、[ErrorCode] 列と [ErrorColumn] 列を選択します。  
  
8.  **[入力および出力]** ページで、2 つの新しい列を追加します。  
  
    -   **ErrorDescription** という **String** 型の新しい出力列を追加します。 長いメッセージをサポートするために、新しい列の既定の長さを 255 に拡張します。  
  
    -   **ColumnName** という **String** 型の別の新しい出力列を追加します。 長い値をサポートするために、新しい列の既定の長さを 255 に拡張します。  
  
9. **[スクリプト変換エディター]** を閉じます。  
  
10. スクリプト コンポーネントの出力を、適切な変換先にアタッチします。 アドホック テスト用に最も構成しやすいのは、フラット ファイル変換先です。  
  
11. パッケージを実行します。  

```vb
Public Class ScriptMain      ' VB
    Inherits UserComponent
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)

        Row.ErrorDescription = _
            Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)

        Dim componentMetaData130 = TryCast(Me.ComponentMetaData, IDTSComponentMetaData130)

        If componentMetaData130 IsNot Nothing Then

            If Row.ErrorColumn = 0 Then
                ' 0 means no specific column is identified by ErrorColumn, this time.
                Row.ColumnName = "Check the row for a violation of a foreign key constraint."
            ELSE If Row.ErrorColumn = -1 Then
                ' -1 means you are using Table Lock for a Memory Optimised destination table which is not supported.
                Row.ColumnName = "Table lock is not compatible with Memory Optimised tables."
            Else
                Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn)
            End If
        End If
    End Sub
End Class
```

```csharp
public class ScriptMain:      // C#
    UserComponent
{
    public override void Input0_ProcessInputRow(Input0Buffer Row)
    {
        Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);

        var componentMetaData130 = this.ComponentMetaData as IDTSComponentMetaData130;
        if (componentMetaData130 != null)
        {
            // 0 means no specific column is identified by ErrorColumn, this time.
            if (Row.ErrorColumn == 0)
            {
                Row.ColumnName = "Check the row for a violation of a foreign key constraint.";
            }
            // -1 means you are using Table Lock for a Memory Optimised destination table which is not supported.
            else if (Row.ErrorColumn == -1)
            {
                Row.ColumnName = "Table lock is not compatible with Memory Optimised tables.";
            }
            else
            {
                Row.ColumnName = componentMetaData130.GetIdentificationStringByID(Row.ErrorColumn);
            }
        }
    }
}
```

## <a name="see-also"></a>参照  
 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)   
 [データ フロー コンポーネントでのエラー出力の使用](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [スクリプト コンポーネントによる同期変換の作成](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
  
  
