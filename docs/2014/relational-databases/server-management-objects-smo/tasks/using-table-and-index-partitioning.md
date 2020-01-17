---
title: テーブルとインデックスのパーティション分割を使用する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- partitions [SMO]
- storing data [SMO]
- partitioned tables [SQL Server], SMO
- partitioned indexes [SQL Server], SMO
ms.assetid: 0e682d7e-86c3-4d73-950d-aa692d46cb62
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 936f037852f39f24690e1cb9af3f63a2cfa2a613
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72781831"
---
# <a name="using-table-and-index-partitioning"></a>テーブルおよびインデックスのパーティション分割の使用
  データは、 [Partitioned Tables and Indexes](../../partitions/partitioned-tables-and-indexes.md)によって提供される格納アルゴリズムを使用して格納することができます。 パーティション分割により、大規模なテーブルとインデックスの管理の可能性と拡張性が向上します。  
  
## <a name="index-and-table-partitioning"></a>インデックスとテーブルのパーティション分割  
 この機能によって、インデックス データおよびテーブル データを、パーティション内の複数のファイル グループに分散させることができます。 パーティション関数は、パーティション分割列と呼ばれる特定の列の値に基づいて、テーブルまたはインデックスの行を一連のパーティションにどのようにマップするかを定義します。 パーティション構成は、パーティション関数によって指定された各パーティションをファイル グループにマップします。 これにより、複数のファイル グループにまたがってテーブルを拡張できるような、したがって物理デバイスもまたがって拡張できるような、アーカイブ戦略を開発することができます。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクトには、実装されたパーティション関数を表す <xref:Microsoft.SqlServer.Management.Smo.PartitionFunction> オブジェクトのコレクション、およびファイル グループへのデータのマップ方法を記述する <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme> オブジェクトのコレクションが含まれています。  
  
 各 <xref:Microsoft.SqlServer.Management.Smo.Table> オブジェクトおよび <xref:Microsoft.SqlServer.Management.Smo.Index> オブジェクトは、どのパーティション構成を使用するかを <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme> プロパティで指定し、列を <xref:Microsoft.SqlServer.Management.Smo.PartitionSchemeParameterCollection> で指定します。  
  
## <a name="example"></a>例  
 次のコード例では、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual studio .net での VISUAL BASIC SMO プロジェクトの作成](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)」および「visual [studio .Net での Visual C&#35; SMO プロジェクトの作成](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-visual-basic"></a>Visual Basic でのテーブルのパーティション構成の設定  
 コード例では、 `TransactionHistory` サンプル データベース内の [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] テーブルに対してパーティション関数およびパーティション構成を作成する方法を示します。 これらのパーティションは、古いレコードを `TransactionHistoryArchive` テーブルに分割する目的で、日付によって分割されます。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBPartition1](SMO How to#SMO_VBPartition1)]  -->  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-visual-c"></a>Visual C# でのテーブルのパーティション構成の設定  
 コード例では、 `TransactionHistory` サンプル データベース内の [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] テーブルに対してパーティション関数およびパーティション構成を作成する方法を示します。 これらのパーティションは、古いレコードを `TransactionHistoryArchive` テーブルに分割する目的で、日付によって分割されます。  
  
```csharp
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Define and create three new file groups on the database.   
FileGroup fg2;   
fg2 = new FileGroup(db, "Second");   
fg2.Create();   
FileGroup fg3;   
fg3 = new FileGroup(db, "Third");   
fg3.Create();   
FileGroup fg4;   
fg4 = new FileGroup(db, "Fourth");   
fg4.Create();   
//Define a partition function by supplying the parent database and name arguments in the constructor.   
PartitionFunction pf;   
pf = new PartitionFunction(db, "TransHistPF");   
//Add a partition function parameter that specifies the function uses a DateTime range type.   
PartitionFunctionParameter pfp;   
pfp = new PartitionFunctionParameter(pf, DataType.DateTime);   
pf.PartitionFunctionParameters.Add(pfp);   
//Specify the three dates that divide the data into four partitions.   
object[] val;   
val = new object[] {"1/1/2003", "1/1/2004", "1/1/2005"};   
pf.RangeValues = val;   
//Create the partition function.   
pf.Create();   
//Define a partition scheme by supplying the parent database and name arguments in the constructor.   
PartitionScheme ps;   
ps = new PartitionScheme(db, "TransHistPS");   
//Specify the partition function and the filegroups required by the partition scheme.   
ps.PartitionFunction = "TransHistPF";   
ps.FileGroups.Add("PRIMARY");   
ps.FileGroups.Add("second");   
ps.FileGroups.Add("Third");   
ps.FileGroups.Add("Fourth");   
//Create the partition scheme.   
ps.Create();   
}   
```  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-powershell"></a>PowerShell でのテーブルのパーティション構成の設定  
 コード例では、 `TransactionHistory` サンプル データベース内の [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] テーブルに対してパーティション関数およびパーティション構成を作成する方法を示します。 これらのパーティションは、古いレコードを `TransactionHistoryArchive` テーブルに分割する目的で、日付によって分割されます。  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
$db = $srv.Databases["AdventureWorks"]  
#Create four filegroups  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "First"  
$fg2 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Second"  
$fg3 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Third"  
$fg4 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Fourth"  
  
#Define a partition function by supplying the parent database and name arguments in the constructor.  
$pf =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunction -argumentlist $db, "TransHistPF"  
$T = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$T  
$T.GetType()  
#Add a partition function parameter that specifies the function uses a DateTime range type.  
$pfp =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunctionParameter -argumentlist $pf, $T  
  
#Specify the three dates that divide the data into four partitions.
#Create an array of type object to hold the partition data  
$val = "1/1/2003"."1/1/2004","1/1/2005"  
$pf.RangeValues = $val  
$pf  
#Create the partition function  
$pf.Create()  
  
#Create partition scheme  
$ps = New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionScheme -argumentlist $db, "TransHistPS"  
$ps.PartitionFunction = "TransHistPF"  
  
#add the filegroups to the scheme
$ps.FileGroups.Add("PRIMARY")  
$ps.FileGroups.Add("Second")  
$ps.FileGroups.Add("Third")  
$ps.FileGroups.Add("Fourth")  
  
#Create it at the server  
$ps.Create()  
```  
  
## <a name="see-also"></a>「  
 [Partitioned Tables and Indexes](../../partitions/partitioned-tables-and-indexes.md)  
