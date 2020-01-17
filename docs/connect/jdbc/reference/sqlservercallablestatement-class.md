---
title: SQLServerCallableStatement クラス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 637b56c7f64d35501be0efef30e8f2a055b5be4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971915"
---
# <a name="sqlservercallablestatement-class"></a>SQLServerCallableStatement クラス
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  入力パラメーターおよび出力パラメーターと共に、呼び出すストアド プロシージャの名前を指定できます。 また、? = call( ?, ..) 構文を使用して状態の戻り値を取得することもできます。 = 呼び出し (?, ..) 構文。  
  
 **パッケージ:** com.microsoft.sqlserver.jdbc  
  
 **実装:** [ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **継承:** [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>Remarks  
 SQLServerCallableStatement を使用すると、呼び出すストアド プロシージャの名前と共に、入力および出力パラメーターを指定できます。 SQLServerCallableStatement では、 `? = call( ?, ..)`構文を使用して戻り状態の値を取得することもできます。  
  
 このクラスは、SQLServerCallableStatement クラス、ISQLServerCallableStatement インターフェイス、SQLServerPreparedStatement インターフェイス、およびラップ解除のためにによってサポートされるクラスとインターフェイスへのラップをサポートしています。 詳細については、「[ラッパーとインターフェイス](../../../connect/jdbc/wrappers-and-interfaces.md)」を参照してください。  
  
 型に対して SQLServerCallableStatement set メソッドの1つが呼び出されたときに、その型が[Registeroutparameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)で指定された型と競合する場合、last SQLServerCallableStatement set メソッドによって指定された型が使用されます。 ただし、その結果、データ型の非互換性から変換エラーが発生する可能性があります。 SQLServerCallableStatement の set メソッドが呼び出されなかった場合、最初の [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) 呼び出しで指定された型が使用されます。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 は、結果セットと更新数が OUT パラメーターよりも先に取得されなければならないという JDBC 4.0 の勧告に準拠しています。 結果セットと更新数が完全に処理される前に OUT パラメーターが取得された場合、処理の済んでいない結果セットと更新数はすべて失われます。  
  
## <a name="see-also"></a>参照  
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [JDBC Driver API リファレンス](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
