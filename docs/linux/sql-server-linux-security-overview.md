---
title: SQL Server on Linux に対するセキュリティの制限事項
description: この記事では、SQL Server on Linux の制限事項について説明します。
author: VanMSFT
ms.author: vanto
ms.date: 09/12/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.openlocfilehash: 8a9094977597fd7c2d76f2c80a1773c176b9c6dc
ms.sourcegitcommit: 77293fb1f303ccfd236db9c9041d2fb2f64bce42
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/12/2019
ms.locfileid: "70929807"
---
# <a name="security-limitations-for-sql-server-on-linux"></a>SQL Server on Linux に対するセキュリティの制限事項

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

現在、SQL Server on Linux には、次の制限があります。

* 標準パスワード ポリシーが用意されています。 構成できる唯一のオプションは MUST_CHANGE です。 CHECK_POLICY オプションはサポートされていません。
* 拡張キー管理はサポートされていません。 
* Azure キー コンテナーに格納されているキーの使用はサポートされていません。
* SQL Server では、接続の暗号化で独自の自己署名証明書が生成されます。 ユーザーが提供した TLS 証明書を使用するように SQL Server を構成できます。 

SQL Server で使用できるセキュリティ機能の詳細については、「[SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)」を参照してください。

## <a name="next-steps"></a>次の手順

一般的なセキュリティ タスクについては、[SQL Server on Linux のセキュリティ機能の概要](sql-server-linux-security-get-started.md)に関する記事を参照してください。 TCP ポート番号または SQL Server ディレクトリの変更と、トレース フラグまたは照合順序の構成を行うスクリプトについては、「[mssql-conf を使用して SQL Server on Linux を構成する](sql-server-linux-configure-mssql-conf.md)」を参照してください。
