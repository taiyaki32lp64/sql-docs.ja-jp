---
title: JDBC driver | でステートメントを使用するMicrosoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7f8f3e8f-841e-4449-9154-b5366870121f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ddd61d15e3c363766c7e49b8e9045b60a7be164
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025795"
---
# <a name="using-statements-with-the-jdbc-driver"></a>JDBC ドライバーでのステートメントの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] データベース内のデータは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用して、さまざまな方法で操作することができます。 入力パラメーターや出力パラメーターを使用して、データベースに SQL ステートメントを実行したり、データベースのストアド プロシージャを呼び出したりできます。 JDBC ドライバーは、バッチ操作による SQL エスケープ シーケンス、更新数、自動生成キーの使用、および更新の実行もサポートしています。  
  
JDBC ドライバーには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースからデータを取得するための 3 つのクラスがあります。  
  
1. [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) - パラメーターを指定せずに SQL ステートメントを実行するために使用されます。  
  
2. [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) - (SQLServerStatement から継承されます) IN パラメーターを含む、コンパイル済みの SQL ステートメントを実行するために使用されます。  
  
3. [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) - (SQLServerPreparedStatement から継承されます) IN パラメーター、OUT パラメーター、またはその両方を含むストアド プロシージャを実行するために使用されます。  
  
 このセクションのトピックでは、これら 3 つのステートメント クラスを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのデータを処理する方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  

| トピック                                                                                                    | [説明]                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [SQL でのステートメントの使用](../../connect/jdbc/using-statements-with-sql.md)                             | JDBC ドライバーで SQL ステートメントを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのデータを処理する方法について説明します。    |
| [ストアド プロシージャでのステートメントの使用](../../connect/jdbc/using-statements-with-stored-procedures.md) | JDBC ドライバーでストアド プロシージャを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのデータを処理する方法について説明します。 |
| [複数の結果セットの使用](../../connect/jdbc/using-multiple-result-sets.md)                           | JDBC ドライバーを使用して複数の結果セットからデータを取得する方法について説明します。                                                                       |
| [SQL エスケープ シーケンスの使用](../../connect/jdbc/using-sql-escape-sequences.md)                           | 日付および時刻のリテラルや関数のような SQL エスケープ シーケンスの使用方法について説明します。                                                               |
| [自動生成キーの使用](../../connect/jdbc/using-auto-generated-keys.md)                             | 自動生成キーの使用方法について説明します。                                                                                                     |
| [バッチ操作の実行](../../connect/jdbc/performing-batch-operations.md)                         | JDBC ドライバーを使用してバッチ操作を行う方法について説明します。                                                                                      |
| [複雑なステートメントの処理](../../connect/jdbc/handling-complex-statements.md)                         | JDBC ドライバーを使用して、さまざまなタスクを実行しさまざまな型のデータを返す複雑なステートメントを実行する方法について説明します。               |
  
## <a name="see-also"></a>参照

[JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
