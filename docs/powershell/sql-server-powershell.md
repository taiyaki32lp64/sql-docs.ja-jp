---
title: SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7a2725586a094aed0cb7d933553bc3fc389adfdf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912211"
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

**[SQL Server PowerShell のインストール](download-sql-server-ps-module.md)**

> [!NOTE]
> SQL Server PowerShell モジュールには **SqlServer** と **SQLPS** の 2 つがあります。 **SQLPS** モジュールは (後方互換性のため) SQL Server のインストールに含まれていますが、今後更新されることはありません。 最新の PowerShell モジュールは **SqlServer** モジュールです。 **SqlServer** モジュールには **SQLPS** のコマンドレットの更新バージョンだけでなく、最新の SQL 機能をサポートする新しいコマンドレットも含まれています。  
> SQL Server Management Studio (SSMS) には前のバージョンの **SqlServer** が含まれて*いました*が、SSMS の 16.x バージョンのみです。 PowerShell を SSMS 17.0 以降で使用するには、**SqlServer** モジュールを PowerShell ギャラリーからインストールする必要があります。
> **SqlServer** モジュールをインストールする場合は、「[SQL Server PowerShell のインストール](download-sql-server-ps-module.md)」を参照してください。

**モジュールが SQLPS から SqlServer に変更された理由**

SQL PowerShell の更新プログラムを出荷するため、SQL PowerShell モジュールの ID だけでなく *SQLPS.exe* で知られるラッパーも変更する必要がありました。 この変更によって、SQL PowerShell モジュールが **SqlServer** モジュールと **SQLPS** モジュールの 2 つになりました。  

**SQLPS モジュールをインポートする場合は PowerShell スクリプトを更新します。**

`Import-Module -Name SQLPS` を実行する PowerShell スクリプトがあり、新しいプロバイダーの機能と新しいコマンドレットを活用したい場合は、これらを `Import-Module -Name SqlServer` に変更する必要があります。 新しいモジュールは `%ProgramFiles%\WindowsPowerShell\Modules\SqlServer` フォルダーにインストールされます。 したがって、$env:PSModulePath 変数を更新する必要はありません。 **SqlServer** という名前の、サード パーティ製またはコミュニティ バージョンのモジュールを使用するスクリプトがある場合は、名前の競合を避けるため Prefix パラメーターを使用してください。

SQL Server エージェントで使用されるモジュールの変更はありません。 そのため、型が PowerShell のジョブ ステップでは、SQLPS モジュールが使用されます。 詳細については、[SQL Server エージェントで PowerShell を実行する方法](run-windows-powershell-steps-in-sql-server-agent.md)に関する記事を参照してください。


## <a name="sql-server-powershell-components"></a>SQL Server PowerShell のコンポーネント  
**SqlServer** モジュールは、次の 2 つの Windows PowerShell スナップインを読み込みます。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダー。プロバイダーを使用すると、ファイル システム パスと同様の簡単なナビゲーション メカニズムを使用できます。 ファイル システム パスと同様に、ドライブが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 管理オブジェクト モデルに関連付けられ、ノードがオブジェクト モデルのクラスに基づくパスを構築できます。 その後、 **cd** や **dir** などのなじみのあるコマンドを使用して、コマンド プロンプト ウィンドウでフォルダーを操作するのと同様の方法でパスを操作できます。 **ren** や **del**などの他のコマンドを使用すると、パスのノードで操作を実行できます。  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] または XQuery ステートメントを含む **sqlcmd** コマンドレットを実行するなどの操作をサポートする、コマンドレットのセット。  
  
  
## <a name="sql-server-versions"></a>SQL Server のバージョン  
SQL PowerShell コマンドレットは Azure SQL Database、Azure SQL Data Warehouse、すべての[サポートされる SQL Server 製品](https://support.microsoft.com/lifecycle/search/1044)のインスタンスを管理するために使用できます。  


## <a name="sql-server-identifiers-that-contain-characters-not-supported-in-powershell-paths"></a>PowerShell パスではサポートされない文字を含んだ SQL Server 識別子  
 
**Encode-Sqlname** コマンドレットと **Decode-Sqlname** コマンドレットでは、PowerShell パスではサポートされていない文字を含んだ SQL Server 識別子を指定できます。 詳細については、「 [PowerShell での SQL Server 識別子](sql-server-identifiers-in-powershell.md)」を参照してください。  
  
**Convert-UrnToPath** コマンドレットを使用して、 [!INCLUDE[ssDE](../includes/ssde-md.md)] オブジェクトの Unique Resource Name を SQL Server PowerShell プロバイダーのパスに変換します。 詳細については、「 [URN から SQL Server プロバイダー パスへの変換](https://docs.microsoft.com/powershell/module/sqlserver/Convert-UrnToPath)」を参照してください。  
  
## <a name="query-expressions-and-unique-resource-names"></a>クエリ式および Unique Resource Name  

クエリ式は、オブジェクト モデル階層内の 1 つまたは複数のオブジェクトを列挙する条件のセットを指定するために XPath と同様の構文を使用する文字列です。 URN (Unique Resource Name) は、単一のオブジェクトを一意に識別する特定の種類のクエリ式文字列です。 詳細については、「 [クエリ式と Uniform Resource Name](query-expressions-and-uniform-resource-names.md)」を参照してください。       


## <a name="cmdlet-reference"></a>コマンドレット参照
* [SqlServer のコマンドレット](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS のコマンドレット](https://docs.microsoft.com/powershell/module/sqlps)
