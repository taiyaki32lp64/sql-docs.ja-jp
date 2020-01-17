---
title: MSSQLSERVER_926 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 926 (Database Engine error)
ms.assetid: 57e01668-883b-4be4-84a8-a111caaf0486
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4afdc9adae6f968ca89ff1a9b2bf9e5b67992037
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62912474"
---
# <a name="mssqlserver926"></a>MSSQLSERVER_926
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|926|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DB_SUSPECT|  
|メッセージ テキスト|データベース '%.*ls' を開けません。 このデータベースは、復旧により問題ありと設定されています。 詳細については、SQL Server のエラー ログを参照してください。|  
  
## <a name="explanation"></a>説明  
 データベースが問題ありと設定されるのは、データベースのトランザクションを一貫性のある状態にする復旧処理が失敗したためです。 この現象は、次の操作で発生する場合があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの起動。  
  
-   データベースのインポート。  
  
-   RESTORE データベースまたは RESTORE LOG プロシージャの使用。  
  
## <a name="user-action"></a>ユーザーの操作  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログを調査し、エラーの原因を特定します。 復旧の失敗後に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再起動された場合は、以前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログを参照し、復旧が失敗した原因を確認します。  
  
 永続的な I/O エラー、破損ページ、またはその他のハードウェア障害によって復旧に失敗した場合は、原因となっているハードウェア障害を解決してから、バックアップを使用してデータベースを復元します。 バックアップが用意されていない場合は、DBCC CHECKDB の修復オプションを使用する方法があります。  
  
 この問題を解決できない場合は、購入元にお問い合わせください。 確認用に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログをご用意ください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server データベースのバックアップと復元](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [sys.sysdatabases &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-compatibility-views/sys-sysdatabases-transact-sql)   
 [データベースのデタッチとアタッチ &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  
