---
title: sqlps ユーティリティ | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqlps utility
- PowerShell [SQL Server], sqlps utility
ms.assetid: 4b2515a6-12c3-44fb-b263-1c567681cd2b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8ff96b99ee7982be89126e79687dbc8a2215f42f
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798137"
---
# <a name="sqlps-utility"></a>sqlps ユーティリティ
  `sqlps` ユーティリティは、Windows PowerShell 2.0 セッションを起動し、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell プロバイダーおよびコマンドレットの読み込みと登録を行います。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell コンポーネントを使用する PowerShell コマンドやスクリプトを入力して、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスとそのオブジェクトを操作できます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)]代わりに `sqlps` PowerShell モジュールを使用してください。 `sqlps` モジュールの詳細については、「 [SQLPS モジュールのインポート](../database-engine/import-the-sqlps-module.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
      sqlps   
[ [ [ -NoLogo ][ -NoExit ][ -NoProfile ]  
    [ -OutPutFormat { Text | XML } ] [ -InPutFormat { Text | XML } ]  
  ]  
  [ -Command { -  
             | script_block [ -argsargument_array ]  
             | string [ command_parameters ]  
             }  
  ]  
]  
[ -? | -Help ]  
```  
  
## <a name="arguments"></a>引数  
 **-NoLogo**  
 `sqlps` ユーティリティの起動時に著作権画面を表示しないように指定します。  
  
 **-NoExit**  
 スタートアップ コマンドの完了後に `sqlps` ユーティリティの実行を継続するように指定します。  
  
 **-NoProfile**  
 `sqlps` ユーティリティがユーザー プロファイルを読み込まないように指定します。 ユーザー プロファイルには、複数の PowerShell セッションで共通して使用する別名、関数、および変数が記録されます。  
  
 **-OutPutFormat** { **Text** | **XML** }  
 `sqlps` ユーティリティの出力を、テキスト文字列 (**テキスト**) またはシリアル化された export-clixml 形式 (**XML**) のいずれかとして書式設定することを指定します。  
  
 **-InPutFormat** { **Text** | **XML** }  
 `sqlps` ユーティリティへの入力が、テキスト文字列 (**テキスト**) またはシリアル化された export-clixml 形式 (**XML**) のいずれかとして書式設定されることを指定します。  
  
 **-Command**  
 `sqlps` ユーティリティで実行するコマンドを指定します。 **-NoExit**も指定されていない限り、`sqlps` ユーティリティはコマンドを実行してから終了します。 **-Command**の後にはその他のスイッチを指定しないでください。指定すると、コマンド パラメーターとして読み取られます。  
  
 **-**  
 **-Command-** `sqlps` ユーティリティが標準入力からの入力を読み取ることを指定します。  
  
 *script_block* [ **-args**_argument_array_ ]  
 実行する PowerShell コマンドのブロックを指定します。ブロックは中かっこ {} で囲む必要があります。 *Script_block*は、`sqlps` ユーティリティを**PowerShell**または別の `sqlps` ユーティリティセッションから呼び出すときにのみ指定できます。 *argument_array* は、 *script_block*内の PowerShell コマンドの引数を含む PowerShell 変数の配列です。  
  
 *string* [ *command_parameters* ]  
 実行する PowerShell コマンドを含む文字列を指定します。 **"& { *`command`* }"** という形式を使用します。 引用符は文字列を示し、invoke 演算子 (&) によって `sqlps` ユーティリティによってコマンドが実行されます。  
  
 [ **-?** |  **-Help** ]  
 `sqlps` ユーティリティ オプションの構文の概要を表示します。  
  
## <a name="remarks"></a>Remarks  
 `sqlps` ユーティリティは、PowerShell 環境 (PowerShell .exe) を起動し、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell モジュールを読み込みます。 モジュールは `sqlps`とも呼ばれ、これらの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell スナップインを読み込んで登録します。  
  
-   Microsoft.SqlServer.Management.PSProvider.dll  
  
     [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell プロバイダーおよび関連するコマンドレット ( **Encode-SqlName** や **Decode-SqlName**など) を実装します。  
  
-   Microsoft.SqlServer.Management.PSSnapin.dll  
  
     **Invoke-Sqlcmd** および **Invoke-PolicyEvaluation** コマンドレットを実装します。  
  
 `sqlps` ユーティリティを使用して、次の操作を行うことができます。  
  
-   PowerShell コマンドを対話的に実行する。  
  
-   PowerShell スクリプト ファイルを実行する。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] コマンドレットを実行する。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダー パスを使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オブジェクトの階層内を移動する。  
  
 既定では、`sqlps` ユーティリティは、スクリプト実行ポリシーが**制限付き**に設定された状態で実行されます。 これにより、PowerShell スクリプトの実行が防止されます。 **Set-ExecutionPolicy** コマンドレットを使用すると、署名されたスクリプトまたは任意のスクリプトの実行を有効にすることができます。 信頼できるソースからのスクリプト以外は実行しないでください。また、適切な NTFS 権限を使用して、すべての入力ファイルと出力ファイルのセキュリティを保護してください。 PowerShell スクリプトの有効化の詳細については、「 [Windows PowerShell スクリプトの実行](https://www.tech-recipes.com/rx/2513/powershell_enable_script_support/)」を参照してください。  
  
 `sqlps` および [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] に採用されていたバージョンの [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] ユーティリティは、Windows PowerShell 1.0 のミニシェルとして実装されていました。 ミニシェルには特定の制限があります。たとえば、ミニシェルによって読み込まれているスナップイン以外、ユーザーは読み込むことができません。 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 以降のバージョンのユーティリティは、`sqlps` モジュールを使用するように変更されており、このような制限は適用されません。  
  
## <a name="examples"></a>使用例  

### <a name="a-run-the-sqlps-utility-in-default-interactive-mode-without-the-copyright-banner"></a>A. 既定の対話モードで著作権画面を表示せずに sqlps ユーティリティを実行する
  
```cmd
sqlps -NoLogo  
```  
  
### <a name="b-run-a-sql-server-powershell-script-from-the-command-prompt"></a>b. コマンド プロンプトから SQL Server PowerShell スクリプトを実行する
  
```cmd
sqlps -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
### <a name="c-run-a-sql-server-powershell-script-from-the-command-prompt-and-keep-running-after-the-script-completes"></a>C. コマンド プロンプトから SQL Server PowerShell スクリプトを実行し、スクリプト完了後も実行を続ける
  
```cmd
sqlps -NoExit -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
## <a name="see-also"></a>参照  
 [サーバー ネットワーク プロトコルの有効化または無効化](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
