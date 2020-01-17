---
title: SQLServerXAResource Members |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a069bf2c-1b70-4817-b084-a508445de799
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b420dd7c4bc714e26c8078112c5af54ae5aa7b0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67970068"
---
# <a name="sqlserverxaresource-members"></a>SQLServerXAResource のメンバー
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  次の表では、[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) クラスによって公開されるメンバーを示します。  
  
## <a name="constructors"></a>コンストラクター  
 [なし] :  
  
## <a name="fields"></a>フィールド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|[SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md)|XA ブランチ トランザクション ID (XID) は異なるが、グローバル トランザクション ID (GTRID) が同じである、密に結合された XA トランザクションを許可するために使用します。|  
  
## <a name="inherited-fields"></a>継承されたフィールド  
  
|継承元のクラス|メソッド|  
|---------------------------|-------------|  
|javax.transaction.xa.XAResource|TMENDRSCAN、TMFAIL、TMJOIN、TMNOFLAGS、TMONEPHASE、TMRESUME、TMSTARTRSCAN、TMSUCCESS、TMSUSPEND、XA_OK、XA_RDONLY|  
  
## <a name="methods"></a>メソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|[commit](../../../connect/jdbc/reference/commit-method-sqlserverxaresource.md)|渡された Xid オブジェクトによって指定されたグローバル トランザクションをコミットします。|  
|[end](../../../connect/jdbc/reference/end-method-sqlserverxaresource.md)|トランザクション ブランチのために実行していた処理を終了します。|  
|[forget](../../../connect/jdbc/reference/forget-method-sqlserverxaresource.md)|リソース マネージャーに対し、ヒューリスティックに決着されたトランザクション ブランチを無視するよう指示します。|  
|[getTransactionTimeout](../../../connect/jdbc/reference/gettransactiontimeout-method-sqlserverxaresource.md)|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) オブジェクトに設定された現在のトランザクション タイムアウト値を取得します。|  
|[isSameRM](../../../connect/jdbc/reference/issamerm-method-sqlserverxaresource.md)|対象オブジェクトが表すリソース マネージャー インスタンスと、渡された XAResource オブジェクトが表すリソース マネージャー インスタンスとが同一であるかどうかを示します。|  
|[prepare](../../../connect/jdbc/reference/prepare-method-sqlserverxaresource.md)|渡された Xid オブジェクトによって指定されたトランザクションのコミットに対する準備を行うように、リソース マネージャーに要求します。|  
|[復元 (recover)](../../../connect/jdbc/reference/recover-method-sqlserverxaresource.md)|準備されたトランザクション ブランチの一覧を、リソース マネージャーから取得します。|  
|[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverxaresource.md)|トランザクション ブランチのために実行した処理をロールバックするように、リソース マネージャーに要求します。|  
|[setTransactionTimeout](../../../connect/jdbc/reference/settransactiontimeout-method-sqlserverxaresource.md)|[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) オブジェクトの現在のトランザクション タイムアウト値を設定します。|  
|[start](../../../connect/jdbc/reference/start-method-sqlserverxaresource.md)|Xid オブジェクトで指定されたトランザクション ブランチのために処理を開始します。|  
  
## <a name="inherited-methods"></a>継承されたメソッド  
  
|継承元のクラス|メソッド|  
|---------------------------|-------------|  
|java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
  
## <a name="see-also"></a>参照  
 [SQLServerXAResource クラス](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
