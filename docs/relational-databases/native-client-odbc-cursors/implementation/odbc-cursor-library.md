---
title: ODBC カーソルライブラリ |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], library
- SQL_CUR_USE_DRIVER option
- ODBC applications, cursors
- ODBC cursors, library
- SQL_CUR_USE_IF_NEEDED option
- SQLSetConnectAttr function
- SQL_CUR_USE_ODBC option
ms.assetid: 3c610d3d-6e06-49cf-9a40-05b6a1c83a32
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eeaef25c0a7c1d09ca3ee52cee2783275aa6133e
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784721"
---
# <a name="odbc-cursor-library"></a>ODBC カーソル ライブラリ
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  一部の ODBC ドライバーでは、既定のカーソル設定のみがサポートされています。これらのドライバーは、 **SQLSetPos**などの位置指定カーソル操作もサポートしていません。 ODBC カーソル ライブラリは、通常はブロック カーソルや静的カーソルがサポートされないドライバーに対して、これらのカーソルを実装するときに使用される MDAC (Microsoft Data Access Components) のコンポーネントです。 カーソルライブラリでは、位置指定の UPDATE および DELETE ステートメントと、作成するカーソルの**SQLSetPos**も実装されています。  
  
 ODBC カーソル ライブラリは、ODBC ドライバー マネージャーと ODBC ドライバーの中間層として実装されます。 ODBC ドライバー マネージャーは、ODBC カーソル ライブラリが読み込まれると、すべてのカーソル関連コマンドをドライバーではなく、読み込んだカーソル ライブラリにルーティングします。 カーソル ライブラリでは、基になるドライバーから結果セット全体をフェッチし、その結果セットをクライアントにキャッシュすることにより、カーソルを実装します。 ODBC カーソル ライブラリを使用しているときは、アプリケーションではカーソル ライブラリのカーソル機能だけをサポートし、基になるドライバーの追加のカーソル機能はサポートしません。  
  
 Odbc カーソルライブラリよりも多くのカーソル機能がサポートされているため、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーと共に ODBC カーソルライブラリを使用する必要はほとんどありません。 ODBC カーソルライブラリを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーと共に使用する唯一の理由は、ドライバーがサーバーカーソルを介してカーソルサポートを実装しており、サーバーカーソルがすべての SQL ステートメントをサポートしていないためです。 ストアド プロシージャ、バッチ、または COMPUTE、COMPUTE BY、FOR BROWSE、INTO などを含む SQL ステートメントで静的カーソルを使用する必要がある場合は、ODBC カーソル ライブラリの使用を検討してください。 ただし、カーソル ライブラリを使用する場合、結果セット全体がクライアントにキャッシュされるので、大量のメモリが使用され、パフォーマンスが低下することがあるので注意が必要です。  
  
 アプリケーションでは、データソースに接続する前に[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)を使用して接続属性を SQL_ATTR_ODBC_CURSORS 設定することによって、接続ごとにカーソルライブラリを呼び出します。 SQL_ATTR_ODBC_CURSORS には、次の 3 つの値のいずれかを設定します。  
  
 SQL_CUR_USE_ODBC  
 このオプションが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーで設定されている場合、ODBC カーソルライブラリは、Native Client ODBC ドライバーのネイティブカーソルのサポート [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] よりも優先されます。 接続で使用できるのは、カーソル ライブラリでサポートされているカーソルのみで、サーバー カーソルは使用できません。  
  
 SQL_CUR_USE_DRIVER  
 このオプションを設定すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーにネイティブでサポートされているすべてのカーソルを接続に使用できます。 この場合、ODBC カーソル ライブラリは使用できません。 すべてのカーソルはサーバー カーソルとして実装されます。  
  
 SQL_CUR_USE_IF_NEEDED  
 このオプションを設定すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーと共に使用した場合と同じ効果が SQL_CUR_USE_DRIVER と同じになります。 ODBC ドライバーマネージャーは、接続時に、接続されている ODBC ドライバーが[Sqlfetchscroll](../../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)の SQL_FETCH_PRIOR オプションをサポートしているかどうかをテストします。 ドライバーでこのオプションがサポートされていない場合、ODBC ドライバー マネージャーは ODBC カーソル ライブラリを読み込みます。 サポートされている場合、ODBC ドライバー マネージャーは ODBC カーソル ライブラリを読み込みません。この場合、アプリケーションではドライバーのネイティブ サポートが使用されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは SQL_FETCH_PRIOR がサポートされているので、odbc ドライバーマネージャーは ODBC カーソルライブラリを読み込みません。  
  
 カーソル ライブラリにより、アプリケーションはスクロール可能なカーソルや更新可能なカーソルを使用できるだけでなく、1 つの接続に対して複数のアクティブ ステートメントを使用できます。 この機能をサポートする場合は、カーソル ライブラリを読み込む必要があります。 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)を使用して、カーソルライブラリの使用方法を指定し、 [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)を使用してカーソルの種類、同時実行、および行セットのサイズを指定します。  
  
## <a name="see-also"></a>参照  
 [カーソルの実装方法](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
