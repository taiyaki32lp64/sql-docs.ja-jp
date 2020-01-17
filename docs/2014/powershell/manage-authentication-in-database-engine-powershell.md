---
title: データベース エンジン PowerShell での認証の管理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4a04e581758748d55b9defcab3beaa6a86f0eecf
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797799"
---
# <a name="manage-authentication-in-database-engine-powershell"></a>データベース エンジン PowerShell での認証の管理
  既定では、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell コンポーネントは、 [!INCLUDE[ssDE](../includes/ssde-md.md)]インスタンスへの接続に Windows 認証を使用します。 SQL Server 認証を使用するには、PowerShell 仮想ドライブを定義するか、`-Username` の `-Password` および `Invoke-Sqlcmd` パラメーターを指定します。  
  
1.  **Before you begin:**  [Permissions](#Permissions)  
  
2.  **認証を設定する方法:**  [仮想ドライブ](#SQLAuthVirtDrv)、 [–Password](#SQLAuthInvSqlCmd)  
  
##  <a name="Permissions"></a> アクセス許可  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] のインスタンスで実行できるすべての操作は、そのインスタンスへの接続に使用された認証資格情報に付与されている権限によって制御されます。 既定では、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダーとコマンドレットは、それが実行されている Windows アカウントを使用して、 [!INCLUDE[ssDE](../includes/ssde-md.md)]への Windows 認証接続を行います。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証接続を行うには、SQL Server 認証のログイン ID およびパスワードを指定する必要があります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダーを使用する場合は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のログイン資格情報を仮想ドライブに関連付けてから、ディレクトリの変更コマンド (`cd`) を使用してそのドライブに接続する必要があります。 Windows PowerShell では、セキュリティ資格情報は仮想ドライブにのみ関連付けることができます。  
  
##  <a name="SQLAuthVirtDrv"></a> 仮想ドライブを使用する SQL Server 認証  
 **SQL Server 認証ログインに関連付けられた仮想ドライブを作成するには**  
  
1.  次のような関数を作成します。  
  
    1.  仮想ドライブに与える名前、ログイン ID、および仮想ドライブに関連付けるプロバイダー パスのためのパラメーターを持っている。  
  
    2.  `read-host` を使用して、ユーザーにパスワードの入力を求める。  
  
    3.  `new-object` を使用して、資格情報オブジェクトを作成する。  
  
    4.  `new-psdrive` を使用して、指定された資格情報で仮想ドライブを作成する。  
  
2.  関数を呼び出して、指定された資格情報で仮想ドライブを作成します。  
  
### <a name="example-virtual-drive"></a>例 (仮想ドライブ)  
 次の例は、指定された **認証ログインおよびインスタンスに関連付けられる仮想ドライブを作成するための、** sqldrive [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] という名前の関数を作成します。  
  
 **sqldrive** 関数は、ユーザーにログインのパスワードの入力を求め、入力されるパスワードをマスクします。 次に、[ディレクトリの変更] コマンド (`cd`) を使用して、仮想ドライブ名を使用してパスに接続するたびに、ドライブの作成時に指定した [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証ログイン資格情報を使用してすべての操作が実行されます。  
  
```powershell
## Create a function that specifies the login and prompts for the password.  
  
function sqldrive  
{  
    param( [string]$name, [string]$login = "MyLogin", [string]$root = "SQLSERVER:\SQL\MyComputer\MyInstance" )  
    $pwd = Read-Host -AsSecureString -Prompt "Password"  
    $cred = New-Object System.Management.Automation.PSCredential -argumentlist $login, $pwd  
    New-PSDrive $name -PSProvider SqlServer -Root $root -Credential $cred -Scope 1  
}  
  
## Use the sqldrive function to create a SQLAuth virtual drive.  
sqldrive SQLAuth  
  
## CD to the virtual drive, which invokes the supplied authentication credentials.  
cd SQLAuth  
```  
  
##  <a name="SQLAuthInvSqlCmd"></a> Invoke-Sqlcmd を使用する SQL Server 認証  
 **SQL Server 認証で Invoke-Sqlcmd を使用するには**  
  
1.  `-Username` パラメーターでログイン ID を指定し、`-Password` パラメーターで関連付けられているパスワードを指定します。  
  
### <a name="example-invoke-sqlcmd"></a>例 (Invoke-Sqlcmd)  
 この例では、read-host コマンドレットを使用してユーザーにパスワードの入力を求め、SQL Server 認証を使用して接続します。  
  
```powershell
## Prompt the user for their password.  
$pwd = Read-Host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" -Username "MyLogin" -Password $pwd  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server PowerShell](sql-server-powershell.md)   
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [Invoke-Sqlcmd コマンドレット](../database-engine/invoke-sqlcmd-cmdlet.md)  
