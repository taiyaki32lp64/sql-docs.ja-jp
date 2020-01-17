---
title: SQLGetConnectOption 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7461304a9aa015eac223dc726e669ad5c4ecd4ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103832"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。非推奨  
  
 **概要**  
 ODBC で*3.x*、ODBC *2.x*関数**SQLGetConnectOption**置き換わりました**SQLGetConnectAttr**します。 詳細については、次を参照してください。 [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)します。  
  
> [!NOTE]
>  どのようなドライバー マネージャーは、ときに、マッピングするには、この関数、ODBC の詳細については*2.x* odbc アプリケーションが動作*3.x*ドライバーを参照してください[非推奨の関数のマッピング](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)付録 g:旧バージョンとの互換性のためのガイドラインをドライバーです。  
> 
> [!NOTE]
>  ODBC 3.8 に導入された SQL_ASYNC_DBC_FUNCTION_ENABLE 属性でサポートされていない**SQLGetConnectOption**します。 接続ハンドルに対して非同期操作を使用するアプリケーションを使用する必要があります**SQLGetConnectAttr**します。  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
