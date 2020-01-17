---
title: MSSQLSERVER_3176 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3176 (Database Engine error)
ms.assetid: 4be24c64-2d52-4cb4-b4d7-36efbe4555b6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bc01cf250840fb42a8c29525974494a21398e1ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105251"
---
# <a name="mssqlserver3176"></a>MSSQLSERVER_3176
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|イベント ID|3176|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|LDDB_FILE_CLAIM|  
|メッセージ テキスト|ファイル '%ls' が '%ls'(%d) と '%ls'(%d) から要求されました。 WITH MOVE 句を使用して、1 つ以上のファイルを再配置できます。|  
  
## <a name="explanation"></a>説明  
ファイルを複数の目的で使用しようとしています。  
  
### <a name="possible-causes"></a>考えられる原因  
既に別のデータベースで同じファイル名が使用されています。  
  
## <a name="user-action"></a>ユーザーの操作  
データベース ファイルを別の場所に復元します。 これには、RESTORE ステートメントで WITH MOVE 句を使用して、各ファイルを移動します。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、 **[データベースの復元オプション]** ダイアログ ボックスの **[次のデータベース ファイルに復元]** グリッドでファイルの場所を変更します。  
  
## <a name="see-also"></a>参照  
[データベースを新しい場所に復元する &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
[新しい場所へのファイルの復元 &#40;SQL Server&#41;](~/relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
[RESTORE &#40;Transact-SQL&#41;](~/t-sql/statements/restore-statements-transact-sql.md)  
  
