---
title: 重大な変更を管理ツールで SQL Server 2014 の機能 |Microsoft Docs
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 3ff3fad8-b569-4516-bd58-5a3efeb537e2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 73e2c6ecb4ae2f829c02897ed5c6ab5d84f1ba4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62787024"
---
# <a name="breaking-changes-to-management-tools-features-in-sql-server-2014"></a>SQL Server 2014 の管理ツール機能における重大な変更
  このトピックでは、管理ツール機能における重大な変更について説明します。 これらの変更によって、以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に基づくアプリケーション、スクリプト、または機能が使用できなくなる場合があります。 この問題は、アップグレードするときに発生することがあります。 詳細については、「 [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)」を参照してください。  
  
## <a name="breaking-changes-in-includesssql14includessssql14-mdmd"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] における重大な変更  
 今後、情報が追加されていきます。  
  
## <a name="breaking-changes-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] における重大な変更  
  
### <a name="you-cannot-use-includesssql11includessssql11-mdmd-management-tools-to-create-a-utility-control-point-on-a-includesskilimanjaroincludessskilimanjaro-mdmd-instance-of-sql-server"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 管理ツールを使用して、SQL Server の [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] インスタンスにユーティリティ コントロール ポイントを作成することはできない  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]のインスタンスにユーティリティ コントロール ポイントを作成するには、 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 管理ツールを使用してください。  
  
### <a name="smo-has-been-reversioned-in-includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] では SMO のバージョンが再設定されている  
 [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] 以前のバージョンの SMO で開発されたコードを [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] でビルドするには、若干の変更が必要になることがあります。 旧バージョンとの互換性については、「 [SMO の旧バージョンとの互換性](../relational-databases/server-management-objects-smo/backward-compatibility-in-smo.md)」を参照してください。  

## <a name="previous-versions"></a> SQL Server 2005 における重大な変更  

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>参照  
 [旧バージョンとの互換性](../../2014/getting-started/backward-compatibility.md)  
 [重大な変更を SQL Server 2014 における管理ツール機能の詳細](breaking-changes-to-database-engine-features-in-sql-server-2016.md?view=sql-server-2014)  
  
  
