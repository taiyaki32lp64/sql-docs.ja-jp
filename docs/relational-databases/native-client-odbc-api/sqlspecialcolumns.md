---
title: Sql特殊列 |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSpecialColumns function
ms.assetid: dffe02ed-8f79-4c9a-af34-98130bbe5462
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d5550503d4c9854fb40e816124c16dbc19c2c6fd
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73785447"
---
# <a name="sqlspecialcolumns"></a>SQLSpecialColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  行識別子 (*Identifiertype* SQL_BEST_ROWID) を要求すると、 **Sqlている列**は、SQL_SCOPE_CURROW 以外の要求されたスコープに対して空の結果セット (データ行がない) を返します。 生成される結果セットは、列がこのスコープ内でのみ有効であることを示します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、識別子の擬似列がサポートされません。 **Sql特殊列**の結果セットでは、すべての列が SQL_PC_NOT_PSEUDO として識別されます。  
  
 **Sql特殊な列**は、静的カーソルで実行できます。 更新可能な (キーセットドリブンまたは動的) で**sqlsp_helptext 列**を実行しようとすると、カーソルの種類が変更されたことを示す SQL_SUCCESS_WITH_INFO が返されます。  
  
## <a name="sqlspecialcolumns-support-for-enhanced-date-and-time-features"></a>SQLSpecialColumns による機能強化された日付と時刻のサポート  
 日付型または時刻型の列 DATA_TYPE、TYPE_NAME、COLUMN_SIZE、BUFFER_LENGTH、および DECIMAL_DIGTS に対して返される値の詳細については、「[カタログメタデータ](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md)」を参照してください。  
  
 一般的な情報については、「[日付&#40;と&#41;時刻の機能強化 ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)」を参照してください。  
  
## <a name="sqlspecialcolumns-support-for-large-clr-udts"></a>SQLSpecialColumns による大きな CLR UDT のサポート  
 **Sqlxl 列**では、大きな CLR ユーザー定義型 (udt) をサポートしています。 詳細については、「 [LARGE CLR ユーザー定義&#40;型&#41;ODBC](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Sql特殊列関数](https://go.microsoft.com/fwlink/?LinkId=59371)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
