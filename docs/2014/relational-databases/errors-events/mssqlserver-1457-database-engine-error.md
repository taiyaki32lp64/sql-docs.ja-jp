---
title: MSSQLSERVER_1457 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1457 (Database Engine error)
ms.assetid: 28434ba1-b033-4866-ab41-111fccef45a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4f45545212b494f955c6b9be97ccf0df7efeb622
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62869914"
---
# <a name="mssqlserver1457"></a>MSSQLSERVER_1457
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|1457|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBM_PAGE_UNDO_PENDING|  
|メッセージ テキスト|ミラー データベース '%.*ls' の同期が中断されました。データベースの一貫性は損なわれた状態のままです。 ALTER DATABASE コマンドが失敗しました。 ミラー データベースがバックアップされ、オンラインであることを確認してから、ミラー サーバー インスタンスに再接続し、ミラー データベースで同期を終了できるようにしてください。|  
  
## <a name="explanation"></a>説明  
 このメッセージは、ALTER DATABASE *database_name* SET PARTNER OFF ステートメントが失敗したことを示しています。 データベース ミラーリングの削除に失敗し、削除を試みたことによってミラー データベースの同期が中断されました。 ミラー データベースは一貫性がない状態になっています。  
  
## <a name="user-action"></a>ユーザーの操作  
 このエラーを解決するには、次のいずれかの操作を実行します。  
  
-   ミラー サーバーとプリンシパル サーバーとの間の接続を再度確立し、ミラー データベースの同期を実行できるようにします。  
  
-   ミラー データベースを削除します。  
  
     ミラー データベースを削除した後、バックアップから新しいミラー データベースを作成できます。  
  
    > [!NOTE]  
    >  SET PARTNER OFF ステートメントが失敗した後でもミラーリングが有効な場合のみ、ミラー データベースを削除できます。  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [データベース ミラーリングの設定 &#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [データベース ミラーリングの削除 &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
  
