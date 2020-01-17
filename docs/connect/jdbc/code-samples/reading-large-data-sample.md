---
title: 大規模なデータの読み取りサンプル |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6c986144-3854-4352-8331-e79eccbefc28
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f39bda7c98382e1bb3a63047a80a2afb34008808
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028318"
---
# <a name="reading-large-data-sample"></a>大きなデータを読み取るサンプル

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

この [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] サンプル アプリケーションでは、[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) メソッドを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースから大きな単一列値を取得する方法を示します。

このサンプルのコード ファイルは ReadLargeData.java という名前で、次の場所にあります。

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples\adaptive
```

## <a name="requirements"></a>必要条件

このサンプル アプリケーションを実行するには、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] サンプル データベースへのアクセス権が必要です。 また、クラスパスの設定で mssql-jdbc jar ファイルを追加します。 クラスパスの設定方法の詳細については、「 [JDBC ドライバーの使用](../../../connect/jdbc/using-the-jdbc-driver.md)」を参照してください。

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] には、必要な Java ランタイム環境 (JRE) 設定に応じて使用される mssql-jdbc クラス ライブラリ ファイルが用意されています。 選択する JAR ファイルの詳細については、「[JDBC Driver のシステム要件](../../../connect/jdbc/system-requirements-for-the-jdbc-driver.md)」を参照してください。

## <a name="example"></a>例

次の例のサンプル コードでは、[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal_md.md)] データベースへの接続を行います。 次に、サンプル データを作成し、パラメーター化クエリを使用して Production.Document テーブルを更新します。

さらに、このサンプル コードでは、[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) クラスの [getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md) メソッドを使用してアダプティブ バッファリング モードを取得する方法も示されています。 JDBC Driver Version 2.0 リリース以降では、responseBuffering 接続プロパティが既定で "adaptive" に設定されていることに注意してください。

次に、サンプル コードでは、[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトで SQL ステートメントを使用して、SQL ステートメントを実行し、返されたデータを [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトに配置します。

最後に、結果セット内のデータ行を繰り返し処理し、[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md) メソッドを使用してデータの一部にアクセスします。

[!code[JDBC#UsingAdaptiveBuffering1](../../../connect/jdbc/codesnippet/Java/reading-large-data-sample_1.java)]

## <a name="see-also"></a>参照

[大きなデータの処理](../../../connect/jdbc/code-samples/working-with-large-data.md)
