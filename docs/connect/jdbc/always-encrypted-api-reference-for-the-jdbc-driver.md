---
title: JDBC ドライバーの Always Encrypted API のリファレンス | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6962a2aa-9508-4d4f-a78c-905e2bc68615
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79cf8ce1b951621d58105d18b847306ff620d114
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028483"
---
# <a name="always-encrypted-api-reference-for-the-jdbc-driver"></a>JDBC ドライバーの Always Encrypted API のリファレンス
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Always Encrypted を使用すると、クライアントは SQL Server に暗号化キーを開示することなく、クライアント アプリケーション内の機密データを暗号化することができます。 クライアント コンピューターにインストールされている、Always Encrypted が有効のドライバーは、SQL Server クライアント アプリケーション内の機密データを自動的に暗号化および暗号化解除することで、この機能を実行します。 ドライバーは、SQL Server にデータを渡す前に機密性の高い列のデータを暗号化し、アプリケーションに対するセマンティクスが維持されるように自動的にクエリを書き換えます。 同様に、ドライバーはクエリ結果内の暗号化されたデータベース列に格納されているデータを透過的に暗号化解除します。 詳細については、「 [Always Encrypted (データベースエンジン)](../../relational-databases/security/encryption/always-encrypted-database-engine.md) 」および「 [JDBC ドライバーでの Always Encrypted の使用](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)」を参照してください。  
  
> [!NOTE]  
>  Always Encrypted は、SQL Server 2016 で使用される Microsoft JDBC Driver 6.0 for SQL Server 以降でのみサポートされています。  
  
 ## <a name="always-encrypted-api-references"></a>Always Encrypted API リファレンス
 
 Always Encrypted を使用するクライアント アプリケーションで使用するために、JDBC ドライバー API に対していくつかの新たな追加と変更が施されています。  
  
 **SQLServerConnection クラス**  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|新しい接続文字列キーワード:<br /><br /> columnEncryptionSetting|columnEncryptionSetting=Enabled は接続で Always Encrypted 機能を有効にし、columnEncryptionSetting=Disabled はこの機能を無効にします。 指定できる値は、Enabled または Disabled です。 既定値は Disabled です。|  
|新しいメソッド:<br /><br /> `public static void setColumnEncryptionTrustedMasterKeyPaths(Map<String, List\<String>> trustedKeyPaths)`<br /><br /> `public static void updateColumnEncryptionTrustedMasterKeyPaths(String server, List\<String> trustedKeyPaths)`<br /><br /> `public static void removeColumnEncryptionTrustedMasterKeyPaths(String server)`|データベース サーバーの信頼されたキー パスの一覧を設定、更新、削除できます。 アプリケーション クエリの処理中に、一覧にないキー パスをドライバーが受け取った場合、クエリは失敗します。 このプロパティは、セキュリティが侵害され、偽のキー パスを送信し、キー ストアの資格情報漏洩につながるおそれがある SQL Server を含めたセキュリティ攻撃に対して、セキュリティ保護をさらに強化します。|  
|新しいメソッド:<br /><br /> `public static Map<String, List\<String>> getColumnEncryptionTrustedMasterKeyPaths()`|データベース サーバーの信頼されたキー パスの一覧を返します。|  
|新しいメソッド:<br /><br /> `public static void registerColumnEncryptionKeyStoreProviders (Map\<String, SQLServerColumnEncryptionKeyStoreProvider> clientKeyStoreProviders)`|カスタム キー ストア プロバイダーを登録できます。 これは、キー ストア プロバイダー名をキー ストア プロバイダー実装にマップするディクショナリです。<br /><br /> JVM キーストアを使用するには、JVM キーストアの資格情報を使用して SQLServerColumnEncryptionJVMKeyStoreProvider オブジェクトをインスタンス化し、ドライバーに登録する必要があります。 このプロバイダーの名前は 'MSSQL_JVM_KEYSTORE' である必要があります。<br /><br /> Azure Key Vault ストアを使用するには、SQLServerColumnEncryptionAzureKeyStoreProvider オブジェクトをインスタンス化し、ドライバーに登録する必要があります。 このプロバイダーの名前は ' AZURE_KEY_VAULT ' である必要があります。|
|`public final boolean getSendTimeAsDatetime()`|SendTimeAsDatetime 接続プロパティの設定を返します。|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)`|SendTimeAsDatetime 接続プロパティの設定を変更します。|

 **SQLServerConnectionPoolProxy クラス**
 
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`public final boolean getSendTimeAsDatetime()` | SendTimeAsDatetime 接続プロパティの設定を返します。|
|`public void setSendTimeAsDatetime(boolean sendTimeAsDateTimeValue)` | SendTimeAsDatetime 接続プロパティの設定を変更します。|
     
  
 **SQLServerDataSource クラス**  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`public void setColumnEncryptionSetting(String columnEncryptionSetting)`|データ ソース オブジェクトに対して Always Encrypted 機能を有効または無効にします。<br /><br /> 既定値は Disabled です。|  
|`public String getColumnEncryptionSetting()`|データ ソース オブジェクトに対して Always Encrypted 機能を取得します。|
|`public void setKeyStoreAuthentication(String keyStoreAuthentication)`|キー ストアを識別する名前を設定します。 サポートされている値は、Java キーストアを識別するための**JavaKeyStorePassword**だけです。<br/><br/>既定値は null です。|
|`public String getKeyStoreAuthentication()`|データソースオブジェクトの keyStoreAuthentication 設定の値を取得します。|
|`public void setKeyStoreSecret(String keyStoreSecret)`|Java キーストアのパスワードを設定します。 キーストアとキーのパスワードは同じである必要があります。 KeyStoreAuthentication は**JavaKeyStorePassword**で設定する必要があることに注意してください。|
|`public void setKeyStoreLocation(String keyStoreLocation)`|Java キーストアのファイル名を含む場所を設定します。 KeyStoreAuthentication は**JavaKeyStorePassword**で設定する必要があることに注意してください。|
|`public String getKeyStoreLocation()`|Java キーストアの keyStoreLocation を取得します。|
  
 **SQLServerColumnEncryptionJavaKeyStoreProvider クラス**  
  
 Java キー ストアにキー ストア プロバイダーを実装します。 このクラスは、Java キー ストアに格納されている証明書を列マスター キーとして使用できるようにします。  
  
 コンストラクター  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionJavaKeyStoreProvider (String keyStoreLocation, char[] keyStoreSecret)`|Java キーストアのキーストアプロバイダー。|  
  
 メソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)`|列暗号化キーの暗号化された指定値を暗号化解除します。 暗号化された値は、指定したキー パスと共に証明書を使用し、指定したアルゴリズムを使用して、暗号化されることが想定されています。<br /><br /> **キー パスの書式は次のいずれかになります。**<br /><br /> Thumbprint:<certificate_thumbprint><br /><br /> Alias:<certificate_alias><br /><br /> (SQLServerColumnEncryptionKeyStoreProvider.encryptColumnEncryptionKey(String, String, Byte[]) をオーバーライドします) decryptColumnEncryptionKey (String, String, Byte []).)|  
|`public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)`|指定したキー パスと共に証明書を使用し、指定したアルゴリズムを使用して、列暗号化キーを暗号化します。<br /><br /> **キー パスの書式は次のいずれかになります。**<br /><br /> Thumbprint:<certificate_thumbprint><br /><br /> Alias:<certificate_alias><br /><br /> (SQLServerColumnEncryptionKeyStoreProvider.encryptColumnEncryptionKey(String, String, Byte[]) をオーバーライドします) こと (String, String, Byte []).)|  
|`public void setName (String name)`|このキーストアプロバイダーの名前を設定します。|
|`public String getName ()`|このキーストアプロバイダーの名前を取得します。|
  
 **SQLServerColumnEncryptionAzureKeyVaultProvider クラス**  
  
 Azure Key Vault のキー ストア プロバイダーを実装します。 このクラスは、列マスターキーとして Azure Key Vault に格納されているキーを使用できるようにします。  
  
 コンストラクター  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`public SQLServerColumnEncryptionAzureKeyVaultProvider (String clientId, String clientKey)`|Azure Key Vault のキーストアプロバイダー。  Azure Key Vault に対する認証のためにトークンを要求するクライアントの識別子とキーを指定する必要があります。|  
  
 メソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
| `public byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)` | Decryptes 暗号化された列暗号化キー (CEK)。 この暗号化解除は、マスターキーパスによって指定された非対称キーを使用する RSA 暗号化アルゴリズムを使用して行われます。<br />(SQLServerColumnEncryptionKeyStoreProvider.encryptColumnEncryptionKey(String, String, Byte[]) をオーバーライドします) decryptColumnEncryptionKey (String, String, Byte []).) |  
| `public byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[] columnEncryptionKey)` | 指定した列マスター キーと指定したアルゴリズムを使用することで、列暗号化キーを暗号化します。<br />(SQLServerColumnEncryptionKeyStoreProvider.encryptColumnEncryptionKey(String, String, Byte[]) をオーバーライドします) こと (String, String, Byte []).) |  
|`public void setName (String name)`|このキーストアプロバイダーの名前を設定します。|
|`public String getName ()`|このキーストアプロバイダーの名前を取得します。|  
  
  
 **SQLServerKeyVaultAuthenticationCallback インターフェイス**  
  
 このインターフェイスには Azure Key Vault 認証用の1つのメソッドが含まれています。これはユーザーによって実装されます。  
  
 メソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`public String getAccessToken(String authority, String resource, String scope);`|メソッドをオーバーライドする必要があります。 メソッドは、Azure Key Vault するアクセストークンを取得するために使用されます。|  
  
 **SQLServerColumnEncryptionKeyStoreProvider クラス**  
  
 カスタム キー ストア プロバイダーを実装するには、このクラスを拡張します。  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|SQLServerColumnEncryptionKeyStoreProvider|すべてのキー ストア プロバイダーの基本クラス。 カスタム プロバイダーはこのクラスから派生し、そのメンバー関数をオーバーライドしてから、SQLServerConnection.registerColumnEncryptionKeyStoreProviders() を使用して登録する必要があります。 Sqlserverconnection.registercolumnencryptionkeystoreproviders ()。|  
  
 メソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`public abstract byte[] decryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte [] encryptedColumnEncryptionKey)`|列暗号化キーの暗号化された指定値を暗号化解除するための基本クラス メソッド。 暗号化された値は、指定したキー パスと共に列マスター キーを使用し、指定したアルゴリズムを使用して、暗号化されることが想定されています。|  
|`public abstract byte[] encryptColumnEncryptionKey (String masterKeyPath, String encryptionAlgorithm, byte[]  columnEncryptionKey)`|指定したキー パスと共に列マスター キーを使用し、指定したアルゴリズムを使用して、列暗号化キーを暗号化するための基本クラス メソッド。|
|`public abstract void setName(String name)`|このキーストアプロバイダーの名前を設定します。|
|`public abstract String getName()`|このキーストアプロバイダーの名前を取得します。|  
  
 **SQLServerPreparedStatement**クラスの新しいメソッドまたはオーバーロードされたメソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`public void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale)`<br /><br /> `public void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale)`<br /><br /> `public void setTime(int parameterIndex, java.sql.Time x, int scale)`<br /><br /> `public void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale)` <br />`public void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale)`|これらのメソッドは、有効桁数または小数点以下桁数の引数を使用してオーバーロードされます。また、有効桁数と小数点以下桁数の情報を必要とする特定のデータ型の Always Encrypted をサポートします。|  
|`public void setMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setSmallMoney(int parameterIndex, BigDecimal x)`<br /><br /> `public void setUniqueIdentifier(int parameterIndex, String guid)`<br /><br /> `public void setDateTime(int parameterIndex, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(int parameterIndex, java.sql.Timestamp x)`|これらのメソッドは、money、smallmoney、uniqueidentifier、datetime、および smalldatetime データ型の Always Encrypted をサポートするために追加されています。 <br/><br/>暗号化された`setTimestamp()` datetime2 列にパラメーター値を送信するために、既存のメソッドが使用されていることに注意してください。 暗号化された datetime および smalldatetime 列の場合`setDateTime()`は`setSmallDateTime()` 、新しいメソッドをそれぞれ使用します。|  
|`public final void setBigDecimal(int parameterIndex, BigDecimal x, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setSmallMoney(int parameterIndex, BigDecimal x, boolean forceEncrypt)`<br /><br /> `public final void setBoolean(int parameterIndex, boolean x, boolean forceEncrypt)`<br /><br /> `public final void setByte(int parameterIndex, byte x, boolean forceEncrypt)`<br /><br /> `public final void setBytes(int parameterIndex, byte x[], boolean forceEncrypt)`<br /><br /> `public final void setUniqueIdentifier(int parameterIndex, String guid, boolean forceEncrypt)`<br /><br /> `public final void setDouble(int parameterIndex, double x, boolean forceEncrypt)`<br /><br /> `public final void setFloat(int parameterIndex, float x, boolean forceEncrypt)`<br /><br /> `public final void setInt(int parameterIndex, int value, boolean forceEncrypt)`<br /><br /> `public final void setLong(int parameterIndex, long x, boolean forceEncrypt)`<br /><br /> `public final setObject(int parameterIndex, Object x, int targetSqlType, Integer precision, int scale, boolean forceEncrypt)`<br /><br /> `public final void setObject(int parameterIndex, Object x, SQLType targetSqlType, Integer precision, Integer scale, boolean forceEncrypt)`<br /><br /> `public final void setShort(int parameterIndex, short x, boolean forceEncrypt)`<br /><br /> `public final void setString(int parameterIndex, String str, boolean forceEncrypt)`<br /><br /> `public final void setNString(int parameterIndex, String value, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTimeOffset(int parameterIndex, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`<br /><br /> `public final void setDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setSmallDateTime(int parameterIndex, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public final void setDate(int parameterIndex, java.sql.Date x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTime(int parameterIndex, java.sql.Time x, java.util.Calendar cal, boolean forceEncrypt)`<br /><br /> `public final void setTimestamp(int parameterIndex, java.sql.Timestamp x, java.util.Calendar cal, boolean forceEncrypt)`|指定されたパラメーターを、渡された java 値に設定します。<br /><br /> ブール型の forceEncrypt を true に設定すると、指定した列が暗号化され、接続またはステートメントで Always Encrypted が有効になっている場合にのみ、クエリパラメーターが設定されます。<br /><br /> ブール型の forceEncrypt が false に設定されている場合、ドライバーはパラメーターの暗号化を強制しません。|  
  
 **SQLServerCallableStatement**クラスの新しいメソッドまたはオーバーロードされたメソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`public void registerOutParameter(int parameterIndex, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(int parameterIndex, SQLType sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, int sqlType, int precision, int scale)`<br /><br /> `public void registerOutParameter(String parameterName, SQLType sqlType, int precision, int scale)`<br />`public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale)`<br/><br/>`public final void setObject(String sCol, Object x, int targetSqlType, Integer precision, int scale)`|これらのメソッドは、有効桁数または小数点以下桁数の引数を使用してオーバーロードされます。また、有効桁数と小数点以下桁数の情報を必要とする特定のデータ型の Always Encrypted をサポートします。|  
|`public void setDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid)`<br /><br /> `public void setMoney(String parameterName, BigDecimal bd)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd)`<br/><br/>`public Timestamp getDateTime(int index)`<br/><br/>`public Timestamp getDateTime(String sCol)`<br/><br/>`public Timestamp getDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(int index)`<br/><br/>`public Timestamp getSmallDateTime(String sCol)`<br/><br/>`public Timestamp getSmallDateTime(int index, Calendar cal)`<br/><br/>`public Timestamp getSmallDateTime(String name, Calendar cal)`<br/><br/>`public BigDecimal getMoney(int index)`<br/><br/>`public BigDecimal getMoney(String sCol)`<br/><br/>`public BigDecimal getSmallMoney(int index)`<br/><br/>`public BigDecimal getSmallMoney(String sCol)`|これらのメソッドは、money、smallmoney、uniqueidentifier、datetime、および smalldatetime データ型の Always Encrypted をサポートするために追加されています。 <br/><br/>暗号化された`setTimestamp()` datetime2 列にパラメーター値を送信するために、既存のメソッドが使用されていることに注意してください。 暗号化された datetime および smalldatetime 列の場合`setDateTime()`は`setSmallDateTime()` 、新しいメソッドをそれぞれ使用します。|  
|`public void setObject(String parameterName, Object o, int n, int m, boolean forceEncrypt)`<br /><br /> `public void setObject(String parameterName, Object obj, SQLType jdbcType, int scale, boolean forceEncrypt)`<br /><br /> `public void setDate(String parameterName, java.sql.Date x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTime(String parameterName, java.sql.Time x, Calendar c, boolean forceEncrypt)`<br /><br /> `public void setDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setDateTimeOffset(String parameterName, microsoft.sql.DateTimeOffset t, int scale, boolean forceEncrypt)`<br /><br /> `public void setSmallDateTime(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp t, int scale, boolean forceEncrypt)`<br /><br /> `public void setTimestamp(String parameterName, java.sql.Timestamp x, boolean forceEncrypt)`<br /><br /> `public void setUniqueIdentifier(String parameterName, String guid, boolean forceEncrypt)`<br /><br /> `public void setBytes(String parameterName, byte[] b, boolean forceEncrypt)`<br /><br /> `public void setByte(String parameterName, byte b, boolean forceEncrypt)`<br /><br /> `public void setString(String parameterName, String s, boolean forceEncrypt)`<br /><br /> `public final void setNString(String parameterName, String value, boolean forceEncrypt)<br /><br /> public void setMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setSmallMoney(String parameterName, BigDecimal bd, boolean forceEncrypt)`<br /><br /> `public void setBigDecimal(String parameterName, BigDecimal bd, int precision, int scale, boolean forceEncrypt)`<br /><br /> `public void setDouble(String parameterName, double d, boolean forceEncrypt)`<br /><br /> `public void setFloat(String parameterName, float f, boolean forceEncrypt)`<br /><br /> `public void setInt(String parameterName, int i, boolean forceEncrypt)`<br /><br /> `public void setLong(String parameterName, long l, boolean forceEncrypt)`<br /><br /> `public void setShort(String parameterName, short s, boolean forceEncrypt)`<br /><br /> `public void setBoolean(String parameterNames, boolean b, boolean forceEncrypt)`<br/><br/>`public void setTimeStamp(String sCol, java.sql.Timestamp x, Calendar c, Boolean forceEncrypt)`|指定されたパラメーターを、渡された java 値に設定します。<br /><br /> ブール型の forceEncrypt を true に設定すると、指定した列が暗号化され、接続またはステートメントで Always Encrypted が有効になっている場合にのみ、クエリパラメーターが設定されます。<br /><br /> ブール型の forceEncrypt が false に設定されている場合、ドライバーはパラメーターの暗号化を強制しません。|
 

 **SQLServerResultSet**クラスの新しいメソッドまたはオーバーロードされたメソッド  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`public String getUniqueIdentifier(int columnIndex)`<br/><br/>`public String getUniqueIdentifier(String columnLabel)`<br/><br/>   `public java.sql.Timestamp getDateTime(int columnIndex)` <br/><br/> `public java.sql.Timestamp getDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getDateTime(int columnIndex, Calendar cal)`   <br/><br/>`public java.sql.Timestamp getDateTime(String colName, Calendar cal)`    <br/><br/>`public java.sql.Timestamp getSmallDateTime(int columnIndex)`    <br/><br/> `public java.sql.Timestamp getSmallDateTime(String columnName)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(int columnIndex, Calendar cal)`   <br/><br/> `public java.sql.Timestamp getSmallDateTime(String colName, Calendar cal)`   <br/><br/>  `public BigDecimal getMoney(int columnIndex)`  <br/><br/> `public BigDecimal getMoney(String columnName)`   <br/><br/> `public BigDecimal getSmallMoney(int columnIndex)`   <br/><br/>  `public BigDecimal getSmallMoney(String columnName)`  <br/><br/>`public void updateMoney(String columnName, BigDecimal x)`    <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x)`  <br/><br/>     `public void updateDateTime(int index, java.sql.Timestamp x)` <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x)` |これらのメソッドは、money、smallmoney、uniqueidentifier、datetime、および smalldatetime データ型の Always Encrypted をサポートするために追加されています。 <br/><br/>暗号化された`updateTimestamp()` datetime2 列の更新には、既存のメソッドが使用されていることに注意してください。 暗号化された datetime および smalldatetime 列の場合`updateDateTime()`は`updateSmallDateTime()` 、新しいメソッドをそれぞれ使用します。|
|`public void updateBoolean(int index, boolean x, boolean forceEncrypt)`  <br/><br/>  `public void updateByte(int index, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(int index, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(int index, int x, boolean forceEncrypt)`   <br/><br/>  `public void updateLong(int index, long x, boolean forceEncrypt)`  <br/><br/> `public void updateFloat(int index, float x, boolean forceEncrypt)`   <br/><br/> `public void updateDouble(int index, double x, boolean forceEncrypt)`   <br/><br/> `public void updateMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateSmallMoney(int index, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallMoney(String columnName, BigDecimal x, boolean forceEncrypt)`  <br/><br/> `public void updateBigDecimal(int index, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateString(int columnIndex, String stringValue, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(int columnIndex, String nString, boolean forceEncrypt)`  <br/><br/>  `public void updateNString(String columnLabel, String nString, boolean forceEncrypt)`  <br/><br/> `public void updateBytes(int index, byte x[], boolean forceEncrypt)   <br/><br/>  public void updateDate(int index, java.sql.Date x, boolean forceEncrypt)`  <br/><br/> `public void updateTime(int index, java.sql.Time x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateTimestamp(int index, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/> `public void updateDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/> `public void updateSmallDateTime(int index, java.sql.Timestamp x, Integer scale, boolean forceEncrypt)`   <br/><br/>  `public void updateDateTimeOffset(int index, microsoft.sql.DateTimeOffset x, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateUniqueIdentifier(int index, String x, boolean forceEncrypt)`    <br/><br/>  `public void updateObject(int index, Object x, int precision, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateObject(int index, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateBoolean(String columnName, boolean x, boolean forceEncrypt)`    <br/><br/>  `public void updateByte(String columnName, byte x, boolean forceEncrypt)`  <br/><br/>  `public void updateShort(String columnName, short x, boolean forceEncrypt)`  <br/><br/> `public void updateInt(String columnName, int x, boolean forceEncrypt)`   <br/><br/>   `public void updateLong(String columnName, long x, boolean forceEncrypt)` <br/><br/>  `public void updateFloat(String columnName, float x, boolean forceEncrypt)`  <br/><br/>  `public void updateDouble(String columnName, double x, boolean forceEncrypt)  <br/><br/> public void updateBigDecimal(String columnName, BigDecimal x, boolean forceEncrypt)`   <br/><br/>  `public void updateBigDecimal(String columnName, BigDecimal x, Integer precision, Integer scale, boolean forceEncrypt)`  <br/><br/> `public void updateString(String columnName, String x, boolean forceEncrypt)`   <br/><br/>  `public void updateBytes(String columnName, byte x[], boolean forceEncrypt)`  <br/><br/> `public void updateDate(String columnName, java.sql.Date x, boolean forceEncrypt)`   <br/><br/>  `public void updateTime(String columnName, java.sql.Time x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateTimestamp(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/> `public void updateDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`   <br/><br/>  `public void updateSmallDateTime(String columnName, java.sql.Timestamp x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateDateTimeOffset(String columnName, microsoft.sql.DateTimeOffset x, int scale, boolean forceEncrypt)`  <br/><br/>  `public void updateUniqueIdentifier(String columnName, String x, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object x, int precision, int scale, boolean forceEncrypt)`<br/><br/>`public void updateObject(String columnName, Object obj, SQLType targetSqlType, int scale, boolean forceEncrypt)`|指定された列を特定の java 値に更新します。<br/><br/>ブール型の forceEncrypt が true に設定されている場合、列は暗号化されていて、接続またはステートメントで Always Encrypted が有効になっている場合にのみ設定されます。<br/><br/>ブール型の forceEncrypt が false に設定されている場合、ドライバーはパラメーターの暗号化を強制しません。|

  
**Microsoft .sql. types**クラスの新しい型

|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|DATETIME、SMALLDATETIME、MONEY、SMALLMONEY、GUID|API メソッドを使用して`setObject()/updateObject()` 、**暗号化さ**れた datetime、smalldatetime、money、smallmoney、uniqueidentifier 列にパラメーター値を送信する場合は、これらの型をターゲット SQL 型として使用します。|  
  
  
 **SQLServerStatementColumnEncryptionSetting 列挙型**  
  
 暗号化された列を読み書きするときにデータを送受信する方法を指定します。 クエリによっては、暗号化されていない列を使用する場合に Always Encrypted ドライバーの処理をバイパスすることにより、パフォーマンスの影響が軽減される可能性があります。 暗号化を回避したり、プレーンテキスト データにアクセスしたりするためにこれらの設定値を使用することはできません。  
  
 **構文**  
  
```java
Public enum  SQLServerStatementColumnEncryptionSetting  
```  
  
 **メンバー**  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|UseConnectionSetting|接続文字列で、コマンドが Always Encrypted 設定を既定として設定するように指定します。|  
|有効|クエリで Always Encrypted を有効にします。|  
|ResultSetOnly|ドライバーでコマンドの結果だけを Always Encrypted ルーチンで処理するよう指定します。 コマンドに暗号化が必要なパラメーターがない場合にこの値を使用します。|  
|Disabled|クエリで Always Encrypted を無効にします。|  
  
 AE のステートメントレベルの設定は、SQLServerConnection クラスと SQLServerConnectionPoolProxy クラスに追加されます。 これらのクラスの次のメソッドは、新しい設定でオーバーロードされます。  
  
|[オブジェクト名]|[説明]|  
|----------|-----------------|  
|`public Statement createStatement(int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|指定された型、同時実行、保持機能、および列の暗号化設定を使用して ResultSet オブジェクトを生成するステートメントオブジェクトを作成します。|  
|`public CallableStatement prepareCall(String sql, int nType, int nConcur, int statementHoldability, SQLServerStatementColumnEncryptionSetting stmtColEncSetiing)`|指定された列の暗号化設定を使用して、指定された型、同時実行、および保持機能を持つ ResultSet オブジェクトを生成する CallableStatement オブジェクトを作成します。|  
|`public PreparedStatement prepareStatement(String sql, int autogeneratedKeys, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|自動的に生成されたキーを取得する機能を持つ、指定された列の暗号化設定を使用して、PreparedStatement オブジェクトを作成します。|  
|`public PreparedStatement prepareStatement(String sql, String[] columnNames, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|指定された列名を使用して ResultSet オブジェクトを生成する、指定された列の暗号化設定を使用して PreparedStatement オブジェクトを作成します。|  
|`public PreparedStatement prepareStatement(String sql, int[] columnIndexes, SQLServerStatementColumnEncryptionSetting stmtColEncSetting`|指定された列インデックスを使用して ResultSet オブジェクトを生成する、指定された列の暗号化設定を使用して PreparedStatement オブジェクトを作成します。|  
|`public PreparedStatement prepareStatement(String sql, int nType, int nConcur, int nHold, SQLServerStatementColumnEncryptionSetting stmtColEncSetting)`|指定された列の暗号化設定を使用して、指定された型、同時実行、および保持機能の ResultSet オブジェクトを生成する PreparedStatement オブジェクトを作成します。|  
  
> [!NOTE]  
>  クエリに対して Always Encrypted が無効になっていて、暗号化する必要があるパラメーター (暗号化された列に対応するパラメーター) がクエリに含まれている場合、クエリは失敗します。  
>   
>  クエリに対して Always Encrypted が無効になっていて、クエリが暗号化された列から結果を返す場合、クエリは暗号化された値を返します。 暗号化された値は varbinary データ型になります。  
  
 ## <a name="see-also"></a>参照  
 [JDBC ドライバーでの Always Encrypted の使用](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)  
  

