---
title: SQL Server PowerShell パスの操作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: f31d8e2c-8d59-4fee-ac2a-324668e54262
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5ca7d915b940296e6de6689e666401b0c3534c9d
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782729"
---
# <a name="work-with-sql-server-powershell-paths"></a>SQL Server PowerShell パスの操作
  [!INCLUDE[ssDE](../includes/ssde-md.md)] プロバイダーのパスでノードに移動した後、ノードに関連付けられている [!INCLUDE[ssDE](../includes/ssde-md.md)] 管理オブジェクトのメソッドとプロパティを使用して、作業を実行したり、情報を取得したりできます。  
  
1.  [はじめに](#BeforeYouBegin)  
  
2.  **パス ノードに関する作業:**  [メソッドとプロパティの一覧表示](#ListPropMeth)、 [メソッドとプロパティの使用](#UsePropMeth)  
  
##  <a name="BeforeYouBegin"></a> はじめに  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] プロバイダーのパスでノードに移動した後、2 種類の操作を実行できます。  
  
-   **Rename-Item**など、ノードを操作する Windows PowerShell コマンドレットを実行できます。  
  
-   関連付けられた [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理オブジェクト モデル (SMO など) のメソッドを呼び出すことができます。 たとえば、パスで <xref:Microsoft.SqlServer.Management.Smo.Database> ノードに移動すると、 クラスのメソッドとプロパティを使用できます。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダーは、 [!INCLUDE[ssDE](../includes/ssde-md.md)]のインスタンスのオブジェクトを管理するために使用されます。 データベース内のデータの処理には使用されません。 テーブルまたはビューに移動した場合に、プロバイダーを使用してデータの選択、挿入、更新、または削除を行うことはできません。 テーブルおよびビューのデータを Windows PowerShell 環境からクエリまたは変更するには、 **Invoke-Sqlcmd** コマンドレットを使用します。 詳細については、「 [Invoke-Sqlcmd コマンドレット](../database-engine/invoke-sqlcmd-cmdlet.md)」を参照してください。  
  
##  <a name="ListPropMeth"></a> メソッドとプロパティの一覧表示
  
 特定のオブジェクトまたはオブジェクト クラスで使用できるメソッドとプロパティを表示するには、 **Get-Member** コマンドレットを使用します。  
  
### <a name="examples-listing-methods-and-properties"></a>例: メソッドとプロパティの一覧表示  
 次の例では、Windows PowerShell 変数に SMO <xref:Microsoft.SqlServer.Management.Smo.Database> クラスを設定し、メソッドとプロパティを一覧表示します。  
  
```powershell
$MyDBVar = New-Object Microsoft.SqlServer.Management.SMO.Database  
$MyDBVar | Get-Member -Type Methods  
$MyDBVar | Get-Member -Type Properties  
```  
  
 また、 **Get-Member** を使用して、Windows PowerShell パスの終了ノードに関連付けられているメソッドとプロパティを一覧表示することもできます。  
  
 次の例では、SQLSERVER: パスで Databases ノードに移動し、コレクションのプロパティを一覧表示します。  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
Get-Item . | Get-Member -Type Properties  
```  
  
 次の例では、SQLSERVER: パスで AdventureWorks2012 ノードに移動し、オブジェクトのプロパティを一覧表示します。  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012  
Get-Item . | Get-Member -Type Properties  
```  
  
##  <a name="UsePropMeth"></a>SMO のメソッドとプロパティの使用  
  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] プロバイダー パスからオブジェクトの操作を実行するには、SMO メソッドとプロパティを使用します。  
  
### <a name="examples-using-methods-and-properties"></a>例: メソッドとプロパティの使用  
 次の例では、SMO の **Schema** プロパティを使用して、AdventureWorks2012 の Sales スキーマからテーブルの一覧を取得します。  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Tables  
Get-ChildItem | Where {$_.Schema -eq "Sales"}  
```  
  
 この例では、SMO の**script**メソッドを使用して、AdventureWorks2012 でビューを再作成するために必要な `CREATE VIEW` ステートメントを含むスクリプトを生成します。  
  
```powershell
Remove-Item C:\PowerShell\CreateViews.sql  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Views  
foreach ($Item in Get-ChildItem) { $Item.Script() | Out-File -Filepath C:\PowerShell\CreateViews.sql -append }  
```  
  
 次の例では、SMO の **Create** メソッドを使用してデータベースを作成し、 **State** プロパティを使用してデータベースが存在するかどうかを確認します。  
  
```powershell
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
$MyDBVar = New-Object Microsoft.SqlServer.Management.SMO.Database  
$MyDBVar.Parent = (Get-Item ..)  
$MyDBVar.Name = "NewDB"  
$MyDBVar.Create()  
$MyDBVar.State  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [SQL Server PowerShell パスの移動](navigate-sql-server-powershell-paths.md)   
 [URN から SQL Server プロバイダー パスへの変換](../database-engine/convert-urns-to-sql-server-provider-paths.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
