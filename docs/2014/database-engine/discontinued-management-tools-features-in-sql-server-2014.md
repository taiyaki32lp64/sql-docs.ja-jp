---
title: 管理ツール機能が SQL Server 2014 で廃止された |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 6e58acd0-73c5-4161-9fbc-8ea531bc681c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7c966c3e4388588810438d7e91a9ae0356ef60c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62780351"
---
# <a name="discontinued-management-tools-features-in-sql-server-2014"></a>SQL Server 2014 で廃止された管理ツール機能
  このトピックでは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] で使用できなくなった [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]管理ツール機能について説明します。  
  
## <a name="features-removed-in-includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] で削除された機能  
 なし  
  
## <a name="features-removed-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] で削除された機能  
  
### <a name="sql-server-compact-edition"></a>SQL Server Compact Edition  
 SQL Server Compact Edition コード エディターは [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]から削除されました。 また、SQL Server Compact Edition のサポートは、オブジェクト エクスプローラー、ソリューション エクスプローラー、およびテンプレート エクスプローラーから削除されました。 Microsoft Visual Studio 2010 Service Pack 1 または Webmatrix の Transact-SQL エディターを使用してください。  
  
### <a name="activex-subsystem-for-sql-server-agent"></a>SQL Server エージェント用の ActiveX サブシステム  
 このリリースでは、SQL Server エージェント用の ActiveX サブシステムが削除されています。 これに代わる機能はありません。  
  
### <a name="spaddtask-spdeletetask-spupdatetask"></a>sp_addtask、sp_deletetask、sp_updatetask  
 このリリースでは、sp_addtask、sp_deletetask、および sp_updatetask が削除されています。 新規または更新済みのアプリケーションでは、この機能を使用しないでください。  
  
### <a name="net-send-and-pager-notification"></a>Net Send およびポケットベルによる通知  
 このリリースでは、Net Send およびポケットベルによる通知が削除されています。 新規または更新済みのアプリケーションでは、この機能を使用しないでください。  
  
### <a name="data-tier-applications"></a>データ層アプリケーション  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] にあった一部のデータ層アプリケーション (DAC) の機能は [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]で削除されました。 ただし、[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] でリリースされたデータ層アプリケーション フレームワーク DACfx (Version 3.0) は [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] および [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] を通じて [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] と互換性があります。 DAC version 3.0 は、 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] の [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] など、以前のバージョンの [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]ではサポートされていません。 Visual Studio 2010 のデータベース プロジェクトは、DACfx Version 3.0 以降で生成される DAC Export (BACPAC) パッケージや DAC 3.0 DACPAC パッケージをサポートしません。  
  
 入手可能な最新バージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools データベース プロジェクトの使用をお勧めします。  
  
 DACfx 3.0 API と [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ツールは、以前の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ツールや DACfx バージョンを使って作成された DACPAC および BACPAC ファイルの読み取りをサポートしません。つまり、これらのバージョンからデータベースを DACPAC ファイルに抽出したり、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] または [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] Data Tools を通じて、サポートされているバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] にデータベースを配置したりすることはできません。  
  
## <a name="see-also"></a>参照  
 [旧バージョンとの互換性](../../2014/getting-started/backward-compatibility.md)  
  
  
