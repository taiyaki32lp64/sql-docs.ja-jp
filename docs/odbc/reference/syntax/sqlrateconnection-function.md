---
title: SQLRateConnection 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 74d7e2c52167682f0993006db3a1125ca741cf35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053640"
---
# <a name="sqlrateconnection-function"></a>SQLRateConnection 関数
**準拠**  
 バージョンが導入されました。ODBC 3.81 規格に準拠します。ODBC  
  
 **概要**  
 **SQLRateConnection**ドライバーが接続プール内の既存の接続を再利用できるかどうかを決定します。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>引数  
 *hRequest*  
 [入力]新しいアプリケーションの接続要求を表すトークンのハンドル。  
  
 *hCandidateConnection*  
 [入力]接続プール内の既存の接続。 接続は開いた状態である必要があります。  
  
 *fRequiredTransactionEnlistment*  
 [入力]TRUE の場合は、既存の接続を再利用*hCandidateConnection*の新しい接続要求 (*hRequest*) 追加の参加が必要です。  
  
 *transId*  
 [入力]場合*fRequiredTransactionEnlistment*が true の場合、 *transId*要求が登録されている DTC トランザクションを表します。 場合*fRequiredTransactionEnlistment* false で、 *transId*は無視されます。  
  
 *pRating*  
 [出力]*hCandidateConnection*のレーティングが再利用、 *hRequest*します。 この評価は、0 から 100 (包括) の間になります。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ドライバー マネージャーは、この関数から返される診断情報を処理しません。  
  
## <a name="remarks"></a>コメント  
 **SQLRateConnection** 0 ~ 100 (包括) の既存の接続が要求に一致する度合いを示すスコアを生成します。  
  
|[スコア]|(ときに関係なく SQL_SUCCESS が返されます) の意味|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection*の再利用する必要があります、 *hRequest*します。|  
|任意の値 1 および 98 (包括)|スコアが高い、近くを*hCandidateConnection*と一致*hRequest*します。|  
|99|意味のない属性には、のみの不一致があります。  ドライバー マネージャーは、評価ループを停止する必要があります。|  
|100|完全に一致します。  ドライバー マネージャーは、評価ループを停止する必要があります。|  
|100 を超えるその他の値|*hCandidateConnection*は配信不能としないを再利用するも、今後の接続要求とマークします。|  
  
 リターン コードが (SQL_SUCCESS_WITH_INFO を含む) に関係なく SQL_SUCCESS 以外または評価が 100 より大きい場合、ドライバー マネージャーは配信不能としての接続をマークします。 で配信不能の接続 (以降の接続要求) であっても再利用しないと最終的にタイムアウトする CPTimeout 経過した後。 ドライバー マネージャーでは、引き続きレートに、プールから別の接続を検索します。  
  
 ドライバー マネージャーは、の点数が 100 (99 を含む) より厳密に小さい接続を再利用、ドライバー マネージャーは、アプリケーションによって要求された状態に戻す接続をリセットする SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN) を呼び出します。 ドライバーでは、この関数の呼び出しで接続をリセットする必要がありますされません。  
  
 場合*fRequiredTransactionEnlistment*場合は TRUE、再利用が*hCandidateConnection*余分な参加リストを必要があります (*transId* ! = NULL)、または参加解除 (*transId* NULL = =)。 これは、接続と、ドライバーの参加/接続を再利用する場合、接続の参加を解除する必要があるかどうかを再利用のコストを示します。 場合*fRequireTransactionEnlistment* false で、ドライバーの値は無視する必要があります*transId*します。  
  
 ドライバー マネージャーは、保証のハンドルを HENV 親*hRequest*と*hCandidateConnection*は同じです。 ドライバー マネージャーは、プール ID に関連付けられたことが保証されます*hRequest*と*hCandidateConnection*は同じです。  
  
 アプリケーションでは、この関数を直接呼び出さないでください。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ODBC ドライバーの開発の sqlspi.h が含まれます。  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
