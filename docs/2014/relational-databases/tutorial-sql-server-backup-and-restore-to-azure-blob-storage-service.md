---
title: チュートリアル:Azure Blob Storage サービスへの SQL Server のバックアップと復元 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 9e1d94ce-2c93-45d1-ae2a-2a7d1fa094c4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b166930b5d077e7294fcdbc13449d40cab309425
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176112"
---
# <a name="tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service"></a>チュートリアル:Azure Blob Storage サービスへの SQL Server のバックアップと復元
  Azure Blob Storage サービスを使用した SQL Server のバックアップと復元に関するチュートリアルのはじめにへようこそ。 このチュートリアルで、Azure Blob Storage サービスへのバックアップの書き込みと、Azure Blob Storage サービスからの復元を実行する方法について学習できます。  
  
## <a name="what-you-will-learn"></a>学習する内容  
 このチュートリアルでは、Windows ストレージ アカウント、BLOB コンテナーを作成し、ストレージ アカウントにアクセスするための資格情報の作成、BLOB サービスへのバックアップの書き込み、簡単な復元の実行を行う方法について説明します。 このチュートリアルは、次の 4 つのレッスンで構成されています。  
  
 [レッスン 1:Azure Storage オブジェクトの作成](../tutorials/lesson-1-create-windows-azure-storage-objects.md)  
 このレッスンでは、Azure ストレージ アカウントおよび BLOB コンテナーを作成します。  
  
 [レッスン 2:SQL Server 資格情報の作成](../tutorials/lesson-2-create-a-sql-server-credential.md)  
 このレッスンでは、Azure ストレージ アカウントへのアクセスに使用するセキュリティ情報を格納するための資格情報を作成します。  
  
 [レッスン 3:Azure Blob Storage サービスにデータベースの完全バックアップを書き込む](../tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)  
 このレッスンでは、T-SQL ステートメントを実行して、Azure Blob Storage サービスに AdventureWorks2012 データベースのバックアップを書き込みます。  
  
 [レッスン 4:データベースの完全バックアップからの復元を実行する](../tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)  
 このレッスンでは、T-SQL ステートメントを実行して、前のレッスンで作成したデータベース バックアップから復元します。  
  
### <a name="requirements"></a>要件  
 このチュートリアルを完了するには、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のバックアップと復元の概念と T-SQL 構文についての知識が必要です。 このチュートリアルを使用するには、以下のシステム要件を満たしている必要があります。  
  
-   [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] インスタンス、およびインストールされた AdventureWorks2012 データベース。  
  
     SQL Server インスタンスは、オンプレミスと Azure Virtual Machine のどちらに存在してもかまいません。  
  
     AdventureWorks2012 の代わりにユーザー データベースを使用し、それに応じて TSQL コマンド構文を変更できます。  
  
-   BACKUP コマンドまたは RESTORE コマンドの発行に使用するユーザー アカウントは、 **資格情報の変更** 権限を持つ **db_backup operator** データベース ロールに属している必要があります。  
  
### <a name="additional-reading"></a>その他の情報  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] バックアップに Azure Blob Storage サービスを使用する場合の概念やベスト プラクティスについて、次の推奨トピックで説明しています。  
  
1.  [Azure Blob Storage サービスを使用したバックアップと復元の SQL Server](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)  
  
2.  [SQL Server Backup to URL に関するベスト プラクティスとトラブルシューティング](backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
