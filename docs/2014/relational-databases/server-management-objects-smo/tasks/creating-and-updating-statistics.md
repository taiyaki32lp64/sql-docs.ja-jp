---
title: 統計の作成と更新 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- statistical information [SMO]
ms.assetid: 47a0a172-a969-4deb-bca9-dd04401a0fe1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 54995cc99aae2065112cbb510203b656c409dcac
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782126"
---
# <a name="creating-and-updating-statistics"></a>統計の作成と更新
  SMO では、<xref:Microsoft.SqlServer.Management.Smo.Statistic> オブジェクトを使用して、データベース内のクエリの処理に関する統計情報を収集することができます。  
  
 任意の列に対する統計の作成は、<xref:Microsoft.SqlServer.Management.Smo.Statistic> および <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> オブジェクトを使用して行うことができます。 <xref:Microsoft.SqlServer.Management.Smo.Statistic.Update%2A> メソッドを実行して、<xref:Microsoft.SqlServer.Management.Smo.Statistic> オブジェクト内の統計を更新することができます。 結果は、クエリ オプティマイザーで表示できます。  
  
## <a name="example"></a>例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual studio .net での VISUAL BASIC SMO プロジェクトの作成](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)」または「visual [studio .Net での Visual C&#35; SMO プロジェクトの作成](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-and-update-statistics-in-visual-basic"></a>Visual Basic での統計の作成および更新  
 このコード例では、既存のデータベースに新しいテーブルを作成し、<xref:Microsoft.SqlServer.Management.Smo.Statistic> オブジェクトおよび <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> オブジェクトを作成しています。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBStatistics1](SMO How to#SMO_VBStatistics1)]  -->  
  
## <a name="creating-and-update-statistics-in-visual-c"></a>Visual C# での統計の作成および更新  
 このコード例では、既存のデータベースに新しいテーブルを作成し、<xref:Microsoft.SqlServer.Management.Smo.Statistic> オブジェクトおよび <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> オブジェクトを作成しています。  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Reference the CreditCard table.   
  
           Table tb = db.Tables["CreditCard", "Sales"];  
            //Define a Statistic object by supplying the parent table and name   
            //arguments in the constructor.   
            Statistic stat = default(Statistic);  
            stat = new Statistic(tb, "Test_Statistics");  
            //Define a StatisticColumn object variable for the CardType column   
            //and add to the Statistic object variable.   
            StatisticColumn statcol = default(StatisticColumn);  
            statcol = new StatisticColumn(stat, "CardType");  
            stat.StatisticColumns.Add(statcol);  
            //Create the statistic counter on the instance of SQL Server.   
            stat.Create();  
        }  
```  
  
## <a name="creating-and-update-statistics-in-powershell"></a>PowerShell での統計の作成および更新  
 このコード例では、既存のデータベースに新しいテーブルを作成し、<xref:Microsoft.SqlServer.Management.Smo.Statistic> オブジェクトおよび <xref:Microsoft.SqlServer.Management.Smo.StatisticColumn> オブジェクトを作成しています。  
  
```powershell
# Example of implementing a full text search on the default instance.  
# Set the path context to the local, default instance of SQL Server and database tables  
  
CD \sql\localhost\default\databases  
$db = get-item AdventureWorks2012  
  
CD AdventureWorks2012\tables  
  
#Get a reference to the table  
$tb = get-item Production.ProductCategory  
  
# Define a FullTextCatalog object variable by specifying the parent database and name arguments in the constructor.  
  
$ftc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextCatalog -argumentlist $db, "Test_Catalog2"  
$ftc.IsDefault = $true  
  
# Create the Full Text Search catalog on the instance of SQL Server.  
$ftc.Create()  
  
# Define a FullTextIndex object variable by supplying the parent table argument in the constructor.  
$fti = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndex -argumentlist $tb  
  
#  Define a FullTextIndexColumn object variable by supplying the parent index   
#  and column name arguments in the constructor.  
  
$ftic = New-Object -TypeName Microsoft.SqlServer.Management.SMO.FullTextIndexColumn -argumentlist $fti, "Name"  
  
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
