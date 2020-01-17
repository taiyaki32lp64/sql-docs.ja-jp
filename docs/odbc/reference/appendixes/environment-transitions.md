---
title: 環境の切り替え |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- environment transitions [ODBC]
- transitioning states [ODBC], environment
- state transitions [ODBC], environment
ms.assetid: 9d11b1ab-f4c8-48ca-9812-8c04303f939d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b1de2f2147357f9e2ed4f71657b9298c4a13684
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910433"
---
# <a name="environment-transitions"></a>環境の遷移
ODBC 環境では、次の 3 つの状態があります。  
  
|状態|説明|  
|-----------|-----------------|  
|E0|未割り当ての環境|  
|E1|割り当てられている環境では、未割り当ての接続|  
|E2|環境では、接続の割り当てください。 の割り当てください。|  
  
 次の表では、各 ODBC 関数が、環境の状態に与える影響を示します。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> 割り当てられました。|E2<br /><br /> 接続|  
|------------------------|----------------------|-----------------------|  
|E1 [1]|--[4]|--[4]|  
|(組み込み)[2]|E2 [5]<br />(HY010)[6]|--[4]|  
|(組み込み)[3]|(組み込み)|--[4]|  
  
 [1] この行は、移行を示しています。 ときに*HandleType* sql_handle_env としてでした。  
  
 [2] この行は、移行を示しています。 ときに*HandleType* sql_handle_dbc としてでした。  
  
 [3] この行は、移行を示しています。 ときに*HandleType* sql_handle_stmt としてまたは SQL_HANDLE_DESC でした。  
  
 [4] 呼び出し**SQLAllocHandle**で*OutputHandlePtr*そのハンドルの有効なハンドルを指すが上書きされます。 これには、アプリケーションのプログラミング エラーがあります。  
  
 [5]、SQL_ATTR_ODBC_VERSION 環境属性は、環境に設定されていました。  
  
 [6]、SQL_ATTR_ODBC_VERSION 環境属性は、環境に設定されていない必要があります。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources と SQLDrivers  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> 割り当てられました。|E2<br /><br /> 接続|  
|------------------------|----------------------|-----------------------|  
|(組み込み)|--[1]<br />(HY010)[2]|--[1]<br />(HY010)[2]|  
  
 [1]、SQL_ATTR_ODBC_VERSION 環境属性は、環境に設定されていました。  
  
 [2] の SQL_ATTR_ODBC_VERSION 環境属性は、環境に設定されていない必要があります。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> 割り当てられました。|E2<br /><br /> 接続|  
|------------------------|----------------------|-----------------------|  
|(組み込み)[1]|--[3]<br />(HY010)[4]|--[3]<br />(HY010)[4]|  
|(組み込み)[2]|(組み込み)|--|  
  
 [1] この行は、移行を示しています。 ときに*HandleType* sql_handle_env としてでした。  
  
 [2] この行は、移行を示しています。 ときに*HandleType* sql_handle_dbc としてでした。  
  
 [3]、SQL_ATTR_ODBC_VERSION 環境属性は、環境に設定されていました。  
  
 [4]、SQL_ATTR_ODBC_VERSION 環境属性は、環境に設定されていない必要があります。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> 割り当てられました。|E2<br /><br /> 接続|  
|------------------------|----------------------|-----------------------|  
|(組み込み)[1]|E0|(HY010)|  
|(組み込み)[2]|(組み込み)|--[4]<br />E1 [5]|  
|(組み込み)[3]|(組み込み)|--|  
  
 [1] この行は、移行を示しています。 ときに*HandleType* sql_handle_env としてでした。  
  
 [2] この行は、移行を示しています。 ときに*HandleType* sql_handle_dbc としてでした。  
  
 [3] この行は、移行を示しています。 ときに*HandleType* sql_handle_stmt としてまたは SQL_HANDLE_DESC でした。  
  
 [他に割り当てられていた接続ハンドルが 4] があります。  
  
 [5] で指定された接続ハンドル*処理*のみ割り当てられていた接続ハンドルをでした。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField と SQLGetDiagRec  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> 割り当てられました。|E2<br /><br /> 接続|  
|------------------------|----------------------|-----------------------|  
|(組み込み)[1]|--|--|  
|(組み込み)[2]|(組み込み)|--|  
  
 [1] この行は、移行を示しています。 ときに*HandleType* sql_handle_env としてでした。  
  
 [2] この行は、移行を示しています。 ときに*HandleType* sql_handle_dbc として、sql_handle_stmt として、または SQL_HANDLE_DESC でした。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> 割り当てられました。|E2<br /><br /> 接続|  
|------------------------|----------------------|-----------------------|  
|(組み込み)|--[1]<br />(HY010)[2]|--|  
  
 [1]、SQL_ATTR_ODBC_VERSION 環境属性は、環境に設定されていました。  
  
 [2] の SQL_ATTR_ODBC_VERSION 環境属性は、環境に設定されていない必要があります。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> 割り当てられました。|E2<br /><br /> 接続|  
|------------------------|----------------------|-----------------------|  
|(組み込み)|--[1]<br />(HY010)[2]|(HY011)|  
  
 [1]、SQL_ATTR_ODBC_VERSION 環境属性は、環境に設定されていました。  
  
 [2]、*属性*引数が SQL_ATTR_ODBC_VERSION、および SQL_ATTR_ODBC_VERSION [環境] 属性は、環境に設定されていない必要があります。  
  
## <a name="all-other-odbc-functions"></a>他のすべての ODBC 関数  
  
|E0<br /><br /> 未割り当て|E1<br /><br /> 割り当てられました。|E2<br /><br /> 接続|  
|------------------------|----------------------|-----------------------|  
|(組み込み)|(組み込み)|--|
