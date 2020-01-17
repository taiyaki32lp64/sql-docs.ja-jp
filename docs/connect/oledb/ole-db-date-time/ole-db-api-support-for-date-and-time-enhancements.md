---
title: OLE DB API による機能強化された日付と時刻のサポート | Microsoft Docs
description: OLE DB API による機能強化された日付と時刻のサポート
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c2671b3df6432e63c0e0b36a24bade60286f72a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015685"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>OLE DB API による機能強化された日付と時刻のサポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  機能強化された日付や時刻をサポートする OLE DB API を次に示します。  
  
|機能|[説明]|  
|--------------|-----------------|  
|IAccessor:: CreateAccessor|DBBINDING 構造体にフラグが追加され、アプリケーションが**datetime**、 **datetime2**、および**smalldatetime**の各値を区別できるようになります。 詳細については、「[パラメーターと行セットのメタデータ](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)」を参照してください。|  
|IBCPSession::BCPColFmt|詳細については、「 [OLE DB&#41;の拡張された日付&#40;/時刻型に対する一括コピーの変更](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)」を参照してください。|  
|ICommandWithParameters::GetParameterInfo|詳細については、「[パラメーターと行セットのメタデータ](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)」を参照してください。|  
|ICommandWithParameters::SetParameterinfo|詳細については、「[パラメーターと行セットのメタデータ](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)」を参照してください。|  
|IColumnsRowset::GetColumnsRowset|詳細については、「[パラメーターと行セットのメタデータ](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)」を参照してください。|  
|IColumnsInfo::GetColumnInfo|詳細については、「[パラメーターと行セットのメタデータ](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)」を参照してください。|  
|IDBSchemaRowset::GetRowset|影響を受けるスキーマ行セットの詳細については、「[日付と時刻およびスキーマ行セット](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md)」を参照してください。|  
|IRowsetFastLoad|このインターフェイスは新しい日付と時刻の型をサポートしますが、インターフェイスに変更はありません。|  
|ITableDefinition::CreateTable|詳細については、「 [OLE DB の日付と時刻の機能強化に関するデータ型のサポート](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)」を参照してください。|  
  
## <a name="see-also"></a>参照  
 [日付と時刻の強化機能 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
