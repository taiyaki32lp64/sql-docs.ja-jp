---
title: Windows PowerShell への SMO アセンブリの読み込み | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 8ca42b69-da5a-47f4-9085-34e443f0e389
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cb70ab2f2098b0857ba632a3b9501d596c0af864
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798052"
---
# <a name="load-the-smo-assemblies-in-windows-powershell"></a>Windows PowerShell への SMO アセンブリの読み込み
  このトピックでは、SQL Server PowerShell プロバイダーを使用しない Windows PowerShell スクリプトに SQL Server 管理オブジェクト (SMO) アセンブリを読み込む方法について説明します。  
  
## <a name="before-you-begin"></a>作業を開始する準備  
 SMO アセンブリを読み込むための推奨メカニズムは、`sqlps` モジュールを読み込むことです。 モジュールに含まれている [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダーは、自動的に SMO アセンブリを読み込み、PowerShell スクリプトでの SMO オブジェクトの実用性を拡張する機能も実装します。  
  
 ただし、次の 2 つの場合については、直接 SMO アセンブリを読み込む必要があります。  
  
-   スクリプトが、プロバイダーを参照する最初のコマンドまたは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] スナップインのコマンドレットより先に SMO オブジェクトを参照する場合。  
  
-   プロバイダーやコマンドレットを使用しない別の言語 (C#、Visual Basic など) から SMO コードを移植する場合。  
  
## <a name="example-loading-the-sql-server-management-objects"></a>例: SQL Server 管理オブジェクトの読み込み  
 SMO アセンブリを読み込むコードを次に示します。  
  
```powershell
# Loads the SQL Server Management Objects (SMO)  
  
$ErrorActionPreference = "Stop"  
  
$sqlpsreg = "HKLM:\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Microsoft.SqlServer.Management.PowerShell.sqlps"  
  
if (Get-ChildItem $sqlpsreg -ErrorAction "SilentlyContinue")  
{  
    throw "SQL Server Provider for Windows PowerShell is not installed."  
}  
else  
{  
    $item = Get-ItemProperty $sqlpsreg  
    $sqlpsPath = [System.IO.Path]::GetDirectoryName($item.Path)  
}  
  
$assemblylist =   
"Microsoft.SqlServer.Management.Common",  
"Microsoft.SqlServer.Smo",  
"Microsoft.SqlServer.Dmf ",  
"Microsoft.SqlServer.Instapi ",  
"Microsoft.SqlServer.SqlWmiManagement ",  
"Microsoft.SqlServer.ConnectionInfo ",  
"Microsoft.SqlServer.SmoExtended ",  
"Microsoft.SqlServer.SqlTDiagM ",  
"Microsoft.SqlServer.SString ",  
"Microsoft.SqlServer.Management.RegisteredServers ",  
"Microsoft.SqlServer.Management.Sdk.Sfc ",  
"Microsoft.SqlServer.SqlEnum ",  
"Microsoft.SqlServer.RegSvrEnum ",  
"Microsoft.SqlServer.WmiEnum ",  
"Microsoft.SqlServer.ServiceBrokerEnum ",  
"Microsoft.SqlServer.ConnectionInfoExtended ",  
"Microsoft.SqlServer.Management.Collector ",  
"Microsoft.SqlServer.Management.CollectorEnum",  
"Microsoft.SqlServer.Management.Dac",  
"Microsoft.SqlServer.Management.DacEnum",  
"Microsoft.SqlServer.Management.Utility"  
  
foreach ($asm in $assemblylist)  
{  
    $asm = [Reflection.Assembly]::LoadWithPartialName($asm)  
}  
  
Push-Location  
cd $sqlpsPath  
Update-FormatData -PrependPath SQLProvider.Format.ps1xml
Pop-Location  
```  
  
## <a name="see-also"></a>「  
 [SQL Server PowerShell](sql-server-powershell.md)  
