---
title: Microsoft SQL Server 用 JDBC Driver のダウンロード
description: SQL Server に接続する Java アプリケーションを開発するには、Microsoft JDBC Driver for SQL Server をダウンロードします。
ms.date: 09/30/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 451181b8-11e6-4d01-b547-9ac5aada8238
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc273bccf054408f48e7bb2bd0409a31bb18bd18
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71682008"
---
# <a name="download-microsoft-jdbc-driver-for-sql-server"></a>Microsoft SQL Server 用 JDBC Driver のダウンロード

この記事では、Microsoft JDBC Driver for SQL Server のダウンロードリンクを提供します。 このドライバーを使用すると、SQL Server に接続する Java アプリケーションを開発できます。  

## <a name="available-downloads-of-jdbc-driver-for-sql-server"></a>JDBC Driver for SQL Server の利用可能なダウンロード

次の表のリンクを使用して、Java Runtime Environment (JRE) に一致する最新の Microsoft JDBC Driver for SQL Server をダウンロードします。

| Version | リリース日 | Java のバージョン |
|---|---|---|
| [Microsoft JDBC Driver 7.4](https://go.microsoft.com/fwlink/?linkid=2099962) | 8/1/2019 | JRE 8、11、12 |
| [Microsoft JDBC Driver 7.2](https://go.microsoft.com/fwlink/?linkid=2063159) | 4/17/2019 | JRE 8、11 |
| [Microsoft JDBC Driver 7.0](https://go.microsoft.com/fwlink/?linkid=2005972) | 7/31/2018 | JRE 8、10 |
| [Microsoft JDBC Driver 6.4](https://go.microsoft.com/fwlink/?linkid=868290)  | 3/26/2018 | JRE 7、8、9 |
| [Microsoft JDBC Driver 6.2](https://go.microsoft.com/fwlink/?linkid=852460) | 2/12/2018 | JRE 7、8 |
| [Microsoft JDBC Driver 6.0](https://go.microsoft.com/fwlink/?LinkId=245496) | 2/27/2018 | JRE 7、8 |
| [Microsoft JDBC Driver 4.2](https://go.microsoft.com/fwlink/?linkid=841534) | 2/26/2018 | JRE 7、8 |
| [Microsoft JDBC Driver 4.1](https://go.microsoft.com/fwlink/?linkid=841533) | 2/27/2018 | JRE 7 |

ドライバーをダウンロードするときに、複数の JAR ファイルがあります。 JAR ファイルの名前は、サポートされている Java のバージョンを示します。 各リリースの詳細については、「[リリースノート](release-notes-for-the-jdbc-driver.md)と[システム要件](system-requirements-for-the-jdbc-driver.md)」を参照してください。

## <a name="using-the-jdbc-driver-with-maven-central"></a>JDBC ドライバーと Maven Central の使用

JDBC ドライバーを Maven プロジェクトに追加するには、次のコードを使って POM.xml ファイルに依存関係としてこれを追加します。

```xml
<dependency>
    <groupId>com.microsoft.sqlserver</groupId>
    <artifactId>mssql-jdbc</artifactId>
    <version>7.4.1.jre11</version>
</dependency>
```  

## <a name="unsupported-drivers"></a>サポートされていないドライバー

サポートされていないバージョンのドライバーは、ここではダウンロードできません。 Microsoft は Java 接続のサポートの向上を継続的に進めています。 そのため、最新バージョンの Microsoft JDBC ドライバーを使用することを強くおすすめします。  
  
## <a name="next-steps"></a>次の手順

Microsoft JDBC driver for SQL Server の詳細については、「 [jdbc ドライバーの概要](overview-of-the-jdbc-driver.md)」と「 [jdbc driver GitHub リポジトリ](https://github.com/microsoft/mssql-jdbc/blob/dev/README.md)」を参照してください。
