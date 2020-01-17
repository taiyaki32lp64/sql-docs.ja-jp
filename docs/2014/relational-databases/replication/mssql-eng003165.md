---
title: MSSQL_ENG003165 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG003165 error
ms.assetid: 707d33dd-644e-4cc9-ac51-dddd49031530
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c4c2c6e01fd3e0b862511f71d90baf31d28948ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62666708"
---
# <a name="mssqleng003165"></a>MSSQL_ENG003165
    
## <a name="message-details"></a>メッセージの詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|3165|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|データベース '%ls' は復元されましたが、レプリケーションの復元または削除中にエラーが発生しました。 データベースはオフラインのままです。 SQL Server オンライン ブックのトピック「MSSQL_ENG003165」を参照してください。|  
  
## <a name="explanation"></a>説明  
 このエラーは、レプリケートされたデータベースのバックアップの復元で問題が生じた場合に発生します。  
  
-   バックアップをその作成元と同じデータベースおよびサーバーに復元している場合、このエラーは、レプリケーション設定を適切に復元できなかったことを示します。  
  
-   バックアップを異なるデータベースまたはサーバーに復元している場合、このエラーは、レプリケーション設定を適切に削除できなかったことを示します (既定では、データベースまたはサーバーが異なる場合、レプリケーション設定は削除されます)。  
  
 このエラーは、復元されたデータベースと、レプリケーション メタデータを含む 1 つ以上のシステム データベース、つまり **msdb**、 **master**、またはディストリビューション データベースの間の状態の不一致が原因と考えられます。  
  
## <a name="user-action"></a>ユーザーの操作  
 この問題を解決するには、次の手順を実行します。  
  
1.  ALTER DATABASE を実行し、データベースをオンラインにします。たとえば、「 `ALTER DATABASE AdventureWorks SET ONLINE`」と実行します。 詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)」を参照してください。 レプリケーションの設定を保存する場合は、手順 2. に進みます。 それ以外の場合は、手順 3. に進みます。  
  
2.  [sp_restoredbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-restoredbreplication-transact-sql) を実行します。 このストアド プロシージャの実行に成功した場合、復元は完了です。 実行に失敗した場合は、手順 3. に進んでください。  
  
3.  [sp_removedbreplication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) を実行して、レプリケーションの設定をすべて削除します。  
  
     必要に応じて、レプリケーションを再構成します。 推奨どおりにレプリケーション トポロジのスクリプトを作成している場合は、スクリプトを使用してトポロジを再構成してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server データベースのバックアップと復元](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [レプリケートされたデータベースのバックアップと復元](administration/back-up-and-restore-replicated-databases.md)   
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](errors-and-events-reference-replication.md)  
  
  
