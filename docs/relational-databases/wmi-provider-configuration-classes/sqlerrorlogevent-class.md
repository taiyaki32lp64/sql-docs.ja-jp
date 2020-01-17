---
title: SqlErrorLogEvent クラス
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f77b7a36e51d08aa3ae82b5d42e28b0173d750cb
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659027"
---
# <a name="sqlerrorlogevent-class"></a>SqlErrorLogEvent クラス
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログ ファイル内のイベントの表示に関するプロパティを提供します。  
  
## <a name="syntax"></a>構文  
  
```  
  
class SQLErrorLogEvent   
{  
   stringFileName;  
   stringInstanceName;  
   datetimeLogDate;  
   stringMessage;  
   stringProcessInfo;  
};  
```  
  
## <a name="properties"></a>プロパティ  
 SQLErrorLogEvent クラスは、次のプロパティを定義します。  
  
|||  
|-|-|  
|FileName|データ型:**文字列**<br /><br /> アクセスの種類: 読み取り専用<br /><br /> <br /><br /> エラー ログ ファイルの名前です。|  
|InstanceName|データ型:**文字列**<br /><br /> アクセスの種類: 読み取り専用<br /><br /> 修飾子: キー<br /><br /> ログ ファイルが存在する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前。|  
|LogDate|データ型: **datetime**<br /><br /> アクセスの種類: 読み取り専用<br /><br /> 修飾子: キー<br /><br /> <br /><br /> イベントがログ ファイルに記録された日時。|  
|メッセージ|データ型:**文字列**<br /><br /> アクセスの種類: 読み取り専用<br /><br /> <br /><br /> イベント メッセージ。|  
|ProcessInfo|データ型:**文字列**<br /><br /> アクセスの種類: 読み取り専用<br /><br /> <br /><br /> イベントのソース サーバー プロセス ID (SPID) に関する情報。|  
  
## <a name="remarks"></a>Remarks  
  
|||  
|-|-|  
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|名前空間|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>例  
 次の例では、指定したログ ファイルに記録されたすべてのイベントの値を取得する方法を示します。 この例を実行するには、\<*Instance_Name*> を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの名前 (' Instance1 ' など) に置き換え、' File_Name ' をエラーログファイルの名前 (' log. 1 ' など) に置き換えます。  
  
```  
on error resume next  
strComputer = "."  
Set objWMIService = GetObject("winmgmts:" _  
    & "{impersonationLevel=impersonate}!\\" _  
    & strComputer & "\root\MICROSOFT\SqlServer\ComputerManagement10")  
set logEvents = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogEvent WHERE InstanceName = '<Instance_Name>' AND FileName = 'File_Name'")  
  
For Each logEvent in logEvents  
WScript.Echo "Instance Name: " & logEvent.InstanceName & vbNewLine _  
    & "Log Date: " & logEvent.LogDate & vbNewLine _  
    & "Log File Name: " & logEvent.FileName & vbNewLine _  
    & "Process Info: " & logEvent.ProcessInfo & vbNewLine _  
    & "Message: " & logEvent.Message & vbNewLine _  
  
Next  
```  
  
## <a name="comments"></a>コメント  
 WQL ステートメントで*InstanceName*または*FileName*が指定されていない場合、クエリは既定のインスタンスと現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログファイルに関する情報を返します。 たとえば、次の WQL ステートメントでは、既定のインスタンス (MSSQLSERVER) の現在のログファイル (エラーログ) からすべてのログイベントが返されます。  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>Security  
 WMI を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログファイルに接続するには、ローカルコンピューターとリモートコンピューターの両方に対して次のアクセス許可を持っている必要があります。  
  
-   **Root\Microsoft\SqlServer\ComputerManagement10** WMI 名前空間への読み取りアクセス。 既定では、すべてのユーザーがアカウントの有効化権限による読み取りアクセスを持ちます。  
  
-   エラー ログを格納したフォルダーへの読み取り権限。 既定では、エラーログは次のパスにあります (\<*ドライブ >* は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールしたドライブを表し、\<*InstanceName*> は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの名前です)。  
  
     **\<Drive >: Server\MSSQL13 を実行** **します。\<InstanceName > \MSSQL\Log**  
  
 ファイアウォール経由で接続する場合は、リモート ターゲット コンピューターのファイアウォールで WMI 用に例外が設定されていることを確認する必要があります。 詳細については、「 [Windows Vista 以降で WMI にリモート接続する](https://go.microsoft.com/fwlink/?LinkId=178848)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Sqlerrorlogfile クラス](../../relational-databases/wmi-provider-configuration-classes/sqlerrorlogfile-class.md)   
 [オフライン ログ ファイルの表示](../../relational-databases/logs/view-offline-log-files.md)  
  
  
