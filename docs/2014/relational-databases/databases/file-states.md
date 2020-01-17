---
title: ファイルの状態 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- restoring file state [SQL Server]
- verifying file states
- current file states
- verifying filegroup states
- file states [SQL Server]
- online file state
- offline file state [SQL Server]
- viewing filegroup states
- viewing file states
- suspect file state
- recovering file state [SQL Server]
- current filegroup state
- recovery pending file state [SQL Server]
- displaying file states
- states [SQL Server], files
- displaying filegroup states
- defunct file state
ms.assetid: b426474d-8954-4df0-b78b-887becfbe8d6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc37fbade038b39d6d05cb5b51ecc3e8ba405e2a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871575"
---
# <a name="file-states"></a>ファイルの状態
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、データベース ファイルの状態はデータベースの状態とは別に管理されます。 ファイルは常に、ONLINE または OFFLINE などの特定の状態にあります。 ファイルの現在の状態を表示するには、 [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql) カタログ ビューまたは [sys.database_files](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql) カタログ ビューを使用します。 データベースがオフラインになっている場合、 [sys.master_files](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql) カタログ ビューからファイルの状態を表示できます。  
  
 ファイル グループ内のファイルの状態により、ファイル グループ全体の可用性が決まります。 ファイル グループを使用可能にするには、ファイル グループ内のすべてのファイルがオンラインである必要があります。 ファイル グループの現在の状態を表示するには、 [sys.filegroups](/sql/relational-databases/system-catalog-views/sys-filegroups-transact-sql) カタログ ビューを使用します。 ファイル グループがオフラインのときに、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用してファイル グループにアクセスしようとすると、エラーが発生して失敗します。 クエリ オプティマイザーで SELECT ステートメントのクエリ プランを作成すると、オフライン ファイル グループに存在する非クラスター化インデックスおよびインデックス付きビューが無視され、これらのステートメントが成功します。 ただし、オフラインのファイル グループに、対象テーブルのヒープやクラスター化インデックスが含まれている場合には、SELECT ステートメントは失敗します。 また、オフラインのファイル グループ内にあるインデックス付きのテーブルを変更する INSERT、UPDATE、または DELETE ステートメントは失敗します。  
  
## <a name="file-state-definitions"></a>ファイルの状態の定義  
 次の表では、ファイルの状態を定義しています。  
  
|状態|定義|  
|-----------|----------------|  
|ONLINE|すべての操作でファイルを使用できます。 データベース自体がオンラインである場合、プライマリ ファイル グループ内のファイルは常にオンラインです。 プライマリ ファイル グループ内のファイルがオンラインでない場合、データベースはオンラインにならないので、セカンダリ ファイルの状態は未定義となります。|  
|OFFLINE|ファイルにアクセスできません。また、ファイルがディスク上に存在しない可能性があります。 ファイルは、ユーザーの明示的な操作によってオフラインになり、ユーザーが追加操作を行うまではオフラインのままになります。<br /><br /> **\*\* 注意 \*\*** ファイルをオフラインにする必要があるのはファイルが破損している場合だけですが、ファイルは復元できます。 オフラインに設定されたファイルをオンラインに設定する唯一の方法は、バックアップからファイルを復元することです。 単一ファイルの復元の詳細については、「[RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)」を参照してください。|  
|RESTORING|ファイルは復元中です。 復元コマンドはページの復元だけでなくファイル全体に影響するため、ファイルが復元状態になります。復元が完了してファイルが復旧されるまではこの状態のままになります。|  
|RECOVERY PENDING|ファイルの復旧が延期されました。 ファイルが復元および復旧されず、復元処理が断片的な状態になると、ファイルは自動的にこの状態になります。 エラーを解決して復旧処理を完了できるようにするには、ユーザーによる追加操作が必要です。 詳細については、「[段階的な部分復元 &#40;SQL Server&#41;](../backup-restore/piecemeal-restores-sql-server.md)」を参照してください。|  
|SUSPECT|オンラインの復元処理中にファイルの復旧に失敗しました。 ファイルがプライマリ ファイル グループにある場合、データベースも問題ありとしてマークされます。 それ以外の場合、ファイルのみが問題ありの状態になり、データベースはオンラインのままになります。<br /><br /> 次の方法のいずれかによってファイルが使用可能になるまで、ファイルは問題ありの状態のままになります。<br /><br /> 復元および復旧<br /><br /> REPAIR_ALLOW_DATA_LOSS を指定した DBCC CHECKDB|  
|DEFUNCT|ファイルがオンラインでないときに削除されました。 オフラインのファイル グループが削除されると、ファイル グループ内のすべてのファイルが機能しなくなります。|  
  
## <a name="related-content"></a>関連コンテンツ  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
 [データベースの状態](database-states.md)  
  
 [ミラーリング状態 &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md)  
  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
 [データベース ファイルとファイル グループ](database-files-and-filegroups.md)  
  
  
