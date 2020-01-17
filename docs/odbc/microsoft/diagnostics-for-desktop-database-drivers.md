---
title: 診断をデスクトップ データベース ドライバー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], diagnostic information
- desktop database drivers [ODBC], diagnostic information
- ODBC desktop database drivers [ODBC], diagnostic information
- diagnostic information [ODBC], desktop database drivers
ms.assetid: 1c3740eb-62c6-4009-b4b2-570fcf5661e4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4e7c8ea96708886f9edf54047bd2a2104ba0ec8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031220"
---
# <a name="diagnostics-for-desktop-database-drivers"></a>デスクトップ データベース ドライバーの診断
すべてのエラーと警告をチェックするか、ドライバー マネージャーによってを部分的にチェックされませんが、ドライバーによって処理されます。 ドライバーにもマップ ネイティブ エラー、またはエラー SQLSTATEs に、データ ソースによって返されます。 記載の各関数、 *ODBC プログラマ リファレンス*条件とメッセージを指定する「診断」セクションが含まれています。  
  
 アプリケーション呼び出し**SQLGetDiagRec** SQLSTATE、ネイティブ エラー コード、および診断メッセージを取得します。 呼び出す**SQLGetDiagField**とフィールドを指定するには、個々 の診断フィールドを取得します。 診断の識別子のサポート レベルは、次の表に表示されます。  
  
|DiagIdentifiers|サポート レベル|  
|---------------------|-------------------|  
|SQL_DIA_DYNAMIC_FUNCTION|サポートされていません|  
|SQL_DIAG_CLASS_ORIGIN|サポートされています。 常に"ODBC 3.0"のバージョン 3.0 と以降のこのドライバー。|  
|SQL_DIAG_COLUMN_NUMBER|Supported|  
|SQL_DIAG_CURSOR_ROW_COUNT|サポートされていません|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|サポートされていません|  
|SQL_DIAG_MESSAGE_TEXT|Supported|  
|SQL_DIAG_NATIVE|Supported|  
|SQL_DIAG_NUMBER|Supported|  
|SQL_DIAG_RETURNCODE|サポートされているドライバー マネージャーによって実装されているが|  
|SQL_DIAG_ROW_COUNT|Supported|  
|SQL_DIAG_ROW_NUMBER|Supported|  
|SQL_DIAG_SERVER_NAME|サポートされていません|  
|SQL_DIAG_SQLSTATE|Supported|  
|SQL_DIAG_SUBCLASS_ORIGIN|Supported|
