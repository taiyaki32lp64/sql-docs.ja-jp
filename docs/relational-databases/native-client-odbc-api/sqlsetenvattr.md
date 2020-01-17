---
title: SQLSetEnvAttr |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8e1d8e6ea962f5cd8fe094fca195a2fa59a5701d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73785633"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Odbc[プログラマーズリファレンス](https://go.microsoft.com/fwlink/?LinkId=45250)では、odbc ドライバーが odbc 2 に書き込まれたアプリケーションから**SQLSetEnvAttr**属性の仕様を解釈する方法を定義します。*x*または ODBC 3。*x* API。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、これらの規則に準拠しています。  
  
 **SQLSetEnvAttr**によって制御される属性の1つは、接続プールを使用するかどうかです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーで接続プールを使用する場合は、 [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)または**SQLConnect**を使用して接続するときに、 *drivercompletion*パラメーターを SQL_DRIVER_NOPROMPT に設定する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQLSetEnvAttr 関数](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
