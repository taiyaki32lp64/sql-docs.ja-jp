---
title: ユーザー定義関数の作成、変更、および削除
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- user-defined functions [SMO]
ms.assetid: 0ebebd3b-0775-41c2-989d-aa4cf81af12a
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8fc10bd6ebb44e0f8b45edb3c669e8216cc313b1
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095568"
---
# <a name="creating-altering-and-removing-user-defined-functions"></a>ユーザー定義関数の作成、変更、および削除
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]
  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> オブジェクトは、ユーザーが [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]でユーザー定義関数をプログラムで管理できるようにする機能を提供します。 ユーザー定義関数では、入力パラメーターおよび出力パラメーターに加えて、テーブル列への直接参照もサポートされます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、ストアド プロシージャ、ユーザー定義関数、トリガー、およびユーザー定義データ型内でアセンブリを使用できるようにするには、アセンブリがデータベース内に登録される必要があります。 SMO は、<xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> オブジェクトを使用してこの機能をサポートします。  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> オブジェクトは、<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.AssemblyName%2A> プロパティ、<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.ClassName%2A> プロパティ、および <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.MethodName%2A> プロパティを使用して .NET アセンブリを参照します。  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> オブジェクトが .NET アセンブリを参照する場合、<xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> オブジェクトを作成し、それを <xref:Microsoft.SqlServer.Management.Smo.SqlAssemblyCollection> オブジェクトに属する <xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクトに追加することによって、アセンブリを登録する必要があります。  
  
## <a name="example"></a>例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual Studio&#35; .Net での Visual C SMO プロジェクトの作成](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-basic"></a>Visual Basic でのユーザー定義スカラー関数の作成  
 このコード例は、入力の <xref:System.DateTime> オブジェクト パラメーターおよび整数型の戻り値を持つユーザー定義のスカラー関数を [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] で作成および削除する方法を示しています。 ユーザー定義関数は [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースに作成されます。 この例では、日付引数を取得して ISO 週番号を計算するユーザー定義関数 ISOweek が作成されます。 この関数で正しい計算を行うためには、関数を呼び出す前に、データベースの DATEFIRST オプションが 1 に設定されている必要があります。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a UserDefinedFunction object variable by supplying the parent database and the name arguments in the constructor.
Dim udf As UserDefinedFunction
udf = New UserDefinedFunction(db, "IsOWeek")
'Set the TextMode property to false and then set the other properties.
udf.TextMode = False
udf.DataType = DataType.Int
udf.ExecutionContext = ExecutionContext.Caller
udf.FunctionType = UserDefinedFunctionType.Scalar
udf.ImplementationType = ImplementationType.TransactSql
'Add a parameter.
Dim par As UserDefinedFunctionParameter
par = New UserDefinedFunctionParameter(udf, "@DATE", DataType.DateTime)
udf.Parameters.Add(par)
'Set the TextBody property to define the user defined function.
udf.TextBody = "BEGIN  DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;"
'Create the user defined function on the instance of SQL Server.
udf.Create()
'Remove the user defined function.
udf.Drop()
``` 
  
## <a name="creating-a-scalar-user-defined-function-in-visual-c"></a>Visual C# でのユーザー定義スカラー関数の作成  
 このコード例は、入力の <xref:System.DateTime> オブジェクト パラメーターおよび整数型の戻り値を持つユーザー定義のスカラー関数を [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] で作成および削除する方法を示しています。 ユーザー定義関数は [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースに作成されます。 この例では、次のユーザー定義関数を作成します。 `ISOweek`。 この関数は、日付引数を受け取って、ISO 週番号を計算します。 この関数で正しい計算を行うためには、関数を呼び出す前に、データベースの `DATEFIRST` オプションが `1` に設定されている必要があります。  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
           Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
           Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a UserDefinedFunction object variable by supplying the parent database and the name arguments in the constructor.   
            UserDefinedFunction udf = new UserDefinedFunction(db, "IsOWeek");  
  
            //Set the TextMode property to false and then set the other properties.   
            udf.TextMode = false;  
            udf.DataType = DataType.Int;  
            udf.ExecutionContext = ExecutionContext.Caller;  
            udf.FunctionType = UserDefinedFunctionType.Scalar;  
            udf.ImplementationType = ImplementationType.TransactSql;  
  
            //Add a parameter.   
  
     UserDefinedFunctionParameter par = new UserDefinedFunctionParameter(udf, "@DATE", DataType.DateTime);  
            udf.Parameters.Add(par);  
  
            //Set the TextBody property to define the user-defined function.   
            udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;";  
  
            //Create the user-defined function on the instance of SQL Server.   
            udf.Create();  
  
            //Remove the user-defined function.   
            udf.Drop();  
        }  
```  
  
## <a name="creating-a-scalar-user-defined-function-in-powershell"></a>PowerShell でのユーザー定義スカラー関数の作成  
 このコード例は、入力の <xref:System.DateTime> オブジェクト パラメーターおよび整数型の戻り値を持つユーザー定義のスカラー関数を [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] で作成および削除する方法を示しています。 ユーザー定義関数は [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースに作成されます。 この例では、次のユーザー定義関数を作成します。 `ISOweek`。 この関数は、日付引数を受け取って、ISO 週番号を計算します。 この関数で正しい計算を行うためには、関数を呼び出す前に、データベースの `DATEFIRST` オプションが `1` に設定されている必要があります。  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a user defined function object variable by supplying the parent database and name arguments in the constructor.   
$udf  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunction `  
-argumentlist $db, "IsOWeek"  
  
# Set the TextMode property to false and then set the other properties.   
$udf.TextMode = $false  
$udf.DataType = [Microsoft.SqlServer.Management.SMO.DataType]::Int   
$udf.ExecutionContext = [Microsoft.SqlServer.Management.SMO.ExecutionContext]::Caller  
$udf.FunctionType = [Microsoft.SqlServer.Management.SMO.UserDefinedFunctionType]::Scalar  
$udf.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Define a Parameter object variable by supplying the parent function, name and type arguments in the constructor.  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$par  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunctionParameter `  
-argumentlist $udf, "@DATE",$type  
  
# Add the parameter to the function  
$udf.Parameters.Add($par)  
  
#Set the TextBody property to define the user-defined function.   
$udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;"  
  
# Create the user-defined function on the instance of SQL Server.   
$udf.Create()  
  
# Remove the user-defined function.   
$udf.Drop()  
```  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction>  
  
  
