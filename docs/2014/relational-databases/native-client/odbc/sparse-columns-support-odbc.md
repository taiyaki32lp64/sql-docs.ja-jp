---
title: スパース列のサポート (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 11ae959f-2fb6-4b85-ac5d-1476a82136d4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6e1583dad869860bdd2f555a354850c7f7a1198
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691958"
---
# <a name="sparse-columns-support-odbc"></a>スパース列のサポート (ODBC)
  このトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC でのスパース列のサポートについて説明します。 スパース列に対する ODBC サポートを示すサンプルについては、次を参照してください。[スパース列を含むテーブルに対して SQLColumns を呼び出す](../../native-client-odbc-how-to/call-sqlcolumns-on-a-table-with-sparse-columns.md)します。 スパース列の詳細については、次を参照してください。 [SQL Server Native Client におけるスパース列のサポート](../features/sparse-columns-support-in-sql-server-native-client.md)します。  
  
## <a name="statement-metadata"></a>ステートメント メタデータ  
 アプリケーション パラメーター記述子 (APD) の記述子フィールドと SQL_SOPT_SS_NAME_SCOPE ステートメント属性は、追加の値 SQL_SS_NAME_SCOPE_EXTENDED および SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET を受け入れます。 これらの値がによって返される結果セットに含まれる列を指定[SQLColumns](../../native-client-odbc-api/sqlcolumns.md)します。 SQL_SOPT_SS_NAME_SCOPE の詳細については、次を参照してください。 [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)します。  
  
 新しい実装行記述子 (IRD) の、SQL_CA_SS_IS_COLUMN_SET という名前の読み取り専用 SQLSMALLINT フィールドを使用して、列が XML `column_set` 値かどうかを確認できます。 SQL_CA_SS_IS_COLUMN_SET は、値 SQL_TRUE および SQL_FALSE を受け取ります。  
  
## <a name="catalog-metadata"></a>カタログ メタデータ  
 2 つ[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]の結果セットに特定の列 (SS_IS_SPARSE と SS_IS_COLUMN_SET) が追加された[SQLColumns](../../native-client-odbc-api/sqlcolumns.md)します。  
  
## <a name="odbc-function-support-for-sparse-columns"></a>ODBC 関数によるスパース列のサポート  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client でスパース列をサポートするために、次の ODBC 関数が更新されました。  
  
-   [SQLColAttribute](../../native-client-odbc-api/sqlcolattribute.md)  
  
-   [SQLColumns](../../native-client-odbc-api/sqlcolumns.md)  
  
-   [SQLGetDescField](../../native-client-odbc-api/sqlgetdescfield.md)  
  
-   [SQLSetDescField](../../native-client-odbc-api/sqlsetdescfield.md)  
  
-   [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
