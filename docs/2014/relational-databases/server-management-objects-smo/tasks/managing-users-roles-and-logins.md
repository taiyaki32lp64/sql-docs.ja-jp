---
title: ユーザー、ロール、およびログインの管理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- logins [SMO]
- roles [SMO]
- users [SMO]
ms.assetid: 74e411fa-74ed-49ec-ab58-68c250f2280e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 86b67202537e650619f835e9c64d2c35a8e78fc2
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72796608"
---
# <a name="managing-users-roles-and-logins"></a>ユーザー、ロール、およびログインの管理
  SMO では、<xref:Microsoft.SqlServer.Management.Smo.Login> オブジェクトでログインが表現されます。 ログオンが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]に存在する場合、サーバー ロールに追加することができます。 サーバー ロールは、<xref:Microsoft.SqlServer.Management.Smo.ServerRole> オブジェクトで表現されます。 データベース ロールは <xref:Microsoft.SqlServer.Management.Smo.DatabaseRole> オブジェクトで表現され、アプリケーション ロールは <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> オブジェクトで表現されます。  
  
 サーバー レベルに関連付けられた権限は、<xref:Microsoft.SqlServer.Management.Smo.ServerPermission> オブジェクトのプロパティとしてリストされます。 サーバー レベル権限は、個々のログオン アカウントに対して、許可、拒否、取り消しを行うことができます。  
  
 各 <xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクトには、データベース内のすべてのユーザーを指定する <xref:Microsoft.SqlServer.Management.Smo.UserCollection> オブジェクトがあります。 各ユーザーはログオンに関連付けられています。 1 つのログオンを 2 つ以上のデータベース内のユーザーに関連付けることもできます。 ログオンに関連付けられた各データベース内のすべてのユーザーをリストするには、<xref:Microsoft.SqlServer.Management.Smo.Login> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> メソッドを使用します。 または、<xref:Microsoft.SqlServer.Management.Smo.User> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Login> プロパティで、ユーザーに関連付けられたログオンを指定します。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースには、ユーザーに対して特定のタスクの実行を許可するための、データベース レベル権限のセットを指定するロールもあります。 サーバー ロールと異なり、データベース ロールは固定されていません。 データベース ロールは、作成、変更、および削除を行うことができます。 権限およびユーザーは、データベースに割り当てて、一括管理することができます。  
  
## <a name="example"></a>例  
 次のコード例では、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual studio .net での VISUAL BASIC SMO プロジェクトの作成](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)」および「visual [studio .Net での Visual C&#35; SMO プロジェクトの作成](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="enumerating-logins-and-associated-users-in-visual-basic"></a>Visual Basic でのログインおよび関連付けられたユーザーの列挙  
 データベース内の各ユーザーは、ログオンに関連付けられています。 ログオンは 2 つ以上のデータベース内のユーザーに関連付けることもできます。 コード例では、<xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Login> メソッドを呼び出して、ログオンに関連付けられているすべてのデータベース ユーザーをリストする方法を示します。 この例では、 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースのログオンおよびユーザーを作成して、列挙するマッピング情報の存在を確認します。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBLogins1](SMO How to#SMO_VBLogins1)]  -->  
  
## <a name="enumerating-logins-and-associated-users-in-visual-c"></a>Visual C# でのログインおよび関連付けられたユーザーの列挙  
 データベース内の各ユーザーは、ログオンに関連付けられています。 ログオンは 2 つ以上のデータベース内のユーザーに関連付けることもできます。 コード例では、<xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Login> メソッドを呼び出して、ログオンに関連付けられているすべてのデータベース ユーザーをリストする方法を示します。 この例では、 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースのログオンおよびユーザーを作成して、列挙するマッピング情報の存在を確認します。  
  
```csharp
{   
Server srv = new Server();   
//Iterate through each database and display.   
  
foreach ( Database db in srv.Databases) {   
   Console.WriteLine("========");   
   Console.WriteLine("Login Mappings for the database: " + db.Name);   
   Console.WriteLine(" ");   
   //Run the EnumLoginMappings method and return details of database user-login mappings to a DataTable object variable.   
   DataTable d;  
   d = db.EnumLoginMappings();   
   //Display the mapping information.   
   foreach (DataRow r in d.Rows) {   
      foreach (DataColumn c in r.Table.Columns) {   
         Console.WriteLine(c.ColumnName + " = " + r[c]);   
      }   
      Console.WriteLine(" ");   
   }   
}   
}  
```  
  
## <a name="enumerating-logins-and-associated-users-in-powershell"></a>PowerShell でのログインおよび関連付けられたユーザーの列挙  
 データベース内の各ユーザーは、ログオンに関連付けられています。 ログオンは 2 つ以上のデータベース内のユーザーに関連付けることもできます。 コード例では、<xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Login> メソッドを呼び出して、ログオンに関連付けられているすべてのデータベース ユーザーをリストする方法を示します。 この例では、 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースのログオンおよびユーザーを作成して、列挙するマッピング情報の存在を確認します。  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\Default\Databases  
  
#Iterate through all databases  
 foreach ($db in Get-ChildItem)  
 {  
 "====="  
 "Login Mappings for the database: "+ $db.Name  
  
 #get the datatable containing the mapping from the smo database object  
 $dt = $db.EnumLoginMappings()  
  
 #display the results  
 foreach($row in $dt.Rows)  
     {  
        foreach($col in $row.Table.Columns)  
      {  
        $col.ColumnName + "=" + $row[$col]  
       }
     }  
 }  
```  
  
## <a name="managing-roles-and-users"></a>ロールとユーザーの管理  
 このサンプルでは、ロールおよびユーザーの管理方法を示します。 最初のサンプルでは C# を使用し、2 番目のサンプルでは Visual Basic を使用しています。 これらのサンプルでは、次に示すアセンブリへの参照が必要です。  
  
-   Microsoft.SqlServer.Smo.dll  
  
-   Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
-   Microsoft.SqlServer.ConnectionInfo.dll  
  
-   Microsoft.SqlServer.SqlEnum.dll  
  
```csharp
using Microsoft.SqlServer.Management.Smo;  
using System;  
  
public class A {  
   public static void Main() {  
      Server svr = new Server();  
      Database db = new Database(svr, "TESTDB");  
      db.Create();  
  
      // Creating Logins  
      Login login = new Login(svr, "Login1");  
      login.LoginType = LoginType.SqlLogin;  
      login.Create("password@1");  
  
      Login login2 = new Login(svr, "Login2");  
      login2.LoginType = LoginType.SqlLogin;  
      login2.Create("password@1");  
  
      // Creating Users in the database for the logins created  
      User user1 = new User(db, "User1");  
      user1.Login = "Login1";  
      user1.Create();  
  
      User user2 = new User(db, "User2");  
      user2.Login = "Login2";  
      user2.Create();  
  
      // Creating database permission Sets  
      DatabasePermissionSet dbPermSet = new DatabasePermissionSet(DatabasePermission.AlterAnySchema);  
      dbPermSet.Add(DatabasePermission.AlterAnyUser);  
  
      DatabasePermissionSet dbPermSet2 = new DatabasePermissionSet(DatabasePermission.CreateType);  
      dbPermSet2.Add(DatabasePermission.CreateSchema);  
      dbPermSet2.Add(DatabasePermission.CreateTable);  
  
      // Creating Database roles  
      DatabaseRole role1 = new DatabaseRole(db, "Role1");  
      role1.Create();  
  
      DatabaseRole role2 = new DatabaseRole(db, "Role2");  
      role2.Create();  
  
      // Granting Database Permission Sets to Roles  
      db.Grant(dbPermSet, role1.Name);  
      db.Grant(dbPermSet2, role2.Name);  
  
      // Adding members (Users / Roles) to Role  
      role1.AddMember("User1");  
  
      role2.AddMember("User2");  
  
      // Role1 becomes a member of Role2  
      role2.AddMember("Role1");  
  
      // Enumerating through explicit permissions granted to Role1  
      // enumerates all database permissions for the Grantee  
      DatabasePermissionInfo[] dbPermsRole1 = db.EnumDatabasePermissions("Role1");     
      foreach (DatabasePermissionInfo dbp in dbPermsRole1) {  
         Console.WriteLine(dbp.Grantee + " has " + dbp.PermissionType.ToString() + " permission.");  
      }  
      Console.WriteLine(" ");  
   }  
}  
```  
  
 Visual Basic バージョンを次に示します。  
  
```vb
Imports Microsoft.SqlServer.Management.Smo  
  
Public Class A  
   Public Shared Sub Main()  
      Dim svr As New Server()  
      Dim db As New Database(svr, "TESTDB")  
      db.Create()  
  
      ' Creating Logins  
      Dim login As New Login(svr, "Login1")  
      login.LoginType = LoginType.SqlLogin  
      login.Create("password@1")  
  
      Dim login2 As New Login(svr, "Login2")  
      login2.LoginType = LoginType.SqlLogin  
      login2.Create("password@1")  
  
      ' Creating Users in the database for the logins created  
      Dim user1 As New User(db, "User1")  
      user1.Login = "Login1"  
      user1.Create()  
  
      Dim user2 As New User(db, "User2")  
      user2.Login = "Login2"  
      user2.Create()  
  
      ' Creating database permission Sets  
      Dim dbPermSet As New DatabasePermissionSet(DatabasePermission.AlterAnySchema)  
      dbPermSet.Add(DatabasePermission.AlterAnyUser)  
  
      Dim dbPermSet2 As New DatabasePermissionSet(DatabasePermission.CreateType)  
      dbPermSet2.Add(DatabasePermission.CreateSchema)  
      dbPermSet2.Add(DatabasePermission.CreateTable)  
  
      ' Creating Database roles  
      Dim role1 As New DatabaseRole(db, "Role1")  
      role1.Create()  
  
      Dim role2 As New DatabaseRole(db, "Role2")  
      role2.Create()  
  
      ' Granting Database Permission Sets to Roles  
      db.Grant(dbPermSet, role1.Name)  
      db.Grant(dbPermSet2, role2.Name)  
  
      ' Adding members (Users / Roles) to Role  
      role1.AddMember("User1")  
  
      role2.AddMember("User2")  
  
      ' Role1 becomes a member of Role2  
      role2.AddMember("Role1")  
  
      ' Enumerating through explicit permissions granted to Role1  
      ' enumerates all database permissions for the Grantee  
      Dim dbPermsRole1 As DatabasePermissionInfo() = db.EnumDatabasePermissions("Role1")  
      For Each dbp As DatabasePermissionInfo In dbPermsRole1  
         Console.WriteLine(dbp.Grantee + " has " & dbp.PermissionType.ToString() & " permission.")  
      Next  
      Console.WriteLine(" ")  
   End Sub  
End Class  
```  
