---
title: SQL Server on Linux の管理
description: この記事では、Linux で実行されている SQL Server の一般的な管理タスクとツールへのリンクを提供します。
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 6bd8eb0b-593d-467e-87ea-ab1c4dbcd1ea
ms.openlocfilehash: e38e51eb1db6c335175b2fc55636532df88ac27d
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68000057"
---
# <a name="choose-the-right-tool-to-manage-sql-server-on-linux"></a>SQL Server on Linux を管理するための適切なツールの選択

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server on Linux を管理するには、いくつかの方法があります。 以下のセクションでは、各種管理ツールについて概説すると共に、他の資料へのリンクを示します。

## <a name="mssql-conf"></a>mssql-conf 

**mssql-conf** ツールでは、SQL Server on Linux の構成を行うことができます。 詳しくは、「[mssql-conf ツールを利用して Linux 上で SQL Server を構成する](sql-server-linux-configure-mssql-conf.md)」をご覧ください。

## <a name="transact-sql"></a>Transact-SQL

クライアント ツールで実行できる処理はほぼすべて、Transact-SQL ステートメントを使用しても行うことができます。 SQL Server には、SQL Server の状態と構成を照会する[動的管理ビュー (DMV)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) が用意されています。 また、データベース管理タスク用の [Transact-SQL コマンド](../t-sql/language-reference.md)もあります。 これらのコマンドは、SQL Server への接続と Transact-SQL クエリの実行をサポートする任意のクライアント ツール ([sqlcmd](sql-server-linux-setup-tools.md) や [Visual Studio Code](sql-server-linux-develop-use-vscode.md) など) で実行できます。

## <a name="azure-data-studio"></a>Azure Data Studio

新しい Azure Data Studio は、SQL Server を管理するためのクロスプラットフォーム ツールです。 詳細については、[Azure Data Studio](../azure-data-studio/what-is.md) に関するページを参照してください。

## <a name="sql-server-management-studio-on-windows"></a>Windows 上の SQL Server Management Studio

SQL Server Management Studio (SSMS) は、SQL Server を管理するためのグラフィカル ユーザー インターフェイスを提供する Windows アプリケーションです。 現在、Windows でのみ実行できますが、Linux SQL Server インスタンスにリモート接続するために使用できます。 SSMS を使用した SQL Server の管理の詳細については、「[SSMS を使用して SQL Server on Linux を管理する](sql-server-linux-manage-ssms.md)」を参照してください。

## <a name="mssql-cli-preview"></a>mssql-cli (プレビュー)

Microsoft は、SQL Server 用の新しいクロスプラットフォーム スクリプト ツール、[mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/) をリリースしました。 このツールは現在プレビュー段階です。

## <a name="powershell"></a>PowerShell

PowerShell には、SQL Server on Linux を管理するための高機能なコマンドライン環境が用意されています。 詳細については、[PowerShell を使用した SQL Server on Linux の管理](sql-server-linux-manage-powershell.md)に関するページを参照してください。

## <a name="next-steps"></a>次の手順

SQL Server on Linux について詳しくは、「[SQL Server on Linux](sql-server-linux-overview.md)」をご覧ください。
