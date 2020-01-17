---
title: Java データ型
titleSuffix: SQL Server Language Extensions
description: 入力および出力のデータ構造と、sp_execute_external_script に対する入力パラメーターのデータ型を Java から SQL Server にマップします。
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d1df57079acd79fc5370d0f2f198dc2d624d6983
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73658835"
---
# <a name="java-and-sql-server-supported-data-types"></a>Java および SQL Server のサポートされるデータ型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

この記事では、SQL Server データ型を [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) のデータ構造とパラメーターの Java データ型にマップします。

現在、次の SQL および Java データ型が入力/出力データ セットおよび入力/出力パラメーターでサポートされています。

| SQL データ型        | Java データ型 | 解説 | |
| ------------- |-------------|-|-|
| bit      | boolean | | |
| Tinyint      | short      | | |
| Smallint | short      | | |
| Int | INT      | | |
| Real | FLOAT      | | |
| Bigint | long      | | |
| FLOAT | double      | | |
| nchar(n) | String      | | |
| nvarchar(n) | String      | | |
| binary(n) | byte[]      | | |
| varbinary(n) | byte[]      | | |
| nvarchar(max) | String      | | |
| varbinary(max) | byte[]      | | |
| UNIQUEIDENTIFIER | String | | |
| char(n) | String | UTF8 文字列のみがサポートされています | |
| varchar(n) | String | UTF8 文字列のみがサポートされています | |
| varchar(max) | String | UTF8 文字列のみがサポートされています | |
| date | java.sql.date  | | |
| NUMERIC | java.math.BigDecimal  | | |
| Decimal | java.math.BigDecimal  | | |
| money | java.math.BigDecimal  | | |
| SMALLMONEY | java.math.BigDecimal  | | |
| smalldatetime | java.sql.timestamp  | | |
| DATETIME | java.sql.timestamp  | | |
| datetime2 | java.sql.timestamp  | | |


## <a name="next-steps"></a>次の手順

+ [SQL Server で Java を呼び出す方法](../how-to/call-java-from-sql.md)
