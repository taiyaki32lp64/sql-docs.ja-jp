---
title: レッスン 2:SQL Server Credential | を作成します。Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 64f8805c-1ddc-4c96-a47c-22917d12e1ab
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: baa337d33173f292145d92b60d6192af2a716c5e
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/25/2019
ms.locfileid: "70154336"
---
# <a name="lesson-2-create-a-sql-server-credential"></a>レッスン 2:SQL Server 資格情報の作成
  **資格情報:**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資格情報は、SQL Server の外部にあるリソースへの接続に必要な認証情報を保存するために使用されるオブジェクトです。  ここで[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]は、バックアップと復元のプロセスで、Azure Blob ストレージサービスに対する認証に資格情報を使用します。 資格情報には、ストレージ アカウントの名前とその **アクセス キー** 値が格納されます。 作成した資格情報は、BACKUP/RESTORE ステートメントの実行時に WITH CREDENTIAL オプションで指定する必要があります。 ストレージアカウントの**アクセスキー**を表示、コピー、または再生成する方法の詳細については、「[ストレージアカウントのアクセスキー](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx)」を参照してください。  
  
 資格情報の全般的な情報については、「 [資格情報](../relational-databases/security/authentication-access/credentials-database-engine.md)」を参照してください。  
  
 資格情報が使用されるその他の例については、「 [SQL Server エージェント プロキシの作成](../ssms/agent/create-a-sql-server-agent-proxy.md)」参照してください。  
  
> [!IMPORTANT]  
>  以下で説明する SQL Server 資格情報を作成するための要件は、SQL Server バックアッププロセス ([SQL Server backup TO URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)、および[SQL Server Managed backup to Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)) に固有のものです。 SQL Server では、Azure ストレージにアクセスしてバックアップの書き込みまたは読み取りを行う場合、ストレージ アカウント名とアクセス キーの情報を使用します。  Azure storage にデータベースファイルを格納するための資格情報を作成する[方法の詳細については、「レッスン 3:SQL Server 資格情報の作成](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="create-a-sql-server-credential"></a>SQL Server 資格情報の作成  
 SQL Server 資格情報を作成するには、次の手順を実行します。  
  
1.  SQL Server Management Studio に接続します。  
  
2.  オブジェクト エクスプローラーで、AdventureWorks2012 データベースがインストールされているデータベース エンジンのインスタンスに接続するか、このチュートリアルに使用する独自のデータベースを使用します。  
  
3.  **[標準]** ツール バーの **[新しいクエリ]** をクリックします。  
  
4.  次の例をコピーしてクエリ ウィンドウに貼り付け、必要に応じて変更します。  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account (See Lesson 1)   
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account (See Lesson 1)  
  
    ```  
  
     ![ストレージアカウントを sql 資格情報にマップしています](../../2014/tutorials/media/backuptocloud-storage-credential-mapping.gif "ストレージアカウントを sql 資格情報にマップしています")  
  
5.  T-sql ステートメントを確認し、[**実行**] をクリックします。  
  
 バックアップの概念と要件に関する Azure Blob storage サービスの詳細については、「 [Azure Blob Storage サービスを使用したバックアップと復元の SQL Server](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)」を参照してください。  
  
### <a name="next-lesson"></a>次のレッスン  
 [レッスン 3:Azure Blob Storage サービス](../../2014/tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md)にデータベースの完全バックアップを書き込みます。  
  
  
