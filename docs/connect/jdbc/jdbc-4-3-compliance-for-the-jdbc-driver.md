---
title: Jdbc driver の JDBC 4.3 への準拠 |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36025ec0-3c72-4e68-8083-58b38e42d03b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ed9b10ad9e9a927789505c7d7327c6cf4d1ff3c
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027942"
---
# <a name="jdbc-43-compliance-for-the-jdbc-driver"></a>JDBC ドライバーの JDBC 4.3 への準拠

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

> [!NOTE]  
> Microsoft JDBC Driver 6.4 for SQL Server より前のバージョンは、Java Database Connectivity (JDBC) API 4.2 仕様にのみ準拠しています。 このセクションは、6.4 リリースより前のバージョンには適用されません。

バージョン6.4 では、Microsoft jdbc Driver for SQL Server は JAVA 9 と互換性が`SQLFeatureNotSupportedException`あり、実装されていないメソッドを持つ新しい jdbc 4.3 api に対してスローされます。

Microsoft JDBC Driver 7.0 for SQL Server リリースでは、ドライバーは JAVA 10 と互換性があり、以下の Api をサポートしています。 このドライバーは`SQLFeatureNotSupportedException` 、JDBC 4.3 仕様の他の実装されていないメソッドに対してをスローします。

|新しい API|[説明]|注目に値する実装|  
|-----------------|-----------------|-------------------------------|  
|void java.sql.connection.beginRequest()|要求 (独立した作業単位) がこの接続から開始されることをドライバーにヒントします。 詳細については、「[java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#beginRequest--)」を参照してください。|パブリック API メソッド`databaseAutoCommitMode` `transactionIsolationLevel` `holdability` (、`sendTimeAsDatetime`、 、`networkTimeout` 、、`enablePrepareOnFirstPreparedStatementCall`、、、、) によって変更可能な接続フィールドの値を保存します。 `statementPoolingCacheSize` `disableStatementPooling` `serverPreparedStatementDiscardThreshold``catalogName`, `sqlWarnings`, `useBulkCopyForBatchInsert`.|
|void java.sql.connection.endRequest()|要求 (独立した作業単位) が完了したことをドライバーに示すヒント。 詳細については、「[java.sql.Connection](https://docs.oracle.com/javase/9/docs/api/java/sql/Connection.html#endRequest--)」を参照してください。|作業単位中に作成されたステートメントを閉じ、開いているトランザクションをロールバックします。 また、メソッドは、上に示した接続フィールドに変更を戻します。|
