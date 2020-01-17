---
title: ネイティブエラー番号 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b1bc1f9383ab615a24b0506b86cf0ec5e37b6c74
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783398"
---
# <a name="native-error-numbers"></a>ネイティブ エラー番号
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって返されたデータソースで発生したエラーの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]によって返されたネイティブエラー番号を返します。 ドライバーによって検出されたエラーの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、ネイティブエラー番号0を返します。 ネイティブエラー番号の一覧の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の**master**データベースにある**sysmessages**システムテーブルの error 列を参照してください。  
  
 状態エラーコードの詳細については、「 [SQLSTATE &#40;ODBC&#41;エラーコード](../../relational-databases/native-client-odbc-error-messages/sqlstate-odbc-error-codes.md)」を参照してください。 Net-Library から返されたエラーについては、ネイティブ エラー番号は基になるネットワーク ソフトウェアから返されます。  
  
## <a name="see-also"></a>参照  
 [エラーとメッセージの処理](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
