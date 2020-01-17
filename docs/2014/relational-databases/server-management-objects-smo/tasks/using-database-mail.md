---
title: データベースメール | を使用するMicrosoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- e-mail [SMO]
- Database Mail [SMO]
- mail [SMO]
ms.assetid: 7605390f-b485-48cc-8d97-e364a066067b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2db385919c30037612f00e53b2b990c1a7df0429
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72781855"
---
# <a name="using-database-mail"></a>データベース メールの使用
  SMO では、<xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> プロパティによって参照される <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> オブジェクトで、データベース メール サブシステムを表現します。 SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> オブジェクトを使用すると、データベース メール サブシステムを構成して、プロファイルおよびメール アカウントを管理することができます。 SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> オブジェクトは `Server` オブジェクトに属しています。これは、メール アカウントのスコープがサーバー レベルであることを意味しています。  
  
## <a name="examples"></a>使用例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual studio .net での VISUAL BASIC SMO プロジェクトの作成](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)」または「visual [studio .Net での Visual C&#35; SMO プロジェクトの作成](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
 @No__t_0 データベースメールを使用するプログラムでは、メール名前空間を修飾する `Imports` ステートメントを含める必要があります。 アプリケーションの宣言の前、かつ他の `Imports` ステートメントの後に、次のようにステートメントを挿入します。  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Mail`  
  
## <a name="creating-a-database-mail-account-by-using-visual-basic"></a>Visual Basic によるデータベース メール アカウントの作成  
 このコード例では、SMO で電子メール アカウントを作成する方法を示します。 データベース メールは <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> オブジェクトで表現され、<xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Server> プロパティによって参照されます。 SMO は、プログラムでデータベース メールを構成するために使用することはできますが、電子メールを送信したり、受信した電子メールを処理したりするために使用することはできません。  
  
 VB.NET  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMail1](SMO How to#SMO_VBMail1)]  -->  
  
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
$a = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Mail.MailAccount -ArgumentList $sm, `  
"Adventure Works Administrator", "Adventure Works Automated Mailer",`  
 "Mail account for administrative e-mail.", "dba@Adventure-Works.com"  
$a.Create()  
```  
