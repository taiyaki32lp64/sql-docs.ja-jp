---
title: 環境ハンドルを割り当てる |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eae9e11006a8a832523a7f72bdade6e943e57f50
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784739"
---
# <a name="allocating-an-environment-handle"></a>環境ハンドルの割り当て
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  どの ODBC 関数をアプリケーションから呼び出す場合でも、呼び出す前に ODBC 環境を初期化して環境ハンドルを割り当てる必要があります。 環境ハンドルはグローバルなコンテキスト ハンドルで、ODBC の他のハンドルのプレースホルダーです。 これを行うには、 *Handletype*パラメーターを SQL_HANDLE_ENV に設定し、 *InputHandle*を SQL_NULL_HANDLE に設定して、 **SQLAllocHandle**を呼び出します。  
  
 環境ハンドルを割り当てたら、使用する ODBC 関数呼び出しのバージョンを指定する環境属性を設定する必要があります。 ODBC 3 を使用する場合はです。*x*関数は、*属性*パラメーターを SQL_ATTR_ODBC_VERSION に設定し、 *valueptr*を SQL_OV_ODBC3 に設定して、 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)を呼び出します。  
  
## <a name="see-also"></a>参照  
 [SQL Server &#40;ODBC との通信&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
