---
title: MSSQLSERVER_3313 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3313 (Database Engine error)
ms.assetid: a244227b-8553-42df-9435-034f906c4c74
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 37f4a65aa023952232e2237a1c4ac38887af1cb3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908373"
---
# <a name="mssqlserver3313"></a>MSSQLSERVER_3313
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|3313|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|ERR_LOG_RID1|  
|メッセージ テキスト|データベース '%.*ls' でログに記録された操作をやり直しているときにエラーが発生しました。エラーが発生したログ レコード ID は %S_LSN です。 通常、この前に特定のエラーが Windows イベント ログ サービスにログ記録されます。 完全バックアップからデータベースを復元するか、データベースを修復してください。|  
  
## <a name="explanation"></a>説明  
これは、再実行の復旧のロールアップ エラーです。 このエラーによって、データベースは SUSPECT 状態になっています。 プライマリ ファイル グループ、また場合によってはその他のファイル グループには、問題があり、損傷している可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動中はデータベースを復旧できないため、データベースを使用できません。 問題を解決するには、ユーザーによる操作が必要です。  
  
このエラーが **tempdb**で発生した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスはシャットダウンします。  
  
## <a name="user-action"></a>ユーザーの操作  
このエラーは、サーバー インスタンスの起動またはデータベースの復旧を試行したときのシステム上の一時的な状態が原因である可能性があります。 また、データベースを起動しようとするたびに発生する永続的なエラーが原因である可能性もあります。 原因の詳細については、Windows イベント ログで、具体的な問題点を示しているこれより前のエラーを調べてください。  
  
このエラー状態が発生すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、通常、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **LOG** フォルダーに 3 つのファイルが生成されます。 SQLDump*nnnn*.txt ファイルには、問題が発生したトランザクションやページの詳細など、エラーに関する詳しい診断情報が含まれています。 この情報は、通常、失敗の理由を分析するために製品サポート チームが使用します。  
  
このエラー 3313 の発生の原因については、Windows イベント ログをさかのぼって、具体的な問題点を示すエラーを調べてください。 ユーザーに求められる適切な対処は、Windows イベント ログが示している情報、つまり、その [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーが一時的な状態によって引き起こされたのか、永続的なエラーが原因で引き起こされたのかによって異なります。 エラー 3313 をトラブルシューティングするためのユーザー操作の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックを参照してください。  
  
## <a name="see-also"></a>参照  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[データベースの全体復元 &#40;単純復旧モデル&#41;](~/relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
[MSSQLSERVER_824](~/relational-databases/errors-events/mssqlserver-824-database-engine-error.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
