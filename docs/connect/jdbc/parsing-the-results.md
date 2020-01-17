---
title: 結果の解析 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 127c97ec155ef1e19df4103b12a6e10b8b67fe74
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027863"
---
# <a name="parsing-the-results"></a>結果の解析

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

この記事では、ユーザーが任意のクエリから返された結果を完全に処理することを期待する SQL Server 方法について説明します。

## <a name="update-counts-and-result-sets"></a>更新数と結果セット

このセクションでは、SQL Server から返される最も一般的な2つの結果について説明します。更新数と ResultSet です。 一般に、ユーザーが実行するすべてのクエリによって、次のいずれかの結果が返されます。ユーザーは、結果の処理時に両方を処理することが想定されています。

次のコードは、ユーザーがサーバーからのすべての結果を反復処理する方法を示しています。
```java
try (Connection connection = DriverManager.getConnection(URL); Statement statement = connection.createStatement()) {
    boolean resultsAvailable = statement.execute(USER_SQL);
    int updateCount = -2;
    while (true) {
        updateCount = statement.getUpdateCount();
        if (!resultsAvailable && updateCount == -1)
            break;
        if (resultsAvailable) {
            // handle ResultSet
        } else {
            // handle Update Count
        }
        resultsAvailable = statement.getMoreResults();
    }
}
```

## <a name="exceptions"></a>例外
エラーまたは情報メッセージを返すステートメントを実行すると、実行プランを生成できるかどうかによって SQL Server の応答が異なります。 エラーメッセージは、ステートメントの実行直後にスローすることも、別の結果セットが必要になる場合もあります。 後者の場合、アプリケーションでは、例外を取得するために結果セットを解析する必要があります。

SQL Server が実行プランを生成できない場合、直ちに例外がスローされます。

```java
String SQL = "SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    statement.execute(SQL);
} catch (SQLException e) {
    e.printStackTrace();
}
```

SQL Server が結果セットにエラーメッセージを返す場合は、例外を取得するために結果セットを処理する必要があります。

```java
String SQL = "SELECT 1/0;";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    if (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            // Exception is thrown on next().
            while (rs.next()) {}
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

ステートメントの実行によって複数の結果セットが生成される場合、各結果セットは、例外が発生するまで処理する必要があります。

```java
String SQL = "SELECT 1; SELECT * FROM nonexistentTable;";
try (Statement statement = connection.createStatement();) {
    // Does not throw an exception on execute().
    boolean hasResult = statement.execute(SQL);
    while (hasResult) {
        try (ResultSet rs = statement.getResultSet()) {
            while (rs.next()) {
                System.out.println(rs.getString(1));
            }
        }
        // Moves the next result set that generates the exception.
        hasResult = statement.getMoreResults();
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```

の`String SQL = "SELECT * FROM nonexistentTable; SELECT 1;";`場合、例外はすぐ`SELECT 1`に`execute()`スローされ、実行されません。

SQL Server からのエラーの重大度がの`0` `9`場合は、情報メッセージと見なされ、として`SQLWarning`返されます。

```java
String SQL = "RAISERROR ('WarningLevel5', 5, 2);";
try (Statement statement = connection.createStatement();) {
    boolean hasResult = statement.execute(SQL);
    SQLWarning warning = statement.getWarnings();
    System.out.println(warning);
}
```

## <a name="see-also"></a>参照

[JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)
