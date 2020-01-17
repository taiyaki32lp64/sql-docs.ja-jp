---
title: Always Encrypted を使用したアプリケーションの開発 | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0dbf983f044118a5d59812f1183d0733b20cb449
ms.sourcegitcommit: a26cb217adfbbfb3636dff43fb19a46462e2e994
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2019
ms.locfileid: "74492012"
---
# <a name="develop-applications-using-always-encrypted"></a>Always Encrypted を使用したアプリケーションの開発
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

クライアント側の暗号化テクノロジ [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) により、機微なデータ (および関連する暗号化キー) が SQL Server や Azure SQL Database に開示されることはありません。 Always Encrypted では、クライアント ドライバーが、データベース エンジンにデータを渡す前に機微なデータを透過的に暗号化します。同様に、クライアント ドライバーは、暗号化されたデータベース列から取得したデータを透過的に暗号化解除します。

Always Encrypted の保護するデータベースを使用したアプリケーションの開発、および Always Encrypted をサポートするクライアント ドライバーとそのバージョンの詳細については、次を参照してください。

- [Always Encrypted と .NET Framework Data Provider for SQL Server を使用する](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [JDBC ドライバーで Always Encrypted を使用する](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [ODBC ドライバーで Always Encrypted を使用する](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [PHP ドライバーで Always Encrypted を使用する](../../../connect/php/using-always-encrypted-php-drivers.md)
- [.NET Core および .NET Framework アプリケーションの Microsoft .NET Data Provider for SQL Server で Always Encrypted を使用する](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md)
- [常に暗号化](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
