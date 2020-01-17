---
title: 日付と時刻の強化 (OLE DB) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1dec9e1281d2ff61dcab9312cdf5a7ad1ecb8da3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62866839"
---
# <a name="date-and-time-improvements-ole-db"></a>日付と時刻の強化機能 (OLE DB)
  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では、新しい日付と時刻のデータ型が導入されています。 このセクションでは、拡張機能としてこれらの新しい型を公開する方法について説明します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client。 概要については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client、新しい日付と時刻のデータ型のサポートを参照してください[日付と時刻の強化](../native-client/features/date-and-time-improvements.md)します。 サンプルについては、次を参照してください。[使用の強化された日付と時刻の機能&#40;OLE DB&#41;](../native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md)します。  
  
 日付と時刻のデータ型についての一般的なは、次を参照してください。 [datetime &#40;TRANSACT-SQL&#41;](/sql/t-sql/data-types/datetime-transact-sql)します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [OLE DB の日付/時刻の強化に対するデータ型のサポート](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 OLE DB の概要情報を提供します ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client) をサポートする型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]日付と時刻のデータ型。  
  
 [メタデータ&#40;OLE DB&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
 DBBINDING 構造体、`ICommandWithParameters::GetParameterInfo`、`ICommandWithParameters::SetParameterInfo`、`IColumnsRowset::GetColumnsRowset`、および `ColumnsInfo::GetColumnInfo` について説明します。また、OLE DB スキーマ行セットの更新についても説明します。  
  
 [バインドと変換 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 既存の日付型と新しい日付型の両方を対象とした、サーバーとクライアント間における変換の規則について説明します。  
  
 [強化された日付と時刻型向けの一括コピー変更&#40;OLE DB および ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 一括コピー操作をサポートする日付または時刻の機能強化について説明します。  
  
 [OLE DB API による機能強化された日付と時刻のサポート](ole-db-api-support-for-date-and-time-enhancements.md)  
 機能強化された日付や時刻をサポートする OLE DB API について説明します。  
  
 [IRowsetFind での比較](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 日付型または時刻型、および `IRowsetFind` について説明します。  
  
 [新しい日付と時刻の機能を以前のバージョンの SQL Server で&#40;OLE DB&#41;](new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 機能強化された日付や時刻を使用するクライアント アプリケーションが以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と通信する場合、および以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client でコンパイルされたクライアントから、機能強化された日付や時刻をサポートするサーバーにコマンドを送信する場合に想定される動作について説明します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
