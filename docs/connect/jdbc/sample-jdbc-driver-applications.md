---
title: サンプル JDBC driver applications |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e136b87c-a138-45d6-8c3e-bcef94b7e483
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e6a8ac2279446e70c6d31467eacbe54ad50386d
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027805"
---
# <a name="sample-jdbc-driver-applications"></a>サンプル JDBC ドライバー アプリケーション

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] サンプル アプリケーションは、JDBC ドライバーのさまざまな機能を示しています。 さらに、JDBC ドライバーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースで使用するときに参考にできる、適切なプログラミング例も示します。  
  
すべてのサンプル アプリケーションは、ローカル コンピューターでコンパイルおよび実行することができる *.java コード ファイルに含まれ、これらは次の場所の各サブフォルダーに格納されています。  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples  
```

このセクションのトピックでは、サンプル アプリケーションを構成および実行する方法と、サンプル アプリケーションが示す内容について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
| トピック                                                                                                        | [説明]                                                                                                                                                                                                                                                             |
| ------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [接続およびデータの取得](../../connect/jdbc/connecting-and-retrieving-data.md)                       | これらのサンプル アプリケーションは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへの接続方法を示します。 また、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースからデータを取得するさまざまな方法も示します。 |
| [データ型の処理 &#40;JDBC&#41;](../../connect/jdbc/working-with-data-types-jdbc.md)                 | これらのサンプル アプリケーションは、JDBC ドライバーのデータ型のメソッドを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内のデータを処理する方法を示します。                                                                                           |
| [結果セットの処理](../../connect/jdbc/working-with-result-sets.md)                                   | これらのサンプル アプリケーションは、結果セットを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに含まれるデータを処理する方法を示します。                                                                                                         |
| [大きなデータの処理](../../connect/jdbc/working-with-large-data.md)                                     | これらのサンプル アプリケーションは、アダプティブ バッファリングを使用して、サーバー カーソルのオーバーヘッドを発生させることなく、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースから大きな値のデータを取得する方法を示します。                                                      |
| [SQL データの検出と分類](../../connect/jdbc/data-discovery-classification-sample.md) | このサンプルアプリケーションは、JDBC ドライバーを使用して、ResultSet オブジェクトから[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データベースに含まれているデータ検出と分類情報を取得する方法を示しています。                                      |
  
## <a name="see-also"></a>参照

[JDBC ドライバーの概要](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
