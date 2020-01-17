---
title: Hello World のサンプル |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: fed6c358-f5ee-4d4c-9ad6-089778383ba7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ac48f47b7455fd68245cec23c68132e4070835f9
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637764"
---
# <a name="hello-world-sample"></a>Hello World サンプル
  Hello World サンプルでは、共通言語ランタイム (CLR) 統合ベースの単純なストアド プロシージャの作成、展開、およびテストにかかわる基本的な操作について示します。 また、このサンプルでは、ストアド プロシージャによって動的に構築されて呼び出し元に返されるレコードを使用してデータを返す方法についても示します。  
  
 `HelloWorld` ストアドプロシージャは、文字列 "Hello world!" を返します。 1つの行で構成される結果セット。 この例では、 [SqlDataRecord](https://go.microsoft.com/fwlink/?LinkID=193573)および[microsoft](https://go.microsoft.com/fwlink/?LinkID=193571). sqlserver. サーバーのクラスのいくつかの使用[方法を示し](https://go.microsoft.com/fwlink/?LinkID=193572)ています。この例を次に示します。  
  
## <a name="prerequisites"></a>前提条件  
 このプロジェクトを作成して実行するには、次のソフトウェアがインストールされている必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express ドキュメントとサンプルの [Web サイト](https://www.microsoft.com/sql-server/sql-server-editions-express)から無償で入手できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] デベロッパー [Web サイト](https://go.microsoft.com/fwlink/?linkid=62796)から入手できる AdventureWorks データベース。  
  
-   .NET Framework SDK 2.0 以降または Microsoft Visual Studio 2005 以降。 .NET Framework SDK は無償で入手できます。  
  
-   また、次の条件を満たしている必要があります。  
  
-   使用している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで CLR 統合が有効になっている必要があります。  
  
-   CLR 統合を有効にするには、次の手順に従います。  
  
    #### <a name="enabling-clr-integration"></a>CLR 統合の有効化  
  
    -   以下の [!INCLUDE[tsql](../../includes/tsql-md.md)] コマンドを実行します。  
  
     `sp_configure 'clr enabled', 1`  
  
     `GO`  
  
     `RECONFIGURE`  
  
     `GO`  
  
    > [!NOTE]  
    >  CLR を有効にするには、`ALTER SETTINGS` サーバーレベルの権限を持っている必要があります。この権限は、固定サーバーロール `sysadmin` と `serveradmin` のメンバーによって暗黙的に保持されます。  
  
-   使用している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに AdventureWorks データベースがインストールされている必要があります。  
  
-   使用している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの管理者でない場合、インストールを完了するには、 **Createassembly**アクセス許可を管理者に付与する必要があります。  
  
## <a name="building-the-sample"></a>サンプルのビルド  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>次の手順に従ってサンプルを作成し、実行します。  
  
1.  Visual Studio または .NET Framework のコマンド プロンプトを開きます。  
  
2.  必要な場合は、サンプル用のディレクトリを作成します。 この例では C:\MySample を使用します。  
  
3.  c:\MySample で、`HelloWorld.vb` (Visual Basic サンプル) または `HelloWorld.cs` (C# サンプル) を作成し、適切な Visual Basic または C# のサンプル コード (下記) をこのファイルにコピーします。  
  
4.  選択した言語に応じて次のいずれかをコマンド プロンプトで実行し、サンプル コードをコンパイルします。  
  
    -   `vbc C:HelloWorld.vb /target:library`  
  
    -   `csc /target:library HelloWorld.cs`  
  
5.  [!INCLUDE[tsql](../../includes/tsql-md.md)] インストール コードをファイルにコピーし、`Install.sql` としてサンプル ディレクトリに保存します。  
  
6.  次のコマンドを実行して、アセンブリとストアド プロシージャを配置します。  
  
    -   `sqlcmd -E -I -i install.sql -v root = "C:\MySample\"`  
  
7.  テストコマンドスクリプトをファイルにコピー [!INCLUDE[tsql](../../includes/tsql-md.md)]、`test.sql` としてサンプルディレクトリに保存します。  
  
8.  次のコマンドを使用してテスト スクリプトを実行します。  
  
    -   `sqlcmd -E -I -i test.sql`  
  
9. [!INCLUDE[tsql](../../includes/tsql-md.md)] クリーンアップ スクリプトをファイルにコピーし、`cleanup.sql` としてサンプル ディレクトリに保存します。  
  
10. 次のコマンドを使用してこのスクリプトを実行します。  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>サンプル コード  
 このサンプルのコード リストを次に示します。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
public partial class StoredProcedures  
{  
    [Microsoft.SqlServer.Server.SqlProcedure]  
    public static void HelloWorld()  
    {  
        Microsoft.SqlServer.Server.SqlMetaData columnInfo  
                = new Microsoft.SqlServer.Server.SqlMetaData("Column1", SqlDbType.NVarChar, 12);  
        SqlDataRecord greetingRecord  
            = new SqlDataRecord(new Microsoft.SqlServer.Server.SqlMetaData[] { columnInfo });  
        greetingRecord.SetString(0, "Hello world!");  
        SqlContext.Pipe.Send(greetingRecord);  
    }  
};  
  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Partial Public NotInheritable Class StoredProcedures  
    <Microsoft.SqlServer.Server.SqlProcedure()> _  
    Public Shared Sub HelloWorld()  
        Dim columnInfo As New Microsoft.SqlServer.Server.SqlMetaData("Column1", _  
            SqlDbType.NVarChar, 12)  
        Dim greetingRecord As New SqlDataRecord(New  _  
            Microsoft.SqlServer.Server.SqlMetaData() {columnInfo})  
        greetingRecord.SetString(0, "Hello World!")  
        SqlContext.Pipe.Send(greetingRecord)  
    End Sub  
End Class  
```  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] インストール スクリプト (`Install.sql`) は、アセンブリを展開し、データベースにストアド プロシージャを作成します。  
  
```  
USE AdventureWorks  
GO  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorld')  
DROP PROCEDURE usp_HelloWorld;  
GO  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorld')  
DROP ASSEMBLY HelloWorld;  
GO  
DECLARE @SamplesPath nvarchar(1024)  
set @SamplesPath = '$(root)'  
CREATE ASSEMBLY HelloWorld   
FROM @SamplesPath + 'HelloWorld.dll'  
WITH permission_set = Safe;  
GO  
  
CREATE PROCEDURE usp_HelloWorld  
--(  
--    @Greeting nvarchar(12) OUTPUT  
--)  
AS EXTERNAL NAME HelloWorld.[StoredProcedures].HelloWorld;  
GO  
```  
  
 次の `test.sql` は、ストアド プロシージャを実行してサンプルをテストします。  
  
```  
use AdventureWorks  
go  
execute usp_HelloWorld  
  
USE AdventureWorks;  
GO  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorld')  
DROP PROCEDURE usp_HelloWorld;  
GO  
```  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] は、データベースからアセンブリとストアド プロシージャを削除します。  
  
```  
USE AdventureWorks  
GO  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorld')  
DROP PROCEDURE usp_HelloWorld;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorld')  
DROP ASSEMBLY HelloWorld;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CLR &#40;共通言語ランタイム&#41; 統合の使用シナリオと例](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
