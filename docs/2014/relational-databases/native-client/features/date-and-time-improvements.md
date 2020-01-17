---
title: 日付と時刻の機能強化 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 9b1d0d9d-1f6e-4399-8f61-e23f9a486a7a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 160731a6749b3741a68dcccafedd3499db465349
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75231761"
---
# <a name="date-and-time-improvements"></a>日付と時刻の強化機能
  このトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に追加された日付と時刻のデータ型の [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client サポートについて説明します。  
  
 日付/時刻の強化の詳細については、「[日付と時刻の機能強化 &#40;OLE DB&#41;](../../native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)および[日付と時刻の機能強化 &#40;ODBC&#41;](../../native-client-odbc-date-time/date-and-time-improvements-odbc.md)」を参照してください。  
  
 この機能を説明するサンプル アプリケーションについては、「[SQL Server データ プログラミング サンプル](https://msftdpprodsamples.codeplex.com/)」を参照してください。  
  
## <a name="usage"></a>使用法  
 ここでは、新しい日付型と時刻型のさまざまな使用方法について説明します。  
  
### <a name="use-date-as-a-distinct-data-type"></a>個別のデータ型として日付を使用する  
 
  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 以降、日付型と時刻型のサポートの強化により、SQL_TYPE_DATE ODBC 型 (ODBC 2.0 アプリケーションの場合は SQL_DATE) と DBTYPE_DBDATE OLE DB 型をより効果的に使用できるようになります。  
  
### <a name="use-time-as-a-distinct-data-type"></a>個別のデータ型として時刻を使用する  
 OLE DB には既に、有効桁数が 1 秒のデータ型として DBTYPE_DBTIME があります。このデータ型には時刻のみが含まれます。 この型は、ODBC の SQL_TYPE_TIME (ODBC 2.0 アプリケーションの場合は SQL_TIME) に相当します。  
  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の新しい時刻データ型では、秒の小数部の精度が 100 ナノ秒です。 これには、Native [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client の新しい型 (DBTYPE_DBTIME2 (OLE DB) と SQL_SS_TIME2 (ODBC) が必要です。 秒の小数部を含まない時刻を使用するように記述された既存のアプリケーションでは、time(0) 列を使用できます。 アプリケーションがメタデータに返される型に依存しない場合は、既存の OLE DB DBTYPE_TIME 型と ODBC SQL_TYPE_TIME 型、およびそれに対応する構造体が正常に動作します。  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>秒の有効桁数が拡張された個別のデータ型として時刻を使用する  
 プロセス制御や製造アプリケーションなど、アプリケーションによっては、有効桁数が 100 ナノ秒までの時刻データを処理できる必要があります。 このための新しい型が DBTYPE_DBTIME2 (OLE DB) と SQL_SS_TIME2 (ODBC) です。  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>秒の有効桁数が拡張された Datetime を使用する  
 OLE DB では既に、有効桁数が 1 ナノ秒までの型が定義されています。 ただし、この型は既に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既存のアプリケーションで使用されており、このようなアプリケーションでは、有効桁数を 1/300 秒までしか想定していません。 新しい `datetime2(3)` 型は、既存の datetime 型と直接的な互換性がありません。 これがアプリケーションの動作に影響するというリスクがある場合、アプリケーションは新しい DBCOLUMN フラグを使用して、実際のサーバーの種類を判断する必要があります。  
  
 ODBC DB でも既に、有効桁数が 1 ナノ秒までの型が定義されています。 ただし、この型は既に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既存のアプリケーションで使用されており、このようなアプリケーションでは、有効桁数を 3 ミリ秒までしか想定していません。 新しい `datetime2(3)` 型は、既存の `datetime` 型と直接的な互換性がありません。 
  `datetime2(3)` の有効桁数は 1 ミリ秒、`datetime` の有効桁数は 1/300 秒です。 ODBC では、アプリケーションが SQL_DESC_TYPE_NAME 記述子フィールドで使用されているサーバーの種類を判断できます。 したがって、既存の型 SQL_TYPE_TIMESTAMP (ODBC 2.0 アプリケーションの場合は SQL_TIMESTAMP) は両方の型に使用できます。  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>秒の有効桁数とタイム ゾーンが拡張された Datetime を使用する  
 アプリケーションによっては、タイム ゾーン情報を含む datetime 値が必要です。 これは、新しい型 DBTYPE_DBTIMESTAMPOFFSET (OLE DB) および SQL_SS_TIMESTAMPOFFSET (ODBC) でサポートされています。  
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>既存の変換と一貫性のあるクライアント側変換で Date/Time/Datetime/Datetimeoffset データを使用する  
 ODBC 標準では、既存の date 型、time 型、および timestamp 型の間の変換のしくみについて説明します。 このような変換は、[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] で導入されたすべての日付型と時刻型との間の変換を含めるように一貫して拡張されます。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client 機能](sql-server-native-client-features.md)  
  
