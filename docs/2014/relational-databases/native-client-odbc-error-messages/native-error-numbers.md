---
title: ネイティブ エラー番号 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC error handling, native error numbers
- SQL Server Native Client ODBC driver, errors
- native error numbers [SQL Server Native Client]
- messages [ODBC], native error numbers
- errors [ODBC], native error numbers
ms.assetid: 77cbc826-f47f-4803-8e7a-223d6df069b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e7cd24a3eb1ccdeea1b6e6cbb97e2d0f222193f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63223497"
---
# <a name="native-error-numbers"></a>ネイティブ エラー番号
  データ ソースで発生するエラー (によって返される[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーによって返されたネイティブ エラー番号を返します[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 ドライバーで検出されたエラー、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、ネイティブ エラー番号は 0 を返します。 ネイティブ エラー番号の一覧については、のエラー列を参照して、 **sysmessages**システム テーブルに、**マスター**データベース[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
 状態エラー コードについては、次を参照してください。 [SQLSTATE &#40;ODBC エラー コード&#41;](sqlstate-odbc-error-codes.md)します。 Net-Library から返されたエラーについては、ネイティブ エラー番号は基になるネットワーク ソフトウェアから返されます。  
  
## <a name="see-also"></a>参照  
 [エラーとメッセージの処理](handling-errors-and-messages.md)  
  
  
