---
title: PowerShell の拡張機能
titleSuffix: Azure Data Studio
description: Azure Data Studio 用に PowerShell をインストールして使用する
ms.custom: seodec18
ms.date: 04/19/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
manager: matthend
ms.openlocfilehash: 72c4d64cc93ab564b9b8b04a838f8226982890f0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257586"
---
# <a name="powershell-editor-support-for-azure-data-studio"></a>PowerShell エディターによる Azure Data Studio のサポート

この拡張機能で、[Azure Data Studio](https://github.com/Microsoft/azuredatastudio) に高機能な PowerShell エディターのサポートが提供されます。
Azure Data Studio が提供する、優れた IDE に似たインターフェイスを使用して PowerShell スクリプトを作成およびデバッグできるようになります。

![PowerShell の拡張機能](media/powershell-extension/powershell-extension.png)


## <a name="features"></a>[機能]

- 構文の強調表示
- コード スニペット
- コマンドレットなどの IntelliSense
- [PowerShell Script Analyzer](http://github.com/PowerShell/PSScriptAnalyzer) で提供されるルールベースの分析
- コマンドレットと変数の定義に進む
- コマンドレットと変数のリファレンスを探す
- ドキュメントとワークスペースのシンボル検出
- <kbd>F8</kbd> キーを使用して選択した PowerShell コードの選択を実行する
- <kbd>Ctrl</kbd>+<kbd>F1</kbd> キーを使用してカーソルの下にあるシンボルのオンライン ヘルプを起動する
- 基本的な対話型コンソールのサポート


## <a name="installing-the-extension"></a>拡張機能のインストール

PowerShell の拡張機能の公式リリースをインストールするには、[Azure Data Studio のドキュメント](https://docs.microsoft.com/sql/azure-data-studio/extensions)の手順に従います。
[機能拡張] ウィンドウで「PowerShell」の拡張機能を検索し、そこでインストールします。  今後、拡張機能の更新があれば、自動的に通知されます。

[リリース ページ](https://github.com/PowerShell/vscode-powershell/releases)から VSIX パッケージをインストールし、コマンド ラインからインストールすることもできます。

```powershell
azuredatastudio --install-extension PowerShell-<version>.vsix
```

## <a name="platform-support"></a>プラットフォームのサポート

- Windows PowerShell v3 以降、および PowerShell Core がインストールされた **Windows 7 から 10**
- PowerShell Core がインストールされた **Linux** (PowerShell がサポートされているすべてのディストリビューション)
- PowerShell Core がインストールされた **macOS**

よく寄せられる質問の回答については、「[FAQ](https://github.com/PowerShell/vscode-powershell/wiki/FAQ)」を参照してください。

## <a name="installing-powershell-core"></a>PowerShell Core のインストール

macOS または Linux 上で Azure Data Studio を実行している場合は、必要に応じて PowerShell Core もインストールします。

PowerShell Core は [GitHub](https://github.com/powershell/powershell) のオープン ソース プロジェクトです。
PowerShell Core を macOS または Linux プラットフォームにインストールする方法について詳細については、次の記事を参照してください。

- [Linux に PowerShell Core をインストールする](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [macOS に PowerShell Core をインストールする](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)

## <a name="example-scripts"></a>スクリプトの例

拡張機能の `examples` フォルダーには、PowerShell の編集およびデバッグ機能を確認するために使用できるスクリプトの例がいくつかあります。  これらの使用方法の詳細については、付属の [README.md](https://github.com/PowerShell/vscode-powershell/blob/master/examples/README.md) ファイルを参照してください。

このフォルダーは次のパスにあります。

```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.PowerShell-<version>/examples
```

または、プレビュー バージョンの拡張機能を使用している場合

 ```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.powershell-preview-<version>/examples
```

Azure Data Studio で拡張機能の例を開いたり表示したりするには、PowerShell コマンド プロンプトから次のコードを実行します。

```powershell
azuredatastudio (Get-ChildItem $Home\.azuredatastudio\extensions\ms-vscode.PowerShell-*\examples)[-1]
```

### <a name="creating-and-opening-files"></a>ファイルを作成して開く

エディター内で新しいファイルを作成して開くには、PowerShell 統合ターミナル内から New-EditorFile を使用します。

```powershell
PS C:\temp> New-EditorFile ExportData.ps1
```

このコマンドは、PowerShell ファイルだけでなく、あらゆるファイルの種類に使用できます。

```powershell
PS C:\temp> New-EditorFile ImportData.py
```

Azure Data Studio で 1 つ以上のファイルを開くには、`Open-EditorFile` コマンドを使用します。

```powershell
Open-EditorFile ExportData.ps1, ImportData.py
```

### <a name="no-focus-on-console-when-executing"></a>実行時にコンソールにフォーカスなし

SSMS での作業に慣れているユーザーの場合、クエリを実行できること、そしてクエリ ウィンドウに切り替えることなくクエリを再実行できることに慣れています。  このような場合、コード エディターの既定の動作は奇妙に感じられるかもしれません。  <kbd>F8</kbd> キーを押して実行するときにエディターのフォーカスを維持するには、次の設定を変更します。

```json
"powershell.integratedConsole.focusConsoleOnExecute": false
```

アクセシビリティのため、既定値は `true` です。

`Get-Credential` のように明示的に入力を要求するコマンドを使用した場合でも、この設定によってフォーカスがコンソールに変更されなくなることに注意してください。

## <a name="sql-powershell-examples"></a>SQL PowerShell の例
これらの (以下の) 例を使用するには、[PowerShell ギャラリー](https://www.powershellgallery.com/packages/SqlServer)から SqlServer モジュールをインストールする必要があります。

```powershell
Install-Module -Name SqlServer
```

> [!NOTE]
> バージョン `21.1.18102` 以降では、`SqlServer` モジュールは Windows PowerShell に加えて [PowerShell Core](https://github.com/PowerShell/PowerShell) 6.2 以降をサポートします。

この例では、`Get-SqlInstance` コマンドレットを使用して ServerA と ServerB のサーバー SMO オブジェクトを取得します。  このコマンドの既定に出力には、インスタンスのインスタンス名、バージョン、サービス パック、および CU の更新レベルが含まれます。

```powershell
Get-SqlInstance -ServerInstance ServerA, ServerB
```

出力例は次のようになります。

```
Instance Name             Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------             -------    ------------ -----------  ------------ ----------------
ServerA                   13.0.5233  SP2          CU4          Windows      Windows Server 2016 Datacenter
ServerB                   14.0.3045  RTM          CU12         Linux        Ubuntu
```
`SqlServer` モジュールには `SQLRegistration` というプロバイダーが含まれています。これを使用すると、次の種類の保存済み SQL Server 接続にプログラムでアクセスできます。

+ データベース エンジン サーバー (登録済みサーバー)
+ 中央管理サーバー (CMS)
+ Analysis Services
+ Integration Services
+ Reporting Services

 次の例では、登録済みサーバー ファイルに記載されているすべての SQL Server インスタンスの一覧を取得するために `dir` (`Get-ChildItem` のエイリアス) を実行します。

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse 
```

出力例は次のようになります。

```powershell
Mode Name
---- ----
-    ServerA
-    ServerB
-    localhost\SQL2017
-    localhost\SQL2016Happy
-    localhost\SQL2017
```

データベースが関係するさまざまな操作に対して、あるいはデータベース内のオブジェクトに対して `Get-SqlDatabase` コマンドレットを使用できます。  `-ServerInstance` パラメーターと `-Database` パラメーターの両方に値を提供する場合、その 1 つのデータベース オブジェクトだけが取得されます。  ただし、`-ServerInstance` パラメーターのみを指定した場合、そのインスタンス上のすべてのデータベースの完全な一覧が返されます。

出力例は次のようになります。

```
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2017   Normal      336.00 MB   57.01 MB Simple       140 sa
master               Normal        6.00 MB  368.00 KB Simple       140 sa
model                Normal       16.00 MB    5.53 MB Full         140 sa
msdb                 Normal       48.44 MB    1.70 MB Simple       140 sa
PBIRS                Normal      144.00 MB   55.95 MB Full         140 sa
PBIRSTempDB          Normal       16.00 MB    4.20 MB Simple       140 sa
SSISDB               Normal      325.06 MB   26.21 MB Full         140 sa
tempdb               Normal       72.00 MB   61.25 MB Simple       140 sa
WideWorldImporters   Normal         3.2 GB     2.6 GB Simple       130 sa
```

次の例では、`Get-SqlDatabase` コマンドレットを使用して ServerB インスタンス上のすべてのデータベースの一覧を取得し、(`Out-GridView` コマンドレットを使用して) グリッド/テーブルを表示して、バックアップするデータベースを選択します。  ユーザーが [OK] ボタンをクリックすると、強調表示されたデータベースのみがバックアップされます。

```powershell
Get-SqlDatabase -ServerInstance ServerB |
Out-GridView -PassThru |
Backup-SqlDatabase -CompressionOption On
```

この例でも、Registered Servers ファイルに記載されているすべての SQL Server インスタンスの一覧を取得し、記載されている各 SQL Server インスタンスについて、午前 0 時以降に失敗したすべての SQL エージェント ジョブを報告する `Get-SqlAgentJobHistory` を呼び出します。

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE {$_.Mode -ne 'd' } |
FOREACH {
    Get-SqlAgentJobHistory -ServerInstance  $_.Name -Since Midnight -OutcomesType Failed
}
```

この例では、`dir` (`Get-ChildItem` のエイリアス) を実行して Registered Servers ファイルに記載されているすべての SQL Server インスタンスの一覧を取得してから、`Get-SqlDatabase` コマンドレットを使用してそれらの各インスタンスについてデータベースの一覧を取得します。

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE { $_.Mode -ne 'd' } |
FOREACH {
    Get-SqlDatabase -ServerInstance $_.Name
}
```

出力例は次のようになります。

```
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level      
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2017   Normal      336.00 MB   57.01 MB Simple       140 sa   
master               Normal        6.00 MB  368.00 KB Simple       140 sa   
model                Normal       16.00 MB    5.53 MB Full         140 sa   
msdb                 Normal       48.44 MB    1.70 MB Simple       140 sa   
PBIRS                Normal      144.00 MB   55.95 MB Full         140 sa   
PBIRSTempDB          Normal       16.00 MB    4.20 MB Simple       140 sa   
SSISDB               Normal      325.06 MB   26.21 MB Full         140 sa   
tempdb               Normal       72.00 MB   61.25 MB Simple       140 sa   
WideWorldImporters   Normal         3.2 GB     2.6 GB Simple       130 sa   
```

## <a name="reporting-problems"></a>問題の報告

PowerShell 拡張機能に関する問題が発生した場合は、問題の診断と報告の詳細については[トラブルシューティングのドキュメント](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md)を参照してください。

#### <a name="security-note"></a>セキュリティに関する注意

セキュリティの問題については、[こちら](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md#note-on-security)を参照してください。

## <a name="contributing-to-the-code"></a>コードへの貢献

この拡張機能に貢献する方法の詳細については、[開発ドキュメント](https://github.com/PowerShell/vscode-powershell/blob/master/docs/development.md)を参照してください。

## <a name="maintainers"></a>保守担当者

- [Keith Hill](https://github.com/rkeithhill) - [@r_keith_hill](http://twitter.com/r_keith_hill)
- [Tyler Leonhardt](https://github.com/tylerl0706) - [@TylerLeonhardt](http://twitter.com/tylerleonhardt)
- [Rob Holt](https://github.com/rjmholt)

## <a name="license"></a>ライセンス

この拡張機能は [MIT ライセンスに従ってライセンスが付与](https://github.com/PowerShell/vscode-powershell/blob/master/LICENSE.txt)されます。 このプロジェクトのリリースに含まれているサードパーティ製バイナリの詳細については、[サードパーティに関する通知](https://github.com/PowerShell/vscode-powershell/blob/master/Third%20Party%20Notices.txt)のファイルを参照してください。

## <a name="code-of-conductconduct-md"></a>[倫理規定][conduct-md]

このプロジェクトは、「[Microsoft のオープン ソースの倫理規定][conduct-code]」を採用しています。
詳細については、[倫理規定の FAQ][conduct-FAQ] のページを参照してください。また、追加の質問やコメントがある場合は [opencode@microsoft.com][conduct-email] にお問い合わせください。

[conduct-code]: https://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: https://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
