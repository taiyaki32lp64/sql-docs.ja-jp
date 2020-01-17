---
title: SQLCancel |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLCancel function
ms.assetid: d4c965ae-c1ac-4e9d-b4b9-32b561401106
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 80b0ac3e21933c378d67b41f1bbc846f04811ed5
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787659"
---
# <a name="sqlcancel"></a>SQLCancel
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)のトピックでは、ODBC 2.x では、ステートメントに対して処理が実行されていないときにアプリケーションが**SQLCancel**を呼び出した場合、 **SQLCancel**は**SQLFreeStmt**と同じ効果を**SQL_CLOSE**持つということを示しています。この動作は、完全な場合にのみ定義され、アプリケーションは**SQLFreeStmt**または**sqlcloを**呼び出してカーソルを閉じる必要があります。 ただし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client アプリケーションが ODBC API バージョンを 3.5. x 以降に設定している場合でも、 **SQLCancel**関数では odbc 2.x の動作が使用されます。  
  
## <a name="see-also"></a>参照  
 [SQLCancel](https://go.microsoft.com/fwlink/?LinkId=203516)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
