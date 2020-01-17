---
title: トランザクションについて |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d3e0414c-6809-4bb1-93b1-4960507faecc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d5a6caa9c9bf1766b59aa813719d1461b6ef1aa
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027337"
---
# <a name="understanding-transactions"></a>トランザクションについて

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

トランザクションは、一連の操作を結合した論理的な作業単位です。 トランザクションを使用すると、エラーが発生した場合でも、トランザクションの各操作の一貫性と整合性を制御および維持できます。

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] を使用すると、トランザクションをローカルにすることも、分散することもできます。 トランザクションで分離レベルを使用することもできます。 JDBC ドライバーでサポートされる分離レベルの詳細については、「[分離レベル](../../connect/jdbc/understanding-isolation-levels.md)について」を参照してください。

アプリケーションからトランザクションを制御する際には、Transact-SQL ステートメントか、JDBC ドライバーに備わっているメソッドのどちらかを使用します。両方を使用することはできません。 同じトランザクションで Transact-SQL ステートメントと JDBC API メソッドの両方を使用した場合、トランザクションを適切なタイミングでコミットできない、突然トランザクションがコミットまたはロールバックされて新しいトランザクションが開始される、"トランザクションを再開できませんでした" という例外が発生するなどの問題が生じる可能性があります。

## <a name="using-local-transactions"></a>ローカル トランザクションの使用

単一フェーズであり、データベースによって直接処理されるトランザクションは、ローカル トランザクションであると見なされます。 JDBC ドライバーは、[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスのさまざまなメソッド ([setAutoCommit](../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)、[commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md)、[rollback](../../connect/jdbc/reference/rollback-method.md) など) を使用して、ローカル トランザクションをサポートします。 通常、ローカル トランザクションはアプリケーションによって明示的に管理されるか、Java Platform, Enterprise Edition (Java EE) アプリケーション サーバーによって自動的に管理されます。

次の例では、`try` ブロック内の 2 つの個別のステートメントで構成されるローカル トランザクションを実行しています。 ステートメントは、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースの Production.ScrapReason テーブルに対して実行され、例外がスローされない場合にコミットされます。 `catch` ブロック内のコードは、例外がスローされた場合にトランザクションをロールバックします。

[!code[JDBC#UnderstandingTransactions1](../../connect/jdbc/codesnippet/Java/understanding-transactions_1.java)]

## <a name="using-distributed-transactions"></a>分散トランザクションの使用

分散トランザクションは、トランザクション処理の重要な ACID (原子性、一貫性、分離性、および持続性) のプロパティを維持しながら、ネットワーク上の複数のデータベースのデータを更新します。 分散トランザクションのサポートは、JDBC 2.0 オプション API 仕様で JDBC API に追加されました。 分散トランザクションの管理は、通常、Java EE アプリケーション サーバー環境内で Java Transaction Service (JTS) トランザクション マネージャーによって自動的に実行されます。 ただし、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] は、すべての Java Transaction API (JTA) 準拠のトランザクション マネージャーで分散トランザクションをサポートします。

JDBC ドライバーは、[!INCLUDE[msCoName](../../includes/msconame_md.md)] 分散トランザクション コーディネーター (MS DTC) とシームレスに統合することで、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] による真の分散トランザクション サポートを提供します。 MS DTC は、[!INCLUDE[msCoName](../../includes/msconame_md.md)] によって [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows システム用に提供される分散トランザクション機能です。 MS DTC は、[!INCLUDE[msCoName](../../includes/msconame_md.md)] の実証済みのトランザクション処理技術を使用して、完全な 2 フェーズ分散コミット プロトコルや分散トランザクションの回復などの XA 機能をサポートします。

分散トランザクションの使用方法の詳細については、「 [XA トランザクション](../../connect/jdbc/understanding-xa-transactions.md)について」を参照してください。

## <a name="see-also"></a>参照

[JDBC ドライバーを使用したトランザクションの実行](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
