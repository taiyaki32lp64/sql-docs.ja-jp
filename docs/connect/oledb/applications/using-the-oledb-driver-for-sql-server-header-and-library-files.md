---
title: OLE DB Driver for SQL Server のヘッダーとライブラリ ファイルの使用 | Microsoft Docs
description: SQL Server ヘッダーとライブラリ ファイルでの OLE DB ドライバーの使用
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- header files [OLE DB Driver for SQL Server]
- MSOLEDBSQL, header files
- OLE DB, header files
- library files [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, header files
- data access [OLE DB Driver for SQL Server], header files
- data access [OLE DB Driver for SQL Server], library files
- OLE DB Driver for SQL Server, library files
- MSOLEDBSQL, library files
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 93b906a0604772fe224b1e63eaf6eed9eb8af983
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989233"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>SQL Server ヘッダーとライブラリ ファイルでの OLE DB ドライバーの使用
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server ヘッダーファイルとライブラリファイルの OLE DB ドライバーは、インストールプロセス中に [OLE DB Driver for SQL Server SDK] オプションを選択したときにインストールされます。 アプリケーションを開発するときは、開発に必要なすべてのファイルを開発環境にコピーしてインストールすることが重要です。 SQL Server 用 OLE DB ドライバーのインストールと再配布の詳細については、「 [SQL Server の OLE DB ドライバーのインストール](../../oledb/applications/installing-oledb-driver-for-sql-server.md)」を参照してください。  
  
 SQL Server ヘッダーファイルとライブラリファイルの OLE DB ドライバーは、次の場所にインストールされます。  
  
 *%PROGRAM FILES%* \Microsoft SQL Server\Client SDK\OLEDB\182\SDK  
  
 SQL Server ヘッダーファイル (msoledbsql) の OLE DB ドライバーを使用して、カスタムアプリケーションに SQL Server データアクセス機能用の OLE DB ドライバーを追加できます。 OLE DB Driver for SQL Server ヘッダー ファイルには、[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] で導入された新しい機能を使用するために必要なすべての定義、属性、プロパティ、およびインターフェイスが含まれています。  
  
 SQL Server ヘッダーファイルの OLE DB ドライバーに加えて、msoledbsql ライブラリファイルもあります。これは、 [Opensqlfilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)機能のエクスポートライブラリです。  
  
 OLE DB Driver for SQL Server ヘッダー ファイルは、MDAC (Microsoft Data Access Components) と共に使用する sqloledb.h ヘッダー ファイルに対して下位互換性がありますが、SQLOLEDB (MDAC 付属の OLE DB provider for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) の CLSID や (OLE DB Driver for SQL Server でサポートされない) XML 機能のシンボルは含まれていません。    
  
 SQL Server の OLE DB ドライバーを使用する OLE DB アプリケーションは、msoledbsql を参照するだけでよいです。 1 つのアプリケーションで MDAC (SQLOLEDB) と OLE DB Driver for SQL Server の両方を使用する場合、sqloledb.h と msoledbsql.h の両方を参照できますが、sqloledb.h を先に参照する必要があります。  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>SQL Server ヘッダーファイルに OLE DB ドライバーを使用する  
 SQL Server ヘッダーファイルに OLE DB ドライバーを使用するには、C/  C++プログラミングコード内で **include** ステートメントを使用する必要があります。 以下のセクションでは、OLE DB アプリケーションでの実行方法について説明します。  
  
> [!NOTE]  
>  SQL Server ヘッダーファイルとライブラリファイルの OLE DB ドライバーは、Visual Studio C++ 2012 以降を使用してのみコンパイルできます。  
  
### <a name="ole-db"></a>OLE DB (OLE DB)  
 OLE DB アプリケーションで SQL Server ヘッダーファイルの OLE DB ドライバーを使用するには、次のプログラミングコード行を使用します。  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  アプリケーションに sqloledb の**include**ステートメントが含まれている場合は、msoledbsql の**include**ステートメントをその後に記述する必要があります。  
  
 OLE DB Driver for SQL Server を使用してデータソースへの接続を作成する場合は、プロバイダー名の文字列として "MSOLEDBSQL" を使用します。  

  
## <a name="component-names-and-properties-by-version"></a>各バージョンのコンポーネント名とプロパティ  

|プロパティ|OLE DB Driver for SQL Server|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|OLE DB ヘッダー ファイル名|msoledbsql|Sqloledb.h|  
|OLE DB プロバイダー DLL|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>静的リンクと BCP 関数  
 BCP 関数を使用するアプリケーションでは、アプリケーションのコンパイルに使用されたヘッダー ファイルおよびライブラリに付属するのと同じバージョンのドライバーを接続文字列で指定することが重要です。  
  
 詳細については、「[一括コピー操作](../../oledb/features/performing-bulk-copy-operations.md)の実行」を参照してください。  
  
## <a name="see-also"></a>参照  
 [OLE DB Driver for SQL Server を使用したアプリケーションの構築](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
