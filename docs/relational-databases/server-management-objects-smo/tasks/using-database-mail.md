---
title: データベースメール | を使用するMicrosoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- e-mail [SMO]
- Database Mail [SMO]
- mail [SMO]
ms.assetid: 7605390f-b485-48cc-8d97-e364a066067b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3e29aaf45306c9ed5d8c8dd7c132dacd9af1e926
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148351"
---
# <a name="using-database-mail"></a>データベース メールの使用
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO では、<xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> プロパティによって参照される <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> オブジェクトで、データベース メール サブシステムを表現します。 SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> オブジェクトを使用すると、データベース メール サブシステムを構成して、プロファイルおよびメール アカウントを管理することができます。 SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail>オブジェクトは**サーバー**オブジェクトに属しています。つまり、メールアカウントのスコープがサーバーレベルであることを意味します。  
  
## <a name="examples"></a>使用例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio&#35; .Net での Visual C SMO プロジェクトの作成](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
 データベースメールを使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]するプログラムでは、Mail 名前空間を修飾する**Imports**ステートメントを含める必要があります。 アプリケーションの宣言の前、かつ他の **Imports** ステートメントの後に、次のようにステートメントを挿入します。  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Mail`  
  
## <a name="creating-a-database-mail-account-by-using-visual-basic"></a>Visual Basic によるデータベース メール アカウントの作成  
 このコード例では、SMO で電子メール アカウントを作成する方法を示します。 データベース メールは <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> オブジェクトで表現され、<xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Server> プロパティによって参照されます。 SMO は、プログラムでデータベース メールを構成するために使用することはできますが、電子メールを送信したり、受信した電子メールを処理したりするために使用することはできません。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server()
'Define the Database Mail service with a SqlMail object variable and reference it using the Server Mail property.
Dim sm As SqlMail
sm = srv.Mail
'Define and create a mail account by supplying the Database Mail service, name, description, display name, and email address arguments in the constructor.
Dim a As MailAccount
a = New MailAccount(sm, "AdventureWorks Administrator", "AdventureWorks Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com")
a.Create()
```
  
## <a name="creating-a-database-mail-account-by-using-visual-c"></a>Visual C# によるデータベース メール アカウントの作成  
 このコード例では、SMO で電子メール アカウントを作成する方法を示します。 データベース メールは <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> オブジェクトで表現され、<xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Server> プロパティによって参照されます。 SMO は、プログラムでデータベース メールを構成するために使用することはできますが、電子メールを送信したり、受信した電子メールを処理したりするために使用することはできません。  
  
```csharp  
{  
         //Connect to the local, default instance of SQL Server.  
         Server srv = default(Server);   
           srv = new Server();   
           //Define the Database Mail service with a SqlMail object variable   
           //and reference it using the Server Mail property.   
           SqlMail sm;   
           sm = srv.Mail;   
           //Define and create a mail account by supplying the Database Mail  
           //service, name, description, display name, and email address  
           //arguments in the constructor.   
           MailAccount a = default(MailAccount);   
           a = new MailAccount(sm, "AdventureWorks2012 Administrator", "AdventureWorks2012 Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com");   
           a.Create();    
}  
```  
  
## <a name="creating-a-database-mail-account-by-using-powershell"></a>PowerShell によるデータベース メール アカウントの作成  
 このコード例では、SMO で電子メール アカウントを作成する方法を示します。 データベース メールは <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> オブジェクトで表現され、<xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Server> プロパティによって参照されます。 SMO は、プログラムでデータベース メールを構成するために使用することはできますが、電子メールを送信したり、受信した電子メールを処理したりするために使用することはできません。  
  
  
  
```powershell  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define the Database Mail; reference it using the Server Mail property.  
$sm = $srv.Mail  
  
#Define and create a mail account by supplying the Database Mail service,  
#name, description, display name, and email address arguments in the constructor.  
$a = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Mail.MailAccount -argumentlist $sm, `  
"Adventure Works Administrator", "Adventure Works Automated Mailer",`  
 "Mail account for administrative e-mail.", "dba@Adventure-Works.com"  
$a.Create()  
```  
  
  
