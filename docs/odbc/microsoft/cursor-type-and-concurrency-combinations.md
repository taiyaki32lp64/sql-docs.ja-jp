---
title: カーソルの種類および同時実行の組み合わせ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], concurrency options
- cursors [ODBC], ODBC driver for Oracle
- concurrency options [ODBC]
- ODBC driver for Oracle [ODBC], cursor options
ms.assetid: db63d610-f86f-4029-9d66-fed616c8a818
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a29fc2d02cb46dda44fa22b2344cbab475443f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096526"
---
# <a name="cursor-type-and-concurrency-combinations"></a>カーソルの種類およびコンカレンシーの組み合わせ
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 カーソルの種類は、ユーザーに提供されたカーソルの機能を制御します。 同時実行オプションは、更新と結果セットのロック動作を制御します。  
  
|カーソルの種類|同時実行制御 (許可されている値)|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1]</sup>を参照してください[のキーセット ドリブン カーソルの使用に関する制限](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md)します。  
  
 <sup>[2]</sup> SQL_CONCUR_LOCK は SQL_AUTOCOMMIT 接続オプションが SQL_AUTOCOMMIT_OFF に設定されている場合にのみサポートされています。  
  
## <a name="see-also"></a>関連項目  
 [接続のオプション](../../odbc/microsoft/connect-options.md)
