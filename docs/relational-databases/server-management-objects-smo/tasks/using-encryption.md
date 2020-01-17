---
title: Encryption | を使用するMicrosoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- database master key [SMO]
- cryptography [SMO]
- cryptography [SQL Server], SMO
- encryption keys [SMO]
- encryption [SQL Server], SMO
- encryption [SMO]
- certificates [SMO]
- service master key [SMO]
ms.assetid: 405e0ed7-50a9-430e-a343-471f54b4af76
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fceb0baa62b7998534a5b7620d2c99fd1afc1f8f
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148313"
---
# <a name="using-encryption"></a>暗号化の使用
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  SMO では、サービス マスター キーは <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey> オブジェクトで表現します。 これは、<xref:Microsoft.SqlServer.Management.Smo.Server.ServiceMasterKey%2A> オブジェクトの <xref:Microsoft.SqlServer.Management.Smo.Server> プロパティによって参照されます。 <xref:Microsoft.SqlServer.Management.Smo.ServiceMasterKey.Regenerate%2A> メソッドを使用して、再生成することができます。  
  
 データベース マスター キーは、<xref:Microsoft.SqlServer.Management.Smo.MasterKey> オブジェクトによって表されます。 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.IsEncryptedByServer%2A> プロパティでは、データベース マスター キーがサービス マスター キーによって暗号化されるのかどうかが示されます。 master データベース内の暗号化されたコピーは、データベース マスター キーが変更されるたびに自動的に更新されます。  
  
 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> メソッドを使用してサービス キー暗号化を削除し、パスワードを使ってデータベース マスター キーを暗号化することが可能です。 この場合、セキュリティで保護された秘密キーにアクセスする前に、データベース マスター キーを明示的に開く必要があります。  
  
 データベースを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスにアタッチする際には、データベース マスター キーのパスワードを指定するか、サービス マスター キーでの暗号化に使用できるデータベース マスター キーの非暗号化コピーを作成するための <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> メソッドを実行する必要があります。 データベース マスター キーを明示的に開く必要性を回避するには、この手順をお勧めします。  
  
 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.Regenerate%2A> メソッドは、データベース マスター キーを再生成します。 データベース マスター キーが再生成されると、このデータベース マスター キーで暗号化されたすべてのキーの暗号化が解除され、これらのキーが新しいデータベース マスター キーで暗号化されます。 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.DropServiceKeyEncryption%2A> メソッドは、サービス マスター キーを使用してデータベース マスター キーの暗号化を削除します。 <xref:Microsoft.SqlServer.Management.Smo.MasterKey.AddServiceKeyEncryption%2A> は、サービス マスター キーを使用してマスター キーのコピーを暗号化し、現在のデータベースおよび master データベースの両方に格納します。  
  
 SMO では、証明書は <xref:Microsoft.SqlServer.Management.Smo.Certificate> オブジェクトで表現します。 <xref:Microsoft.SqlServer.Management.Smo.Certificate> オブジェクトには、公開キー、サブジェクト名、有効期間、および発行者に関する情報を指定するプロパティがあります。 証明書にアクセスする権限は、 **Grant**メソッド、 **Revoke** メソッド、および **Deny** メソッドを使用して制御されます。  
  
## <a name="example"></a>例  
 次のコード例では、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio&#35; .Net での Visual C SMO プロジェクトの作成](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="adding-a-certificate-in-visual-c"></a>Visual C# での証明書の追加  
 コード例では、暗号化パスワードを持つ簡単な証明書を作成します。 他のオブジェクトと異なり、<xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> メソッドには複数のオーバーロードがあります。 この例で使用するオーバーロードは、暗号化パスワードを持つ新しい証明書を作成しています。  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
            {  
                Server srv = new Server();  
  
                //Reference the AdventureWorks2012 database.   
                Database db = srv.Databases["AdventureWorks2012"];  
  
                //Define a Certificate object variable by supplying the parent database and name in the constructor.   
                Certificate c = new Certificate(db, "Test_Certificate");  
  
                //Set the start date, expiry date, and description.   
                System.DateTime dt;  
                DateTime.TryParse("January 01, 2010", out dt);  
                c.StartDate = dt;  
                DateTime.TryParse("January 01, 2015", out dt);  
                c.ExpirationDate = dt;  
                c.Subject = "This is a test certificate.";  
                //Create the certificate on the instance of SQL Server by supplying the certificate password argument.   
                c.Create("pGFD4bb925DGvbd2439587y");  
            }  
        }   
```  
  
## <a name="adding-a-certificate-in-powershell"></a>PowerShell での証明書の追加  
 コード例では、暗号化パスワードを持つ簡単な証明書を作成します。 他のオブジェクトと異なり、<xref:Microsoft.SqlServer.Management.Smo.Certificate.Create%2A> メソッドには複数のオーバーロードがあります。 この例で使用するオーバーロードは、暗号化パスワードを持つ新しい証明書を作成しています。  
  
```powershell  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
#Create a certificate  
  
$c = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Certificate -argumentlist $db, "Test_Certificate"  
$c.StartDate = "January 01, 2010"  
$c.Subject = "This is a test certificate."  
$c.ExpirationDate = "January 01, 2015"  
  
#Create the certificate on the instance of SQL Server by supplying the certificate password argument.  
$c.Create("pGFD4bb925DGvbd2439587y")  
  
```  
  
## <a name="see-also"></a>参照  
 [暗号化キーの使用](../../../relational-databases/server-management-objects-smo/tasks/using-encryption.md)  
  
  
