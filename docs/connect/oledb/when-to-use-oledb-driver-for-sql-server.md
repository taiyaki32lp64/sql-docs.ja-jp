---
title: OLE DB Driver for SQL Server をいつ使用するか | Microsoft Docs
description: OLE DB Driver for SQL Server をいつ使用するか
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 74bd79c24b913cd3c3d2f782b77cf2bb4c23e397
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015192"
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server をいつ使用するか
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  SQL Server 用の OLE DB ドライバーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベース内のデータにアクセスするために使用できる1つのテクノロジです。  各種データ アクセス テクノロジの詳細については、「[データ アクセス テクノロジのロードマップ](https://go.microsoft.com/fwlink/?LinkID=179186)」を参照してください。  
  
 アプリケーションのデータ アクセス テクノロジとして OLE DB Driver for SQL Server を使用するかどうかを決める場合は、いくつかの要素を検討する必要があります。  
  
 新しいアプリケーションで、Microsoft Visual C# や Visual Basic などのマネージド プログラミング言語を使用しており、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新機能にアクセスする必要がある場合は、.NET Framework に含まれている .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用する必要があります。  
  
 COM ベースのアプリケーションを開発しており、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で導入された新機能にアクセスする必要がある場合は、OLE DB Driver for SQL Server を使用する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新機能にアクセスする必要がない場合は、引き続き Windows Data Access Components (WDAC) を使用できます。  
  
 既存の OLE DB アプリケーションの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新機能にアクセスする必要があるかどうかが重要な問題になります。 アプリケーションが既に完成していて、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新機能を必要としない場合は、引き続き WDAC を使用できます。 ただし、[xml データ型](../../t-sql/xml/xml-transact-sql.md)などの新機能にアクセスする必要がある場合は、OLE DB Driver for SQL Server を使用する必要があります。  
  
 SQL Server と MDAC 用の OLE DB ドライバーはどちらも、行のバージョン管理を使用した read committed トランザクション分離をサポートしますが、スナップショットトランザクション分離をサポートしているのは、SQL Server の OLE DB ドライバーだけです。 (プログラミング用語では、"行のバージョン管理機能を使用した Read Committed トランザクション分離" は "Read Committed トランザクション" と同義です)。  
  
 SQL Server と MDAC の OLE DB ドライバーの違いについては、「 [mdac から SQL Server の OLE DB ドライバーへのアプリケーションの更新](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server](../oledb/oledb-driver-for-sql-server.md)     
 [OLE DB の使用法に関するトピック](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
