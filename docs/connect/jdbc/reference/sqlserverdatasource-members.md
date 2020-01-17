---
title: SQLServerDataSource Members |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7e749bc5-d765-4864-be2b-7822d4c20c09
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 800f87c82987396743ec4c0c278444c4ba61d49b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971414"
---
# <a name="sqlserverdatasource-members"></a>SQLServerDataSource のメンバー
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  次の表は、[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) クラスによって公開されるメンバーを示しています。  
  
## <a name="constructors"></a>コンストラクター  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|[SQLServerDataSource ()](../../../connect/jdbc/reference/sqlserverdatasource-constructor.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) クラスの新しいインスタンスを初期化します。|  
  
## <a name="fields"></a>フィールド  
 [なし] :  
  
## <a name="inherited-fields"></a>継承されたフィールド  
 [なし] :  
  
## <a name="methods"></a>メソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|**Applicationintent**接続プロパティの値を返します。|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|アプリケーション名を返します。|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトが示すデータ ソースとの接続の確立を試みます。|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|データベース名が返されます。|  
|[getDisableStatementPooling](../../../connect/jdbc/reference/getdisablestatementpooling-method-sqlserverdatasource.md)|**DisableStatementPooling** connection プロパティの値を返します。 この設定は、この接続に対してステートメントプールを有効にするかどうかを制御します。|  
|[getEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/getenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource.md)|**EnablePrepareOnFirstPreparedStatementCall** connection プロパティの値を返します。|  
|[getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md)|encrypt プロパティが有効であるかどうかを示す **Boolean** 値を返します。|  
|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|データ ソースの記述を返します。|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|データベース ミラーリング構成で使用されるフェールオーバー サーバーの名前を返します。|  
|[getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md)|SQL Server の SSL (Secure Sockets Layer) 証明書の検証に使用されるホスト名を返します。|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名が返されます。|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|lastUpdateCount プロパティが有効であるかどうかを示す**ブール**値が返されます。|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|データベースがロック タイムアウトを通知するまでに待機する時間 (ミリ秒) を示す **int** 値が返されます。|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|接続の試行中にこの [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトが待機する秒数が返されます。|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|すべてのログ メッセージとトレース メッセージで使用される文字出力ストリームを返します。|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|**MultiSubnetFailover** connection プロパティの値を返します。|  
|[getPacketSize](../../../connect/jdbc/reference/getpacketsize-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] との通信に使用される現在のネットワーク パケット サイズを返します (バイト数で指定します)。|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] との通信に使用される現在のポート番号が返されます。|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトへの参照が返されます。|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトの応答バッファリング モードが返されます。|  
|[getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトを使用して作成されるすべての結果セットで使用される、既定のカーソルの種類が返されます。|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|サーバーへの文字列パラメーターの UNICODE 形式による送信が有効になっているかどうかを示す**ブール**値が返されます。|  
|[getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|**SendTimeAsDatetime**接続プロパティの設定を返します。|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行しているコンピューターの名前が返されます。|  
|[getServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/getserverpreparedstatementdiscardthreshold-method-sqlserverdatasource.md)|**ServerPreparedStatementDiscardThreshold** connection プロパティの値を返します。|  
|[getStatementPoolingCacheSize](../../../connect/jdbc/reference/getstatementpoolingcachesize-method-sqlserverdatasource.md)|この接続に対して準備されたステートメントキャッシュのサイズを返します。|  
|[getTrustManagerClass](../../../connect/jdbc/reference/gettrustmanagerclass-method-sqlserverdatasource.md)|TrustManagerClass 接続プロパティの文字列値を返します。|  
|[getTrustManagerConstructorArg](../../../connect/jdbc/reference/gettrustmanagerconstructorarg-method-sqlserverdatasource.md)|TrustManagerConstructorArg connection プロパティの文字列値を返します。|  
|[getTrustServerCertificate](../../../connect/jdbc/reference/gettrustservercertificate-method-sqlserverdatasource.md)|trustServerCertificate プロパティが有効であるかどうかを示す**ブール**値が返されます。|  
|[getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md)|証明書の trustStore ファイルへのパス (ファイル名を含む) を返します。|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|データ ソースへの接続に使用される URL を返します。|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|データ ソースへの接続に使用されるユーザー名が返されます。|  
|[getUseSQLServerBaseDate](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|useSQLServerBaseDate 接続プロパティの設定を返します。|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|データ ソースへの接続に使用されるクライアント コンピューターの名前が返されます。|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|XOPEN 互換の状態への SQL 状態の変換が有効になっているかどうかを示す**ブール**値が返されます。|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)|データ ソース オブジェクトが指定されたインターフェイスのラッパーであるかどうかを示します。|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|**Applicationintent**接続プロパティの値を設定します。|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|アプリケーション名を設定します。|  
|[setAuthenticationScheme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|アプリケーションで使用する統合セキュリティの種類を示します。|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|接続するデータベース名を設定します。|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|データ ソースの記述を設定します。|  
|[setDisableStatementPooling](../../../connect/jdbc/reference/setdisablestatementpooling-method-sqlserverdatasource.md)|ステートメントプーリングを true または false に設定します。|  
|[setEnablePrepareOnFirstPreparedStatementCall](../../../connect/jdbc/reference/setenableprepareonfirstpreparedstatementcall-method-sqlserverdatasource.md)|**EnablePrepareOnFirstPreparedStatementCall**接続プロパティの新しい値を指定します。|  
|[setEncrypt](../../../connect/jdbc/reference/setencrypt-method-sqlserverdatasource.md)|encrypt プロパティが有効であるかどうかを示す **Boolean** 値を設定します。|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|データベース ミラーリング構成で使用されるフェールオーバー サーバーの名前を設定します。|  
|[setHostNameInCertificate](../../../connect/jdbc/reference/sethostnameincertificate-method-sqlserverdatasource.md)|SQL Server の SSL (Secure Sockets Layer) 証明書の検証に使用されるホスト名を設定します。|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス名が設定されます。|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|integratedSecurity プロパティが有効であるかどうかを示す **Boolean** 値を設定します。|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|lastUpdateCount プロパティが有効であるかどうかを示す**ブール** 値を設定します。|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|データベースがロック タイムアウトを通知するまでに待機する時間 (ミリ秒) を示す **int** 値を設定します。|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|接続の試行中にこの [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトが待機する秒数を設定します。|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|すべてのログ メッセージとトレース メッセージで文字出力ストリームが使用されるように設定します。|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|**MultiSubnetFailover** connection プロパティの値を設定します。|  
|[setPacketSize](../../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] との通信に使用される現在のネットワーク パケット サイズが設定されます (バイトで指定します)。|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] への接続に使用されるパスワードを設定します。|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] との通信に使用されるポート番号を設定します。|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトを使用して作成された接続の応答バッファリング モードを設定します。|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|[SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) オブジェクトを使用して作成されるすべての結果セットで使用される、既定のカーソルの種類を設定します。|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|サーバーへの文字列パラメーターの UNICODE 形式による送信が有効になっているかどうかを示す**ブール** 値を設定します。|  
|[setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)|java.sql.Time 値をサーバーに送信する方法を指定します。|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] を実行しているコンピューターの名前を設定します。|  
|[setServerPreparedStatementDiscardThreshold](../../../connect/jdbc/reference/setserverpreparedstatementdiscardthreshold-method-sqlserverdatasource.md)|**ServerPreparedStatementDiscardThreshold**接続プロパティの新しい値を設定します。|  
|[setStatementPoolingCacheSize](../../../connect/jdbc/reference/setstatementpoolingcachesize-method-sqlserverdatasource.md)|この接続に対して準備されたステートメントキャッシュのサイズを設定します。|  
|[setTrustManagerClass](../../../connect/jdbc/reference/settrustmanagerclass-method-sqlserverdatasource.md)|TrustManagerClass 接続プロパティの文字列値を設定します。|  
|[setTrustManagerConstructorArg](../../../connect/jdbc/reference/settrustmanagerconstructorarg-method-sqlserverdatasource.md)|TrustManagerConstructorArg connection プロパティの文字列値を設定します。|  
|[setTrustServerCertificate](../../../connect/jdbc/reference/settrustservercertificate-method-sqlserverdatasource.md)|trustServerCertificate プロパティが有効であるかどうかを示す**ブール**値を設定します。|  
|[setTrustStore](../../../connect/jdbc/reference/settruststore-method-sqlserverdatasource.md)|証明書の trustStore ファイルへのパス (ファイル名を含む) を設定します。|  
|[setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)|trustStore データの整合性を確認するために使用するパスワードを設定します。|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|データ ソースへの接続に使用される URL を設定します。|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|データ ソースへの接続に使用されるユーザー名を設定します。|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|データ ソースへの接続に使用されるクライアント コンピューターの名前を設定します。|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|XOPEN 互換の状態への SQL 状態の変換が有効になっているかどうかを示す**ブール**値を設定します。|  
|[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)|指定されたインターフェイスを実装するオブジェクトを返します。このメソッドから返されたオブジェクトを使用することで、[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 固有のメソッドにアクセスできます。|  
  
## <a name="inherited-methods"></a>継承されたメソッド  
  
|継承元のクラス|メソッド|  
|---------------------------|-------------|  
|java.lang.Object|clone、equals、finalize、getClass、hashCode、notify、notifyAll、toString、wait|  
|java.sql.Wrapper|isWrapperFor、unwrap|  
  
## <a name="see-also"></a>参照  
 [SQLServerDataSource クラス](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
