---
title: 結果セットのメタデータを使用する |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5e37529a-30db-48c8-b90a-ae9657d0f6b0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ed0b1eedcafa1fab59d17f756523fc0fc189200
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026123"
---
# <a name="using-result-set-metadata"></a>結果セットのメタデータの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

結果セットに格納されている列の情報をクエリするために、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] には、[SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) クラスが実装されています。 このクラスには、単一値の形式で情報を返すメソッドが多数存在します。

SQLServerResultSetMetaData オブジェクトを作成するには、 [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)クラスの[getmetadata](../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)メソッドを使用します。

次の例では、 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]サンプルデータベースに対して開いている接続を関数に渡し、SQLServerResultSet クラスの getmetadata メソッドを使用して SQLServerResultSetMetaData オブジェクトを返します。その後、SQLServerResultSetMetaData オブジェクトは、結果セット内に含まれる列の名前とデータ型に関する情報を表示するために使用されます。

[!code[JDBC#UsingResultSetMetaData1](../../connect/jdbc/codesnippet/Java/using-result-set-metadata_1.java)]

## <a name="see-also"></a>参照

[JDBC ドライバーによるメタデータの処理](../../connect/jdbc/handling-metadata-with-the-jdbc-driver.md)
