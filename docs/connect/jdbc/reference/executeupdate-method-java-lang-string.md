---
title: executeUpdate メソッド (java.lang.String, int[]) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String, int[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b3d5b60-4285-4047-b13e-106754ca0d98
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 059f463c6a448c6ae2ab302542a50cde1f533db8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67954700"
---
# <a name="executeupdate-method-javalangstring-int"></a>executeUpdate (java.lang.String, int[]) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された SQL ステートメントを実行し、渡された配列に示される自動生成キーを検索可能にするように、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] に通知します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               int[] columnIndexes)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *sql*  
  
 SQL ステートメントを含む**文字列**です。  
  
 *columnIndexes*  
  
 検索可能にする自動生成キーの列インデックスを示す int 配列です。  
  
## <a name="return-value"></a>戻り値  
 影響を受けた行数を示す **int** です。DDL ステートメントを使用している場合は 0 です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Remarks  
 この executeUpdate メソッドは、java.sql.Statement インターフェイスの executeUpdate メソッドで規定されています。  
  
 更新数が 1 より大きくなる (または複数の結果セットが生成される) ストアド プロシージャは [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) メソッドを使用して実行してください。  
  
## <a name="see-also"></a>参照  
 [executeUpdate メソッド &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
