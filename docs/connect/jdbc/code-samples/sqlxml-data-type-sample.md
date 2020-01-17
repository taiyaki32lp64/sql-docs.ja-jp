---
title: SQLXML データ型のサンプル |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8f2ff25b-71fd-46d7-b6de-d656095d2aad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df376535f8f6c6a7d98e1744a2d2b70e813d400a
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028284"
---
# <a name="sqlxml-data-type-sample"></a>SQLXML データ型のサンプル

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

この [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] サンプル アプリケーションでは、**SQLXML** Java データ型を使用して、XML データをリレーショナル データベースに格納する方法、XML データをデータベースから取得する方法、および XML データを解析する方法を紹介します。

このセクションのコード例には、Simple API for XML (SAX) パーサーが使用されます。 SAX はイベント ベースで XML ドキュメントを解析する用途向けに、有志で策定された標準です。 XML データを操作するためのアプリケーション プログラミング インターフェイスも用意されています。 このアプリケーションでは、Document Object Model (DOM)、Streaming API for XML (StAX) など、他の任意の XML パーサーも利用できます。

Document Object Model (DOM) は、XML のドキュメント、フラグメント、ノード、またはノード セットのプログラミング的な表現を可能にします。 XML データを操作するためのアプリケーション プログラミング インターフェイスも用意されています。 同様に、Streaming API for XML (StAX) は、XML のプル解析を可能にする Java ベースの API です。

> [!IMPORTANT]  
> SAX パーサー API を使用するには、javax.xml パッケージから、標準の SAX 実装をインポートする必要があります。

このサンプルのコード ファイルは SqlXmlDataType.java という名前で、次の場所にあります。

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\datatypes
```

## <a name="requirements"></a>必要条件

このサンプル アプリケーションを実行するには、クラスパスを設定して sqljdbc4.jar ファイルを含める必要があります。 クラスパスに sqljdbc4.jar のエントリがない場合、サンプル アプリケーションで "Class not found" という例外がスローされます。 クラスパスの設定方法の詳細については、「 [JDBC ドライバーの使用](../../../connect/jdbc/using-the-jdbc-driver.md)」を参照してください。

また、このサンプル アプリケーションを実行するには、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースにアクセスする必要があります。

## <a name="example"></a>例

次のサンプル コードは、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] データベースへの接続を確立した後、createSampleTables メソッドを呼び出します。

createSampleTables メソッドは、テスト テーブル、TestTable1、TestTable2 が存在する場合、これらのテーブルを削除します。 そのうえで、TestTable1 に 2 つの行を挿入します。

また、コード サンプルには、後述する 3 つのメソッドと 1 つのクラス (ExampleContentHandler) が含まれています。

ExampleContentHandler クラスには、パーサー イベント用のメソッドを定義したカスタム コンテンツ ハンドラーが実装されています。

showGetters メソッドは、SQLXML オブジェクト内のデータを、SAX、ContentHandler、および XMLReader を使用して解析します。 まず、カスタム コンテンツ ハンドラー (ExampleContentHandler) のインスタンスを作成します。 次に、TestTable1 から一連のデータを返す SQL ステートメントを作成して実行します。 さらに、SAX パーサーを取得して、XML データを解析します。

showSetters メソッドは、SAX、ContentHandler、および ResultSet を使用して、**xml** 列を設定します。 まず、Connection クラスの [createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) メソッドを使用して、空の SQLXML オブジェクトを作成します。 次に、コンテンツ ハンドラーのインスタンスを取得して、そのデータを SQLXML オブジェクトに書き込みます。 その後、データを TestTable1 に書き込みます。 最後に、結果セット内のデータの行を繰り返し処理しながら、[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) メソッドを使用して、XML データを読み取ります。

showTransformer メソッドは、一方のテーブルから XML データを取得し、SAX および Transformer を使用して、その XML データを別のテーブルに挿入します。 最初に、TestTable1 からソース SQLXML オブジェクトを取得します。 次に、Connection クラスの [createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md) メソッドを使用して、ターゲット (挿入先) となる空の SQLXML オブジェクトを作成します。 その後、ターゲットの SQLXML オブジェクトを更新し、XML データを TestTable2 に書き込みます。 最後に、結果セット内のデータの行を繰り返し処理しながら、[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md) メソッドを使用して、TestTable2 の XML データを読み取ります。

[!code[JDBC#UsingSQLXML1](../../../connect/jdbc/codesnippet/Java/sqlxml-data-type-sample_1.java)]

## <a name="see-also"></a>参照

[データ型の処理 &#40;JDBC&#41;](../../../connect/jdbc/code-samples/working-with-data-types-jdbc.md)
