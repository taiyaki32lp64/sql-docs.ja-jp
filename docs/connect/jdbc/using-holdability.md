---
title: Using 保持機能 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: aa48306c-e7a0-4dcb-af21-9ebb6898e45a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1c126385955ce6e9fa9098ec5a09ba115b94ffb0
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026199"
---
# <a name="using-holdability"></a>保持可能性の使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

既定では、トランザクション内で作成される結果セットは、トランザクションがデータベースにコミットされた後、またはロールバックされるときに開かれたままになります。 ただし、トランザクションがコミットされた後で結果セットを閉じると便利な場合があります。 このため、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] は結果セットの保持機能をサポートしています。

結果セットの保持機能は、[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [setHoldability](../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md) メソッドを使用して設定できます。 setHoldability メソッドを使用して保持機能を設定する場合、結果セット保持機能の定数である `ResultSet.HOLD_CURSORS_OVER_COMMIT` または `ResultSet.CLOSE_CURSORS_AT_COMMIT` を使用できます。

JDBC ドライバーも、Statement オブジェクトのいずれか 1 つを作成する場合に、保持機能の設定をサポートします。 結果セットの保持機能パラメーターがあるオーバーロードを持つ Statement オブジェクトを作成する場合、ステートメント オブジェクトの保持機能が接続の保持機能と一致する必要があります。 両者が一致しない場合、例外がスローされます。 これは、SQL Server では接続レベルのみで保持機能がサポートされるためです。

結果セットの保持機能は、結果セットがサーバー側のカーソル専用に作成されている場合にその結果セットと関連付けられる SQLServerConnection オブジェクトの保持機能です。 クライアント側のカーソルには適用されません。 クライアント側のカーソルがあるすべての結果セットの保持機能の値は、常に `ResultSet.HOLD_CURSORS_OVER_COMMIT` です。

サーバー側のカーソルについては、SQL Server 2005 以降に接続されている場合に、保持機能の設定が、その接続でこれから作成される新しい結果セットの保持機能にのみ影響を与えます。 つまり、保持機能を設定しても、以前に作成され、その接続で既に開かれている結果セットの保持機能には影響しません。

次の例では、結果セットの保持機能は、`try` ブロック内の 2 つの個別のステートメントで構成されるローカル トランザクションの実行時に設定されます。 ステートメントは、[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] サンプル データベースの Production.ScrapReason テーブルに対して実行されます。 例では、最初に自動コミットを `false` に設定して、手動トランザクション モードに切り替えます。 自動コミット モードが無効になると、アプリケーションで明示的に [commit](../../connect/jdbc/reference/commit-method-sqlserverconnection.md) メソッドを呼び出すまで、SQL ステートメントはコミットされません。 catch ブロック内のコードは、例外がスローされた場合にトランザクションをロールバックします。

[!code[JDBC#UsingHoldability1](../../connect/jdbc/codesnippet/Java/using-holdability_1.java)]

## <a name="see-also"></a>参照

[JDBC ドライバーを使用したトランザクションの実行](../../connect/jdbc/performing-transactions-with-the-jdbc-driver.md)
