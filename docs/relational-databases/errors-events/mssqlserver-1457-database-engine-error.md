---
title: MSSQLSERVER_1457 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1457 (Database Engine error)
ms.assetid: 28434ba1-b033-4866-ab41-111fccef45a2
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d6d92d7be754fd8bfde48f53da2acf849229989e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033459"
---
# <a name="mssqlserver1457"></a>MSSQLSERVER_1457
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
    > SET PARTNER OFF ステートメントが失敗した後でもミラーリングが有効な場合のみ、ミラー データベースを削除できます。  
  
## <a name="see-also"></a>参照  
[データベース ミラーリング &#40;SQL Server&#41;](~/database-engine/database-mirroring/database-mirroring-sql-server.md)  
[ALTER DATABASE &#40;Transact-SQL&#41;](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
[データベース ミラーリングの設定 &#40;SQL Server&#41;](~/database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)  
[データベース ミラーリングの削除 &#40;SQL Server&#41;](~/database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
[ミラーリングのためのミラー データベースの準備 &#40;SQL Server&#41;](~/database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
