---
title: ODBC 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], ODBC
- ODBC connection manager
- data sources [Integration Services], connections
- connection managers [Integration Services], ODBC
ms.assetid: e8c77aa7-6772-485e-918e-cef9eeb18c58
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c6c7ecd59bcf3a3ece0d61ecbb428bb39a80068f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833764"
---
# <a name="odbc-connection-manager"></a>ODBC 接続マネージャー
  ODBC 接続マネージャーを使用すると、パッケージは Open Database Connectivity (ODBC) の仕様を使用して、さまざまなデータベース管理システムに接続できます。  
  
 ODBC 接続をパッケージに追加の接続マネージャーのプロパティを設定すると[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]接続マネージャーを作成し、接続マネージャーを追加します、`Connections`パッケージのコレクション。 接続マネージャーは、実行時に物理 ODBC 接続として解決されます。  
  
 接続マネージャーの `ConnectionManagerType` プロパティは、`ODBC` に設定されます。  
  
 ODBC 接続マネージャーは、次の方法で構成できます。  
  
-   ユーザーまたはシステム データ ソースの名前を参照する、接続文字列を指定します。  
  
-   接続先のサーバーを指定します。  
  
-   接続を実行時に保持するかどうかを示します。  
  
## <a name="configuration-of-the-odbc-connection-manager"></a>ODBC 接続マネージャーの構成  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [ODBC 接続マネージャーの UI リファレンス](../odbc-connection-manager-ui-reference.md)  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
## <a name="see-also"></a>関連項目  
 [Integration Services &#40;SSIS&#41; の接続](integration-services-ssis-connections.md)  
  
  
