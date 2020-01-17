---
title: エラー メッセージ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], types
- ODBC error handling, message types
- errors [ODBC], types
ms.assetid: 46c0c22e-d105-4d5b-bb9d-5694472e8651
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b38734544ac3accb3ddfdbcae8ae92f67b252e54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62805856"
---
# <a name="error-messages"></a>エラー メッセージ
  によって返されるメッセージのテキスト、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で Native Client ODBC ドライバーが配置された、 *MessageText*パラメーターの**SQLGetDiagRec**します。 メッセージのヘッダーには、次のようにエラーの発生元が記載されます。  
  
 [Microsoft][ODBC Driver Manager]  
 このヘッダーに関連するエラーは、ODBC ドライバー マネージャーで発生しています。  
  
 [Microsoft][ODBC Cursor Library]  
 このヘッダーに関連するエラーは、ODBC カーソル ライブラリで発生しています。  
  
 [Microsoft][SQL Server Native Client]  
 によってこれらのエラーが発生する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバー。 Net-Library または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前が付いているノードが他にない場合、エラーはドライバー内で発生しています。  
  
 [Microsoft][SQL Server Native Client][*Net-transportname*]  
 によってこれらのエラーが発生する、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Net-library を場所*Net-transportname*の表示名には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]クライアント ネットワーク トランスポート (たとえば、名前付きパイプ、共有メモリ、TCP/IP ソケットの場合、または VIA など)。 エラー メッセージの残りの部分には、呼び出された Net-Library 関数と、TDS 関数から呼び出された基になるネットワーク API の関数が含まれています。 *PfNative*これらのエラーと共に返されたエラー コードは、基になるネットワーク プロトコル スタックのエラー コードです。  
  
 [Microsoft][SQL Server Native Client][[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]]  
 このヘッダーに関連するエラーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で発生しています。 エラー メッセージの残りの部分は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー メッセージのテキストです。 *PfNative*これらのエラーと共に返されるコードはエラー番号から[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 によって返されるエラー メッセージ (および番号) の一覧の詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、説明とエラー列の表示、 **sysmessages**システム テーブルに、**マスター**データベースの[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。  
  
## <a name="see-also"></a>関連項目  
 [エラーとメッセージの処理](handling-errors-and-messages.md)  
  
  
