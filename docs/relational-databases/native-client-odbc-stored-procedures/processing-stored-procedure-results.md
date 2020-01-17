---
title: ストアドプロシージャの結果を処理しています |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- stored procedures [ODBC], results
ms.assetid: 788ef2a4-17de-4526-960b-46bf29aafc9f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9240940a05768dfbc577cf0c5ef40a44a1f7c497
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73778933"
---
# <a name="processing-stored-procedure-results"></a>ストアド プロシージャの結果の処理
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャには、データを返す際に使用する次の 4 つのメカニズムがあります。  
  
-   プロシージャ内の各 SELECT ステートメントで結果セットを生成する。  
  
-   プロシージャが出力パラメーターによってデータを返すことができる。  
  
-   カーソルの出力パラメーターから、[!INCLUDE[tsql](../../includes/tsql-md.md)] サーバー カーソルを返すことができる。  
  
-   プロシージャに整数のリターン コードを含めることができる。  
  
 アプリケーションでは、ストアド プロシージャからのこれらすべての出力を処理できる必要があります。 CALL ステートメントや EXECUTE ステートメントには、リターン コードと出力パラメーター用のパラメーター マーカーを含める必要があります。 [SQLBindParameter](../../relational-databases/native-client-odbc-api/sqlbindparameter.md)を使用してすべてを出力パラメーターとしてバインドし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] NATIVE Client ODBC ドライバーは、バインドされた変数に出力値を転送します。 出力パラメーターとリターンコードは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によってクライアントに返される最後の項目です。[Sqlmoreresults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)が SQL_NO_DATA を返すまで、アプリケーションには返されません。  
  
 ODBC は、[!INCLUDE[tsql](../../includes/tsql-md.md)] カーソル パラメーターのバインドをサポートしません。 プロシージャの実行前にすべての出力パラメーターをバインドしておく必要があるので、出力カーソル パラメーターを含む [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャを ODBC アプリケーションから呼び出すことはできません。  
  
## <a name="see-also"></a>参照  
 [ストアド プロシージャの実行](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
