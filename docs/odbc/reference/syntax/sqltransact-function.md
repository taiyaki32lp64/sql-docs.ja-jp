---
title: SQLTransact 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTransact
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTransact
helpviewer_keywords:
- SQLTransact function [ODBC]
ms.assetid: 496249e0-8eff-4c60-8358-5543bc3ead9c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c96c903b68dee2d1d215804d318d47b4c39a7a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039499"
---
# <a name="sqltransact-function"></a>SQLTransact 関数
**準拠**  
 バージョンが導入されました。ODBC 1.0 規格に準拠します。非推奨  
  
 **概要**  
 ODBC で*3.x*、ODBC *2.x*関数**SQLTransact**置き換わりました**SQLEndTran**します。 詳細については、次を参照してください。 [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)します。  
  
> [!NOTE]  
>  ODBC 3.8 にで導入された、SQL_ASYNC_DBC_FUNCTION_ENABLE 属性がサポートされていない**SQLTransact**します。 接続ハンドルでの非同期操作を使用してアプリケーションを使用する必要があります**SQLEndTran**します。  
  
## <a name="see-also"></a>参照  
 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC ヘッダー ファイル](../../../odbc/reference/install/odbc-header-files.md)
