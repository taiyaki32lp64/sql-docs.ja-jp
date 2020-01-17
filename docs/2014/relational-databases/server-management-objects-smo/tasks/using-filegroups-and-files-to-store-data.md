---
title: ファイルグループとファイルを使用したデータの格納 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- filegroups [SMO]
- storing data [SMO]
- files [SMO]
- files [SMO], about files
- storage [SMO]
ms.assetid: 7e2327ce-e1a6-4904-83d1-0944b24a7b43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 270df8181fe42f48619736ba858dc0c16d9e30c7
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72781810"
---
# <a name="using-filegroups-and-files-to-store-data"></a>ファイルとファイル グループを使用したデータの格納
  データベース ファイルの格納には、データ ファイルを使用します。 データ ファイルは、ファイル グループに細分化されます。 <xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクトには、<xref:Microsoft.SqlServer.Management.Smo.Database.FileGroups%2A> オブジェクトを参照する <xref:Microsoft.SqlServer.Management.Smo.FileGroupCollection> プロパティがあります。 このコレクション内の各 <xref:Microsoft.SqlServer.Management.Smo.FileGroup> オブジェクトには、<xref:Microsoft.SqlServer.Management.Smo.FileGroup.Files%2A> プロパティがあります。 このプロパティは、データベースに属するすべてのデータ ファイルが含まれる、<xref:Microsoft.SqlServer.Management.Smo.DataFileCollection> コレクションを参照します。 ファイル グループは主に、データベース オブジェクトの格納に使用されるファイルをグループ化するために使用します。 データベース オブジェクトを複数のファイルに分散する理由の 1 つは、これによってパフォーマンスを向上させることができるからです。パフォーマンスの向上は、ファイルを複数のディスク ドライブに格納されていれば特に期待できます。  
  
 自動的に作成される各データベースには、"Primary" という名前のファイル グループと、データベースと同じ名前を持つデータ ファイルがあります。 コレクションにはファイルおよびグループを追加することもできます。  
  
## <a name="examples"></a>使用例  
 次のコード例では、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual studio .net での VISUAL BASIC SMO プロジェクトの作成](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)」および「visual [studio .Net での Visual C&#35; SMO プロジェクトの作成](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-basic"></a>Visual Basic でファイル グループおよびデータ ファイルをデータベースに追加する  
 プライマリ ファイル グループおよびデータ ファイルは、既定のプロパティ値を使用して自動的に作成されます。 コード例では、使用できるいくつかのプロパティ値を指定しています。 指定しなかった場合は、既定のプロパティ値が使用されます。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups1](SMO How to#SMO_VBFileGroups1)]  -->  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-c"></a>Visual C# でファイル グループおよびデータ ファイルをデータベースに追加する  
 プライマリ ファイル グループおよびデータ ファイルは、既定のプロパティ値を使用して自動的に作成されます。 コード例では、使用できるいくつかのプロパティ値を指定しています。 指定しなかった場合は、既定のプロパティ値が使用されます。  
  
```csharp
{  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a FileGroup object called SECONDARY on the database.   
            FileGroup fg1 = default(FileGroup);  
            fg1 = new FileGroup(db, "SECONDARY");  
            //Call the Create method to create the file group on the instance of SQL Server.   
            fg1.Create();  
            //Define a DataFile object on the file group and set the FileName property.   
            DataFile df1 = default(DataFile);  
            df1 = new DataFile(fg1, "datafile1");  
            df1.FileName = "c:\\Program Files\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Data\\datafile2.ndf";  
            //Call the Create method to create the data file on the instance of SQL Server.   
            df1.Create();  
        }  
```  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-powershell"></a>PowerShell でのファイル グループおよびデータ ファイルのデータベースへの追加  
 プライマリ ファイル グループおよびデータ ファイルは、既定のプロパティ値を使用して自動的に作成されます。 コード例では、使用できるいくつかのプロパティ値を指定しています。 指定しなかった場合は、既定のプロパティ値が使用されます。  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a new filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "SECONDARY"  
$fg1.Create()  
  
#Define a DataFile object on the file group and set the FileName property.   
$df1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.DataFile -argumentlist $fg1, "datafile1"  
  
#Make sure to have a directory created to hold the designated data file  
$df1.FileName = "c:\\TestData\\datafile2.ndf"  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$df1.Create()  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-basic"></a>Visual Basic でのログ ファイルの作成、変更、および削除  
 コード例では、<xref:Microsoft.SqlServer.Management.Smo.LogFile> オブジェクトを作成し、プロパティの 1 つを変更して、このオブジェクトをデータベースから削除しています。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups3](SMO How to#SMO_VBFileGroups3)]  -->  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-c"></a>Visual C# でのログ ファイルの作成、変更、および削除  
 コード例では、<xref:Microsoft.SqlServer.Management.Smo.LogFile> オブジェクトを作成し、プロパティの 1 つを変更して、このオブジェクトをデータベースから削除しています。  
  
```csharp
//Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a LogFile object and set the database, name, and file name properties in the constructor.   
            LogFile lf1 = default(LogFile);  
            lf1 = new LogFile(db, "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf");  
            //Set the file growth to 6%.   
            lf1.GrowthType = FileGrowthType.Percent;  
            lf1.Growth = 6;  
            //Run the Create method to create the log file on the instance of SQL Server.   
            lf1.Create();  
            //Alter the growth percentage.
            lf1.Growth = 7;  
            lf1.Alter();  
            //Remove the log file.
            lf1.Drop();
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-powershell"></a>PowerShell でのログ ファイルの作成、変更、および削除  
 コード例では、<xref:Microsoft.SqlServer.Management.Smo.LogFile> オブジェクトを作成し、プロパティの 1 つを変更して、このオブジェクトをデータベースから削除しています。  
  
```powershell
#Load the assembly containing the enums used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlEnum")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012  
$db = get-item AdventureWorks2012  
  
#Create a filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Secondary"  
  
#Call the Create method to create the file group on the instance of SQL Server.   
$fg1.Create()  
  
#Define a LogFile object on the file group and set the FileName property.   
$lf1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LogFile -argumentlist $db, "LogFile2"  
  
#Set a location for it - make sure the directory exists  
$lf1.FileName = "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf"  
  
#Set file growth to 6%  
$lf1.GrowthType = [Microsoft.SqlServer.Management.Smo.FileGrowthType]::Percent  
$lf1.Growth = 6.0  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$lf1.Create()  
  
#Alter a value and drop the log file  
$lf1.Growth = 7.0  
$lf1.Alter()  
$lf1.Drop()
```  
  
## <a name="see-also"></a>「  
 <xref:Microsoft.SqlServer.Management.Smo.FileGroup>   
 [データベース ファイルとファイル グループ](../../databases/database-files-and-filegroups.md)  
