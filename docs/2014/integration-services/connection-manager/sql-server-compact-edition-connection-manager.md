---
title: SQL Server Compact Edition 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 752c825cb34fbf2afe5d2306afbd562a49f74b7f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833147"
---
# <a name="sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 接続マネージャー
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 接続マネージャーを使用すると、パッケージは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースに接続できます。  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact 変換先は、この接続マネージャーを使用して、データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースに接続できます。  
  
> [!NOTE]  
>  64 ビット コンピューターでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データ ソースに接続するパッケージを 32 ビット モードで実行する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Compact データ ソースへの接続に使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact Provider は、32 ビット版でのみ使用できます。  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>SQL Server Compact Edition 接続マネージャーの構成  
 追加すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 接続マネージャーをパッケージに[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]接続を解決するマネージャーを作成、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 接続、実行時に、接続マネージャーのプロパティを設定し、接続マネージャーを追加します、`Connections`パッケージのコレクション。  
  
 接続マネージャーの `ConnectionManagerType` プロパティは、`SQLMOBILE` に設定されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 接続マネージャーは、次の方法で構成できます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact データベースの場所を指定する接続文字列を指定します。  
  
-   パスワードで保護されているデータベースのパスワードを指定します。  
  
-   データベースが格納されるサーバーを指定します。  
  
-   接続マネージャーから作成される接続を、実行時に保持するかどうかを指定します。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[SQL Server Compact Edition 接続マネージャー エディター] &#40;[接続] ページ&#41;](../sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
-   [[SQL Server Compact Edition 接続マネージャー エディター] &#40;[すべて] ページ&#41;](../sql-server-compact-edition-connection-manager-editor-all-page.md)  
  
 プログラムによる接続マネージャーの構成については、「 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 」と「 [プログラムによる接続の追加](../building-packages-programmatically/adding-connections-programmatically.md)に設定されます。  
  
  
