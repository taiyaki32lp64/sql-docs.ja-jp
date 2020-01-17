---
title: Invoke-Sqlcmd コマンドレット | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], Invoke-Sqlcmd
- Cmdlets [SQL Server], Invoke-Sqlcmd
- Invoke-Sqlcmd cmdlet
- sqlcmd utility, PowerShell
ms.assetid: 0c74d21b-84a5-4fa4-be51-90f0f7230044
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c6aff97c8bee8fe8ccc469c2ee57bc94466e1e31
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797856"
---
# <a name="invoke-sqlcmd-cmdlet"></a>Invoke-Sqlcmd コマンドレット
  **Invoke-Sqlcmd** は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コマンドレットであり、言語 ([!INCLUDE[tsql](../includes/tsql-md.md)] と XQuery) のステートメントと **sqlcmd** ユーティリティでサポートされているコマンドを含んだスクリプトを実行します。  
  
## <a name="using-invoke-sqlcmd"></a>Invoke-Sqlcmd の使用  
 **Invoke-Sqlcmd** コマンドレットを使用すると、Windows PowerShell 環境で **sqlcmd** スクリプト ファイルを実行できます。 **sqlcmd** で実行できる処理の多くは、 **Invoke-Sqlcmd**を使用しても実行できます。  
  
 次の例では、Invoke-Sqlcmd を呼び出して単純なクエリを実行しています。これは、 **sqlcmd** で **-Q** および **-S** オプションを指定する場合と同様です。  
  
```powershell
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance"  
```  
  
 次の例では、 **Invoke-Sqlcmd**を呼び出し、入力ファイルを指定して、出力をファイルにパイプしています。これは、 **sqlcmd** に **-i** および **-o** オプションを指定する場合と同様です。  
  
```powershell
Invoke-Sqlcmd -InputFile "C:\MyFolder\TestSQLCmd.sql" | Out-File -FilePath "C:\MyFolder\TestSQLCmd.rpt"  
```  
  
 次の例では、Windows PowerShell 配列を使用して複数の **sqlcmd** スクリプト変数を **Invoke-Sqlcmd**に渡しています。 SELECT ステートメントで **sqlcmd** スクリプト変数を識別する "$" 文字をエスケープするために、PowerShell のバック ティック "`" エスケープ文字が使用されています。  
  
```powershell
$MyArray = "MyVar1 = 'String1'", "MyVar2 = 'String2'"  
Invoke-Sqlcmd -Query "SELECT `$(MyVar1) AS Var1, `$(MyVar2) AS Var2;" -Variable $MyArray  
```  
  
 次の例では、Windows PowerShell 用の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダーを使用して [!INCLUDE[ssDE](../includes/ssde-md.md)]のインスタンスに移動した後に、Windows PowerShell の **Get-Item** コマンドレットを使用してそのインスタンスの SMO サーバー オブジェクトを取得し、 **Invoke-Sqlcmd**に渡しています。  
  
```powershell
Set-Location SQLSERVER:\SQL\MyComputer\MyInstance  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance (Get-Item .)  
```  
  
 -Query パラメーターは位置で指定するパラメーターであり、名前を指定する必要はありません。 **Invoke-Sqlcmd**に渡された最初の文字列に名前が付いていない場合、その文字列は -Query パラメーターとして扱われます。  
  
```powershell
Invoke-Sqlcmd "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance"  
```  
  
## <a name="path-context-in-invoke-sqlcmd"></a>Invoke-Sqlcmd のパス コンテキスト  
 -Database パラメーターを使用しない場合、Invoke-Sqlcmd のデータベース コンテキストは、コマンドレットが呼び出されたときにアクティブなパスによって設定されます。  
  
|パス|データベース コンテキスト|  
|----------|----------------------|  
|SQLSERVER: 以外のドライブで始まります。|ローカル コンピューター上の既定のインスタンスのログイン ID の既定のデータベースです。|  
|SQLSERVER:\SQL|ローカル コンピューター上の既定のインスタンスのログイン ID の既定のデータベースです。|  
|SQLSERVER:\SQL\ComputerName|指定したコンピューター上の既定のインスタンスのログイン ID の既定のデータベースです。|  
|SQLSERVER:\SQL\ComputerName\InstanceName|指定したコンピューター上の指定したインスタンスのログイン ID の既定のデータベースです。|  
|SQLSERVER:\SQL\ComputerName\InstanceName\Databases|指定したコンピューター上の指定したインスタンスのログイン ID の既定のデータベースです。|  
|SQLSERVER:\SQL\ComputerName\InstanceName\Databases\DatabaseName|指定したコンピューター上の指定したインスタンスの指定したデータベースです。 これは、より長いパス (たとえばデータベース内の Tables ノードや Columns ノードを指定するパス) にも適用されます。|  
  
 たとえば、ローカル コンピューターの既定のインスタンスの Windows アカウントの既定のデータベースが master であるとします。 次のコマンドを実行すると、master が返されます。  
  
```powershell
Set-Location SQLSERVER:\SQL  
Invoke-Sqlcmd "SELECT DB_NAME() AS DatabaseName;"  
```  
  
 次のコマンドを実行すると、 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]が返されます。  
  
```powershell
Set-Location SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Person  
Invoke-Sqlcmd "SELECT DB_NAME() AS DatabaseName;"  
```  
  
 Invoke-Sqlcmd は、パス データベース コンテキストを使用するときに警告を表示します。 -SuppressProviderContextWarning パラメーターを使用すると、警告メッセージが出力されないようにすることができます。 -IgnoreProviderContext パラメーターを使用すると、Invoke-Sqlcmd を実行するときに常にログインの既定のデータベースが使用されます。  
  
## <a name="comparing-invoke-sqlcmd-and-the-sqlcmd-utility"></a>Invoke-Sqlcmd と sqlcmd ユーティリティの比較  
 **Invoke-Sqlcmd** では、 **sqlcmd** ユーティリティを使用して実行できるスクリプトの多くを実行できます。 ただし、 **Invoke-Sqlcmd** が実行される Windows PowerShell 環境は、 **sqlcmd** が実行されるコマンド プロンプト環境とは異なります。 **Invoke-Sqlcmd** の動作は、Windows PowerShell 環境で機能するように変更されています。  
  
 すべての **sqlcmd** コマンドが **Invoke-Sqlcmd**で実装されるわけではありません。 実装されないコマンドには、 **:!!** 、 **:connect**、 **:error**、 **:out**、 **:ed**、 **:list**、 **:listvar**、 **:reset**、 **:perftrace**、 **:serverlist**があります。  
  
 **Invoke-Sqlcmd** では **sqlcmd** 環境または SQLCMDDBNAME や SQLCMDWORKSTATION などのスクリプト変数が初期化されません。  
  
 **Invoke-Sqlcmd** では、Windows PowerShell の **-Verbose** 共通パラメーターを指定しない限り、PRINT ステートメントの出力などのメッセージが表示されません。 例 :  
  
```powershell
Invoke-Sqlcmd -Query "PRINT N'abc';" -Verbose  
```  
  
 **sqlcmd** のすべてのパラメーターが PowerShell 環境で必要となるわけではありません。 たとえば、Windows PowerShell ではコマンドレットからのすべての出力の書式が自動的に設定されるため、書式設定オプションを指定する **sqlcmd** のパラメーターは **Invoke-Sqlcmd**には実装されていません。 **Invoke-Sqlcmd** のパラメーターと **sqlcmd** のオプションの関係を次の表に示します。  
  
|[説明]|sqlcmd オプション|Invoke-Sqlcmd パラメーター|  
|-----------------|-------------------|------------------------------|  
|サーバーとインスタンスの名前|-S|-ServerInstance|  
|使用する初期データベース|-d|-Database|  
|指定したクエリの実行と終了|-Q|-Query|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証ログイン ID|-U|-Username|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 認証パスワード|-p|-Password|  
|変数の定義|-v|-Variable|  
|クエリのタイムアウト間隔|-t|-QueryTimeout|  
|エラー発生時の実行停止|-b|-AbortOnError|  
|専用管理者接続|-a|-DedicatedAdministratorConnection|  
|対話型コマンド、スタートアップ スクリプト、および環境変数の無効化|-x|-DisableCommands|  
|変数の代入の無効化|-x|-DisableVariables|  
|レポートする最小重大度レベル|-v|-SeverityLevel|  
|レポートする最小エラー レベル|-m|-ErrorLevel|  
|ログインのタイムアウト間隔|-l|-ConnectionTimeout|  
|ホスト名|-h|-HostName|  
|パスワードの変更と終了|-Z|-NewPassword|  
|クエリが含まれている入力ファイル|-i|-InputFile|  
|文字出力の最大長|-w|-MaxCharLength|  
|バイナリ出力の最大長|-w|-MaxBinaryLength|  
|SSL 暗号化を使用した接続|パラメーターなし|-EncryptConnection|  
|エラーの表示|パラメーターなし|-OutputSqlErrors|  
|stderr へのメッセージの出力|-r|パラメーターなし|  
|クライアントの地域別設定の使用|-r|パラメーターなし|  
|指定したクエリの実行と実行の継続|-q|パラメーターなし|  
|出力データに使用するコード ページ|-f|パラメーターなし|  
|パスワードの変更と実行の継続|-Z|パラメーターなし|  
|パケット サイズ|-a|パラメーターなし|  
|列の区切り|-s|パラメーターなし|  
|出力ヘッダーの制御|-H|パラメーターなし|  
|制御文字の指定|-k|パラメーターなし|  
|固定長表示幅|-Y|パラメーターなし|  
|可変長表示幅|-Y|パラメーターなし|  
|入力のエコー|-e|パラメーターなし|  
|引用符で囲まれた識別子の有効化|-I|パラメーターなし|  
|末尾のスペースの削除|-W|パラメーターなし|  
|インスタンスの一覧表示|-L|パラメーターなし|  
|出力の形式を Unicode に設定|-u|パラメーターなし|  
|統計情報の印刷|-p|パラメーターなし|  
|コマンドの終了|-c|パラメーターなし|  
|Windows 認証を使用した接続|-E|パラメーターなし|  
  
## <a name="see-also"></a>参照  
 [データベース エンジン コマンドレットの使用](../../2014/database-engine/use-the-database-engine-cmdlets.md)   
 [sqlcmd ユーティリティ](../tools/sqlcmd-utility.md)   
 [sqlcmd ユーティリティの使用](../relational-databases/scripting/sqlcmd-use-the-utility.md)  
