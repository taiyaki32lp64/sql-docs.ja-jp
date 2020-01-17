---
title: Hello World 準備完了のサンプル |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
ms.assetid: 1cb94266-f702-4a57-a1ae-689a89c98757
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8303c387ff38ab5448d15e478534df165e05bddf
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637656"
---
# <a name="hello-world-ready-sample"></a>Hello World Ready サンプル
  Hello World Ready サンプルでは、国際化対応の、CLR (共通言語ランタイム) 統合ベースの単純なストアド プロシージャの作成、配置、およびテストにかかわる基本的な操作を示しています。 国際化対応コンポーネントは、コンポーネントのソース コードを変更することなく、世界中の市場に向けて、異なる言語へのローカライズを簡単に行うことができます。 また、このサンプルでは、ストアド プロシージャによって動的に構築されてクライアントに返されるレコードおよび出力パラメーターを使用してデータを返す方法についても示します。このサンプルは、Hello World サンプルとほぼ同じですが、このアプリケーションのローカライズをより簡単かつ安全に行うことができます。 ローカライズ済みテキストを変更するには、次の作業を実行する必要があります。  
  
1.  XML ファイルの変更 (.`resx` ファイル) を参照してください。  
  
2.  `resgen` を使用して、カルチャに応じたリソース ファイルをビルドします。  
  
3.  そのカルチャに関して更新されたサテライト DLL をビルドします。  
  
4.  このアセンブリを SQL Server でいったん削除してから、追加します。  
  
 CLR ストアド プロシージャ自体のソース コードおよびアセンブリは変更されません。 リソース アセンブリのコンパイル方法とリンク方法を示す `build.cmd` スクリプトが用意されています。アプリケーションのソース コードによって、現在実行しているアセンブリに基づいたリソース マネージャーが作成されますが、ストアド プロシージャを含む DLL にカルチャ ニュートラル リソースを埋め込む必要はありません。 `System.Resources.NeutralResourcesLanguage attribute` によって、カルチャ ニュートラル リソースがサテライト DLL に存在することが許可されます。 この目的でそれぞれ別の DLL を使用すると、ローカライズ済みテキストの追加や変更が必要な場合でも、CLR ストアド プロシージャを含んでいるプライマリ DLL の変更が必要なくなるため非常に便利です。 これは、型の削除と再追加を困難にするような列やその他の依存関係を含んでいることのある、CLR ユーザー定義型には特に役立ちます。通常、サテライト DLL バージョンはメイン アセンブリ バージョンと同じである必要があります。 ただし、`SatelliteContractVersion` 属性を使用して、サテライト アセンブリを更新せずにメイン アセンブリの更新を許可することもできます。 詳細については、Microsoft .NET のドキュメントで `ResourceManager` クラスを参照してください。  
  
## <a name="prerequisites"></a>前提条件  
 このサンプルは、SQL Server 2005 以降のバージョンでのみ動作します。  
  
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
  
-   使用している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの管理者でない場合は、インストールを完了するために **CreateAssembly** 権限が管理者から付与されている必要があります。  
  
## <a name="building-the-sample"></a>サンプルのビルド  
  
#### <a name="create-and-run-the-sample-by-using-the-following-instructions"></a>次の手順に従ってサンプルを作成し、実行します。  
  
1.  Visual Studio または .NET Framework のコマンド プロンプトを開きます。  
  
2.  必要な場合は、サンプル用のディレクトリを作成します。 この例では C:\MySample を使用します。  
  
3.  c:\MySample で、`HelloWorld.vb` (Visual Basic サンプル) または `HelloWorld.cs` (C# サンプル) を作成し、適切な Visual Basic または C# のサンプル コード (下記) をこのファイルにコピーします。  
  
4.  C:\MySample で、ファイル `messages.resx` を作成し、サンプルコードをファイルにコピーします。  
  
5.  C:\MySample で、行を変更した後 `messages.de.resx` としてファイル `messages.resx` を保存して、ファイル `messages.de.resx` を作成します。  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   次のように変更  
  
    -   `<value xml:space="preserve">Hallo Welt!</value>`  
  
6.  C:\MySample で、行を変更した後 `messages.es.resx` としてファイル `messages.resx` を保存して、ファイル `messages.es.resx` を作成します。  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   次のように変更  
  
    -   `<value xml:space="preserve">Hola a todos</value>`  
  
7.  C:\MySample で、行を変更した後 `messages.fr.resx` としてファイル `messages.resx` を保存して、ファイル `messages.fr.resx` を作成します。  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   次のように変更  
  
    -   `<value xml:space="preserve">BonjourÂ !</value>`  
  
8.  C:\MySample で、行を変更した後 `messages.fr-FR.resx` としてファイル `messages.resx` を保存して、ファイル `messages.fr-FR.resx` を作成します。  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   次のように変更  
  
    -   `<value xml:space="preserve">Bonjour de France!</value>`  
  
9. C:\MySample で、行を変更した後 `messages.it.resx` としてファイル `messages.resx` を保存して、ファイル `messages.it.resx` を作成します。  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   次のように変更  
  
    -   `<value xml:space="preserve">Buongiorno</value>`  
  
10. C:\MySample で、行を変更した後 `messages.ja.resx` としてファイル `messages.resx` を保存して、ファイル `messages.ja.resx` を作成します。  
  
    -   `<value xml:space="preserve">Hello, World!</value>`  
  
    -   次のように変更  
  
    -   `<value xml:space="preserve">` `ã"ã‚"ã«ã¡ã¯</value>`  
  
11. c:\MySample で、ファイル `build.com` を作成し、サンプル コードをこのファイルにコピーします。  
  
12. ビルドされたファイルをコマンド プロンプトで実行して、サテライト アセンブリをビルドします。  
  
13. 次のいずれかをコマンド プロンプトで実行して、サンプル コードをコンパイルします。  
  
    -   `Vbc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll,C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Xml.dll /out:HelloWorldReady.dll /target:library HelloWorld.vb`  
  
    -   `Csc /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.Data.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.dll /reference:C:\Windows\Microsoft.NET\Framework\v2.0.50727\System.XML.dll /out:HelloWorldReady.dll /target:library Hello.csCopy the tsql installation code into a file and save it as Install.sql in the sample directory.`  
  
14. サンプルが `C:\MySample\`以外のディレクトリにインストールされている場合は、その場所を示すように、ファイル `Install.sql` を編集します。  
  
15. 次のコマンドを実行して、アセンブリとストアド プロシージャを配置します。  
  
    -   `sqlcmd -E -I -i install.sql`  
  
16. テストコマンドスクリプトをファイルにコピー [!INCLUDE[tsql](../../includes/tsql-md.md)]、`test.sql` としてサンプルディレクトリに保存します。  
  
17. 次のコマンドを使用してテスト スクリプトを実行します。  
  
    -   `sqlcmd -E -I -i test.sql`  
  
18. [!INCLUDE[tsql](../../includes/tsql-md.md)] クリーンアップ スクリプトをファイルにコピーし、`cleanup.sql` としてサンプル ディレクトリに保存します。  
  
19. 次のコマンドを使用してこのスクリプトを実行します。  
  
    -   `sqlcmd -E -I -i cleanup.sql`  
  
## <a name="sample-code"></a>サンプル コード  
 このサンプルのコード リストを次に示します。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.Sql;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
using System.Globalization;  
using System.Threading;  
using System.Resources;  
using System.Reflection;  
using System.Runtime.CompilerServices;  
  
[assembly: System.Resources.NeutralResourcesLanguage("", System.Resources.UltimateResourceFallbackLocation.Satellite)]  
[assembly: System.Security.Permissions.SecurityPermissionAttribute(System.Security.Permissions.SecurityAction.RequestMinimum)]  
[assembly: System.Runtime.ConstrainedExecution.ReliabilityContract(System.Runtime.ConstrainedExecution.Consistency.MayCorruptInstance, System.Runtime.ConstrainedExecution.Cer.None)]  
  
    public sealed partial class StoredProcedures  
    {  
        private StoredProcedures()  
        {  
        }  
  
        [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1021:AvoidOutParameters"), Microsoft.SqlServer.Server.SqlProcedure]  
        public static void HelloWorldReady(string culture, out string greeting)  
        {  
ResourceManager rm   
= new ResourceManager("Messages",   
Assembly.GetExecutingAssembly());  
  
string message = rm.GetString("HelloWorld", CultureInfo.GetCultureInfo(culture));  
  
            Microsoft.SqlServer.Server.SqlMetaData columnInfo  
                = new Microsoft.SqlServer.Server.SqlMetaData("Column1", SqlDbType.NVarChar, 24);  
            SqlDataRecord greetingRecord  
                = new SqlDataRecord(new Microsoft.SqlServer.Server.SqlMetaData[] { columnInfo });  
            greetingRecord.SetString(0, message);  
            SqlContext.Pipe.Send(greetingRecord);  
            greeting = message;  
        }  
    }  
  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Globalization  
Imports System.Resources  
Imports System.Reflection  
Imports System.Runtime.InteropServices  
<Assembly: AssemblyVersion("1.0.*")>   
<Assembly: System.Runtime.InteropServices.ComVisible(False)>   
<Assembly: System.CLSCompliant(True)>   
<Assembly: System.Resources.NeutralResourcesLanguage("", System.Resources.UltimateResourceFallbackLocation.Satellite)>   
<Assembly: System.Security.Permissions.SecurityPermissionAttribute(System.Security.Permissions.SecurityAction.RequestMinimum)>   
<Assembly: System.Runtime.ConstrainedExecution.ReliabilityContract(System.Runtime.ConstrainedExecution.Consistency.WillNotCorruptState, Runtime.ConstrainedExecution.Cer.None)>   
  
Partial Public NotInheritable Class StoredProcedures  
    Private Sub New()  
    End Sub  
    <Microsoft.SqlServer.Server.SqlProcedure()> _  
    Public Shared Sub HelloWorldReady(ByVal culture As String, ByRef greeting As String)  
        Dim rm As New ResourceManager("Messages", Assembly.GetExecutingAssembly())  
        Dim message As String = rm.GetString("HelloWorld", CultureInfo.GetCultureInfo(culture))  
        Dim columnInfo As New Microsoft.SqlServer.Server.SqlMetaData("Column1", _  
            SqlDbType.NVarChar, 24)  
        Dim greetingRecord As New SqlDataRecord(New  _  
            Microsoft.SqlServer.Server.SqlMetaData() {columnInfo})  
        greetingRecord.SetString(0, message)  
        SqlContext.Pipe.Send(greetingRecord)  
        greeting = message  
    End Sub  
End Class  
  
```  
  
 次の `build.com` は、サテライト アセンブリをビルドします。  
  
```  
resgen Messages.resx  
resgen Messages.de.resx  
resgen Messages.es.resx  
resgen Messages.fr.resx  
resgen Messages.fr-Fr.resx  
resgen Messages.it.resx  
resgen Messages.ja.resx  
if not exist de/ mkdir de  
if not exist es/ mkdir es  
if not exist fr/ mkdir fr  
if not exist fr-FR/ mkdir fr-FR  
if not exist it/ mkdir it  
if not exist ja/ mkdir ja  
al /t:lib /culture:de /embed:Messages.de.resources /out:de\HelloWorldReady.resources.dll  
al /t:lib /culture:es /embed:Messages.es.resources /out:es\HelloWorldReady.resources.dll  
al /t:lib /culture:fr /embed:Messages.fr.resources /out:fr\HelloWorldReady.resources.dll  
al /t:lib /culture:fr-FR /embed:Messages.fr-FR.resources /out:fr-FR\HelloWorldReady.resources.dll  
al /t:lib /culture:it /embed:Messages.it.resources /out:it\HelloWorldReady.resources.dll  
al /t:lib /culture:ja /embed:Messages.ja.resources /out:ja\HelloWorldReady.resources.dll  
al /t:lib /culture:"" /embed:Messages.resources /out:HelloWorldReady.resources.dll  
```  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] インストール スクリプト (`Install.sql`) は、アセンブリを配置し、データベース内にストアド プロシージャを作成します。  
  
```  
USE AdventureWorks  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorldReady')  
DROP PROCEDURE usp_HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady')  
DROP ASSEMBLY HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.neutral')  
DROP ASSEMBLY [HelloWorldReady.resources.neutral]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.de')  
DROP ASSEMBLY [HelloWorldReady.resources.de]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.es')  
DROP ASSEMBLY [HelloWorldReady.resources.es]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr')  
DROP ASSEMBLY [HelloWorldReady.resources.fr]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr-FR')  
DROP ASSEMBLY [HelloWorldReady.resources.fr-FR]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.it')  
DROP ASSEMBLY [HelloWorldReady.resources.it]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.ja')  
DROP ASSEMBLY [HelloWorldReady.resources.ja]  
GO  
  
DECLARE @SamplesPath nvarchar(1024)  
-- You may need to modify the value of this variable if you have installed the sample someplace other than the default location.  
Set @SamplesPath = N'C:\MySample\'  
  
-- Add the assembly and CLR integration based stored procedure  
  
CREATE ASSEMBLY HelloWorldReady  
FROM @SamplesPath + 'HelloWorldReady.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.neutral]  
FROM @SamplesPath + 'HelloWorldReady.resources.dll'  
WITH permission_set = Safe;   
  
CREATE ASSEMBLY [HelloWorldReady.resources.de]  
FROM @SamplesPath + '\de\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.es]  
FROM @SamplesPath + '\es\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.fr]  
FROM @SamplesPath + '\fr\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.fr-FR]  
FROM @SamplesPath + '\fr-FR\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.it]  
FROM @SamplesPath + '\it\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
  
CREATE ASSEMBLY [HelloWorldReady.resources.ja]  
FROM @SamplesPath + '\ja\HelloWorldReady.resources.dll'  
WITH permission_set = Safe;  
GO  
  
CREATE PROCEDURE usp_HelloWorldReady  
(  
@Culture NVarchar(12),  
@Greeting NVarchar(24) OUTPUT  
)  
AS EXTERNAL NAME HelloWorldReady.StoredProcedures.HelloWorldReady;  
GO  
  
USE master;  
GO  
```  
  
 次の `test.sql` は、各ロケールで関数を実行してサンプルをテストします。  
  
```  
USE AdventureWorks  
GO  
  
DECLARE @GreetingDe nvarchar(24);  
DECLARE @GreetingDe_CH nvarchar(24);  
DECLARE @GreetingEn nvarchar(24);  
DECLARE @GreetingEs nvarchar(24);  
DECLARE @GreetingFr nvarchar(24);  
DECLARE @GreetingFr_FR nvarchar(24);  
DECLARE @GreetingIt nvarchar(24);  
DECLARE @GreetingJa nvarchar(24);  
  
--German as spoken anywhere in the world (the neutral German culture)  
EXEC usp_HelloWorldReady 'de', @GreetingDe OUTPUT;  
--German as spoken in Switzerland.  Because we don't have a specific assembly  
--for this case, the .NET Framework will automatically fall back to the neutral German culture DLL.  
EXEC usp_HelloWorldReady 'de-CH', @GreetingDe_CH OUTPUT;  
EXEC usp_HelloWorldReady 'en', @GreetingEn OUTPUT;  
EXEC usp_HelloWorldReady 'es', @GreetingEs OUTPUT;  
--French as spoken anywhere in the world (the neutral French culture)  
EXEC usp_HelloWorldReady 'fr', @GreetingFr OUTPUT  
--French as spoken in France.  Since we do have a specific assembly for this case, a specific   
--greeting is provided from that DLL.  The neutral French culture DLL is not used in this case.  
EXEC usp_HelloWorldReady 'fr-FR', @GreetingFr_FR OUTPUT  
EXEC usp_HelloWorldReady 'it', @GreetingIt OUTPUT;  
EXEC usp_HelloWorldReady 'ja', @GreetingJa OUTPUT;  
  
SELECT @GreetingDe AS OUTPUT_PARAMETER_DE;  
SELECT @GreetingDe_CH AS OUTPUT_PARAMETER_De_CH;  
SELECT @GreetingEn AS OUTPUT_PARAMETER_EN;  
SELECT @GreetingEs AS OUTPUT_PARAMETER_ES;  
SELECT @GreetingFr AS OUTPUT_PARAMETER_FR;  
SELECT @GreetingFr_FR AS OUTPUT_PARAMETER_Fr_FR;  
SELECT @GreetingIt AS OUTPUT_PARAMETER_IT;  
SELECT @GreetingJa AS OUTPUT_PARAMETER_JA;  
  
GO  
```  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] は、データベースからアセンブリとストアド プロシージャを削除します。  
  
```  
USE AdventureWorks;  
GO  
  
-- Drop existing sproc and assembly if any.  
  
IF EXISTS (SELECT * FROM sys.procedures WHERE [name] = 'usp_HelloWorldReady')  
DROP PROCEDURE usp_HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady')  
DROP ASSEMBLY HelloWorldReady;  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.neutral')  
DROP ASSEMBLY [HelloWorldReady.resources.neutral]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.de')  
DROP ASSEMBLY [HelloWorldReady.resources.de]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.es')  
DROP ASSEMBLY [HelloWorldReady.resources.es]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr')  
DROP ASSEMBLY [HelloWorldReady.resources.fr]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.fr-FR')  
DROP ASSEMBLY [HelloWorldReady.resources.fr-FR]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.it')  
DROP ASSEMBLY [HelloWorldReady.resources.it]  
GO  
  
IF EXISTS (SELECT * FROM sys.assemblies WHERE [name] = 'HelloWorldReady.resources.ja')  
DROP ASSEMBLY [HelloWorldReady.resources.ja]  
GO  
  
USE master;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [CLR &#40;共通言語ランタイム&#41; 統合の使用シナリオと例](../../../2014/database-engine/dev-guide/usage-scenarios-and-examples-for-common-language-runtime-clr-integration.md)  
  
  
