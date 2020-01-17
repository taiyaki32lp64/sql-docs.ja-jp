---
title: SQL Server Native Client を使用する場合 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
ms.assetid: 08f18b36-209d-4cf7-9623-ebc61859a91d
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b8d956d8e27a9511e5f9d6cb2ee555110210760
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73759460"
---
# <a name="when-to-use-sql-server-native-client"></a>SQL Server Native Client を使用する場合
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのデータにアクセスする際に使用できるテクノロジの 1 つです。  各種データ アクセス テクノロジの詳細については、「[データ アクセス テクノロジのロードマップ](https://go.microsoft.com/fwlink/?LinkID=179186)」を参照してください。  
  
 アプリケーションのデータ アクセス テクノロジとして [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client を使用するかどうかを決める場合は、いくつかの要素を検討する必要があります。  
  
 新しいアプリケーションで、Microsoft Visual C# や Visual Basic などのマネージド プログラミング言語を使用しており、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新機能にアクセスする必要がある場合は、.NET Framework に含まれている .NET Framework Data Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用する必要があります。  
  
 COM ベースのアプリケーションを開発しており、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で導入された新機能にアクセスする必要がある場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client を使用する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新機能にアクセスする必要がない場合は、引き続き Windows Data Access Components (WDAC) を使用できます。  
  
 既存の OLE DB アプリケーションや ODBC アプリケーションの場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新機能にアクセスする必要があるかどうかが重要な問題になります。 アプリケーションが既に完成していて、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新機能を必要としない場合は、引き続き WDAC を使用できます。 ただし、 [xml データ型](../../t-sql/xml/xml-transact-sql.md)などの新機能にアクセスする必要がある場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client を使用する必要があります。  
  
 行のバージョン管理機能を使用した Read Committed トランザクション分離は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client と MDAC の両方でサポートされていますが、スナップショット トランザクション分離は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client のみでサポートされています (プログラミング用語では、"行のバージョン管理機能を使用した Read Committed トランザクション分離" は "Read Committed トランザクション" と同義です)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client と MDAC の違いについては、「 [mdac から SQL Server Native Client するようにアプリケーションを更新する](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client プログラミング](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [ODBC の操作方法に関するトピック](../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [OLE DB の使用法に関するトピック](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
