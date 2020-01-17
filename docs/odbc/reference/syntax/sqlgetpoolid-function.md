---
title: SQLGetPoolID 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7daef4785a77df294a831d69089108cbb1d88489
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061483"
---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID 関数
**準拠**  
 バージョンが導入されました。ODBC 3.81 規格に準拠します。ODBC  
  
 **概要**  
 **SQLGetPoolID**プール ID を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>引数  
 *hDbcInfoToken*  
 [入力]すべての接続情報を含むトークン ハンドル。  
  
 *pPoolID*  
 [出力]プール ID は、同じ意味で使用できる接続のセットを特定するために使用 (追加のリセットが必要な可能性があります)。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ときに**SQLGetPoolID**返します SQL_ERROR または SQL_SUCCESS_WITH_INFO、ドライバー マネージャーを使用して、 **HandleType** SQL_HANDLE_DBC_INFO_TOKEN の**処理**の*hDbcInfoToken*します。  
  
## <a name="remarks"></a>コメント  
 **SQLGetPoolID**一連の接続情報を指定されたプールの ID を取得するために使用 (から**SQLSetConnectAttrForDbcInfo**、 **SQLSetDriverConnectInfo**、および**SQLSetConnectInfo**)。 このプールを置き換えて使用できる接続のセットを識別する ID を使用 (追加のリセットが必要な可能性があります)。 プール ID がそのグループの接続の接続プールを識別するために使用されます。  
  
 ドライバー マネージャーが、アプリケーションにエラーを返します、ドライバーが SQL_ERROR または SQL_INVALID_HANDLE を返すたびに (で[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)または[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 ドライバー マネージャーがから診断情報を取得するたびに、ドライバーは SQL_SUCCESS_WITH_INFO を返します、 *hDbcInfoToken*でアプリケーションに SQL_SUCCESS_WITH_INFO を返すと[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)と[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)します。  
  
 アプリケーションでは、この関数を直接呼び出さないでください。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ODBC ドライバーの開発の sqlspi.h が含まれます。  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
