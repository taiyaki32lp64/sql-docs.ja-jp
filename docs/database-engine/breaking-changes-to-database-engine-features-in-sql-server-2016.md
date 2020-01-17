---
title: SQL Server 2016 におけるデータベース エンジン機能の重大な変更 | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 875e78cee077ec902dc1f845a330148e93f9edb8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013341"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2016"></a>SQL Server 2016 におけるデータベース エンジン機能の重大な変更
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  このトピックでは、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] および以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に関する重要な変更について説明します。 これらの変更によって、以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に基づくアプリケーション、スクリプト、または機能が使用できなくなる場合があります。 この問題は、アップグレードするときに発生することがあります。  
  
##  <a name="SQL15"></a> [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] における重大な変更  
  
-   `sys.dm_io_virtual_file_stats` の *sample_ms* 列が **int** データ型から **bigint** データ型に拡張されました。  
  
-   `sys.fn_virtualfilestats` の *TimeStamp* 列が **int** データ型から **bigint** データ型に拡張されました。  

-   データベース互換性レベル 130 の下で、 **datetime** から **datetime2** にデータ型を暗黙的に変換するとき、精度が上がります。小数ミリ秒が計算に入り、結果的にさまざまな変換値が生成されます。 datetime データ型と datetime2 データ型の間で混合比較シナリオが存在する場合、datetime2 データ型への明示的型変換を使用します。 詳しくは、こちらの [Microsoft サポート技術情報](https://support.microsoft.com/help/4010261)をご覧ください。

-   データベース互換性レベル 130 では、特定の数値データ型と datetime データ型の間で暗黙的な変換を実行する操作の精度が向上し、変換後の値が異なる可能性があります。 これには、`DATEDIFF` や `ROUND` などの計算が必要な関数の使用が含まれます。 詳しくは、こちらの [Microsoft サポート技術情報](https://support.microsoft.com/help/4010261)をご覧ください。

## <a name="previous-versions"></a> 以前のバージョン  

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] およびそれより前の一部のバージョンでの重大な変更については、「[SQL Server 2014 におけるデータベース エンジン機能の重大な変更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md?view=sql-server-2014)」をご覧ください。

#### <a name="archived-documentation-for-very-old-versions-of-sql-server"></a>SQL Server の非常に古いバージョンのアーカイブされたドキュメント

[!INCLUDE[Archived documentation for very old versions of SQL Server](../includes/paragraph-content/previous-versions-archive-documentation-sql-server.md)]

## <a name="see-also"></a>参照  
 [SQL Server 2016 データベース エンジンの非推奨の機能](../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [SQL Server 2016 で廃止されたデータベース エンジンの機能](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [SQL Server データベース エンジンの旧バージョンとの互換性](../database-engine/sql-server-database-engine-backward-compatibility.md)   
 [ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [いくつかのデータ型と一般的でない操作を処理するときの SQL Server と Azure の SQL データベースの機能強化](https://support.microsoft.com/help/4010261)   
