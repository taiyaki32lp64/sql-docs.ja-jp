---
title: 日付と時刻の機能強化 (OLE DB) |Microsoft Docs
description: 日付と時刻の強化機能 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c4a93078b84cf5146f94043496bea0fdaed9fc80
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015705"
---
# <a name="date-and-time-improvements-ole-db"></a>日付と時刻の強化機能 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] では、新しい日付と時刻のデータ型が導入されています。 このセクションでは、これらの新しい型を SQL Server 用の OLE DB ドライバーの拡張機能として公開する方法について説明します。 新しい日付と時刻のデータ型の SQL Server サポートのための OLE DB ドライバーの概要については、「[日付と時刻の機能強化](../../oledb/features/date-and-time-improvements.md)」を参照してください。 サンプルについては、「拡張された[日付/時刻&#40;機能の&#41;使用 OLE DB](../../oledb/ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)」を参照してください。  
  
 日付と時刻のデータ型に関する一般的な情報については、「 [datetime &#40;transact-sql&#41;](../../../t-sql/data-types/datetime-transact-sql.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [OLE DB の日付/時刻の強化に対するデータ型のサポート](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 日付と時刻のデータ型をサポート[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]する OLE DB (OLE DB Driver for SQL Server) の種類に関する情報を提供します。  
  
 [メタ&#40;データ OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
 **ICommandWithParameters:: GetParameterInfo**、 **ICommandWithParameters:: setparameterinfo**、 **IColumnsRowset:: GetColumnsRowset**、I DBBINDING**info:: GetColumnInfo に関する情報が含まれています。** . また、OLE DB スキーマ行セットの更新についても説明します。  
  
 [バインドと変換 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
 既存の日付型と新しい日付型の両方を対象とした、サーバーとクライアント間における変換の規則について説明します。  
  
 [機能強化された日付型と時刻型向けの一括コピーの変更 (OLE DB)](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)  
 一括コピー操作をサポートする日付または時刻の機能強化について説明します。  
  
 [OLE DB API による機能強化された日付と時刻のサポート](../../oledb/ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 機能強化された日付や時刻をサポートする OLE DB API について説明します。  
  
 [IRowsetFind での比較](../../oledb/ole-db-date-time/comparability-for-irowsetfind.md)  
 日付/時刻型と**IRowsetFind**について説明します。  
 
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server のプログラミング](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
