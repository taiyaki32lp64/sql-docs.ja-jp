---
title: SQL Server on Linux にデータベースを移行する
description: この記事では、SQL Server on Linux にデータベースとデータを移行するためのさまざまなオプションについて説明します。
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1619489d-377a-4f32-8930-d4f536539689
ms.openlocfilehash: e7affa88f1856571d0b2142f7dcfdf762ed79197
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/25/2019
ms.locfileid: "68129351"
---
# <a name="migrate-databases-and-structured-data-to-sql-server-on-linux"></a>データベースと構造化データを SQL Server on Linux に移行する 

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Linux 上で実行されている SQL Server にデータベースとデータを移行することができます。 使用する方法は、ソース データと具体的なシナリオによって異なります。 以下のセクションでは、さまざまな移行シナリオのベスト プラクティスについて説明します。

## <a name="migrate-from-sql-server-on-windows"></a>Windows 上の SQL Server から移行する
Windows 上の SQL Server データベースを SQL Server on Linux に移行する場合は、SQL Server のバックアップと復元を使用することをお勧めします。

1. Windows マシン上でデータベースのバックアップを作成します。
2. バックアップ ファイルをターゲット SQL Server Linux マシンに転送します。
3. Linux マシン上でバックアップを復元します。 

バックアップと復元を使用したデータベースの移行のチュートリアルについては、次のトピックを参照してください。

- [Windows から Linux へ SQL Server データベースを移行する](sql-server-linux-migrate-restore-database.md)

また、データベースを BACPAC ファイル (データベース スキーマとデータを含む圧縮ファイル) にエクスポートすることもできます。 BACPAC ファイルがある場合は、このファイルを Linux マシンに転送し、それを SQL Server にインポートすることができます。 詳細については、次の各トピックを参照してください。

- [SSMS または SqlPackage.exe を使用してデータベースをエクスポートおよびインポートする](sql-server-linux-migrate-ssms.md)

## <a name="migrate-from-other-database-servers"></a>他のデータベース サーバーから移行する
他のデータベース システム上のデータベースを SQL Server on Linux に移行することができます。 これには、Microsoft Access、DB2、MySQL、Oracle、Sybase の各データベースが含まれます。 このシナリオでは、SQL Server Management Assistant (SSMA) を使用して、SQL Server on Linux への移行を自動化します。 詳細については、「[SSMA を使用して SQL Server on Linux にデータベースを移行する](sql-server-linux-migrate-ssma.md)」を参照してください。  

## <a name="migrate-structured-data"></a>構造化データを移行する
生データをインポートする手法もあります。 他のデータベースまたはデータ ソースからエクスポートされた構造化データ ファイルを持っている場合があります。 このような場合は、bcp ツールを使用してデータを一括挿入できます。 また、Windows 上で SQL Server Integration Services を実行して、Linux 上の SQL Server データベースにデータをインポートすることもできます。 SQL Server Integration Services を使用すると、インポート時にデータに対してより複雑な変換を実行できます。 

これらの手法の詳細については、次のトピックを参照してください。

- [bcp を使用したデータの一括コピー](sql-server-linux-migrate-bcp.md)
- [SSIS を使用した SQL Server on Linux のデータの抽出、変換、読み込み](sql-server-linux-migrate-ssis.md) 
