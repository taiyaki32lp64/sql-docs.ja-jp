---
title: スクリプト タスクによる空のフラット ファイルの検出 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- flat files
- Script task [Integration Services], empty flat files
- SSIS Script task, empty flat files
- Script task [Integration Services], examples
ms.assetid: 1b4defb8-886a-483d-8056-d1b91d37bc90
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 34462589141133e04ca8728361e3a173f0944f12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62895501"
---
# <a name="detecting-an-empty-flat-file-with-the-script-task"></a>スクリプト タスクによる空のフラット ファイルの検出
  フラット ファイル ソースでは、フラット ファイルを処理する前にデータ行が含まれるかどうかを判定しません。 データ行を含まないファイルをスキップすることにより、パッケージの効率、特に多数のフラット ファイルを繰り返し処理するパッケージの効率を向上させることができます。 スクリプト タスクによって、パッケージがデータ フローの処理を開始する前に空のフラット ファイルを確認できます。  
  
> [!NOTE]  
>  複数のパッケージでより簡単に再利用できるタスクを作成する場合は、このスクリプト タスク サンプルのコードを基にした、カスタム タスクの作成を検討してください。 詳細については、「 [カスタム タスクの開発](../extending-packages-custom-objects/task/developing-a-custom-task.md)」を参照してください。  
  
## <a name="description"></a>説明  
 次の例では、`System.IO` 名前空間のメソッドを使用して、フラット ファイル接続マネージャーで指定されたフラット ファイルをテストし、ファイルが空かどうか、または列ヘッダーなどの必要な非データ行や空の行だけが含まれるかどうかを確認します。 このスクリプトは最初にファイルのサイズをチェックします。サイズがゼロ バイトの場合、ファイルは空です。 ファイル サイズがゼロより大きい場合、行がなくなるまで、または必要な非データ行の数を超えるまでファイルから行を読み取ります。 ファイル内の行数が必要な非データ行の数以下の場合、そのファイルは空と見なされます。 結果はユーザー変数内のブール値として返されます。この値は、パッケージの制御フローでの分岐に使用できます。 `FireInformation`メソッドでは、結果も表示されます、**出力**のウィンドウ、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)。  
  
#### <a name="to-configure-this-script-task-example"></a>このスクリプト タスクの例を構成するには  
  
1.  作成し、という名前のフラット ファイル接続マネージャーを構成する`EmptyFlatFileTest`します。  
  
2.  `FFNonDataRows` という名前の整数変数を作成し、その値をフラット ファイルで必要な、非データ行の数に設定します。  
  
3.  `FFIsEmpty` という名前のブール変数を作成します。  
  
4.  スクリプト タスクの **ReadOnlyVariables** プロパティに `FFNonDataRows` 変数を追加します。  
  
5.  スクリプト タスクの **ReadWriteVariables** プロパティに `FFIsEmpty` 変数を追加します。  
  
6.  コードに `System.IO` 名前空間をインポートします。  
  
 単一のフラット ファイル接続マネージャーを使用する代わりに、Foreach File 列挙子を含むファイルを繰り返し処理する場合、接続マネージャーからではなく列挙値が格納される変数からファイル名とパスを取得するように、次のサンプル コードを変更する必要があります。  
  
### <a name="code"></a>コード  
  
```vb  
Public Sub Main()  
  
  Dim nonDataRows As Integer = _  
      DirectCast(Dts.Variables("FFNonDataRows").Value, Integer)  
  Dim ffConnection As String = _  
      DirectCast(Dts.Connections("EmptyFlatFileTest").AcquireConnection(Nothing), _  
      String)  
  Dim flatFileInfo As New FileInfo(ffConnection)  
  ' If file size is 0 bytes, flat file does not contain data.  
  Dim fileSize As Long = flatFileInfo.Length  
  If fileSize > 0 Then  
    Dim lineCount As Integer = 0  
    Dim line As String  
    Dim fsFlatFile As New StreamReader(ffConnection)  
    Do Until fsFlatFile.EndOfStream  
      line = fsFlatFile.ReadLine  
      lineCount += 1  
      ' If line count > expected number of non-data rows,  
      '  flat file contains data (default value).  
      If lineCount > nonDataRows Then  
        Exit Do  
      End If  
      ' If line count <= expected number of non-data rows,  
      '  flat file does not contain data.  
      If lineCount <= nonDataRows Then  
        Dts.Variables("FFIsEmpty").Value = True  
      End If  
    Loop  
  Else  
    Dts.Variables("FFIsEmpty").Value = True  
  End If  
  
  Dim fireAgain As Boolean = False  
  Dts.Events.FireInformation(0, "Script Task", _  
      String.Format("{0}: {1}", ffConnection, _  
      Dts.Variables("FFIsEmpty").Value.ToString), _  
      String.Empty, 0, fireAgain)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            int nonDataRows = (int)(Dts.Variables["FFNonDataRows"].Value);  
            string ffConnection = (string)(Dts.Connections["EmptyFlatFileTest"].AcquireConnection(null) as String);  
            FileInfo flatFileInfo = new FileInfo(ffConnection);  
            // If file size is 0 bytes, flat file does not contain data.  
            long fileSize = flatFileInfo.Length;  
            if (fileSize > 0)  
            {  
  
                int lineCount = 0;  
                string line;  
                StreamReader fsFlatFile = new StreamReader(ffConnection);  
                while (!(fsFlatFile.EndOfStream))  
                {  
                    Console.WriteLine (fsFlatFile.ReadLine());  
                    lineCount += 1;  
                    // If line count > expected number of non-data rows,  
                    //  flat file contains data (default value).  
                    if (lineCount > nonDataRows)  
                    {  
                        break;  
                    }  
                    // If line count <= expected number of non-data rows,  
                    //  flat file does not contain data.  
                    if (lineCount <= nonDataRows)  
                    {  
                        Dts.Variables["FFIsEmpty"].Value = true;  
                    }  
                }  
            }  
            else  
            {  
                Dts.Variables["FFIsEmpty"].Value = true;  
            }  
  
            bool fireAgain = false;  
            Dts.Events.FireInformation(0, "Script Task", String.Format("{0}: {1}", ffConnection, Dts.Variables["FFIsEmpty"].Value), String.Empty, 0, ref fireAgain);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
```  
  
![Integration Services のアイコン (小)](../media/dts-16.gif "Integration Services アイコン (小)")**Integration Services の日付を維持します。**<br /> マイクロソフトが提供する最新のダウンロード、アーティクル、サンプル、ビデオ、およびコミュニティで選択されたソリューションについては、MSDN の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のページを参照してください。<br /><br /> [MSDN の Integration Services のページを参照してください。](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> これらの更新が自動で通知されるようにするには、ページの RSS フィードを定期受信します。  
  
## <a name="see-also"></a>参照  
 [スクリプト タスクの例](../extending-packages-scripting-task-examples/script-task-examples.md)  
  
  
