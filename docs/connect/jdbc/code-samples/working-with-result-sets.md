---
title: 結果セットを操作する |Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4fc4b1c6-3075-4ad7-9244-865d9ede7ae6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44eac2fbcc156b3591bdf02fd00ff0d6bd19366b
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028242"
---
# <a name="working-with-result-sets"></a>結果セットの処理

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに格納されているデータを操作するための方法の 1 つに、結果セットを使用する方法があります。 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] は、[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトを介して結果セットの使用をサポートします。 SQLServerResultSet オブジェクトを使用することで、SQL ステートメントまたはストアド プロシージャから返されたデータを取得し、必要に応じてデータを更新し、データをデータベースに戻して保持できます。  
  
また、SQLServerResultSet オブジェクトは、このオブジェクトのデータ行間を移動したり、オブジェクトに含まれるデータを取得または設定したり、基になるデータベースの変更に対するさまざまなレベルの応答性を確立したりするためのメソッドを提供します。  
  
> [!NOTE]  
> 変更に対する感度など、結果セットの管理の詳細については、「 [JDBC ドライバーを使用した結果セットの管理](../../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)」を参照してください。  
  
このセクションのトピックでは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースに含まれているデータを操作するために結果セットを使用できるさまざまな方法について説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
| トピック                                                                                           | [説明]                                                                                                                                                                                             |
| ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [結果セットのデータ サンプルの取得](../../../connect/jdbc/code-samples/retrieving-result-set-data-sample.md) | 結果セットを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースからデータを取得し、表示する方法について説明します。                                                         |
| [結果セットのデータ サンプルの変更](../../../connect/jdbc/code-samples/modifying-result-set-data-sample.md)   | 結果セットを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースのデータを挿入、取得、および変更する方法について説明します。                                                      |
| [結果セットのデータ サンプルのキャッシング](../../../connect/jdbc/code-samples/caching-result-set-data-sample.md)       | 結果セットを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースから大量のデータを取得し、そのデータがクライアント上でキャッシュされる方法を制御する方法について説明します。 |
  
## <a name="see-also"></a>参照  

[サンプル JDBC ドライバー アプリケーション](../../../connect/jdbc/code-samples/sample-jdbc-driver-applications.md)  
  
