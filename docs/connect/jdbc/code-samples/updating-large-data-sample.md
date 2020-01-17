---
title: 大きなデータサンプルを更新しています |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 76ecc05f-a77d-40a2-bab9-91a7fcf17347
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bd284f6fb8021164aa3edf6aa31761b7483406e
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028264"
---
# <a name="updating-large-data-sample"></a>大きなデータを更新するサンプル

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

この [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] サンプル アプリケーションは、データベース内の大きな列値を更新する方法を示しています。

このサンプルのコード ファイルは UpdateLargeData.java という名前で、次の場所にあります。

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>必要条件

このサンプル アプリケーションを実行するには、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースへのアクセス権が必要です。 また、クラスパスの設定で sqljdbc4.jar ファイルを追加します。 クラスパスに sqljdbc4.jar のエントリがない場合、サンプル アプリケーションで "Class not found" という一般的な例外がスローされます。 クラスパスの設定方法の詳細については、「 [JDBC ドライバーの使用](../../../connect/jdbc/using-the-jdbc-driver.md)」を参照してください。

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] には、sqljdbc.jar、sqljdbc4.jar、sqljdbc41.jar、または sqljdbc42.jar のクラス ライブラリ ファイルが用意されており、必要な Java ランタイム環境 (JRE) 設定によって自由に使い分けることができます。 このサンプルは、JDBC 4.0 API で導入された [isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) メソッドと [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) メソッドを使用して、ドライバー固有の応答バッファリング メソッドにアクセスします。 このサンプルをコンパイルして実行するには、JDBC 4.0 をサポートする sqljdbc4.jar クラス ライブラリが必要となります。 選択する JAR ファイルの詳細については、「[JDBC Driver のシステム要件](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)」を参照してください。

## <a name="example"></a>例

次の例のサンプル コードでは、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] データベースへの接続を行います。 さらに、Statement オブジェクトを作成し、[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md) メソッドを使用して、Statement オブジェクトが、指定された [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) クラスのラッパーであるかどうかをチェックします。 ドライバー固有の応答バッファリング メソッドにアクセスするために、[unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) メソッドが使用されています。

次に、[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) クラスの [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) メソッドを使用して、応答バッファリング モードを "**adaptive**" に設定します。サンプル コードを見ると、アダプティブ バッファリング モードの取得方法も確認できます。

さらに、SQL ステートメントを実行し、返されたデータを更新可能な [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトに設定しています。

最後に、結果セット内のデータ行を繰り返し処理します。 空のドキュメント概要が見つかった場合、[updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md) メソッドと [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) メソッドを組み合わせて使用して、データの行を更新し、再度データベースに格納します。 既にデータが存在する場合は、[getString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md) メソッドを使用して、データの一部が表示されます。

ドライバーの既定の動作は "**adaptive**" です。 ただし、順方向専用の更新可能な結果セットの場合で、なおかつ、結果セットのデータのサイズが、アプリケーションのメモリ容量を超える場合は、[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) クラスの [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) メソッドを使用して、アプリケーションからアダプティブ バッファリング モードを明示的に設定する必要があります。

[!code[JDBC#UsingAdaptiveBuffering3](../../../connect/jdbc/codesnippet/Java/updating-large-data-sample_1.java)]

## <a name="see-also"></a>参照

[大きなデータの処理](../../../connect/jdbc/code-samples/working-with-large-data.md)
