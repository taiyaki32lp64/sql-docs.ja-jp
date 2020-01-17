---
title: MSSQL_ENG021286 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021286 error
ms.assetid: b63620b7-1c6d-46f7-90ea-3a8e99af8de4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 54e5d7b496affcd6d9ead2c50f50e807e7e920a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63023229"
---
# <a name="mssqleng021286"></a>MSSQL_ENG021286
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|21286|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|競合テーブル '%s' が存在しません。|  
  
## <a name="explanation"></a>説明  
 このエラーは、[sysmergearticles &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysmergearticles-transact-sql) にリストされているアーティクルの競合テーブルが実際には存在しない場合に発生します。 このエラーは、マージ レプリケーション用にパブリッシュされたテーブルへの列の追加または削除を試みたときに発生することがあります。  
  
## <a name="user-action"></a>ユーザーの操作  
 競合テーブルが見つからないデータベース上で [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) を実行し、データの一貫性の問題がないかどうかを確認します。  
  
 サブスクライバーに競合テーブルがない場合は、サブスクリプションを削除し、再作成します。 パブリッシャーに競合テーブルがない場合は、すべてのサブスクリプションを削除し、パブリケーションを削除してから、パブリケーションおよびすべてのサブスクリプションを再作成します。 詳細については、「[データとデータベース オブジェクトのパブリッシュ](publish/publish-data-and-database-objects.md)」および「[パブリケーションのサブスクライブ](subscribe-to-publications.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)  
  
  
