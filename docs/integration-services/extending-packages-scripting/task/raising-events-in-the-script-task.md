---
title: スクリプト タスクでのイベントの発生 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- events [Integration Services], scripts
- warnings [Integration Services]
- SSIS events, scripts
- errors [Integration Services], events
- SSIS Script task, events
- Events property
- Script task [Integration Services], events
ms.assetid: 21ea07d1-e267-4fb1-a6cc-82c95a39beae
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f213a9eb8375f05967700a6aeec81bae5e41ec1d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71286057"
---
# <a name="raising-events-in-the-script-task"></a>スクリプト タスクでのイベントの発生

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  イベントは、エラーや警告、タスクの進行状況や状態などのその他の情報を、親パッケージにレポートする方法を提供するものです。 パッケージには、イベントの通知機能を管理するためのイベント ハンドラーがあります。 スクリプト タスクは、**Dts** オブジェクトの <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> プロパティに対してメソッドを呼び出して、イベントを発生させることができます。 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] パッケージのイベントの処理の詳細については、「[Integration Services &#40;SSIS&#41; のイベント ハンドラー](../../../integration-services/integration-services-ssis-event-handlers.md)」を参照してください。  
  
 イベントは、パッケージ内で有効な任意のログ プロバイダーに記録できます。 ログ プロバイダーは、イベントに関する情報をデータ ストアに保存します。 スクリプト タスクは、イベントを発生させずに <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> メソッドを使用して、情報をログ プロバイダーに記録することもできます。 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> メソッドの使用方法の詳細については、「[スクリプト タスクでのログ記録](../../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)」を参照してください。  
  
 イベントを発生させるには、スクリプト タスクは <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> プロパティによって公開されるメソッドのいずれかを呼び出します。 次の表に、<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> プロパティにより公開されているメソッドの一覧を示します。  
  
|イベント|[説明]|  
|-----------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireCustomEvent%2A>|パッケージ内でユーザー定義のカスタム イベントを発生させます。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A>|パッケージにエラー条件を通知します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireInformation%2A>|ユーザーに情報を提供します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireProgress%2A>|タスクの進行状況をパッケージに通知します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireQueryCancel%2A>|パッケージがタスクを途中でシャットダウンする必要があるかどうかを示す値を返します。|  
|<xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A>|エラー条件ではないが、タスクがユーザーに通知する正当な理由がある状態であることをパッケージに通知します。|  
  
## <a name="events-example"></a>イベントの例  
 次の例では、スクリプト タスク内でイベントを発生させる方法を示します。 この例では、ネイティブ Windows API 関数を使用して、インターネット接続が使用できるかどうかを確認します。 接続が使用できない場合、エラーを発生させます。 使用されているモデム接続が切断される可能性がある場合、この例では警告が発生します。 それ以外の場合は、インターネット接続が検出されたことを示す情報メッセージを返します。  
  
```vb  
Private Declare Function InternetGetConnectedState Lib "wininet" _  
    (ByRef dwFlags As Long, ByVal dwReserved As Long) As Long  
  
Private Enum ConnectedStates  
    LAN = &H2  
    Modem = &H1  
    Proxy = &H4  
    Offline = &H20  
    Configured = &H40  
    RasInstalled = &H10  
End Enum  
  
Public Sub Main()  
  
    Dim dwFlags As Long  
    Dim connectedState As Long  
    Dim fireAgain as Boolean  
  
    connectedState = InternetGetConnectedState(dwFlags, 0)  
  
    If connectedState <> 0 Then  
        If (dwFlags And ConnectedStates.Modem) = ConnectedStates.Modem Then  
            Dts.Events.FireWarning(0, "Script Task Example", _  
                "Volatile Internet connection detected.", String.Empty, 0)  
        Else  
            Dts.Events.FireInformation(0, "Script Task Example", _  
                "Internet connection detected.", String.Empty, 0, fireAgain)  
        End If  
    Else  
        ' If not connected to the Internet, raise an error.  
        Dts.Events.FireError(0, "Script Task Example", _  
            "Internet connection not available.", String.Empty, 0)  
    End If  
  
    Dts.TaskResult = ScriptResults.Success  
  
End Sub  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Windows.Forms;  
using System.Runtime.InteropServices;  
  
public class ScriptMain  
{  
  
[DllImport("wininet")]  
        private extern static long InternetGetConnectedState(ref long dwFlags, long dwReserved);  
  
        private enum ConnectedStates  
        {  
            LAN = 0x2,  
            Modem = 0x1,  
            Proxy = 0x4,  
            Offline = 0x20,  
            Configured = 0x40,  
            RasInstalled = 0x10  
        };  
  
        public void Main()  
        {  
            //  
            long dwFlags = 0;  
            long connectedState;  
            bool fireAgain = true;  
            int state;  
  
            connectedState = InternetGetConnectedState(ref dwFlags, 0);  
            state = (int)ConnectedStates.Modem;  
            if (connectedState != 0)  
            {  
                if ((dwFlags & state) == state)  
                {  
                    Dts.Events.FireWarning(0, "Script Task Example", "Volatile Internet connection detected.", String.Empty, 0);  
                }  
                else  
                {  
                    Dts.Events.FireInformation(0, "Script Task Example", "Internet connection detected.", String.Empty, 0, ref fireAgain);  
                }  
            }  
            else  
            {  
                // If not connected to the Internet, raise an error.  
                Dts.Events.FireError(0, "Script Task Example", "Internet connection not available.", String.Empty, 0);  
            }  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
```  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; のイベント ハンドラー](../../../integration-services/integration-services-ssis-event-handlers.md)   
 [パッケージにイベント ハンドラーを追加する](https://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  
