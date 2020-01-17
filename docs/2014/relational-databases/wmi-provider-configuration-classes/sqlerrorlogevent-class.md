---
title: SqlErrorLogEvent クラス |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- SqlErrorLogEvent class
- SqlErrorLogFile class
ms.assetid: bde6c467-38d0-4766-a7af-d6c9d6302b07
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 558e60a5638ab3af75c5450e3f6fc22c6f9d9601
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721073"
---
# <a name="sqlerrorlogevent-class"></a>SqlErrorLogEvent クラス
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
  
## <a name="properties"></a>[プロパティ]  
 SQLErrorLogEvent クラスは、次のプロパティを定義します。  
  
|||  
|-|-|  
|FileName|データ型: `string`<br /><br /> アクセスの種類:読み取り専用です。<br /><br /> <br /><br /> エラー ログ ファイルの名前です。|  
|InstanceName|データ型: `string`<br /><br /> アクセスの種類:読み取り専用です。<br /><br /> 修飾子:キー<br /><br /> ログ ファイルが存在する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前。|  
|よう|データ型: `datetime`<br /><br /> アクセスの種類:読み取り専用です。<br /><br /> 修飾子:キー<br /><br /> <br /><br /> イベントがログ ファイルに記録された日時。|  
|メッセージ|データ型: `string`<br /><br /> アクセスの種類:読み取り専用です。<br /><br /> <br /><br /> イベント メッセージ。|  
|ProcessInfo|データ型: `string`<br /><br /> アクセスの種類:読み取り専用です。<br /><br /> <br /><br /> イベントのソース サーバー プロセス ID (SPID) に関する情報。|  
  
## <a name="remarks"></a>コメント  
  
|||  
|-|-|  
|MOF|Sqlmgmproviderxpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|Namespace|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>例  
 次の例では、指定したログ ファイルに記録されたすべてのイベントの値を取得する方法を示します。 例を実行する\< *Instance_Name*> のインスタンスの名前を持つ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を 'Instance1' など 'を 'errorlog.1' など、エラー ログ ファイルの名前を持つ ' File_Name' に置き換えます。  
  
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
 ときに*InstanceName*または*FileName*クエリが既定のインスタンスと現在の情報を返す WQL ステートメントで提供されていない[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログ ファイル。 たとえば、次の WQL ステートメントは既定のインスタンス (MSSQLSERVER) の現在のログ ファイル (ERRORLOG) からすべてのログ イベントを返します。  
  
```  
"SELECT * FROM SqlErrorLogEvent"  
```  
  
## <a name="security"></a>セキュリティ  
 接続するため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログ ファイルは、WMI からはローカルおよびリモートの両方のコンピューターで次のアクセス許可が必要があります。  
  
-   読み取りアクセス、 **root \microsoft\sqlserver\computermanagement10** WMI 名前空間。 既定では、すべてのユーザーがアカウントの有効化権限による読み取りアクセスを持ちます。  
  
-   エラー ログを格納したフォルダーへの読み取り権限。 既定では、エラー ログは、次のパスにあります (ここ\<*ドライブ >* インストール先ドライブを表す[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と\< *InstanceName*> は、インスタンスの名前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。  
  
     **\<ドライブ >: \Program Files\Microsoft SQL Server\MSSQL12** **.\<InstanceName > \MSSQL\Log**  
  
 ファイアウォール経由で接続する場合は、リモート ターゲット コンピューターのファイアウォールで WMI 用に例外が設定されていることを確認する必要があります。 詳細については、次を参照してください。 [WMI は、Windows Vista でリモート起動に接続する](https://go.microsoft.com/fwlink/?LinkId=178848)します。  
  
## <a name="see-also"></a>参照  
 [SqlErrorLogFile クラス](sqlerrorlogfile-class.md)   
 [オフライン ログ ファイルの表示](../logs/view-offline-log-files.md)  
  
  
