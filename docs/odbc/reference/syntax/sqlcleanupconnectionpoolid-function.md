---
title: SQLCleanupConnectionPoolID 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee8f9b9879a3533e8196bbc89f8ae0b0a132293a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036089"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID 関数
**準拠**  
 バージョンが導入されました。ODBC 3.81 規格に準拠します。ODBC  
  
 **概要**  
 **SQLCleanupConnectionPoolID**プール ID がタイムアウトになったドライバーに通知します。そのプール ID に関連付けられたプール内のすべての接続されたときに ID がタイムアウトには、プールがタイムアウトしました。参照してください[、Microsoft Data Access Components のプーリング](https://msdn.microsoft.com/library/ms810829.aspx)接続タイムアウトの詳細についてはします。  
  
## <a name="syntax"></a>構文  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>引数  
 *EnvironmentHandle*  
 [入力]プールの環境ハンドル。  
  
 *PoolID*  
 [入力]タイムアウトするプールの ID に関連付けられたプール。  
  
## <a name="returns"></a>戻り値  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、または SQL_INVALID_HANDLE します。  
  
## <a name="diagnostics"></a>診断  
 ドライバー マネージャーはから返された診断情報を処理しません**SQLCleanupConnectionPoolID**します。  
  
 アプリケーションでは、ドライバーによって返されるエラー メッセージを受信できません。  
  
## <a name="remarks"></a>コメント  
 **SQLCleanupConnectionPoolID** 、いつでも呼び出すことができますが、ドライバー マネージャーを他のスレッドが同時を呼び出していないことを保証**SQLGetPoolID**およびその他のスレッドが同時に呼び出しありません**SQLRateConnection**と**SQLPoolConnect**そのプール ID に割り当てられている接続情報トークンを使用して そのため、ドライバーはこの関数はスレッド セーフであることを確認してください。  
  
 ドライバーはプール ID に関連付けられたリソースをクリーンアップできます。  
  
 アプリケーションでは、この関数を直接呼び出さないでください。 ドライバー対応接続プールをサポートする ODBC ドライバーでは、この関数を実装する必要があります。  
  
 ODBC ドライバーの開発の sqlspi.h が含まれます。  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [ドライバー対応接続プール](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [ODBC ドライバー対応接続プールの開発](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
