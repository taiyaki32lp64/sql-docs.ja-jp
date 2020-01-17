---
title: SQL Server PowerShell モジュールのダウンロード | Microsoft Docs
ms.custom: ''
ms.date: 01/31/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
keywords:
- sql server powershell のインストール, sql server powershell のダウンロード
ms.assetid: ''
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 82daddf2589970c415a53ca756599ac892be1a35
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71713204"
---
# <a name="install-sql-server-powershell-module"></a>SQL Server PowerShell モジュールのインストール
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

この記事は、**SqlServer** PowerShell モジュールをインストールする手順を説明しています。
> [!NOTE]
> 2 つの SQL Server PowerShell モジュールがあります。 
> * **SQLPS**: このモジュールは (後方互換性のため) SQL Server のインストールに含まれていますが、今後更新されることはありません。 最新の PowerShell モジュールは **SqlServer** モジュールです。
> * **SqlServer**: このモジュールには、最新の SQL 機能をサポートする新しいコマンドレットが含まれています。 モジュールには、**SQLPS** 内のコマンドレットの更新バージョンも含まれています。 

SQL Server Management Studio (SSMS) には前のバージョンの **SqlServer** が含まれて*いました*が、SSMS の 16.x バージョンのみです。 PowerShell を SSMS 17.0 以降で使用するには、**SqlServer** モジュールを [PowerShell ギャラリー](https://www.powershellgallery.com/packages/Sqlserver)からインストールする必要があります。

モジュールのプレリリース版は、より頻繁に利用できるようになる可能性があります。モジュールのこのようなバージョンを取得する方法については、このページの下部のセクションを参照してください。

PowerShell ギャラリーから **SqlServer** モジュールをインストールするには、[PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting) セッションを開始し、次のコマンドを使用します。 インストールに問題が発生した場合は、[Install-module のドキュメント](https://www.powershellgallery.com/packages/PowerShellGet/2.2.1)と [Install-Module の参照](https://docs.microsoft.com/powershell/module/powershellget/Install-Module)をご覧ください。

**SqlServer** モジュールをインストールするには:

```Install-Module -Name SqlServer```

以前のバージョンの **SqlServer** モジュールがコンピューター上にある場合、`Update-Module` (この記事で後述) を使用できる、または `-AllowClobber` パラメーターを指定できる場合があります。  

```Install-Module -Name SqlServer -AllowClobber```

管理者として PowerShell セッションを実行できない場合は、次のようにして現在のユーザーにインストールできます。

```Install-Module -Name SqlServer -Scope CurrentUser```

**SqlServer** モジュールの更新バージョンがある場合、`Update-Module` を使用してバージョンを更新できます。

```Update-Module -Name SqlServer```

インストールされているモジュールのバージョンを表示する場合:

```Get-Module SqlServer -ListAvailable```

モジュールの特定のバージョンを使用するには、次のような特定のバージョン番号でインポートできます。

```Import-Module SqlServer -Version 21.1.18080```

> [!NOTE]
> モジュールのプレリリース ("プレビュー") バージョンは、PowerShell ギャラリーで入手できます。 [PowerShellGet](https://www.powershellgallery.com/packages/PowerShellGet) モジュール) の一部である、更新された *Find-Module* コマンドレットと *Install-Module* コマンドレットを使用して *-AllowPrerelease* スイッチを渡すことで、これらを検出してインストールできます。
>
> モジュールのプレリリース/プレビュー バージョンを検出するには、次のコマンドを実行できます。
>
> ```Find-Module SqlServer -AllowPrerelease```
>
> モジュールの特定のプレリリース/プレビュー バージョンをインストールするには、次のような特定のバージョン番号でインストールできます。
>
> ```Install-Module SqlServer -RequiredVersion 21.1.18040-preview -AllowPrerelease```
> 

PowerShell ギャラリーの **SqlServer** モジュールのバージョンは、バージョン管理をサポートし、PowerShell バージョン 5.0 以降が必要です。 

* [PowerShell ギャラリーの SqlServer モジュール](https://www.powershellgallery.com/packages/Sqlserver) 
* [SqlServer のコマンドレット](https://docs.microsoft.com/powershell/module/sqlserver)
* [SQLPS のコマンドレット](https://docs.microsoft.com/powershell/module/sqlps)
