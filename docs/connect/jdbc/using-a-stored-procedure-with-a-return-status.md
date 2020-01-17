---
title: 状態の戻り値があるストアド プロシージャの使用 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4b126e95-8458-41d6-af37-fc6662859f19
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b5b5425dcc88a3f4a2b5bc24c85ab41beb04bb48
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027111"
---
# <a name="using-a-stored-procedure-with-a-return-status"></a>状態の戻り値があるストアド プロシージャの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

呼び出すことができる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャは、状態パラメーターまたは結果パラメーターを返すプロシージャです。 この戻り値は一般的に、ストアド プロシージャの成功または失敗を示すために使用されます。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] が提供する [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスを使用することで、この種類のストアド プロシージャを呼び出し、返されるデータを処理することができます。

JDBC ドライバーを使用してこの種類のストアド プロシージャを呼び出す場合は、`call` SQL エスケープ シーケンスを、[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) メソッドと組み合わせて使用する必要があります。 状態の戻り値パラメーターを持つ `call` エスケープ シーケンスの構文は次のとおりです。

`{[?=]call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> SQL エスケープシーケンスの詳細については、「 [sql エスケープシーケンスの使用](../../connect/jdbc/using-sql-escape-sequences.md)」を参照してください。

`call` エスケープ シーケンスを作成する場合、状態の戻り値パラメーターは? (疑問符) 文字で指定します。 この文字は、ストアド プロシージャから返されるパラメーター値のプレースホルダーになります。 状態の戻り値パラメーターの値を指定するには、ストアド プロシージャを実行する前に、SQLServerCallableStatement クラスの [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) メソッドを使用して、各パラメーターのデータ型を指定する必要があります。

> [!NOTE]  
> SQL Server のデータベースと合わせて JDBC ドライバーを使用する場合、registerOutParameter メソッドで状態の戻り値パラメーターに対して指定した値は、常に整数になります。この値は、java.sql.Types.INTEGER データ型を使用して指定できます。

さらに、registerOutParameter メソッドに状態の戻り値パラメーターの値を渡す場合は、パラメーターに使用するデータ型だけでなく、ストアド プロシージャの呼び出しにおいてパラメーターの順序も指定する必要があります。 状態の戻り値パラメーターは、ストアド プロシージャの呼び出しにおいて常に最初のパラメーターであるため、位置を示す序数は常に 1 になります。 SQLServerCallableStatement クラスでは、パラメーター名を使用したパラメーター指定がサポートされていますが、状態の戻り値パラメーターに使用できるのは、パラメーターの序数位置番号だけです。

たとえば、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースで次のストアド プロシージャを作成します。

```sql
CREATE PROCEDURE CheckContactCity  
   (@cityName CHAR(50))  
AS  
BEGIN  
   IF ((SELECT COUNT(*)  
   FROM Person.Address  
   WHERE City = @cityName) > 1)  
   RETURN 1  
ELSE  
   RETURN 0  
END  
```

このストアド プロシージャでは、cityName パラメーターで指定された都市名が Person.Address テーブルに存在するかどうかによって、1 または 0 の状態値が返されます。

次の例は、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースに対して開いている接続を関数に渡し、[execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) メソッドを使用して CheckContactCity ストアド プロシージャを呼び出しています。

[!code[JDBC#UsingSprocWithReturnStatus1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_1_1.java)]

## <a name="see-also"></a>参照

[ストアド プロシージャでのステートメントの使用](../../connect/jdbc/using-statements-with-stored-procedures.md)
