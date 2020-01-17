---
title: データソースのプロパティを設定する |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f3363d05-07fc-4bf8-ae5e-2a7a968808ad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0b3093b87557917655fcbfd6cf7c2ec37151ca44
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027735"
---
# <a name="setting-the-data-source-properties"></a>データ ソースのプロパティの設定

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

データ ソースは、Java Platform, Enterprise Edition (Java EE) 環境で JDBC 接続を作成するために推奨される機構です。 データ ソースは、接続、プールされた接続、および分散接続を提供します。このとき、Java コードに接続プロパティをハード コーディングする必要がありません。 すべての [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] のデータ ソースは、適切な setter メソッドと getter メソッドを使用して、任意のプロパティの値を設定または取得できます。

アプリケーション サーバーやサーブレット/JSP エンジンなどの Java EE 製品では、通常、データベース アクセス用にデータ ソースを構成できます。 構成で "プロパティ=値" ペアとしてプロパティを入力できる場合は、「[接続プロパティの設定](../../connect/jdbc/setting-the-connection-properties.md)」に記載されているすべてのプロパティを指定できます。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデータ ソースの詳細については、「[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) クラス」を参照してください。 SQLServerDataSource クラスを使用して[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースに接続する方法の例については、「[データソースのサンプル](../../connect/jdbc/data-source-sample.md)」を参照してください。

## <a name="see-also"></a>参照

[JDBC ドライバーによる SQL Server への接続](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)
