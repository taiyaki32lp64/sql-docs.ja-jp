---
title: スクリプト コンポーネントによるエラー出力の強化 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- transformations [Integration Services], components
- Script component [Integration Services], examples
- error outputs [Integration Services], enhancing
- Script component [Integration Services], transformation components
ms.assetid: f7c02709-f1fa-4ebd-b255-dc8b81feeaa5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3dd935387e8d6e4a95a25d21eb5d5d229f9599bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62895491"
---
# <a name="enhancing-an-error-output-with-the-script-component"></a>スクリプト コンポーネントによるエラー出力の強化
  既定では、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のエラー出力の 2 つの追加列 (ErrorCode と ErrorColumn) には、エラー番号を表す数値コードと、エラーが発生した列の ID しか含まれていません。 これらの数値は、対応するエラー説明がないとあまり役に立ちません。  
  
 ここでは、スクリプト コンポーネントを使用して、データ フローの既存のエラー出力データにエラー説明の列を追加する方法を説明します。 この例では、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> インターフェイスの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> メソッドを使用して、事前定義された特定の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] エラー コードに対応するエラーの説明を追加します。これは、スクリプト コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> プロパティから使用できます。  
  
> [!NOTE]  
>  複数のデータ フロー タスクおよび複数のパッケージでより簡単に再利用できるコンポーネントを作成する場合は、このスクリプト コンポーネント サンプルのコードを基にした、カスタム データ フロー コンポーネントの作成を検討してください。 詳細については、「 [カスタム データ フロー コンポーネントの開発](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)」を参照してください。  
  
## <a name="example"></a>例  
 次に示す例では、変換として構成されたスクリプト コンポーネントを使用して、データ フローの既存のエラー出力データにエラー説明の列を追加します。  
  
 データ フローで変換として使用するためのスクリプト コンポーネントを構成する方法の詳細については、次を参照してください[スクリプト コンポーネントによる同期変換の作成](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)と[、非同期の作成。スクリプト コンポーネントによる変換](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)します。  
  
#### <a name="to-configure-this-script-component-example"></a>このスクリプト コンポーネントの例を構成するには  
  
1.  新しいスクリプト コンポーネントを作成する前に、データ フローの上流コンポーネントを構成して、エラーや切り捨てが発生した場合に行をエラー出力にリダイレクトするようにします。 テスト目的の場合、たとえば、参照が失敗するような 2 つのテーブル間の参照変換を構成するなどして、エラーが発生するような形でコンポーネントを構成します。  
  
2.  新しいスクリプト コンポーネントを [データ フロー] デザイナー画面に追加し、変換として構成します。  
  
3.  上流コンポーネントからのエラー出力を新しいスクリプト コンポーネントに接続します。  
  
4.  **[スクリプト変換エディター]** を開き、 **[スクリプト]** ページの **[ScriptLanguage]** プロパティでスクリプト言語を選択します。  
  
5.  **[スクリプトの編集]** をクリックして [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE を開き、以下に示すサンプル コードを追加します。  
  
6.  VSTA を閉じます。  
  
7.  スクリプト変換エディターで、**入力列**ページで、[ErrorCode] 列を選択します。  
  
8.  **入力と出力**型の新しい出力列の追加 ページで、`String`という**ErrorDescription**。 長いメッセージをサポートするために、新しい列の既定の長さを 255 に拡張します。  
  
9. **[スクリプト変換エディター]** を閉じます。  
  
10. スクリプト コンポーネントの出力を、適切な変換先にアタッチします。 アドホック テスト用に最も構成しやすいのは、フラット ファイル変換先です。  
  
11. パッケージを実行します。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
  Row.ErrorDescription = _  
    Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
{  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
  
  Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
    }  
}  
  
```  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [データのエラー処理](../data-flow/error-handling-in-data.md)   
 [データ フロー コンポーネントでのエラー出力の使用](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [スクリプト コンポーネントによる同期変換の作成](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) 
  
  
