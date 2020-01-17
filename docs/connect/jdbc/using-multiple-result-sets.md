---
title: 複数の結果セットを使用する |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ab6a3cfa-073b-44e9-afca-a8675cfe5fd1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 802ade7a34eb5c5174efc35032587f801ef12179
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026274"
---
# <a name="using-multiple-result-sets"></a>複数の結果セットの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

複数の結果セットを返すインライン SQL または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャを処理する場合、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] では返される各データのセットを取得するために、[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) クラスの [getResultSet](../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md) メソッドを提供します。 また、複数の結果セットを返すステートメントの実行時には、SQLServerStatement クラスの [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) メソッドを使用できます。これは、返される値が結果セットと更新数のどちらであるかを示す **boolean** 値を返せるためです。

execute メソッドから **true** が返された場合、実行されたステートメントから返されるのは 1 つ以上の結果セットです。 最初の結果セットには、getResultSet メソッドを呼び出すことでアクセスできます。 他にも使用可能な結果セットがあるかどうかを判断するには、[getMoreResults](../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md) メソッドを呼び出すことができます。このメソッドでは、他にも使用可能な結果セットがある場合、**boolean** 値として **true** が返されます。 他にも結果セットが使用可能な場合は、getResultSet メソッドを再度呼び出して結果セットにアクセスし、すべての結果セットが処理されるまで続けます。 GetMoreResults メソッドから**false**が返された場合、処理する結果セットはこれ以上ありません。

execute メソッドから **false** が返された場合、実行されたステートメントから返されるのは更新数の値です。更新数の値は、[getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) メソッドを呼び出すことで取得できます。

> [!NOTE]  
> 更新数の詳細については、「 [update count を使用したストアドプロシージャの使用](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)」を参照してください。

次の例では、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースに対して開いている接続が関数に渡され、実行時に 2 つの結果セットを返す SQL ステートメントが作成されています。

[!code[JDBC#UsingMultipleResultSets1](../../connect/jdbc/codesnippet/Java/using-multiple-result-sets_1.java)]

この例では、返される結果セット数は 2 であることがわかっています。 ただし、ストアド プロシージャを呼び出す場合のように、返される結果セット数が不明でも、すべての結果セットが処理されるようにコードが作成されています。 複数の結果セットと更新数を返すストアド プロシージャを呼び出す例については、「[複雑なステートメントの処理](../../connect/jdbc/handling-complex-statements.md)」を参照してください。

> [!NOTE]  
> SQLServerStatement クラスの getMoreResults メソッドを呼び出すと、以前に返された結果セットは暗黙的に閉じられます。

## <a name="see-also"></a>参照

[JDBC ドライバーでのステートメントの使用](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)
