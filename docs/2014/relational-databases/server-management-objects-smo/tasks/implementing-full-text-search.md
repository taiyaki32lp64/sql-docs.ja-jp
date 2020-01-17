---
title: フルテキスト検索の実装 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- full-text search [SMO]
ms.assetid: 9ce9ad9c-f671-4760-90b5-e0c8ca051473
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6ddc3521031f34f179cdfef08abf178f21f5f47e
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72796715"
---
# <a name="implementing-full-text-search"></a>フルテキスト検索の実装
  フルテキスト検索は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスごとに使用することができ、SMO では <xref:Microsoft.SqlServer.Management.Smo.Server.FullTextService%2A> オブジェクトで表現されます。 <xref:Microsoft.SqlServer.Management.Smo.FullTextService> オブジェクトは、`Server` オブジェクトの下位に位置します。 このオブジェクトは、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] フルテキスト検索サービスの構成オプションを管理するために使用します。 <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalogCollection> オブジェクトは <xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクトに属し、データベースに対して定義されるフルテキスト カタログを表す <xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> オブジェクトのコレクションです。 通常のインデックスとは異なり、フルテキスト インデックスは各テーブルに対して 1 つのみ定義されます。 これは、<xref:Microsoft.SqlServer.Management.Smo.FullTextIndexColumn> オブジェクト内の <xref:Microsoft.SqlServer.Management.Smo.Table> オブジェクトで表現されます。  
  
 フルテキスト検索サービスを作成するには、データベースにフルテキスト カタログが定義されており、データベース内のいずれかのテーブルにフルテキスト検索インデックスが定義されている必要があります。  
  
 まず、<xref:Microsoft.SqlServer.Management.Smo.FullTextCatalog> コンストラクターを呼び出し、カタログ名を指定して、データベースにフルテキスト カタログを作成します。 次に、コンストラクターを呼び出し、フルテキスト インデックスを作成するテーブルを指定して、フルテキスト インデックスを作成します。 次に、<xref:Microsoft.SqlServer.Management.Smo.FullTextIndexColumn> オブジェクトを使用して、テーブル内の列の名前を指定し、フルテキスト インデックスのインデックス列を追加します。 次に、<xref:Microsoft.SqlServer.Management.Smo.FullTextIndex.CatalogName%2A> プロパティを、作成したカタログに設定します。 最後に、<xref:Microsoft.SqlServer.Management.Smo.FullTextIndex.Create%2A> メソッドを呼び出して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のインスタンスにフルテキスト インデックスを作成します。  
  
## <a name="example"></a>例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual studio .net での VISUAL BASIC SMO プロジェクトの作成](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)」または「visual [studio .Net での Visual C&#35; SMO プロジェクトの作成](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-a-full-text-search-service-in-visual-basic"></a>Visual Basic でのフルテキスト検索サービスの作成  
 このコード例では、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] サンプル データベースの `ProductCategory` テーブルに対してフルテキスト検索カタログを作成します。 次に、`ProductCategory` テーブル内の Name 列にフルテキスト検索インデックスを作成します。 フルテキスト検索インデックスを作成する列には、既に定義されている一意のインデックスが存在する必要があります。  
  
```vb
' compile with:   
' /r:Microsoft.SqlServer.SqlEnum.dll   
' /r:Microsoft.SqlServer.Smo.dll   
' /r:Microsoft.SqlServer.ConnectionInfo.dll   
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Sdk.Sfc  
Imports Microsoft.SqlServer.Management.Common  
  
Public Class A  
   Public Shared Sub Main()  
      ' Connect to the local, default instance of SQL Server.  
      Dim srv As Server = Nothing  
      srv = New Server()  
  
      ' Reference the AdventureWorks database.  
      Dim db As Database = Nothing  
      db = srv.Databases("AdventureWorks")  
  
      ' Reference the ProductCategory table.  
      Dim tb As Table = Nothing  
      tb = db.Tables("ProductCategory", "Production")  
  
      ' Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
      Dim ftc As FullTextCatalog = Nothing  
      ftc = New FullTextCatalog(db, "Test_Catalog")  
      ftc.IsDefault = True  
  
      ' Create the Full-Text Search catalog on the instance of SQL Server.  
      ftc.Create()  
  
      ' Define a FullTextIndex object varaible by supplying the parent table argument in the constructor.  
      Dim fti As FullTextIndex = Nothing  
      fti = New FullTextIndex(tb)  
  
      ' Define a FullTextIndexColumn object variable by supplying the parent index and column name arguments in the constructor.  
      Dim ftic As FullTextIndexColumn = Nothing  
      ftic = New FullTextIndexColumn(fti, "Name")  
  
      ' Add the indexed column to the index.  
      fti.IndexedColumns.Add(ftic)  
      fti.ChangeTracking = ChangeTracking.Automatic  
  
      ' Specify the unique index on the table that is required by the Full Text Search index.  
      fti.UniqueIndexName = "AK_ProductCategory_Name"  
  
      ' Specify the catalog associated with the index.  
      fti.CatalogName = "Test_Catalog"  
  
      ' Create the Full Text Search index on the instance of SQL Server.  
      fti.Create()  
   End Sub  
End Class  
```  
  
## <a name="creating-a-full-text-search-service-in-visual-c"></a>Visual C# でのフルテキスト検索サービスの作成  
 このコード例では、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] サンプル データベースの `ProductCategory` テーブルに対してフルテキスト検索カタログを作成します。 次に、`ProductCategory` テーブル内の Name 列にフルテキスト検索インデックスを作成します。 フルテキスト検索インデックスを作成する列には、既に定義されている一意のインデックスが存在する必要があります。  
  
```csharp
// compile with:   
// /r:Microsoft.SqlServer.SqlEnum.dll   
// /r:Microsoft.SqlServer.Smo.dll   
// /r:Microsoft.SqlServer.ConnectionInfo.dll   
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Sdk.Sfc;  
using Microsoft.SqlServer.Management.Common;  
  
public class A {  
   public static void Main() {  
      // Connect to the local, default instance of SQL Server.  
      Server srv = default(Server);  
      srv = new Server();  
  
      // Reference the AdventureWorks database.  
      Database db = default(Database);  
      db = srv.Databases ["AdventureWorks"];  
  
      // Reference the ProductCategory table.  
      Table tb = default(Table);  
      tb = db.Tables["ProductCategory", "Production"];  
  
      // Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
      FullTextCatalog ftc = default(FullTextCatalog);  
      ftc = new FullTextCatalog(db, "Test_Catalog");  
      ftc.IsDefault = true;  
  
      // Create the Full-Text Search catalog on the instance of SQL Server.  
      ftc.Create();  
  
      // Define a FullTextIndex object varaible by supplying the parent table argument in the constructor.  
      FullTextIndex fti = default(FullTextIndex);  
      fti = new FullTextIndex(tb);  
  
      // Define a FullTextIndexColumn object variable by supplying the parent index and column name arguments in the constructor.  
      FullTextIndexColumn ftic = default(FullTextIndexColumn);  
      ftic = new FullTextIndexColumn(fti, "Name");  
  
      // Add the indexed column to the index.  
      fti.IndexedColumns.Add(ftic);  
      fti.ChangeTracking = ChangeTracking.Automatic;  
  
      // Specify the unique index on the table that is required by the Full Text Search index.  
      fti.UniqueIndexName = "AK_ProductCategory_Name";  
  
      // Specify the catalog associated with the index.  
      fti.CatalogName = "Test_Catalog";  
  
      // Create the Full Text Search index on the instance of SQL Server.  
      fti.Create();  
   }  
}  
```  
  
## <a name="creating-a-full-text-search-service-in-powershell"></a>PowerShell でのフルテキスト検索サービスの作成  
 このコード例では、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] サンプル データベースの `ProductCategory` テーブルに対してフルテキスト検索カタログを作成します。 次に、`ProductCategory` テーブル内の Name 列にフルテキスト検索インデックスを作成します。 フルテキスト検索インデックスを作成する列には、既に定義されている一意のインデックスが存在する必要があります。  
  
```powershell
# Example of implementing a full text search on the default instance.  
# Set the path context to the local, default instance of SQL Server and database tables  
  
CD \sql\localhost\default\databases  
$db = Get-Item AdventureWorks2012  
  
CD AdventureWorks\tables  
  
#Get a reference to the table  
$tb = Get-Item Production.ProductCategory  
  
# Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
  
$ftc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextCatalog -ArgumentList $db, "Test_Catalog2"  
$ftc.IsDefault = $true  
  
# Create the Full Text Search catalog on the instance of SQL Server.  
$ftc.Create()  
  
# Define a FullTextIndex object variable by supplying the parent table argument in the constructor.  
$fti = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndex -ArgumentList $tb  
  
#  Define a FullTextIndexColumn object variable by supplying the parent index
#  and column name arguments in the constructor.  
  
$ftic = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndexColumn -ArgumentList $fti, "Name"  
  
# Add the indexed column to the index.  
$fti.IndexedColumns.Add($ftic)  
  
# Set change tracking  
$fti.ChangeTracking = [Microsoft.SqlServer.Management.SMO.ChangeTracking]::Automatic  
  
# Specify the unique index on the table that is required by the Full Text Search index.  
$fti.UniqueIndexName = "AK_ProductCategory_Name"  
  
# Specify the catalog associated with the index.  
$fti.CatalogName = "Test_Catalog2"  
  
# Create the Full Text Search Index  
$fti.Create()  
```  
