---
title: 大規模なデータを操作する |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 5b93569f-eceb-4f05-b49c-067564cd3c85
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 425beac7bcae36170ff378b59d36da05838df645
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028252"
---
# <a name="working-with-large-data"></a>大きなデータの処理

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

JDBC ドライバーは、サーバー カーソルのオーバーヘッドを発生させることなく、あらゆる種類の大きな値のデータを取得できるアダプティブ バッファリングをサポートします。 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] でアダプティブ バッファリングを使用すると、ステートメントの実行結果を [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] から取得する処理が、すべて一度にではなく、アプリケーションの必要に応じて行われます。 また、アプリケーションからアクセスできなくなった結果は、ドライバーによって直ちに破棄されます。  
  
[!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] JDBC Driver バージョン 1.2 のバッファリング モードの既定値は "**full**" でした。 アプリケーションで、接続プロパティを使用するか、[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトの [setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) メソッドを使用して、"responseBuffering" 接続プロパティを "**adaptive**" に設定しなかった場合、サーバーから結果全体を一度に読み取るという動作になっていました。 アダプティブ バッファリングの動作をアプリケーションに実装するには、明示的に "responseBuffering" 接続プロパティを "**adaptive**" に設定する必要があります。  
  
**adaptive** 値はバッファリング モードの規定値であり、JDBC ドライバーは、必要に応じて最小限のデータをバッファリングします。 アダプティブバッファリングの使用方法の詳細については、「[アダプティブバッファリングの使用](../../../connect/jdbc/using-adaptive-buffering.md)」を参照してください。  
  
このセクションのトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースから大きな値のデータを取得するための、さまざまな方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
| トピック                                                                                                                         | [説明]                                                              |
| ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| [大きなデータを読み取るサンプル](../../../connect/jdbc/code-samples/reading-large-data-sample.md)                                               | SQL ステートメントを使用して大きな値のデータを取得する方法について説明します。       |
| [ストアド プロシージャで大きなデータを読み取るサンプル](../../../connect/jdbc/code-samples/reading-large-data-with-stored-procedures-sample.md) | 大きな CallableStatement OUT パラメーター値を取得する方法について説明します。 |
| [大きなデータを更新するサンプル](../../../connect/jdbc/code-samples/updating-large-data-sample.md)                                             | データベース内の大きな値のデータを更新する方法について説明します。                |
  
## <a name="see-also"></a>参照

[サンプル JDBC ドライバー アプリケーション](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
  
