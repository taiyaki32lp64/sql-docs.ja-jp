---
title: SQLXML を使用したプログラミング |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4d2cc57c-7293-4d92-b8b1-525e2b35f591
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22f225799e704b7a34449bbfc69ef351cc4d4ac1
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027769"
---
# <a name="programming-with-sqlxml"></a>SQLXML でのプログラミング
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  このセクションでは、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] API のメソッドを使用し、**SQLXML** オブジェクトを介して、リレーショナル データベースに XML ドキュメントを格納したり、リレーショナル データベースから XML ドキュメントを取得したりする方法について説明します。  
  
 また、SQLXML オブジェクトの型についての情報や、SQLXML オブジェクトを使用するうえでの重要なガイドラインおよび制限事項の一覧も掲載されています。  
  
## <a name="reading-and-writing-xml-data-with-sqlxml-objects"></a>SQLXML オブジェクトを使用した XML データの読み取りと書き込み  
 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] API のメソッドと SQLXML オブジェクトを使用して、XML データの読み取りと書き込みを行う方法は次のとおりです。  
  
-   SQLXML オブジェクトを作成するには、[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) メソッドを使用します。 このメソッドで作成される SQLXML オブジェクトにはデータが一切含まれていないことに注意してください。 SQLXML オブジェクトに**xml**データを追加するには、sqlxml インターフェイスで指定されている次のいずれかのメソッドを呼び出します: setresult、Setresult Stream、setbinarystream、または setresult。  
  
-   SQLXML オブジェクトそのものを取得するには、[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) クラスまたは [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスの getSQLXML メソッドを使用します。  
  
-   SQLXML オブジェクトから**xml**データを取得するには、sqlxml インターフェイスに指定されている次のメソッドのいずれかを使用します。 getsource、Getsource Stream、getbinarystream、または getString。  
  
-   SQLXML オブジェクト内の **xml** データを更新するには、[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) クラスの [updateSQLXML](../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md) メソッドを使用します。  
  
-   SQLXML オブジェクトをデータベース テーブルの **xml** 型の列に格納するには、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスまたは [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスの setSQLXML メソッドを使用します。  
  
 「[SQLXML データ型のサンプル](../../connect/jdbc/sqlxml-data-type-sample.md)」に記載されているコード例では、これらの一般的な API タスクを実行する方法が示されています。  
  
## <a name="readable-and-writable-sqlxml-objects"></a>読み取り/書き込み可能な SQLXML オブジェクト  
 次の表は、JDBC API の setter、getter、および updater メソッドによってサポートされる SQLXML オブジェクトの種類を一覧にしたものです。 この表の各列の意味は次のとおりです。  
  
-   「**メソッド名**」列は、JDBC API でサポートされている getter、setter、および updater メソッドの一覧です。  
  
-   「**getter SQLXML オブジェクト**」列は、[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスの [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlservercallablestatement.md) メソッドまたは [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) クラスの [getSQLXML](../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) メソッドによって作成される SQLXML オブジェクトを表します。  
  
-   「**setter SQLXML オブジェクト**」列は、[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) メソッドによって作成される SQLXML オブジェクトを表します。 以下の setter メソッドは、[createSQLXML](../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) メソッドによって作成された SQLXML オブジェクトしか受け付けない点に注意してください。  
  
|メソッド名|getter SQLXML オブジェクト<br /><br /> (読み取り可能)|setter SQLXML オブジェクト<br /><br /> (書き込み可能)|  
|-----------------|-------------------------------------------|-------------------------------------------|  
|CallableStatement. setSQLXML ()|サポートされていません|Supported|  
|CallableStatement.setObject()|サポートされていません|Supported|  
|PreparedStatement.setSQLXML()|サポートされていません|Supported|  
|PreparedStatement.setObject()|サポートされていません|Supported|  
|ResultSet.updateSQLXML()|サポートされていません|Supported|  
|ResultSet.updateObject()|サポートされていません|Supported|  
|ResultSet。 getSQLXML ()|Supported|サポートされていません|  
|CallableStatement。 getSQLXML ()|Supported|サポートされていません|  
  
 この表を見るとわかるように、setter SQLXML メソッドは、読み取り可能な SQLXML オブジェクトでは使用できません。同様に、getter メソッドを書き込み可能な SQLXML オブジェクトで使用することもできません。  
  
 アプリケーションから setObject メソッドを呼び出すときに、SQLXML オブジェクトとの組み合わせで、scale パラメーターまたは length パラメーターを指定した場合、これらのパラメーターは無視されます。  
  
## <a name="guidelines-and-limitations-when-using-sqlxml-objects"></a>SQLXML オブジェクトを使用する場合のガイドラインと制限  
 アプリケーションは SQLXML オブジェクトを使用して、データベースとの間で XML データの読み取りと書き込みを行うことができます。 以下に、SQLXML オブジェクトを使用するうえでの特定の制限と指針を箇条書きでまとめました。  
  
-   SQLXML オブジェクトの有効期間は、そのオブジェクトが作成されたトランザクションの期間内に限られます。  
  
-   getter メソッドから受け取った SQLXML オブジェクトは、データの読み取りにしか使用できません。  
  
-   接続オブジェクトによって作成された SQLXML オブジェクトは、データの書き込みにしか使用できません。  
  
-   アプリケーションは、読み取り可能な SQLXML オブジェクトの getter メソッドを 1 つだけ呼び出してデータを読み取ることができます。 getter メソッドを呼び出した後で、同じ SQLXML オブジェクトの他の getter メソッドまたは setter メソッドを呼び出そうとするとエラーになります。  
  
-   アプリケーションは SQLXML オブジェクトの読み取りまたは書き込みが完了した後、その SQLXML オブジェクトに対して free メソッドのみを呼び出すことができます。 ただし、基になる列またはパラメーターが有効である限り、返されたストリームまたはソースを処理することは可能です。 基になる列またはパラメーターが無効になった場合、SQLXML オブジェクトに関連付けられていたストリームやソースは閉じられます。 基になる列またはパラメーターが無効になった時点で、ストリーム、SAX (Simple API for XML)、および StAX (Streaming API for XML) の getter の基となっているデータが利用できなくなります。  
  
-   アプリケーションは、書き込み可能な SQLXML オブジェクトの setter メソッドを 1 つだけ呼び出すことができます。 setter メソッドを呼び出した後で、同じ SQLXML オブジェクトの他の setter メソッドまたは getter メソッドを呼び出そうとするとエラーになります。  
  
-   SQLXML オブジェクトに対してデータを設定するには、返されたオブジェクトの適切な setter メソッドや関数を使用する必要があります。  
  
-   基になる列が **null** の場合、[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスおよび [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) クラスの getSQLXML メソッドは、**null** データを返します。  
  
-   setter オブジェクトは、そのオブジェクトが作成された接続の間、有効です。  
  
-   アプリケーションから、SQLXML インターフェイスに定義されている setter メソッドを使用して **null** 値を設定することはできません。 アプリケーションから、SQLXML インターフェイスに定義されている setter メソッドを使用して空の文字列 ("") を設定することはできます。 **null** 値を設定するには、次のいずれかを呼び出す必要があります。  
  
    -   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスおよび [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスの setNull メソッド。  
  
    -   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスおよび [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスの setObject メソッド。  
  
    -   [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスおよび [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスの setSQLXML メソッド (パラメーター値として **null** を指定)。  
  
-   XML ドキュメントを扱う場合は、パフォーマンス上の理由から、Document Object Model (DOM) パーサーではなく、Simple API for XML (SAX) および Streaming API for XML (StAX) パーサーの使用をお勧めします。  
  
 XML パーサーは空の値を処理できません。 ただし、SQL Server が介在することで、アプリケーションが、XML データ型のデータベース列から空の値を取得したり、空の値を格納したりできるようになっています。 つまり、XML データを解析する際、基になる値が空である場合は、パーサーによって例外がスローされます。 DOM 出力の場合、JDBC ドライバーがその例外をキャッチして、エラーをスローします。 SAX および Stax 出力の場合、エラーは直接パーサーから送られます。  
  
## <a name="adaptive-buffering-and-sqlxml-support"></a>アダプティブ バッファリングと SQLXML サポート  
 SQLXML オブジェクトから返されたバイナリ ストリームと文字ストリームは、アダプティブ バッファリング モードまたはフル バッファリング モードに従います。 一方、XML パーサーがストリームではない場合、アダプティブとフルのいずれの設定にも従いません。 アダプティブバッファリングの詳細については、「[アダプティブバッファリングの使用](../../connect/jdbc/using-adaptive-buffering.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML データのサポート](../../connect/jdbc/supporting-xml-data.md)  
  
  
