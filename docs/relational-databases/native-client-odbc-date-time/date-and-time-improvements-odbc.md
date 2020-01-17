---
title: 日付と時刻の強化 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC]
- ODBC, date/time improvements
ms.assetid: e31d5ca5-2103-498f-954c-1ee93e217186
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7cc697c60857f47630dd041762f90f789dd170d5
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783882"
---
# <a name="date-and-time-improvements-odbc"></a>日付と時刻の強化機能 (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では、新しい日付と時刻のデータ型が導入されました。 このセクションでは、これらの新しい型を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の拡張機能として公開する方法について説明します。 新しい日付と時刻のデータ型に対する Native Client のサポート [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 概要については、「[日付と時刻の機能強化](../../relational-databases/native-client/features/date-and-time-improvements.md)」を参照してください。 ODBC の日付と時刻のサポートを示すサンプルについては、「[日付と時刻の型の使用](../../relational-databases/native-client-odbc-how-to/use-date-and-time-types.md)」を参照してください。  
  
 日付と時刻のデータ型に関する一般的な情報については、「 [datetime &#40;transact-sql&#41;](../../t-sql/data-types/datetime-transact-sql.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [ODBC の日付/時刻の強化に対するデータ型のサポート](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の日付と時刻のデータ型をサポートする ODBC 型について説明します。  
  
 [メタ&#40;データ ODBC&#41;](https://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
 実装パラメーター記述子 (IPD) および実装行記述子 (IRD) フィールドに返される情報、および**Sqlcolumns**と**SQLProcedureColumns**によって返される列のメタデータについて説明します。 また、 **SQLGetTypeInfo**によって返されるデータ型のメタデータについても説明します。  
  
 [datetime データ型変換&#40;(ODBC)&#41;](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-odbc.md)  
 datetime 値と datetimeoffset 値の間で変換を行う方法について説明します。  
  
 [sql_variant による日付型と時刻型のサポート](../../relational-databases/native-client-odbc-date-time/sql-variant-support-for-date-and-time-types.md)  
 SQL_VARIANT 関数による機能強化された日付と時刻のサポートについて説明します。  
  
 [拡張された日付/時刻型&#40;OLE DB および ODBC の一括コピーの変更&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 一括コピー操作をサポートする日付または時刻の機能強化について説明します。  
  
 [以前のバージョン&#40;の SQL Server ODBC での日付と時刻の型の動作の強化&#41;](../../relational-databases/native-client-odbc-date-time/enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 強化された日付と時刻の機能を使用するクライアントアプリケーションが古いバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と通信する場合、および古いバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client でコンパイルされたクライアントが、をサポートするサーバーにコマンドを送信する場合の想定される動作について説明します。強化された日付と時刻の機能。  
  
 [ODBC API による機能強化された日付と時刻のサポート](../../relational-databases/native-client-odbc-date-time/odbc-api-support-for-enhanced-date-and-time-features.md)  
 機能強化された日付と時刻をサポートする ODBC 関数の一覧を示します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
