---
title: 同期中のスクリプトの実行 (レプリケーション Transact-SQL プログラミング) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synchronization [SQL Server replication], scripts
- scripts [SQL Server replication], synchronization and
- sp_addscriptexec
ms.assetid: b58a0877-4e43-4fab-a281-24e6022d3fb1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2565eb2be68c1e964b82d46d9aa8fc9f39a01f70
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165026"
---
# <a name="execute-scripts-during-synchronization-replication-transact-sql-programming"></a>同期中のスクリプトの実行 (レプリケーション Transact-SQL プログラミング)
  レプリケーションでは、トランザクション パブリケーションおよびマージ パブリケーションのサブスクライバーに対し、要求時にスクリプトを実行できます。 スクリプトはレプリケーションの作業ディレクトリにコピーされ、サブスクライバー側で **sqlcmd** を使って適用されます。 トランザクション パブリケーションのサブスクリプションに対してスクリプトを適用しているときにエラーが発生した場合、既定では、ディストリビューション エージェントの実行が停止します。 レプリケーションのストアド プロシージャを使用すると、指定した [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトをプログラムから実行できます。  
  
### <a name="to-specify-a-script-to-run-for-all-subscribers-to-a-snapshot-transactional-or-merge-publication"></a>スナップショット、トランザクション、マージ パブリケーションのすべてのサブスクライバーに対して実行するスクリプトを指定するには  
  
1.  要求時に実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトを作成およびテストします。  
  
2.  スクリプト ファイルを、パブリケーションのスナップショット エージェントがアクセスできる場所に保存します。  
  
3.  パブリッシャー側のパブリケーション データベースに対して、[sp_addscriptexec &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql) を実行します。 **\@のパブリケーション**を指定し、手順 2. で作成した完全な UNC パスを含むスクリプトファイルの名前を **\@scriptfile**に指定し、 **\@skiperror**に次のいずれかの値を指定します。  
  
    -   **0** - エラーが発生した場合、エージェントがスクリプトの実行を停止します。  
  
    -   **1** - エラーが発生した場合、エージェントによってエラー ログが記録され、スクリプトの実行が継続されます。  
  
4.  指定したスクリプトは、エージェントが次にサブスクリプションを同期するときに、各サブスクライバーで実行されます。  
  
## <a name="see-also"></a>参照  
 [データベースの同期](synchronize-data.md)  
  
  
