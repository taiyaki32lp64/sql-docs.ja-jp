---
title: 手順 3:エラー フロー リダイレクトの追加 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5683a45d-9e73-4cd5-83ca-fae8b26b488c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4a3626878ba4be6d56bb56b545f3d0cdc24a407a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283200"
---
# <a name="lesson-4-3-add-error-flow-redirection"></a>レッスン 4-3: エラー フロー リダイレクションを追加する

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



前のタスクでは、壊れているサンプル フラット ファイルを Lookup Currency Key 変換で処理しようとするとエラーが発生し、変換を行うことができません。 この変換ではエラー出力に既定の設定を使用するため、エラーが発生すると変換は失敗します。 変換が失敗すると、それ以降のパッケージも失敗します。  
  
エラー出力を使用し、失敗した行を別の処理パスにリダイレクトするようにコンポーネントを構成することで、変換の失敗を回避できます。 個別のエラー処理パスを使用する場合は、より多くのオプションを利用できます。 たとえば、データを消去した後に、失敗した行を再処理することができます。 または、失敗した行を詳細なエラー情報と共に保存し、後の検証や再処理に役立てることも可能です。  
  
ここでは、失敗した行をエラー出力にリダイレクトするよう Lookup Currency Key 変換を構成します。 データ フローのエラー分岐では、これらの行が [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] によってファイルに書き込まれます。  
  
既定では、[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] エラー出力内の 2 つの追加列 (**ErrorCode** と **ErrorColumn**) には、エラーの数値コードと、エラーが発生した列の ID しか含まれていません。 この実習では、パッケージによって失敗行がファイルに書き込まれる前に、スクリプト コンポーネントを使用して [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] API にアクセスし、エラーの説明を取得します。  
  
## <a name="configure-an-error-output"></a>エラー出力を構成する  
  
1.  **[SSIS ツールボックス]** で **[共通]** を展開し、 **[スクリプト コンポーネント]** を **[データ フロー]** タブのデザイン画面にドラッグします。 **[スクリプト]** を **[Lookup Currency Key]** 変換の右に配置します。  
  
2.  **[スクリプト コンポーネントの種類を選択]** ダイアログ ボックスで、 **[変換]** を選択し、 **[OK]** を選択します。  
  
3.  2 つのコンポーネントを接続するには、 **[Lookup Currency Key]** 変換を選択して、赤色の矢印を、新しい **[スクリプト]** 変換までドラッグします。  
  
    赤い矢印は、 **[Lookup Currency Key]** 変換のエラー出力を表します。 エラー処理をスクリプト コンポーネントにリダイレクトするには、赤い矢印を使用して変換をスクリプト コンポーネントに接続します。スクリプト コンポーネントではエラーが処理され、変換先に送信されます。  
  
4.  **[エラー出力の構成]** ダイアログ ボックスの **[エラー]** 列で、 **[行のリダイレクト]** を選択し、 **[OK]** を選択します。  
  
5.  **[データ フロー]** デザイン画面で、新しい **[ScriptComponent]** にある名前 **[Script Component]** を選択し、その名前を「 **Get Error Description**」に変更します。  
  
6.  **[Get Error Description]** 変換をダブルクリックします。  
  
7.  **[スクリプト変換エディター]** ダイアログ ボックスの **[入力列]** ページで、 **[ErrorCode]** 列を選択します。  
  
8.  **[入力および出力]** ページで **[出力 0]** を展開し、 **[出力列]** を選択してから、 **[列の追加]** を選択します。  
  
9. **Name** プロパティで「*ErrorDescription*」と入力し、**DataType** プロパティを **[Unicode 文字列 [DT_WSTR]]** に設定します。  
  
10. **[スクリプト]** ページで、**LocaleID** プロパティが **[英語 (米国)]** に設定されていることを確認します。
  
11. **[スクリプトの編集]** を選択して、[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA) を開きます。 **Input0_ProcessInputRow** メソッドに、次のコードを入力するか貼り付けます。  
  
    [Visual Basic]  
  
    ```vb  
    Row.ErrorDescription =   
      Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
    ```  
  
    [Visual C#]  
  
    ```cs
    Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
    ```  
  
    完成したサブルーチンのコードは次のようになります。  
  
    [Visual Basic]  
  
    ```vb
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
  
      Row.ErrorDescription =   
        Me.ComponentMetaData.GetErrorDescription(Row.ErrorCode)  
  
    End Sub  
    ```  
  
    [Visual C#]  
  
    ```cs
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
        {  
  
            Row.ErrorDescription = this.ComponentMetaData.GetErrorDescription(Row.ErrorCode);  
  
        }  
    ```  
  
12. **[ビルド]** メニューの **[ソリューションのビルド]** を選択し、スクリプトをビルドして変更を保存し、VSTA を閉じます。  
  
13. **[OK]** を選択して、 **[スクリプト変換エディター]** ダイアログ ボックスを閉じます。  
  
## <a name="go-to-next-task"></a>次の実習に進む
[手順 4: フラット ファイル変換先を追加する](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
  
  
