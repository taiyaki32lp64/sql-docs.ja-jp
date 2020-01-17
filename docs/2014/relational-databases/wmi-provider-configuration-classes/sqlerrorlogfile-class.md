---
title: SqlErrorLogFile クラス |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
ms.assetid: 2b83ae4a-c0d4-414c-b6e5-a41ec7c13159
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 8c5c6f1998cffc268a57318e0124f74d3411a3b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63249316"
---
# <a name="sqlerrorlogfile-class"></a>SqlErrorLogFile クラス
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログ ファイルの情報の表示に関するプロパティを提供します。  
  
## <a name="syntax"></a>構文  
  
```  
  
class SQLErrorLogFile  
{  
   uint32ArchiveNumber;  
   stringInstanceName;  
   datetimeLastModified;  
   uint32LogFileSize;  
   stringName;  
  
};  
```  
  
## <a name="properties"></a>プロパティ  
 SQLErrorLogFile クラスは、次のプロパティを定義します。  
  
|||  
|-|-|  
|ArchiveNumber|データ型: `uint32`<br /><br /> アクセスの種類:読み取り専用です。<br /><br /> <br /><br /> ログ ファイルのアーカイブ番号。|  
|InstanceName|データ型: `string`<br /><br /> アクセスの種類:読み取り専用です。<br /><br /> 修飾子:キー<br /><br /> <br /><br /> ログ ファイルが存在する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前。|  
|LastModified|データ型: `datetime`<br /><br /> アクセスの種類:読み取り専用です。<br /><br /> <br /><br /> ログ ファイルの最終変更日。|  
|LogFileSize|データ型: `uint32`<br /><br /> アクセスの種類:読み取り専用です。<br /><br /> <br /><br /> ログ ファイルのサイズ (バイト単位)。|  
|名前|データ型: `string`<br /><br /> アクセスの種類:読み取り専用です。<br /><br /> 修飾子:キー<br /><br /> <br /><br /> ログ ファイルの名前。|  
  
## <a name="remarks"></a>コメント  
  
|||  
|-|-|  
|MOF|Sqlmgmprovider xpsp2up.mof|  
|DLL|Sqlmgmprovider.dll|  
|Namespace|\root\Microsoft\SqlServer\ComputerManagement10|  
  
## <a name="example"></a>例  
 次の例では、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス上にあるすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログ ファイルに関する情報を取得します。 例を実行する置換\< *Instance_Name*> 'Instance1' など、インスタンスの名前に置き換えます。  
  
```  
on error resume next  
set strComputer = "."  
set objWMIService = GetObject("winmgmts:\\.\root\Microsoft\SqlServer\ComputerManagement10")  
set LogFiles = objWmiService.ExecQuery("SELECT * FROM SqlErrorLogFile WHERE InstanceName = '<Instance_Name>'")  
  
For Each logFile in LogFiles  
  
WScript.Echo "Instance Name:  " & logFile.InstanceName & vbNewLine _  
    & "Log File Name:  " & logFile.Name & vbNewLine _  
    & "Archive Number: " & logFile.ArchiveNumber & vbNewLine _  
    & "Log File Size:  " & logFile.LogFileSize & " bytes" & vbNewLine _  
    & "Last Modified:  " & logFile.LastModified & vbNewLine _  
  
Next   
```  
  
## <a name="comments"></a>コメント  
 ときに*InstanceName*が指定されていない WQL ステートメントで、クエリには、既定のインスタンスの情報が返されます。 たとえば、次の WQL ステートメントは、既定のインスタンス (MSSQLSERVER) からすべてのログ ファイルに関する情報を返します。  
  
```  
"SELECT * FROM SqlErrorLogFile"  
```  
  
## <a name="security"></a>セキュリティ  
 接続するため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ログ ファイルは、WMI からはローカルおよびリモートの両方のコンピューターで次のアクセス許可が必要があります。  
  
-   読み取りアクセス、 **root \microsoft\sqlserver\computermanagement10** WMI 名前空間。 既定では、すべてのユーザーがアカウントの有効化権限による読み取りアクセスを持ちます。  
  
    > [!NOTE]  
    >  WMI のアクセス許可を確認する方法については、トピックの [セキュリティ] セクションを参照してください。[オフライン ログ ファイルの表示](../logs/view-offline-log-files.md)します。  
  
-   エラー ログを格納したフォルダーへの読み取り権限。 既定では、エラー ログは、次のパスにあります (ここ\<*ドライブ >* インストール先ドライブを表す[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と\< *InstanceName*> は、インスタンスの名前[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])。  
  
     **\<ドライブ >: \Program Files\Microsoft SQL Server\MSSQL11** **.\<InstanceName > \MSSQL\Log**  
  
 ファイアウォール経由で接続する場合は、リモート ターゲット コンピューターのファイアウォールで WMI 用に例外が設定されていることを確認する必要があります。 詳細については、次を参照してください。 [WMI は、Windows Vista でリモート起動に接続する](https://go.microsoft.com/fwlink/?LinkId=178848)します。  
  
## <a name="see-also"></a>参照  
 [SqlErrorLogEvent クラス](sqlerrorlogevent-class.md)   
 [オフライン ログ ファイルの表示](../logs/view-offline-log-files.md)  
  
  
