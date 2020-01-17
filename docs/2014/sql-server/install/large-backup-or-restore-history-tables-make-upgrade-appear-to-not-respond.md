---
title: 大きなバックアップまたは復元の履歴テーブルによってアップグレードが応答しないように見える |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- backup history tables
- history tables
ms.assetid: f88d86ec-324b-4518-b6d7-1af7e7265812
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e4d994eb6d345ab98e6cd51a44c7c90a74bafd3a
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874602"
---
# <a name="large-backup-or-restore-history-tables-make-upgrade-appear-to-not-respond"></a>バックアップまたは復元のサイズの大きい履歴テーブルではアップグレードが応答を停止したように見える
  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] では、バックアップと復元の履歴テーブルの一部に新しい列が追加されました。 これらのテーブルをアップグレードするには、新しい列を追加するためにテーブルを変更する必要があります。 これらのテーブルのうちの 1 つ以上のテーブルに大量の行が含まれている場合、アップグレードの際に、テーブルに列を追加する ALTER TABLE ステートメントで非常に時間がかかります。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>[説明]  
 次のいずれかのバックアップまたは復元履歴テーブルに多数の行が含まれていると、アップグレードが応答を停止する可能性があります。  
  
-   **backupfile**  
  
-   **backupmediafamily**  
  
-   **backupmediaset**  
  
-   **backupset**  
  
-   **restorefile**  
  
-   **restorefilegroup**  
  
-   **restorehistory**  
  
 これらのテーブルに 10,000 以上の行が含まれている場合、アップグレード アドバイザーは不適格であることを示すエラーを報告します。 どのテーブルが許容行数を超えたのかは報告されません。 10,000 行を超える最初のテーブルでエラーが発生します。  
  
## <a name="corrective-action"></a>修正措置  
 テーブルが 10,000 行を超えている場合は、データベースをアップグレードする前に、10,000 行未満に減らすことをお勧めします。 これらのすべてのテーブルの行を減らすには、 **sp_delete_backuphistory**ストアドプロシージャを実行します。 このプロシージャは、バックアップと復元のすべての履歴テーブルに含まれているエントリのうち、指定した日付よりも古いバックアップ セットのエントリを削除します。 詳細については、「[sp_delete_backuphistory (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql)」を参照してください。  
  
> [!NOTE]  
>  バックアップと復元の履歴テーブルが 10,000 行を超えるデータベースはアップグレードできます。 ただし、サイズの大きいテーブルの変更には時間がかかることがあります。 テーブルのサイズが大きいほど、セットアップの完了に時間がかかります。  
  
## <a name="see-also"></a>参照  
 [データベースエンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 Upgrade Advisor &#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
