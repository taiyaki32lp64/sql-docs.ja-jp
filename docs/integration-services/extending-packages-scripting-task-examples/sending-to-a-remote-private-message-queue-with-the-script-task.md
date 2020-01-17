---
title: スクリプト タスクによるリモート プライベート メッセージ キューへの送信 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], remote private message queues
- Message Queue task [Integration Services]
- Script task [Integration Services], examples
ms.assetid: 636314fd-d099-45cd-8bb4-f730d0a06739
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 53fc016bc4657dd1dce7dd0eefcbea58a28ae14e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296992"
---
# <a name="sending-to-a-remote-private-message-queue-with-the-script-task"></a>スクリプト タスクによるリモート プライベート メッセージ キューへの送信

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  メッセージ キュー (MSMQ) では、開発者がメッセージを送受信することにより、アプリケーション プログラムとすばやく確実に通信できます。 メッセージ キューは、ローカル コンピューターまたはリモート コンピューターに存在し、パブリックであることも、プライベートであることもあります。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] の MSMQ 接続マネージャーとメッセージ キュー タスクでは、リモート コンピューター上のプライベート キューへの送信はサポートされません。 ただし、スクリプト タスクを使用することにより、リモート プライベート キューにメッセージを簡単に送信できます。  
  
> [!NOTE]  
>  複数のパッケージでより簡単に再利用できるタスクを作成する場合は、このスクリプト タスク サンプルのコードを基にした、カスタム タスクの作成を検討してください。 詳細については、「 [カスタム タスクの開発](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)」を参照してください。  
  
## <a name="description"></a>[説明]  
 次の例では、既存の MSMQ 接続マネージャーを System.Messaging 名前空間のオブジェクトおよびメソッドと共に使用して、パッケージ変数に含まれているテキストをリモート プライベート メッセージ キューに送信します。 MSMQ 接続マネージャーの M:Microsoft.SqlServer.Dts.ManagedConnections.MSMQConn.AcquireConnection(System.Object) メソッドの呼び出しにより、その **Send** メソッドがこのタスクを実行する **MessageQueue** が返されます。  
  
#### <a name="to-configure-this-script-task-example"></a>このスクリプト タスクの例を構成するには  
  
1.  既定の名前を使用して MSMQ 接続マネージャーを作成します。 有効なリモート プライベート キューのパスを次の形式で設定します。  
  
    ```  
    FORMATNAME:DIRECT=OS:<computername>\private$\<queuename>  
    ```  
  
2.  メッセージ テキストをスクリプトに渡すために、**String** 型の **MessageText** という名前の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 変数を作成します。 この変数の値として既定のメッセージを入力します。  
  
3.  スクリプト タスクをデザイン画面に追加して編集します。 **[スクリプト タスク エディター]** の **[スクリプト]** タブで、**ReadOnlyVariables** プロパティに `MessageText` 変数を追加し、この変数をスクリプト内で使用できるようにします。  
  
4.  **[スクリプトの編集]** をクリックして、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) スクリプト エディターを開きます。  
  
5.  スクリプト プロジェクトに **System.Messaging** 名前空間への参照を追加します。  
  
6.  スクリプト ウィンドウの内容を、次のコードで置き換えます。  
  
## <a name="code"></a>コード  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.Messaging  
  
Public Class ScriptMain  
  
    Public Sub Main()  
  
        Dim remotePrivateQueue As MessageQueue  
        Dim messageText As String  
  
        remotePrivateQueue = _  
            DirectCast(Dts.Connections("Message Queue Connection Manager").AcquireConnection(Dts.Transaction), _  
            MessageQueue)  
        messageText = DirectCast(Dts.Variables("MessageText").Value, String)  
        remotePrivateQueue.Send(messageText)  
  
        Dts.TaskResult = ScriptResults.Success  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Messaging;  
  
public class ScriptMain  
{  
  
    public void Main()  
        {  
  
            MessageQueue remotePrivateQueue = new MessageQueue();  
            string messageText;  
  
            remotePrivateQueue = (MessageQueue)(Dts.Connections["Message Queue Connection Manager"].AcquireConnection(Dts.Transaction) as MessageQueue);  
            messageText = (string)(Dts.Variables["MessageText"].Value);  
            remotePrivateQueue.Send(messageText);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
```  
  
## <a name="see-also"></a>参照  
 [メッセージ キュー タスク](../../integration-services/control-flow/message-queue-task.md)  
  
  
