---
title: 次のフェッチ位置 |Microsoft Docs
description: 行のフェッチ - 次のフェッチ位置
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2ea743770323505c611210c0bb3acd0e93c719cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994191"
---
# <a name="fetching-rows---next-fetch-position"></a>行のフェッチ - 次のフェッチ位置
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server は次のフェッチ位置を追跡します。その結果、**GetNextRows** メソッドの一連の呼び出しでは、行をスキップしたり、同じ行を繰り返すことなく、行セット全体が読み取られます。この場合、この一連の呼び出しの間に、スキップされたり、読み取る方向が変更されたり、**FindNextRow**、**Seek**、または **RestartPosition** の各メソッドの呼び出しによって中断されることはありません。 **IRowset::GetNextRows**、**IRowset::RestartPosition**、または **IRowsetIndex::Seek** を呼び出すか、*pBookmark* 値に NULL を指定して **FindNextRow** を呼び出すことにより、次のフェッチ位置が変更されます。 *pBookmark* 値に NULL 以外の値を指定して **FindNextRow** を呼び出しても、次のフェッチ位置には影響しません。  
  
## <a name="see-also"></a>参照  
 [行のフェッチ](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
