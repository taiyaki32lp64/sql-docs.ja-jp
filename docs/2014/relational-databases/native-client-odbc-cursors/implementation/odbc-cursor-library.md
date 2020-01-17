---
title: ODBC カーソル ライブラリ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 9b81a7871434691a5940a04c7c60aaad9254b645
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63201165"
---
# <a name="odbc-cursor-library"></a>ODBC カーソル ライブラリ
  一部の ODBC ドライバーは、既定のカーソル設定しかサポートします。これらのドライバーもサポートされません、カーソルの位置指定操作など**SQLSetPos**します。 ODBC カーソル ライブラリは、通常はブロック カーソルや静的カーソルがサポートされないドライバーに対して、これらのカーソルを実装するときに使用される MDAC (Microsoft Data Access Components) のコンポーネントです。 カーソル ライブラリは、位置指定の UPDATE および DELETE ステートメントも実装し、 **SQLSetPos**カーソルが作成されます。  
  
 ODBC カーソル ライブラリは、ODBC ドライバー マネージャーと ODBC ドライバーの中間層として実装されます。 ODBC ドライバー マネージャーは、ODBC カーソル ライブラリが読み込まれると、すべてのカーソル関連コマンドをドライバーではなく、読み込んだカーソル ライブラリにルーティングします。 カーソル ライブラリでは、基になるドライバーから結果セット全体をフェッチし、その結果セットをクライアントにキャッシュすることにより、カーソルを実装します。 ODBC カーソル ライブラリを使用しているときは、アプリケーションではカーソル ライブラリのカーソル機能だけをサポートし、基になるドライバーの追加のカーソル機能はサポートしません。  
  
 ODBC カーソル ライブラリを使用する必要はほとんどありません、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバー、ドライバー自体には、ODBC カーソル ライブラリよりも多くのカーソル機能がサポートされているためです。 ODBC カーソル ライブラリを使用する唯一の理由、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーはドライバーがサーバー カーソル、カーソルのサポートを実装するためにサーバー カーソルはすべての SQL ステートメントをサポートしていません。 ストアド プロシージャ、バッチ、または COMPUTE、COMPUTE BY、FOR BROWSE、INTO などを含む SQL ステートメントで静的カーソルを使用する必要がある場合は、ODBC カーソル ライブラリの使用を検討してください。 ただし、カーソル ライブラリを使用する場合、結果セット全体がクライアントにキャッシュされるので、大量のメモリが使用され、パフォーマンスが低下することがあるので注意が必要です。  
  
 アプリケーションを使用して接続の接続によってごとに、カーソル ライブラリを呼び出します[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)データ ソースに接続する前に SQL_ATTR_ODBC_CURSORS 接続属性を設定します。 SQL_ATTR_ODBC_CURSORS には、次の 3 つの値のいずれかを設定します。  
  
 SQL_CUR_USE_ODBC  
 このオプションを設定すると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、ODBC カーソル ライブラリよりも優先、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーのネイティブ カーソル サポートします。 接続で使用できるのは、カーソル ライブラリでサポートされているカーソルのみで、サーバー カーソルは使用できません。  
  
 SQL_CUR_USE_DRIVER  
 カーソルのすべてをサポートするネイティブこのオプションが設定されている場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、接続に使用することができます。 この場合、ODBC カーソル ライブラリは使用できません。 すべてのカーソルはサーバー カーソルとして実装されます。  
  
 SQL_CUR_USE_IF_NEEDED  
 SQL_CUR_USE_DRIVER で使用する場合と同じ効果は、このオプションが設定されている場合、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバー。 接続時に、ODBC ドライバー マネージャーのテストに接続されている ODBC ドライバーの SQL_FETCH_PRIOR オプションでサポートされているかどうかに[SQLFetchScroll](../../native-client-odbc-api/sqlfetchscroll.md)します。 ドライバーでこのオプションがサポートされていない場合、ODBC ドライバー マネージャーは ODBC カーソル ライブラリを読み込みます。 サポートされている場合、ODBC ドライバー マネージャーは ODBC カーソル ライブラリを読み込みません。この場合、アプリケーションではドライバーのネイティブ サポートが使用されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーには SQL_FETCH_PRIOR がサポートしている、ODBC ドライバー マネージャーは ODBC カーソル ライブラリを読み込みません。  
  
 カーソル ライブラリにより、アプリケーションはスクロール可能なカーソルや更新可能なカーソルを使用できるだけでなく、1 つの接続に対して複数のアクティブ ステートメントを使用できます。 この機能をサポートする場合は、カーソル ライブラリを読み込む必要があります。 使用[SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)カーソル ライブラリの使用方法を指定し、 [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md)カーソルの種類、同時実行性、および行セットのサイズを指定します。  
  
## <a name="see-also"></a>参照  
 [カーソルの実装方法](how-cursors-are-implemented.md)  
  
  
