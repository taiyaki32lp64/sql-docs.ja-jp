---
title: Master データベース
description: Parallel Data Warehouse の master データベースについて説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cafef8a5b702b6df4475d34e9395bb12bc9461fb
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400984"
---
# <a name="master-database---parallel-data-warehouse"></a>Master データベース-並列データウェアハウス
SQL Server PDW master データベースには、アプライアンスレベルのログイン情報とデータベースカタログが格納されます。 これは、コントロールノードに存在する SQL Server マスターデータベースです。 そのため、master が SQL Server に提供するのと同様の機能を SQL Server PDW に提供します。  
  
システムデータベースの詳細については、「[システムデータベース](system-databases.md)」を参照してください。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
次の一覧では、SQL Server PDW master データベースに対して実行できない操作について説明します。  
  
*次のことはできません。*  
  
-   Master の差分バックアップを実行します。  
  
-   Master にユーザーオブジェクトを作成します。  
  
-   Master の照合順序を変更します。  
  
-   Master の所有者を変更します。  
  
-   マスターを削除または名前変更します。  
  
-   Master に対するアクセス許可を変更します。  
  
-   **DBCC SHRINKLOG**を実行します。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスク|説明|  
|--------|---------------|  
|Master の完全バックアップを作成します。|例:<br /><br />`BACKUP DATABASE master TO backup_directory;`<br /><br />詳細については、「 [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)」を参照してください。|  
|master データベースの復元|Master データベースを復元するには、Configuration Manager ツールの [ [Master データベースの復元](restore-the-master-database.md)] ページを使用します。|  
|データベースカタログ情報を表示します。|`SELECT * FROM master.sys.databases;`|  
|システム全体のログインとアクセス許可の情報を表示します。|`SELECT * FROM master.sys.server_permissions;`<br /><br />`SELECT * FROM master.sys.server_principals;`<br /><br />`SELECT * FROM master.sys.sql_logins;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
