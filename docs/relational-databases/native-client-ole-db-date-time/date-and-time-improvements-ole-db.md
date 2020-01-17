---
title: 日付と時刻の強化機能 (OLE DB)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
author: MightyPen
ms.author: genemi
ms.custom: seo-dt-2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 35b7629b6c31da805c8284c7c1a7c80d561fe7e3
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095449"
---
# <a name="date-and-time-improvements-ole-db"></a>日付と時刻の強化機能 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では、新しい日付と時刻のデータ型が導入されています。 このセクションでは、これらの新しい型を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の拡張機能として公開する方法について説明します。 新しい日付と時刻のデータ型に対する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client のサポートの概要については、「[日付と時刻の機能強化](../../relational-databases/native-client/features/date-and-time-improvements.md)」を参照してください。 サンプルについては、「拡張された[日付/時刻&#40;機能の&#41;使用 OLE DB](../../relational-databases/native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)」を参照してください。  
  
 日付と時刻のデータ型に関する一般的な情報については、「 [datetime &#40;transact-sql&#41;](../../t-sql/data-types/datetime-transact-sql.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [OLE DB の日付/時刻の強化に対するデータ型のサポート](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の日付と時刻のデータ型をサポートする OLE DB ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client) の型に関する情報を提供します。  
  
 [メタ&#40;データ OLE DB&#41;](https://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
 **ICommandWithParameters:: GetParameterInfo**、 **ICommandWithParameters:: setparameterinfo**、 **IColumnsRowset:: GetColumnsRowset**、I DBBINDING**info:: GetColumnInfo に関する情報が含まれています。** . また、OLE DB スキーマ行セットの更新についても説明します。  
  
 [バインドと変換 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 既存の日付型と新しい日付型の両方を対象とした、サーバーとクライアント間における変換の規則について説明します。  
  
 [拡張された日付/時刻型&#40;OLE DB および ODBC の一括コピーの変更&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 一括コピー操作をサポートする日付または時刻の機能強化について説明します。  
  
 [OLE DB API による機能強化された日付と時刻のサポート](../../relational-databases/native-client-ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 機能強化された日付や時刻をサポートする OLE DB API について説明します。  
  
 [IRowsetFind での比較](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 日付/時刻型と**IRowsetFind**について説明します。  
  
 [以前の SQL Server バージョン&#40;を使用した新しい日付と時刻の機能 OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 機能強化された日付や時刻を使用するクライアント アプリケーションが以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と通信する場合、および以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client でコンパイルされたクライアントから、機能強化された日付や時刻をサポートするサーバーにコマンドを送信する場合に想定される動作について説明します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
