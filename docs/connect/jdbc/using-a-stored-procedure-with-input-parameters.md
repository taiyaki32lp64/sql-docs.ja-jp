---
title: 入力パラメーターがあるストアド プロシージャの使用 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8f491b70-7d1b-42bd-964f-9a8b86af5eaa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c84e4081b9369d504d173387c6944b06d927c9c
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026904"
---
# <a name="using-a-stored-procedure-with-input-parameters"></a>入力パラメーターがあるストアド プロシージャの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャのうち、呼び出すことができるのは、IN パラメーター (ストアド プロシージャにデータを渡す際に使用できるパラメーター) を少なくとも 1 つ持つストアド プロシージャです。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] が提供する [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスを使用することで、この種類のストアド プロシージャを呼び出し、返されるデータを処理することができます。

JDBC ドライバーを使用して IN パラメーターがあるストアド プロシージャを呼び出す場合は、`call` SQL エスケープ シーケンスを、[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) メソッドと一緒に使用する必要があります。 IN パラメーターを持つ `call` エスケープ シーケンスの構文は次のとおりです。

`{call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> SQL エスケープシーケンスの詳細については、「 [sql エスケープシーケンスの使用](../../connect/jdbc/using-sql-escape-sequences.md)」を参照してください。

`call` エスケープ シーケンスを作成する場合、IN パラメーターは? (疑問符) 文字で指定します。 この文字は、ストアド プロシージャに渡されるパラメーター値のプレースホルダーになります。 パラメーターの値を指定するには、SQLServerPreparedStatement クラスの setter メソッドのいずれかを使用します。 使用できる setter メソッドは、IN パラメーターのデータ型で決まります。

setter メソッドに値を渡す場合は、パラメーターで使用する実際の値だけでなく、ストアド プロシージャ内のパラメーターの順序も指定する必要があります。 たとえば、ストアド プロシージャに IN パラメーターが 1 つ存在する場合、その序数値は 1 になります。 ストアド プロシージャに 2 つのパラメーターが存在する場合、1 つ目の序数値は 1 に、2 つ目の序数値は 2 になります。

IN パラメーターを含むストアド プロシージャの呼び出し方の例として、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースで uspGetEmployeeManagers ストアド プロシージャを使用します。 このストアド プロシージャは EmployeeID という名前の入力パラメーターを 1 つ受け入れます。このパラメーターは整数値で、指定された EmployeeID に基づいて従業員およびそのマネージャーの再帰的にリストを返します。 このストアド プロシージャの Java コードは次のとおりです。

```java
public static void executeSprocInParams(Connection con) throws SQLException {  
    try(PreparedStatement pstmt = con.prepareStatement("{call dbo.uspGetEmployeeManagers(?)}"); ) {  

        pstmt.setInt(1, 50);  
        ResultSet rs = pstmt.executeQuery();  

        while (rs.next()) {  
            System.out.println("EMPLOYEE:");  
            System.out.println(rs.getString("LastName") + ", " + rs.getString("FirstName"));  
            System.out.println("MANAGER:");  
            System.out.println(rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));  
            System.out.println();  
        }  
    }
}
```

## <a name="see-also"></a>参照

[ストアド プロシージャでのステートメントの使用](../../connect/jdbc/using-statements-with-stored-procedures.md)
