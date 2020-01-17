---
title: SQLSetScrollOptions 関数 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 77a85caefadb54c3db2716c4db18b504e02da996
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342941"
---
# <a name="sqlsetscrolloptions-function"></a>SQLSetScrollOptions 関数
**互換性**  
 導入されたバージョン:ODBC 1.0 標準準拠:非推奨  
  
 **概要**  
 *Odbc 3.x*では、odbc 2.0 関数**SQLSetScrollOptions**は**SQLGetInfo**と**SQLSetStmtAttr**の呼び出しに置き換えられています。  
  
> [!NOTE]
>  Odbc *2.x アプリケーションが*odbc *2.x ドライバーで*動作しているときに、ドライバーマネージャーがこの関数をマップする方法の詳細については[、「付録](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)G:旧バージョンとの互換性のためのドライバーガイドライン。  
> 
> [!NOTE]
>  ドライバーマネージャーが、 **SQLSetScrollOptions**をサポートしていない ODBC 3.x ドライバーを使用しているアプリケーションの**SQLSetScrollOptions**をマップする場合、ドライバーマネージャーは SQL_ATTR_ROW_ ではなく SQL_ROWSET_SIZE ステートメントオプションを設定し*ます。* ARRAY_SIZE statement 属性を**SQLSetScrollOption**の*RowsetSize*引数に指定します。 結果として、 **Sqlfetch**または**sqlfetchscroll**の呼び出しによって複数の行をフェッチするときに、アプリケーションで**SQLSetScrollOptions**を使用することはできません。 **SQLExtendedFetch**の呼び出しによって複数の行をフェッチする場合にのみ使用できます。  
  
## <a name="remarks"></a>コメント  
 アプリケーションが64ビットオペレーティングシステムで実行される場合は、「 [ODBC 64 ビット情報](../../../odbc/reference/odbc-64-bit-information.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
