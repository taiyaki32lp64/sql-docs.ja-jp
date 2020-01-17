---
title: SQLSetPos の呼び出し |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], calling
- upgrading applications [ODBC], SQLSetPos
- backward compatibility [ODBC], SqlSetPos
- application upgrades [ODBC], SQLSetPos
ms.assetid: 846354b8-966c-4c2c-b32f-b0c8e649cedd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c64575777fc9210c36be5d417cd3def0c2c7102a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068683"
---
# <a name="calling-sqlsetpos"></a>SQLSetPos の呼び出し
ODBC で*2.x*、行の状態配列へのポインターが引数**SQLExtendedFetch**します。 行の状態配列への呼び出しによって更新された後で**SQLSetPos**します。 一部のドライバーがこの配列の間で変更しないという事実に依存していました**SQLExtendedFetch**と**SQLSetPos**します。 ODBC で*3.x*状態配列へのポインターは、記述子フィールド、および、そのため、変えることができます簡単に別の配列を指すようにします。 これは、とき、ODBC の問題となることができます*3.x* odbc アプリケーションが動作*2.x*ドライバーは呼び出すことが**SQLSetStmtAttr**配列状態のポインターを設定してを呼び出し、**SQLFetchScroll**データをフェッチします。 ドライバー マネージャーがへの呼び出しのシーケンスとしてマップ**SQLExtendedFetch**します。 次のコードでは、エラーは通常するときに発生ドライバー マネージャーは、2 つ目のマップ**SQLSetStmtAttr** ODBC を使用するときに呼び出す*2.x*ドライバー。  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 ODBC での行の状態のポインターを変更する方法がない場合、エラーが生成されます*2.x*呼び出しの間で**SQLExtendedFetch**します。 ODBC を使用する場合に、ドライバー マネージャーが、次の手順を実行する代わりに、 *2.x*ドライバー。  
  
1.  内部のドライバー マネージャーのフラグを初期化します*fSetPosError*を TRUE にします。  
  
2.  アプリケーションを呼び出すと**SQLFetchScroll**、ドライバー マネージャーの設定*fSetPosError*を FALSE にします。  
  
3.  アプリケーションを呼び出すと**SQLSetStmtAttr**ドライバー マネージャーを設定し、SQL_ATTR_ROW_STATUS_PTR を設定する*fSetPosError*と等しい値を True です。  
  
4.  アプリケーションを呼び出すと**SQLSetPos**で*fSetPosError* true の場合、ドライバー マネージャーと等しい SQLSTATE HY011 SQL_ERROR を発生させます (属性はここで設定することはできません) ことを示すアプリケーション呼び出すしようとしています。 **SQLSetPos**行の状態のポインターを変更した後は、呼び出す前に**SQLFetchScroll**します。
