---
title: 一括インポートで最小ログ記録を行うための前提条件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- minimal logging [SQL Server]
- logged bulk copy [SQL Server]
- logs [SQL Server], minimal logging
- minimally logged operations [SQL Server]
- bulk importing [SQL Server], minimal logging
ms.assetid: bd1dac6b-6ef8-4735-ad4e-67bb42dc4f66
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ccb9642982b8680e4111346298e7a70bbc606dbb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011886"
---
# <a name="prerequisites-for-minimal-logging-in-bulk-import"></a>一括インポートで最小ログ記録を行うための前提条件
  完全復旧モデルのデータベースの場合、一括インポート中に実行されるすべての行挿入操作が、トランザクション ログに完全に記録されます。 完全復旧モデルを使用する場合、大きなデータをインポートするとトランザクション ログがすぐにいっぱいになってしまいます。 これとは対照的に、単純復旧モデルまたは一括ログ復旧モデルでは、一括インポート操作の最小ログ記録を行うと、一括インポート操作によってログ領域がいっぱいになる可能性が少なくなります。 最小ログ記録は完全ログ記録よりも効率的です。  
  
> [!NOTE]  
>  一括ログ復旧モデルは、大量の一括操作中に完全復旧モデルの代わりとして一時的に使用するためのものです。  
  
## <a name="table-requirements-for-minimally-logging-bulk-import-operations"></a>一括インポート操作の最小ログ記録のためのテーブルの要件  
 最小ログ記録を行うテーブルは、次の条件を満たしている必要があります。  
  
-   テーブルがレプリケート中でないこと。  
  
-   (TABLOCK を使用して) テーブル ロックが指定されていること。  
  
    > [!NOTE]  
    >  最小限のログ記録しか行われない一括インポート操作では、データを挿入してもトランザクション ログに記録されませんが、新しいエクステントがテーブルに割り当てられるたびに、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によりエクステントの割り当てがログに記録されます。  
  
-   テーブルは、メモリ最適化テーブルではありません。  
  
 あるテーブルの最小ログ記録を行うことができるかどうかは、そのテーブルにインデックスがあるかどうか、また、インデックスが存在する場合はテーブルが空かどうかによっても異なります。  
  
-   テーブルにインデックスがない場合、データ ページの最小ログ記録が行われます。  
  
-   テーブルにクラスター化インデックスがなく、非クラスター化インデックスが 1 つ以上ある場合、データ ページは常に最小ログ記録が行われます。 インデックス ページのログがどのように記録されるかは、テーブルが空かどうかにより異なります。  
  
    -   テーブルが空の場合、インデックス ページは最小ログ記録が行われます。  
  
    -   テーブルが空ではない場合、インデックス ページは完全ログ記録が行われます。  
  
        > [!NOTE]  
        >  空のテーブルに複数のバッチのデータを一括インポートする場合、最初のバッチについてはインデックス ページとデータ ページの最小ログ記録が行われますが、2 番目以降のバッチはデータ ページのみの最小ログ記録が行われます。  
  
-   テーブルが空で、クラスター化インデックスがある場合、データ ページとインデックス ページの最小ログ記録が行われます。 これと対照的に、空ではないテーブルにクラスター化インデックスがある場合、いずれの復旧モデルであってもデータ ページとインデックス ページの完全ログ記録が行われます。  
  
    > [!NOTE]  
    >  空のテーブルにバッチのデータを一括インポートする場合、最初のバッチについてはインデックス ページとデータ ページの最小ログ記録が行われますが、2 番目以降のバッチはデータ ページのみ一括ログ記録が行われます。  
  
> [!NOTE]  
>  トランザクション レプリケーションが有効な場合、BULK INSERT 操作は、一括ログ復旧モデルでも完全にログ記録されます。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [データベースの復旧モデルの表示または変更 &#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  

  
## <a name="see-also"></a>関連項目  
 [復旧モデル &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)   
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [テーブル ヒント &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)   
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)  
  
  
