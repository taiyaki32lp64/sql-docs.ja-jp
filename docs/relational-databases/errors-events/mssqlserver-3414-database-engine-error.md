---
title: MSSQLSERVER_3414 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 3414 (Database Engine error)
ms.assetid: f25852f9-b91c-4356-b817-78bec9ec8db4
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c9d5b20ded79569fedd804df81403802a8f2785d
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver3414"></a>MSSQLSERVER_3414
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|3414|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|REC_GIVEUP|  
|メッセージ テキスト|復元中にエラーが発生したので、データベース '%.*ls' (データベース ID %d) は再開されません。 復元エラーを診断して修正するか、既知の適切なバックアップから復元してください。 エラーが修正されない場合は、ご購入元に問い合わせてください。|  
  
## <a name="explanation"></a>説明  
示されているデータベースは復旧されましたが、復旧中にエラーが発生したために起動できませんでした。 このエラーによって、データベースは SUSPECT 状態になっています。 プライマリ ファイル グループ、また場合によってはその他のファイル グループには、問題があり、損傷している可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動中はデータベースを復旧できないため、データベースを使用できません。 問題を解決するには、ユーザーによる操作が必要です。  
  
このエラーが **tempdb**で発生した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスはシャットダウンします。  
  
## <a name="user-action"></a>ユーザーの操作  
このエラーは、サーバー インスタンスの起動またはデータベースの復旧を試行したときのシステム上の一時的な状態が原因である可能性があります。 また、データベースを起動しようとするたびに発生する永続的なエラーが原因である可能性もあります。 原因の詳細については、Windows イベント ログで、具体的な問題点を示しているこれより前のエラーを調べてください。  
  
このエラー 3414 の発生の原因については、Windows イベント ログをさかのぼって、具体的な問題点を示すエラーを調べてください。 ユーザーに求められる適切な対処は、Windows イベント ログが示している情報、つまり、その [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラーが一時的な状態によって引き起こされたのか、永続的なエラーが原因で引き起こされたのかによって異なります。 エラー 3414 をトラブルシューティングするためのユーザー操作の詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックを参照してください。  
  
## <a name="see-also"></a>参照  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[DBCC CHECKDB &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[データベースの全体復元 &#40;単純復旧モデル&#41;](~/relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)  
[MSSQLSERVER_824](~/relational-databases/errors-events/mssqlserver-824-database-engine-error.md)  
[sys.databases &#40;Transact-SQL&#41;](~/relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
