---
title: Filestream および FileTable システム ストアド プロシージャ (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- FileTables [SQL Server], catalog views
ms.assetid: 2c83a4a7-720b-4435-a3b5-788c29f56949
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1ebcaf4659d7be880f0f0e901b2eadcc9002b2d9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942247"
---
# <a name="filestream-and-filetable-system-stored-procedures-transact-sql"></a>Filestream および FileTable システム ストアド プロシージャ (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  このセクションでは、Filestream と FileTable の機能をシステム ストアド プロシージャについて説明します。  

## <a name="filestream-and-filetable-system-stored-procedures"></a>Filestream および Filetable システム ストアド プロシージャ
  [sp_filestream_force_garbage_collection (TRANSACT-SQL)](filestream-and-filetable-sp-filestream-force-garbage-collection.md)

   不要な FILESTREAM ファイルの削除を実行するには、FILESTREAM ガベージ コレクターに強制します。

  [sp_kill_filestream_non_transacted_handles (TRANSACT-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)

  FileTable データに対する非トランザクション ファイル ハンドルを閉じます。


## <a name="see-also"></a>関連項目
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetable](../../relational-databases/blob/filetables-sql-server.md)
<br>[Filestream および FileTable の動的管理ビュー (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Filestream および FileTable のカタログ ビュー (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
  
  
