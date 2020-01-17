---
title: OLE DB Driver for SQL Server のコンポーネント | Microsoft Docs
description: OLE DB Driver for SQL Server のコンポーネント
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 5a5124519bd95ec02e93a007d9881ec80814cfc8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989320"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>OLE DB Driver for SQL Server のコンポーネント
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 用の OLE DB ドライバーには、次のコンポーネントが含まれています。  

|コンポーネント|[説明]|  
|---------------|-----------------|  
|msoledbsql.dll|SQL Server 機能のすべての OLE DB ドライバーを含むダイナミックリンクライブラリ (DLL) ファイル。|  
|msoledbsqlr.rll|SQL Server ライブラリの OLE DB ドライバーに付随するリソースファイル。|   
|msoledbsql|SQL Server に OLE DB ドライバーを使用するために必要な新しい定義がすべて含まれている SQL Server ヘッダーファイルの OLE DB ドライバー。 このヘッダーファイルにより、sqloledb ヘッダーファイルが置き換えられます。<br /><br /> 注: msoledbsql と sqloledb は、最初に sqloledb が定義されていれば、同じプログラムで参照できます。|  
|msoledbsql.lib|SQL Server の OLE DB ドライバーの一部である[Opensqlfilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)関数を直接呼び出すために必要なライブラリファイル。<br /><br /> 注: プログラミング コードで msoledbsql.lib ファイルを参照する場合、使用しているコンピューターのシステム パス、およびアプリケーションを使用するユーザーのシステム パスに msoledbsql.dll ファイルが含まれることを確認する必要があります。|  

## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server を使用したアプリケーションの構築](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
