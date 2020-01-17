---
title: 接続ライブラリとフレームワーク
description: クライアント アプリがさまざまな言語で使用できる接続ドライバーの一覧を示します。これらにより、オンプレミスまたはクラウドで、Linux、Windows、Docker 上で実行されている Microsoft SQL Server や、Azure SQL Database と Azure SQL Data Warehouse にも接続できます。
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.openlocfilehash: a4ed76cde2cd8ff8b9d862b981dcbed2361c6ae8
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049738"
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Microsoft SQL Server の接続ライブラリとフレームワーク

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[開始用のチュートリアル](https://aka.ms/sqldev)を参照すると、C#、Java、Node.js、PHP、Python などプログラミング言語を使用し、Linux、Windows、または macOS 上の Docker で SQL Server を使用するアプリの構築をすぐに始めることができます。

次の表に、クライアント アプリケーションがさまざまな言語から使用できる接続ライブラリすなわち "*ドライバー*" の一覧を示します。これらによって、オンプレミスまたはクラウドで、Linux、Windows、Docker 上で実行されている Microsoft SQL Server や、Azure SQL Database と Azure SQL Data Warehouse にも接続して使用できます。 

| [言語] | プラットフォーム | その他のリソース | ダウンロード | 開始するには |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows、Linux、macOS | [Microsoft ADO.NET for SQL Server](/sql/connect/ado-net/microsoft-ado-net-sql-server) | [ダウンロード](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [開始するには](https://www.microsoft.com/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows、Linux、macOS | [Microsoft SQL Server 用 JDBC Driver](https://msdn.microsoft.com/library/mt484311.aspx) | [ダウンロード](https://go.microsoft.com/fwlink/?LinkId=245496) |  [開始するには](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu)
| PHP (PHP) | Windows、Linux、macOS| [PHP SQL Driver for SQL Server](../connect/php/microsoft-php-driver-for-sql-server.md) | オペレーティング システム: <br/> \* [Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \* [Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \* [macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [開始するには](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows、Linux、macOS | [Node.js Driver for SQL Server](../connect/node-js/node-js-driver-for-sql-server.md) |  [開始するには](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu)
| Python | Windows、Linux、macOS | [Python SQL ドライバー](../connect/python/python-driver-for-sql-server.md) <br/> \* [pyodbc](https://msdn.microsoft.com/library/mt763257.aspx) |  [開始するには](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows、Linux、macOS | [Ruby Driver for SQL Server](../connect/ruby/ruby-driver-for-sql-server.md) | [開始するには](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows、Linux、macOS | [Microsoft ODBC Driver for SQL Server](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) | [ダウンロード](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) |  

次の表に、オブジェクト リレーショナル マッピング (ORM) フレームワークと Web フレームワークの一部の例を示します。クライアント アプリケーションは、オンプレミスまたはクラウドで、Linux、Windows、Docker 上で実行されている Microsoft SQL Server や、Azure SQL Database と Azure SQL Data Warehouse でも、これらを使用できます。 

| [言語] | プラットフォーム | ORM |
| :-- | :-- | :-- |
| C# | Windows、Linux、macOS | [Entity Framework](https://docs.microsoft.com/ef)<br>[Entity Framework Core](https://docs.microsoft.com/ef/core/index) |
| Java | Windows、Linux、macOS |[Hibernate ORM](https://hibernate.org/orm)|
| PHP (PHP) | Windows、Linux | [Laravel (Eloquent)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows、Linux、macOS | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | Windows、Linux、macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows、Linux、macOS | [Ruby on Rails](https://rubyonrails.org/) |

## <a name="related-links"></a>関連リンク
- クライアント アプリケーションから接続するための [SQL Server ドライバー](https://msdn.microsoft.com/library/mt654049.aspx)
