---
title: JDBC ドライバーの準備されたステートメント メタデータ キャッシュ | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97224f53bb716abe3b79dd00df12d0eed4a63cec
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027837"
---
# <a name="prepared-statement-metadata-caching-for-the-jdbc-driver"></a>JDBC ドライバーの準備されたステートメント メタデータ キャッシュ
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

この記事では、ドライバーのパフォーマンスを向上させるために実装される2つの変更について説明します。

## <a name="batching-of-unprepare-for-prepared-statements"></a>準備されたステートメントの unprepare のバッチ処理
バージョン 6.1.6-preview 以降では、サーバーのラウンドトリップ SQL Server を最小限に抑えてパフォーマンスを向上させることができました。 以前は、すべての unprepare ステートメントクエリに対して、呼び出しが送信されました。 これで、ドライバーは unprepare クエリを、既定値の10を持つしきい値 "ServerPreparedStatementDiscardThreshold" までバッチ処理します。

> [!NOTE]  
>  ユーザーは、次のメソッドを使用して既定値を変更できます: setServerPreparedStatementDiscardThreshold (int 値)

6\.1.6 から導入されたもう1つの変更は、これより前のバージョンでは、ドライバーは常に sp_prepexec を呼び出します。 これで、準備されたステートメントの初回実行時に、ドライバーは sp_executesql を呼び出し、rest に対して sp_prepexec を実行してハンドルを割り当てます。 詳細については、[こちら](https://github.com/Microsoft/mssql-jdbc/wiki/PreparedStatement-metadata-caching)を参照してください。

> [!NOTE]  
>  ユーザーは、次のメソッドを使用して enablePrepareOnFirstPreparedStatementCall を**true**に設定することにより、既定の動作を以前のバージョンの sp_prepexec 呼び出しに変更できます。 setEnablePrepareOnFirstPreparedStatementCall (ブール値)

### <a name="list-of-the-new-apis-introduced-with-this-change-for-batching-of-unprepare-for-prepared-statements"></a>準備されたステートメントの unprepare のバッチ処理のために、この変更で導入された新しい Api の一覧

 **SQLServerConnection**
 
|新しいメソッド|[説明]|  
|-----------|-----------------|  
|int getDiscardedServerPreparedStatementCount()|現在未処理の準備されたステートメント unprepare アクションの数を返します。|
|void closeUnreferencedPreparedStatementHandles()|破棄された未処理の準備されたステートメントに対して、強制的に unprepare 要求を実行します。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|特定の接続インスタンスの動作を返します。 False の場合、最初の実行では sp_executesql が呼び出され、ステートメントは準備されません。2回目の実行が行われると、sp_prepexec が呼び出され、実際には準備されたステートメントハンドルが設定されます。 次の実行では、sp_execute を呼び出します。 これにより、ステートメントが1回だけ実行された場合に、準備されたステートメントを閉じる必要がなくなります。 このオプションの既定値は、setDefaultEnablePrepareOnFirstPreparedStatementCall () を呼び出すことによって変更できます。|
|void setEnablePrepareOnFirstPreparedStatementCall(boolean value)|特定の接続インスタンスの動作を指定します。 Value が false の場合、最初の実行では sp_executesql が呼び出され、ステートメントは準備されません。2回目の実行が行われると、sp_prepexec が呼び出され、実際には準備されたステートメントハンドルが設定されます。 次の実行では、sp_execute を呼び出します。 これにより、ステートメントが1回だけ実行された場合に、準備されたステートメントを閉じる必要がなくなります。|
|int getServerPreparedStatementDiscardThreshold()|特定の接続インスタンスの動作を返します。 この設定は、サーバー上の未処理のハンドルをクリーンアップするための呼び出しが実行される前に、1つの接続に対して未処理の準備されたステートメント破棄操作 (sp_unprepare) の数を制御します。 設定が < = 1 の場合、unprepare のアクションは、準備されたステートメントの終了時に直ちに実行されます。 {@literal >} 1 に設定されている場合、sp_unprepare を呼び出すことによるオーバーヘッドを避けるために、これらの呼び出しはまとめてバッチ処理されます。 このオプションの既定値は、getDefaultServerPreparedStatementDiscardThreshold () を呼び出すことによって変更できます。|
|void setServerPreparedStatementDiscardThreshold(int value)|特定の接続インスタンスの動作を指定します。 この設定は、サーバー上の未処理のハンドルをクリーンアップするための呼び出しが実行される前に、1つの接続に対して未処理の準備されたステートメント破棄操作 (sp_unprepare) の数を制御します。 設定が < = 1 の場合、unprepare のアクションは、準備されたステートメントの終了時に直ちに実行されます。 > 1 に設定されている場合は、sp_unprepare の呼び出しが頻繁に行われるオーバーヘッドを避けるために、これらの呼び出しがまとめてバッチ処理されます。|

 **SQLServerDataSource**
 
|新しいメソッド|[説明]|  
|-----------|-----------------|  
|void setEnablePrepareOnFirstPreparedStatementCall(boolean enablePrepareOnFirstPreparedStatementCall)|この構成が false の場合、準備されたステートメントの最初の実行では sp_executesql が呼び出され、ステートメントは準備されません。2回目の実行が行われると、sp_prepexec が呼び出され、実際には準備されたステートメントハンドルが設定されます。 次の実行では、sp_execute を呼び出します。 これにより、ステートメントが1回だけ実行された場合に、準備されたステートメントを閉じる必要がなくなります。|
|boolean getEnablePrepareOnFirstPreparedStatementCall()|この構成が false を返した場合、準備されたステートメントの最初の実行では sp_executesql が呼び出され、ステートメントは準備されません。2回目の実行が行われると、sp_prepexec が呼び出され、実際には準備されたステートメントハンドルが設定されます。 次の実行では、sp_execute を呼び出します。 これにより、ステートメントが1回だけ実行された場合に、準備されたステートメントを閉じる必要がなくなります。|
|void setServerPreparedStatementDiscardThreshold(int serverPreparedStatementDiscardThreshold)|この設定は、サーバー上の未処理のハンドルをクリーンアップするための呼び出しが実行される前に、1つの接続に対して未処理の準備されたステートメント破棄操作 (sp_unprepare) の数を制御します。 設定が < = 1 の場合、unprepare のアクションは、準備されたステートメントの終了時に直ちに実行されます。 {@literal >} 1 に設定されている場合、sp_unprepare を呼び出すことによるオーバーヘッドを避けるために、これらの呼び出しはまとめてバッチ処理されます。|
|int getServerPreparedStatementDiscardThreshold()|この設定は、サーバー上の未処理のハンドルをクリーンアップするための呼び出しが実行される前に、1つの接続に対して未処理の準備されたステートメント破棄操作 (sp_unprepare) の数を制御します。 設定が < = 1 の場合、unprepare のアクションは、準備されたステートメントの終了時に直ちに実行されます。 {@literal >} 1 に設定されている場合、sp_unprepare を呼び出すことによるオーバーヘッドを避けるために、これらの呼び出しはまとめてバッチ処理されます。|

## <a name="prepared-statement-metatada-caching"></a>準備されたステートメントメタデータのキャッシュ
6\.3.0-preview バージョンでは、Microsoft JDBC driver for SQL Server は、準備されたステートメントキャッシュをサポートしています。 V 6.3.0-preview より前のバージョンでは、既に準備され、キャッシュに格納されているクエリを実行すると、同じクエリを再度呼び出すことはできません。 これで、ドライバーはキャッシュ内のクエリを検索し、sp_execute を使用してハンドルを見つけて実行します。
準備されたステートメントメタデータのキャッシュは、既定では**無効になっ**ています。 有効にするには、connection オブジェクトで次のメソッドを呼び出す必要があります。

`setStatementPoolingCacheSize(int value)   //value is the desired cache size (any value bigger than 0)`
`setDisableStatementPooling(boolean value) //false allows the caching to take place`

例: `connection.setStatementPoolingCacheSize(10)`
`connection.setDisableStatementPooling(false)`

### <a name="list-of-the-new-apis-introduced-with-this-change-for-prepared-statement-metadata-caching"></a>準備されたステートメントメタデータのキャッシュのために、この変更で導入された新しい Api の一覧

 **SQLServerConnection**
 
|新しいメソッド|[説明]|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean value)|ステートメントプーリングを true または false に設定します。|
|boolean getDisableStatementPooling()|ステートメントプーリングが無効になっている場合は true を返します。|
|void setStatementPoolingCacheSize(int value)|この接続に対して準備されたステートメントキャッシュのサイズを指定します。 1未満の値は、キャッシュがないことを意味します。|
|int getStatementPoolingCacheSize()|この接続に対して準備されたステートメントキャッシュのサイズを返します。 1未満の値は、キャッシュがないことを意味します。|
|int getStatementHandleCacheEntryCount()|プールされた準備されたステートメントハンドルの現在の数を返します。|
|boolean isPreparedStatementCachingEnabled()|この接続では、ステートメントプーリングが有効かどうか。|

 **SQLServerDataSource**
 
|新しいメソッド|[説明]|  
|-----------|-----------------|  
|void setDisableStatementPooling(boolean disableStatementPooling)|ステートメントプーリングを true または false に設定します。|
|boolean getDisableStatementPooling()|ステートメントプーリングが無効になっている場合は true を返します。|
|void setStatementPoolingCacheSize(int statementPoolingCacheSize)|この接続に対して準備されたステートメントキャッシュのサイズを指定します。 1未満の値は、キャッシュがないことを意味します。|
|int getStatementPoolingCacheSize()|この接続に対して準備されたステートメントキャッシュのサイズを返します。 1未満の値は、キャッシュがないことを意味します。|

## <a name="see-also"></a>参照  
 [JDBC ドライバーによるパフォーマンスと信頼性の強化](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)  
  
  
