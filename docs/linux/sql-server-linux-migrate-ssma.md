---
title: SSMA:Linux 上の SQL Server への移行を自動化する
description: SQL Server Migration Assistant (SSMA) を使用し、Microsoft Access、DB2、MySQL、Oracle、Sybase から Linux 上の SQL Server へのデータベースの移行を自動化します。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 251bc3af-ebce-4d97-adec-afc0e7fab6cc
ms.openlocfilehash: 86e56d998959b4cc425626de249d66597262b50a
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558422"
---
# <a name="automate-database-migration-to-linux-with-the-sql-server-migration-assistant-ssma"></a>SQL Server Migration Assistant (SSMA) を使用して Linux へのデータベースの移行を自動化する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Microsoft Access、DB2、MySQL、Oracle、Sybase から SQL Server on Linux にデータベースを簡単に移行できる [SQL Server Migration Assistant (SSMA)](https://msdn.microsoft.com/library/mt613434.aspx) を紹介します。 SSMA は Windows アプリケーションです。Linux 上のリモート SQL Server インスタンスに接続できる Windows マシンがある場合は SSMA を使用してください。 

SSMA は、Oracle、MySQL、Sybase、DB2、Microsoft Access などのさまざまなソース データベースの SQL Server on Linux への移行をサポートし、次のような移行タスクを自動化するために役立ちます。

- ソース データベースを評価する
- ソース データベース スキーマを Microsoft SQL Server スキーマに変換する
- スキーマを移行する
- データを移行する
- 移行をテストする

まず、次の一覧からソース データベースに適した SQL Server Migration Assistant (SSMA) をダウンロードします。
- [SSMA for Access](https://aka.ms/ssmaforaccess)
- [SSMA for DB2](https://aka.ms/ssmafordb2)
- [SSMA for MySql](https://aka.ms/ssmaformysql) 
- [SSMA for Oracle](https://aka.ms/ssmafororacle)
- [SSMA for Sybase ASE](https://aka.ms/ssmaforsybase) 

次に、[SQL Server Migration Assistant (SSMA)](https://msdn.microsoft.com/library/mt613434.aspx) に従って、ソース データベースを SQL Server on Linux に移行します。

## <a name="see-also"></a>参照
- [Microsoft Data Migration ブログ](https://blogs.msdn.microsoft.com/datamigration)
- [SQL Server Migration Assistant (SSMA) ブログ](https://blogs.msdn.microsoft.com/ssma/)

