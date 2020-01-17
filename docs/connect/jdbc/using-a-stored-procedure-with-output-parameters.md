---
title: 出力パラメーターがあるストアド プロシージャの使用 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: efafaa709666620e7237f2481c392aba25dfd5f8
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026832"
---
# <a name="using-a-stored-procedure-with-output-parameters"></a>出力パラメーターがあるストアド プロシージャの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャのうち、呼び出すことができるのは、OUT パラメーター (呼び出し元のアプリケーションにデータを返す目的で使用されるパラメーター) を少なくとも 1 つ返すストアド プロシージャです。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] が提供する [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスを使用することで、この種類のストアド プロシージャを呼び出し、返されるデータを処理することができます。

JDBC ドライバーを使用してこの種類のストアド プロシージャを呼び出す場合は、`call` SQL エスケープ シーケンスを、[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) メソッドと一緒に使用する必要があります。 OUT パラメーターを持つ `call` エスケープ シーケンスの構文は次のとおりです。

`{call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> SQL エスケープシーケンスの詳細については、「 [sql エスケープシーケンスの使用](../../connect/jdbc/using-sql-escape-sequences.md)」を参照してください。

`call` エスケープ シーケンスを作成する場合、OUT パラメーターは ? (疑問符) 文字で指定します。 この文字は、ストアド プロシージャから返されるパラメーター値のプレースホルダーになります。 OUT パラメーターの値を指定するには、ストアド プロシージャを実行する前に、SQLServerCallableStatement クラスの [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) メソッドを使用して、各パラメーターのデータ型を指定する必要があります。

registerOutParameter メソッドで OUT パラメーターに指定する値は、java.sql.Types に含まれる JDBC データ型のいずれかである必要があります。この値は、ネイティブの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型の 1 つに順にマップされます。 Jdbc と[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型の詳細については、「 [jdbc ドライバーのデータ型](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)について」を参照してください。

registerOutParameter メソッドに OUT パラメーターの値を渡す場合は、パラメーターに使用するデータ型だけでなく、ストアド プロシージャ内のパラメーターの順序またはパラメーター名も指定する必要があります。 たとえば、ストアド プロシージャに 1 つの OUT パラメーターがある場合、その序数値は 1 です。ストアド プロシージャに 2 つのパラメーターがある場合、最初の序数値は 1 で、2 番目の序数値は 2 になります。

> [!NOTE]  
> JDBC ドライバーでは、CURSOR、SQLVARIANT、TABLE、および TIMESTAMP の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型を OUT パラメーターとして使用することはできません。

たとえば、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースで次のストアド プロシージャを作成します。

```sql
CREATE PROCEDURE GetImmediateManager  
   @employeeID INT,  
   @managerID INT OUTPUT  
AS  
BEGIN  
   SELECT @managerID = ManagerID
   FROM HumanResources.Employee
   WHERE EmployeeID = @employeeID  
END
```

このストアド プロシージャでは 1 つの整数の OUT パラメーター (managerID) が返されます。これは、同様に整数である指定した IN パラメーター (employeeID) に基づいています。 OUT パラメーターで返される値は、HumanResources.Employee テーブルに含まれる EmployeeID に基づく ManagerID です。

次の例は、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースに対して開いている接続を関数に渡し、[execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) メソッドを使用して GetImmediateManager ストアド プロシージャを呼び出しています。

```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");) {  
        cstmt.setInt(1, 5);  
        cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt(2));  
    }  
}
```

この例では、序数位置を使用してパラメーターを識別しています。 序数位置の代わりに名前を使用してパラメーターを識別することもできます。 次のコード例では、前の例を変更して、Java アプリケーションで名前付きパラメーターを使用する方法を示します。 パラメーター名は、ストアド プロシージャの定義内にあるパラメーター名に対応しています。

```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}"); ) {  
        cstmt.setInt("employeeID", 5);  
        cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
    }  
}
```

> [!NOTE]  
> これらの例では、SQLServerCallableStatement クラスの execute メソッドを使用してストアドプロシージャを実行します。 このメソッドを使用しているのは、ストアド プロシージャによって結果セットが返されないためです。 結果セットが返される場合は、[executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) メソッドを使用します。

ストアド プロシージャは、更新数および複数の結果セットを返すことができます。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] が準拠している JDBC 3.0 仕様は、複数の結果セットと更新数が、OUT パラメーターの取得前に取得されなければならない旨が規定されています。 つまり、アプリケーションは、すべての ResultSet オブジェクトと更新数を取得してから、CallableStatement. getter メソッドを使用して OUT パラメーターを取得する必要があります。 そうしないと、OUT パラメーターの取得時に、未取得の ResultSet オブジェクトおよび更新数が失われます。 更新数および複数の結果セットの詳細については、「update count を使用し[たストアドプロシージャの使用](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)」および「[複数の結果セットの使用](../../connect/jdbc/using-multiple-result-sets.md)」を参照してください。

## <a name="see-also"></a>参照

[ストアド プロシージャでのステートメントの使用](../../connect/jdbc/using-statements-with-stored-procedures.md)
