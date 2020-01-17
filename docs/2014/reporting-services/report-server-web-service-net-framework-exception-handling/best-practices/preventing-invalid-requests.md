---
title: 無効な要求の回避 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- invalid requests [Reporting Services]
- exceptions [Reporting Services], invalid requests
- valid requests [Reporting Services]
ms.assetid: 4a4a2d97-4c10-43a9-8298-ef5a820ea549
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dcb850ad7e99768781b225978f531ff991766924
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046079"
---
# <a name="preventing-invalid-requests"></a>無効な要求の回避
  アプリケーション フローを分析し、レポート サーバーに送信される要求が有効であることを確認することによって、ある種類の例外がスローされないようにすることができます。 たとえば、ユーザーがレポートの名前、データ ソース、その他のレポート サーバー アイテムを追加または更新できるアプリケーションで、ユーザーが入力するテキストを検証する必要があります。 また、要求をレポート サーバーに送信する前に予約文字を常に確認する必要があります。 コードで条件付きの **if** ステートメントまたは他の論理構造を使って、要求をレポート サーバーに送信するために必要な条件を満たしていないことをユーザーに警告します。  
  
 次の単純な C# の例では、ユーザーがスラッシュ (/) 文字を含む名前でレポートを作成しようとすると、わかりやすいエラー メッセージが表示されます。  
  
```  
// C#  
private void PublishReport()  
{  
   int index;  
   string reservedChar;  
   string message;  
  
   // Check the text value of the name text box for "/",  
   // a reserved character  
   index = nameTextBox.Text.IndexOf(@"/");  
  
   if ( index != -1) // The text contains the character  
   {  
      reservedChar = nameTextBox.Text.Substring(index, 1);  
      // Build a user-friendly error message  
      message = "The name of the report cannot contain the reserved character " +  
         "\"" + reservedChar + "\". " +  
         "Please enter a valid name for the report. " +  
         "For more information about reserved characters, " +  
         "see the help documentation";  
  
      MessageBox.Show(message, "Invalid Input Error");  
   }  
   else // Publish the report  
   {  
      Byte[] definition = null;  
      Warning[] warnings = {};  
      string name = nameTextBox.Text;  
  
      FileStream stream = File.OpenRead("MyReport.rdl");  
      definition = new Byte[stream.Length];  
      stream.Read(definition, 0, (int) stream.Length);  
      stream.Close();  
      // Create report with user-defined name  
      rs.CreateCatalogItem("Report", name, "/Samples", false, definition, null, out warnings);  
      MessageBox.Show("Report: {0} created successfully", name);  
   }  
}  
```  
  
 要求がレポート サーバーに送信される前に回避できるエラーの種類については、「[SoapException エラー テーブル](../soapexception-class/soapexception-errors-table.md)」を参照してください。 try ブロックまたは catch ブロックを使用して上記の例をさらに強化した内容については、「[Try ブロックと Catch ブロックの使用](using-try-and-catch-blocks.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [Reporting Services における例外処理の概要](../introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException クラス](../soapexception-class/reporting-services-soapexception-class.md)  
  
  
