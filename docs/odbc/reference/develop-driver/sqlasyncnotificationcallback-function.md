---
title: SQLAsyncNotificationCallback 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c56aedc9-f7f7-4641-b605-f0f98ed4400c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 96073b8d5e68d10caaff268aae4c5af60554ef76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915543"
---
# <a name="sqlasyncnotificationcallback-function"></a>SQLAsyncNotificationCallback 関数
**準拠**  
 バージョンが導入されました。ODBC 3.8  
  
 標準への準拠:なし  
  
 **概要**  
 **SQLAsyncNotificationCallback**ドライバーに SQL_STILL_EXECUTING が返された後に、現在の非同期操作のいくつかの進行状況がある場合に、ドライバー マネージャーをコールバックするためのドライバーを使用します。 **SQLAsyncNotificationCallback**だけで、ドライバーによって呼び出されることができます。  
  
 ドライバーは呼び出さないでください**SQLAsyncNotificationCallback**関数の名前を持つ**SQLAsyncNotificationCallback**します。 代わりに、ドライバー マネージャーは、関数のポインターを渡しますドライバーに対応する接続ハンドルまたはステートメントのハンドルの SQL_ATTR_ASYNC_DBC_NOTIFICATION_CALLBACK または SQL_ATTR_ASYNC_STMT_NOTIFICATION_CALLBACK 属性の値としてそれぞれします。 別のハンドルには、別の関数ポインターの値を割り当てることができます。 関数ポインターの型は、SQL_ASYNC_NOTIFICATION_CALLBACK として定義されます。  
  
 **SQLAsyncNotificationCallback**スレッド セーフです。 複数のスレッドの呼び出しを使用するドライバーを選択できます**SQLAsyncNotificationCallback**でさまざまな処理に同時にします。  
  
## <a name="syntax"></a>構文  
  
```  
typedef SQLRETURN (SQL_API *SQL_ASYNC_NOTIFICATION_CALLBACK)(  
   SQLPOINTER pContex,   
   BOOL fLast);  
```  
  
## <a name="arguments"></a>引数  
 *pContex*  
 ドライバー マネージャーによって定義されているデータ構造体へのポインター。 値は、SQLSetConnectAttr(SQL_ATTR_ASYNC_DBC_NOTIFICATION_CONTEXT) または SQLSetStmtAttr(SQL_ATTR_ASYNC_STMT_NOTIFICATION_CONTEXT) を使用して、ドライバーに渡されます。  ドライバーでは、値へのアクセスはありません。  
  
 *fLast*  
 ドライバーを使用すると、このコールバック関数の呼び出しが、現在の非同期操作の最後の 1 つであることを示します。 ドライバー マネージャーがもう一度、関数を呼び出すときに、ドライバーは SQL_STILL_EXECUTING 以外のリターン コードを返します。 ドライバー マネージャーは、事前に、アプリケーションは、非同期操作の完了を通知するために、この情報を使用できます。  
  
 場合*処理*で指定された型の有効なハンドルではありません*HandleType*、 **SQLCancelHandle** SQL_INVALID_HANDLE が返されます。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS や SQL_ERROR します。  
  
## <a name="diagnostics"></a>診断  
 **SQLAsyncNotificationCallback** SQL_ERROR を (ドライバーまたはドライバー マネージャーでの実装の問題を示します次の 2 つの状況に戻すことができます。  
  
|Error|説明|  
|-----------|-----------------|  
|接続やステートメントは、通知を要求しませんでした。||  
|無効な*処理*|ドライバーは、内部のドライバー マネージャーの検証テストに失敗した、無効なハンドルで渡されます。|  
  
## <a name="see-also"></a>関連項目  
 [非同期実行 (ポーリング メソッド)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
