---
title: 無効な要求の回避 | Microsoft Docs
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-exception-handling
ms.topic: reference
helpviewer_keywords:
- invalid requests [Reporting Services]
- exceptions [Reporting Services], invalid requests
- valid requests [Reporting Services]
ms.assetid: 4a4a2d97-4c10-43a9-8298-ef5a820ea549
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 219fc1883f395e56f1fd73af32e95ea066df28b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62992215"
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
  
 要求がレポート サーバーに送信される前に回避できるエラーの種類については、「[SoapException エラー テーブル](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)」を参照してください。 try ブロックまたは catch ブロックを使用して上記の例をさらに強化した内容については、「[Try ブロックと Catch ブロックの使用](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-try-and-catch-blocks.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Reporting Services における例外処理の概要](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Reporting Services SoapException クラス](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)  
  
  
