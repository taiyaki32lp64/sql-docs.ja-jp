---
title: ユーザー定義関数の作成、変更、および削除 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- user-defined functions [SMO]
ms.assetid: 0ebebd3b-0775-41c2-989d-aa4cf81af12a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: edde17b3339a6a78f81ddf92da95afb2f8ba851c
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782348"
---
# <a name="creating-altering-and-removing-user-defined-functions"></a>ユーザー定義関数の作成、変更、および削除
  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> オブジェクトは、ユーザーが [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]でユーザー定義関数をプログラムで管理できるようにする機能を提供します。 ユーザー定義関数では、入力パラメーターおよび出力パラメーターに加えて、テーブル列への直接参照もサポートされます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、ストアド プロシージャ、ユーザー定義関数、トリガー、およびユーザー定義データ型内でアセンブリを使用できるようにするには、アセンブリがデータベース内に登録される必要があります。 SMO は、<xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> オブジェクトを使用してこの機能をサポートします。  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> オブジェクトは、<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.AssemblyName%2A> プロパティ、<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.ClassName%2A> プロパティ、および <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.MethodName%2A> プロパティを使用して .NET アセンブリを参照します。  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction> オブジェクトが .NET アセンブリを参照する場合、<xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> オブジェクトを作成し、それを <xref:Microsoft.SqlServer.Management.Smo.SqlAssemblyCollection> オブジェクトに属する <xref:Microsoft.SqlServer.Management.Smo.Database> オブジェクトに追加することによって、アセンブリを登録する必要があります。  
  
## <a name="example"></a>例  
 提供されているコード例を使用するには、アプリケーションを作成するプログラミング環境、プログラミング テンプレート、およびプログラミング言語を選択する必要があります。 詳細については、「 [Visual studio .net での VISUAL BASIC SMO プロジェクトの作成](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)」または「visual [studio .Net での Visual C&#35; SMO プロジェクトの作成](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)」を参照してください。  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-basic"></a>Visual Basic でのユーザー定義スカラー関数の作成  
 このコード例は、入力の <xref:System.DateTime> オブジェクト パラメーターおよび整数型の戻り値を持つユーザー定義のスカラー関数を [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] で作成および削除する方法を示しています。 ユーザー定義関数は [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースに作成されます。 この例では、日付引数を取得して ISO 週番号を計算するユーザー定義関数 ISOweek が作成されます。 この関数で正しい計算を行うためには、関数を呼び出す前に、データベースの DATEFIRST オプションが 1 に設定されている必要があります。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBUserDefFuncs1](SMO How to#SMO_VBUserDefFuncs1)]  -->  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-c"></a>Visual C# でのユーザー定義スカラー関数の作成  
 このコード例は、入力の <xref:System.DateTime> オブジェクト パラメーターおよび整数型の戻り値を持つユーザー定義のスカラー関数を [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] で作成および削除する方法を示しています。 ユーザー定義関数は [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースに作成されます。 この例では、次のユーザー定義関数を作成します。 `ISOweek`に評価されるまで、タスクを繰り返します。 この関数は、日付引数を受け取って、ISO 週番号を計算します。 この関数で正しい計算を行うためには、関数を呼び出す前に、データベースの `DATEFIRST` オプションが `1` に設定されている必要があります。  
  
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
 このコード例は、入力の <xref:System.DateTime> オブジェクト パラメーターおよび整数型の戻り値を持つユーザー定義のスカラー関数を [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] で作成および削除する方法を示しています。 ユーザー定義関数は [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] データベースに作成されます。 この例では、次のユーザー定義関数を作成します。 `ISOweek`に評価されるまで、タスクを繰り返します。 この関数は、日付引数を受け取って、ISO 週番号を計算します。 この関数で正しい計算を行うためには、関数を呼び出す前に、データベースの `DATEFIRST` オプションが `1` に設定されている必要があります。  
  
```powershell
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = Get-Item Adventureworks2012  
  
# Define a user defined function object variable by supplying the parent database and name arguments in the constructor.
$udf  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunction -argumentlist $db, "IsOWeek"  
  
# Set the TextMode property to false and then set the other properties.
$udf.TextMode = $false  
$udf.DataType = [Microsoft.SqlServer.Management.SMO.DataType]::Int
$udf.ExecutionContext = [Microsoft.SqlServer.Management.SMO.ExecutionContext]::Caller  
$udf.FunctionType = [Microsoft.SqlServer.Management.SMO.UserDefinedFunctionType]::Scalar  
$udf.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Define a Parameter object variable by supplying the parent function, name and type arguments in the constructor.  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$par  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunctionParameter -argumentlist $udf, "@DATE",$type  
  
# Add the parameter to the function  
$udf.Parameters.Add($par)  
  
#Set the TextBody property to define the user-defined function.
$udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;"  
  
# Create the user-defined function on the instance of SQL Server.
$udf.Create()  
  
# Remove the user-defined function.
$udf.Drop()  
```  
  
## <a name="see-also"></a>「  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction>  
