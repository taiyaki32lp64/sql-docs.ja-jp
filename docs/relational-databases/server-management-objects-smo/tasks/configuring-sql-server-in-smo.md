---
title: SMO での SQL Server の構成
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server, configuring
- configuration options [SMO]
ms.assetid: 0a372643-15cb-45a7-8665-04f1215df8ed
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f973b47d4b55624e0f78658f7dfa13ec1aebd80c
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095953"
---
# <a name="configuring-sql-server-in-smo"></a>SMO での SQL Server の構成
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO では、<xref:Microsoft.SqlServer.Management.Smo.Information> オブジェクト、<xref:Microsoft.SqlServer.Management.Smo.Settings> オブジェクト、<xref:Microsoft.SqlServer.Management.Smo.UserOptions> オブジェクト、および <xref:Microsoft.SqlServer.Management.Smo.Configuration> オブジェクトに [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスの設定と情報が含まれています。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] には、インストールされたインスタンスの動作を記述する複数のプロパティがあります。 これらのプロパティでは、スタートアップ オプション、サーバーの既定、ファイルとディレクトリ、システムとプロセッサの情報、製品とバージョン、接続情報、メモリ オプション、言語と照合順序の選択、および認証モードについて記述します。  
  
## <a name="sql-server-configuration"></a>SQL Server 構成  
 <xref:Microsoft.SqlServer.Management.Smo.Information> オブジェクト プロパティには、プロセッサやプラットフォームなど、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに関する情報が含まれています。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Settings> オブジェクト プロパティには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに関する情報が含まれています。 Mail Profile および Server Account に加え、既定のデータベース ファイルおよびディレクトリも変更することができます。 これらのプロパティは、接続が続いている間は保持されます。  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserOptions> オブジェクト プロパティには、算術、ANSI 規格、およびトランザクションに関連する現在の接続の動作に関する情報が含まれています。  
  
 また、<xref:Microsoft.SqlServer.Management.Smo.Configuration> オブジェクトで表現される構成オプションのセットもあります。 これには、 **sp_configure** ストアド プロシージャによって変更可能なオプションを表すプロパティのセットが含まれています。 **優先度ブースト**、 **Recovery Interval** 、 **Network Packet Size**などのオプションは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスのパフォーマンスを制御します。 これらのオプションの多くは動的に変更できますが、場合によっては、構成した値が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスの再起動時に変更されることもあります。  
  
 構成オプションごとに <xref:Microsoft.SqlServer.Management.Smo.Configuration> オブジェクト プロパティがあります。 <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> オブジェクトを使用すると、グローバル構成設定を変更することができます。 多くのプロパティには、最大値および最小値が設定されており、これらも <xref:Microsoft.SqlServer.Management.Smo.ConfigProperty> プロパティとして格納されます。 これらのプロパティを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のインスタンスに変更をコミットするには、<xref:Microsoft.SqlServer.Management.Smo.ConfigurationBase.Alter%2A> メソッドが必要です。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Configuration> オブジェクトの構成オプションの変更はすべて、システム管理者が行う必要があります。  
  
## <a name="examples"></a>使用例  
 次のコード例では、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio&#35; .Net での Visual C SMO プロジェクトの作成](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="modifying-sql-server-configuration-options-in-visual-basic"></a>Visual Basic での SQL Server 構成オプションの変更  
 このコード例は、Visual Basic .NET で構成オプションを更新する方法を示しています。 また、指定された構成オプションの最大値と最小値についての情報を取得および表示しています。 最後に、変更が動的に行われたのか、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスが再起動されるまで変更が格納されるのかを、ユーザーに通知しています。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Display all the configuration options.
Dim p As ConfigProperty
For Each p In srv.Configuration.Properties
    Console.WriteLine(p.DisplayName)
Next
Console.WriteLine("There are " & srv.Configuration.Properties.Count.ToString & " configuration options.")
'Display the maximum and minimum values for ShowAdvancedOptions.
Dim min As Integer
Dim max As Integer
min = srv.Configuration.ShowAdvancedOptions.Minimum
max = srv.Configuration.ShowAdvancedOptions.Maximum
Console.WriteLine("Minimum and Maximum values are " & min & " and " & max & ".")
'Modify the value of ShowAdvancedOptions and run the Alter method.
srv.Configuration.ShowAdvancedOptions.ConfigValue = 0
srv.Configuration.Alter()
'Display when the change takes place according to the IsDynamic property.
If srv.Configuration.ShowAdvancedOptions.IsDynamic = True Then
    Console.WriteLine("Configuration option has been updated.")
Else
    Console.WriteLine("Configuration option will be updated when SQL Server is restarted.")
End If
``` 
  
## <a name="modifying-sql-server-settings-in-visual-basic"></a>Visual Basic での SQL Server 設定の変更  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.Information> と <xref:Microsoft.SqlServer.Management.Smo.Settings>での [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに関する情報を表示し、<xref:Microsoft.SqlServer.Management.Smo.Settings> および <xref:Microsoft.SqlServer.Management.Smo.UserOptions>オブジェクトのプロパティの設定を変更します。  
  
 この例では、<xref:Microsoft.SqlServer.Management.Smo.UserOptions> オブジェクトと <xref:Microsoft.SqlServer.Management.Smo.Settings> オブジェクトの両方に <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> メソッドがあります。 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> メソッドは、これらのオブジェクトに対して個別に実行できます。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Display information about the instance of SQL Server in Information and Settings.
Console.WriteLine("OS Version = " & srv.Information.OSVersion)
Console.WriteLine("State = " & srv.Settings.State.ToString)
'Display information specific to the current user in UserOptions.
Console.WriteLine("Quoted Identifier support = " & srv.UserOptions.QuotedIdentifier)
'Modify server settings in Settings.

srv.Settings.LoginMode = ServerLoginMode.Integrated
'Modify settings specific to the current connection in UserOptions.
srv.UserOptions.AbortOnArithmeticErrors = True
'Run the Alter method to make the changes on the instance of SQL Server.
srv.Alter()
```
  
## <a name="modifying-sql-server-settings-in-visual-c"></a>Visual C# での SQL Server 設定の変更  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.Information> と <xref:Microsoft.SqlServer.Management.Smo.Settings>での [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに関する情報を表示し、<xref:Microsoft.SqlServer.Management.Smo.Settings> および <xref:Microsoft.SqlServer.Management.Smo.UserOptions>オブジェクトのプロパティの設定を変更します。  
  
 この例では、<xref:Microsoft.SqlServer.Management.Smo.UserOptions> オブジェクトと <xref:Microsoft.SqlServer.Management.Smo.Settings> オブジェクトの両方に <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> メソッドがあります。 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> メソッドは、これらのオブジェクトに対して個別に実行できます。  
  
 `//Connect to the local, default instance of SQL Server.`  
  
```csharp  
{  
            Server srv = new Server();  
            //Display all the configuration options.   
  
            foreach (ConfigProperty p in srv.Configuration.Properties)  
            {  
                Console.WriteLine(p.DisplayName);  
            }  
            Console.WriteLine("There are " + srv.Configuration.Properties.Count.ToString() + " configuration options.");  
            //Display the maximum and minimum values for ShowAdvancedOptions.   
            int min = 0;  
            int max = 0;  
            min = srv.Configuration.ShowAdvancedOptions.Minimum;  
            max = srv.Configuration.ShowAdvancedOptions.Maximum;  
            Console.WriteLine("Minimum and Maximum values are " + min + " and " + max + ".");  
            //Modify the value of ShowAdvancedOptions and run the Alter method.   
            srv.Configuration.ShowAdvancedOptions.ConfigValue = 0;  
            srv.Configuration.Alter();  
            //Display when the change takes place according to the IsDynamic property.   
            if (srv.Configuration.ShowAdvancedOptions.IsDynamic == true)  
            {  
                Console.WriteLine("Configuration option has been updated.");  
            }  
            else  
            {  
                Console.WriteLine("Configuration option will be updated when SQL Server is restarted.");  
            }  
        }  
```  
  
## <a name="modifying-sql-server-settings-in-powershell"></a>PowerShell での SQL Server 設定の変更  
 このコード例では、<xref:Microsoft.SqlServer.Management.Smo.Information> と <xref:Microsoft.SqlServer.Management.Smo.Settings>での [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスに関する情報を表示し、<xref:Microsoft.SqlServer.Management.Smo.Settings> および <xref:Microsoft.SqlServer.Management.Smo.UserOptions>オブジェクトのプロパティの設定を変更します。  
  
 この例では、<xref:Microsoft.SqlServer.Management.Smo.UserOptions> オブジェクトと <xref:Microsoft.SqlServer.Management.Smo.Settings> オブジェクトの両方に <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> メソッドがあります。 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.Alter%2A> メソッドは、これらのオブジェクトに対して個別に実行できます。  
  
```powershell 
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Display information about the instance of SQL Server in Information and Settings.  
"OS Version = " + $srv.Information.OSVersion  
"State = "+ $srv.Settings.State.ToString()  
  
#Display information specific to the current user in UserOptions.  
"Quoted Identifier support = " + $srv.UserOptions.QuotedIdentifier  
  
#Modify server settings in Settings.  
$srv.Settings.LoginMode = [Microsoft.SqlServer.Management.SMO.ServerLoginMode]::Integrated  
  
#Modify settings specific to the current connection in UserOptions.  
$srv.UserOptions.AbortOnArithmeticErrors = $true  
  
#Run the Alter method to make the changes on the instance of SQL Server.  
$srv.Alter()  
```  
  
## <a name="modifying-sql-server-configuration-options-in-powershell"></a>PowerShell での SQL Server 構成オプションの変更  
 このコード例は、Visual Basic .NET で構成オプションを更新する方法を示しています。 また、指定された構成オプションの最大値と最小値についての情報を取得および表示しています。 最後に、変更が動的に行われたのか、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスが再起動されるまで変更が格納されるのかを、ユーザーに通知しています。  
  
```powershell 
#Get a server object which corresponds to the default instance replace LocalMachine with the physical server  
cd \sql\LocalMachine  
$svr = get-item default  
  
#enumerate its properties  
foreach ($Item in $Svr.Configuration.Properties)   
{  
 $Item.DisplayName  
}  
  
"There are " + $svr.Configuration.Properties.Count.ToString() + " configuration options."  
  
#Display the maximum and minimum values for ShowAdvancedOptions.  
$min = $svr.Configuration.ShowAdvancedOptions.Minimum  
$max = $svr.Configuration.ShowAdvancedOptions.Maximum  
"Minimum and Maximum values are " + $min.ToString() + " and " + $max.ToString() + "."  
  
#Modify the value of ShowAdvancedOptions and run the Alter method.  
$svr.Configuration.ShowAdvancedOptions.ConfigValue = 0  
$svr.Configuration.Alter()  
  
#Display when the change takes place according to the IsDynamic property.  
If ($svr.Configuration.ShowAdvancedOptions.IsDynamic -eq $true)  
 {    
   "Configuration option has been updated."  
 }  
Else  
{  
    "Configuration option will be updated when SQL Server is restarted."  
}  
```  
  
  
