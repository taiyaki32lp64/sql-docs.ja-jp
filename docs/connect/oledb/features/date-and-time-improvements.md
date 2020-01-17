---
title: 日付と時刻の機能強化 |Microsoft Docs
description: OLE DB Driver for SQL Server の日付と時刻の機能強化
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 170404a4f90be10c848c8f15b7663c330f67495a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989125"
---
# <a name="date-and-time-improvements"></a>日付と時刻の強化機能
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  このトピックでは、で[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]追加された日付と時刻のデータ型をサポート SQL Server するための OLE DB ドライバーについて説明します。  
  
 日付/時刻の強化の詳細については、「[日付&#40;と&#41;時刻の機能強化 OLE DB](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)」を参照してください。  
  
 この機能を説明するサンプル アプリケーションについては、「[SQL Server データ プログラミング サンプル](https://msftdpprodsamples.codeplex.com/)」を参照してください。  
  
## <a name="usage"></a>使用方法  
 ここでは、新しい日付型と時刻型のさまざまな使用方法について説明します。  
  
### <a name="use-date-as-a-distinct-data-type"></a>個別のデータ型として日付を使用する  
 以降で[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]は、日付型または時刻型のサポートが強化されたため、DBTYPE_DBDATE OLE DB の型をより効率的に使用できるようになりました。  
  
### <a name="use-time-as-a-distinct-data-type"></a>個別のデータ型として時刻を使用する  
 OLE DB には既に、有効桁数が 1 秒のデータ型として DBTYPE_DBTIME があります。このデータ型には時刻のみが含まれます。
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の新しい時刻データ型では、秒の小数部の精度が 100 ナノ秒です。 これには、OLE DB Driver for SQL Server: DBTYPE_DBTIME2 の新しい型が必要です。 秒の小数部を含まない時刻を使用するように記述された既存のアプリケーションでは、time(0) 列を使用できます。 アプリケーションがメタデータに返される型に依存しない場合は、既存の OLE DB DBTYPE_TIME 型とそれに対応する構造体が正常に動作します。  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>秒の有効桁数が拡張された個別のデータ型として時刻を使用する  
 プロセス制御や製造アプリケーションなど、アプリケーションによっては、有効桁数が 100 ナノ秒までの時刻データを処理できる必要があります。 OLE DB でのこの目的の新しい型は DBTYPE_DBTIME2 です。  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>秒の有効桁数が拡張された Datetime を使用する  
 OLE DB では既に、有効桁数が 1 ナノ秒までの型が定義されています。 ただし、この型は既に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の既存のアプリケーションで使用されており、このようなアプリケーションでは、有効桁数を 1/300 秒までしか想定していません。 新しい **datetime2(3)** 型は、既存の datetime 型と直接的な互換性がありません。 これがアプリケーションの動作に影響するというリスクがある場合、アプリケーションは新しい DBCOLUMN フラグを使用して、実際のサーバーの種類を判断する必要があります。    
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>秒の有効桁数とタイム ゾーンが拡張された Datetime を使用する  
 アプリケーションによっては、タイム ゾーン情報を含む datetime 値が必要です。 これは、新しい DBTYPE_DBTIMESTAMPOFFSET 型によってサポートされています。
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>既存の変換と一貫性のあるクライアント側変換で Date/Time/Datetime/Datetimeoffset データを使用する  
 この変換は、[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] で導入されたすべての日付型と時刻型との間の変換を含めるように一貫して拡張されます。  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server の機能](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
