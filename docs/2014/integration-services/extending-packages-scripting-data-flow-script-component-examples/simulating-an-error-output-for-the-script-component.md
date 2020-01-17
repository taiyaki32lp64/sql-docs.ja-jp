---
title: スクリプト コンポーネントに対するエラー出力のシミュレート | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script component [Integration Services], error output
- error outputs [Integration Services], Script component
ms.assetid: f8b6ecff-ac99-4231-a0e7-7ce4ad76bad0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b7e2324fcfce6c560000bfef798aa966102d674b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62895511"
---
# <a name="simulating-an-error-output-for-the-script-component"></a>スクリプト コンポーネントに対するエラー出力のシミュレート
  エラー行の自動処理のスクリプト コンポーネントでエラー出力として出力を直接構成することはできませんが、別の出力を作成するか、可能な場合はスクリプトで条件ロジックを使用してこの出力に行を送信することによって、組み込みエラー出力の機能を再現することができます。 2 つの出力列を追加してエラー番号、およびエラーが発生した列の ID を受け取ることにより、組み込みエラー出力の動作を模倣することもできます。  
  
 事前定義された特定の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] エラー コードに対応するエラーの説明を追加する場合は、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.GetErrorDescription%2A> インターフェイスの <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> メソッドを使用できます。これは、スクリプト コンポーネントの <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> プロパティから使用できます。  
  
## <a name="example"></a>例  
 次に示す例では、2 つの同期出力を持つ変換として構成された、スクリプト コンポーネントを使用します。 このスクリプト コンポーネントの目的は、AdventureWorks サンプル データベースの住所データから、エラー行をフィルター選択することです。 この架空の例では、北米の顧客向けプロモーションを準備中であり、北米以外の住所をフィルターによって除外する必要があるものとします。  
  
#### <a name="to-configure-the-example"></a>例を構成するには  
  
1.  新しいスクリプト コンポーネントの作成前に、接続マネージャーを作成し、AdventureWorks サンプル データベースから住所データを選択するデータ フローの変換元を構成します。 この例では CountryRegionName 列のみを調べるので、単純に Person.vStateCountryProvinceRegion ビューを使用できます。また、Person.Address、Person.StateProvince、および Person.CountryRegion の表を結合して、データを選択することもできます。  
  
2.  新しいスクリプト コンポーネントを [データ フロー] デザイナー画面に追加し、変換として構成します。 **[スクリプト変換エディター]** を開きます。  
  
3.  **[スクリプト]** ページの **[ScriptLanguage]** プロパティに、スクリプトのコード作成に使用するスクリプト言語を設定します。  
  
4.  **[スクリプトの編集]** をクリックして、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) を開きます。  
  
5.  `Input0_ProcessInputRow` メソッドに、以下に示すサンプル コードを入力するか貼り付けます。  
  
6.  VSTA を閉じます。  
  
7.  **[入力列]** ページで、スクリプト変換で処理する列を選択します。 この例では CountryRegionName 列のみを使用します。 選択しなかった使用可能な入力列は、データ フロー内で変更されず、そのまま渡されます。  
  
8.  **入力と出力**ページ、新しい追加、2 つ目の出力、および設定の`SynchronousInputID`にも、値の入力の ID 値の`SynchronousInputID`既定の出力のプロパティ。 両方の出力の `ExclusionGroup` プロパティを 0 以外の同じ値 (たとえば 1) に設定し、各行が 2 つの出力のうち一方のみに送られるようにします。 新しいエラー出力に、"MyErrorOutput" などのわかりやすい名前を付けます。  
  
9. 必要なエラー情報を取得するため、追加の出力列を新しいエラー出力に追加します。エラー コード、エラーが発生した列の ID、エラーの説明などを含めることができます。 この例では、新しい列 ErrorColumn および ErrorMessage を作成しています。 事前定義された [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] エラーを独自の実装で検出する場合、エラー番号用の ErrorCode 列を必ず追加してください。  
  
10. スクリプト コンポーネントがエラー状態を確認する入力列 (複数の場合もある) の ID 値を書き留めます。 この例では、この列 ID を使用して ErrorColumn 値を設定します。  
  
11. **[スクリプト変換エディター]** を閉じます。  
  
12. スクリプト コンポーネントの出力を、適切な変換先にアタッチします。 アドホック テスト用に最も構成しやすいのは、フラット ファイル変換先です。  
  
13. パッケージを実行します。  
  
```vb  
Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
  If Row.CountryRegionName <> "Canada" _  
      And Row.CountryRegionName <> "United States" Then  
  
    Row.ErrorColumn = 68 ' ID of CountryRegionName column  
    Row.ErrorMessage = "Address is not in North America."  
    Row.DirectRowToMyErrorOutput()  
  
  Else  
  
    Row.DirectRowToOutput0()  
  
  End If  
  
End Sub  
```  
  
```csharp  
public override void Input0_ProcessInputRow(Input0Buffer Row)  
{  
  
  if (Row.CountryRegionName!="Canada"&&Row.CountryRegionName!="United States")  
  
  {  
    Row.ErrorColumn = 68; // ID of CountryRegionName column  
    Row.ErrorMessage = "Address is not in North America.";  
    Row.DirectRowToMyErrorOutput();  
  
  }  
  else  
  {  
  
    Row.DirectRowToOutput0();  
  
  }  
  
}  
```  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>関連項目  
 [データのエラー処理](../data-flow/error-handling-in-data.md)   
 [データ フロー コンポーネントでのエラー出力の使用](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)   
 [スクリプト コンポーネントによる同期変換の作成](../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md) 
  
  
