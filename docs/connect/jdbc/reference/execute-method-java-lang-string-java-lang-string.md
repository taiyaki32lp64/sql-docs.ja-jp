---
title: execute メソッド (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.execute (java.lang.String.java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9451c7c2-4c0d-4d1e-9b42-a26ff28e3f6a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e93875cfc18ed3992fd1680a0c948e38a31f998e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954974"
---
# <a name="execute-method-javalangstring-javalangstring"></a>execute (java.lang.String, java.lang.String) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  複数の結果を返す可能性のある渡された SQL ステートメントを実行し、渡された配列に示される自動生成キーを検索可能にするように、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] に通知します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final boolean execute(java.lang.String sql,  
                             java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sql*  
  
 SQL ステートメントを含む**文字列**です。  
  
 *columnNames*  
  
 検索可能にする自動生成キーの列名を示す文字列の配列です。  
  
## <a name="return-value"></a>戻り値  
 最初の結果が結果セットの場合は **true** です。 それ以外の場合は、 **false**です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この execute メソッドは、java.sql.Statement インターフェイスの execute メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [execute メソッド&#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)   
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
