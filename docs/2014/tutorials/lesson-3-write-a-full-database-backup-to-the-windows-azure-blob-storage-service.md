---
title: 'レッスン 3: Azure Blob Storage サービスにデータベースの完全バックアップを書き込む |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 454c8296-64e9-46ed-b141-5ebfbc8a4fe2
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 1d5a749c61a3bc97de841e1149dd1539cbc990f2
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153476"
---
# <a name="lesson-3-write-a-full-database-backup-to-the-azure-blob-storage-service"></a>レッスン 3: Azure Blob Storage サービスにデータベースの完全バックアップを書き込む
  このレッスンでは、tsql ステートメントを使用して、Azure Blob ストレージサービスへのデータベースの完全バックアップを実行する方法を示します。  
  
## <a name="perform-a-full-database-backup-to-the-azure-blob-storage-service"></a>Azure Blob Storage サービスへのデータベースの完全バックアップを実行する  
 データベースの完全バックアップを実行するには、次の手順を実行します。  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]に接続します。  
  
2.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]のインスタンスに接続します。  
  
3.  [標準] メニュー バーの **[新しいクエリ]** をクリックします。  
  
4.  次の例をコピーしてクエリ ウィンドウに貼り付け、必要に応じて変更して、 **[実行]** をクリックします。  
  
    ```  
    BACKUP DATABASE[AdventureWorks2012]   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/   
    WITH CREDENTIAL = 'mycredential';  
    /* name of the credential you created in the previous step */   
    GO  
  
    ```  
  
5.  オブジェクト エクスプローラーで、Azure ストレージに接続します。 コンテナーと、新しく作成したバックアップ ファイルを参照して指定します。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 4:データベースの完全バックアップ](../../2014/tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md)から復元を実行します。  
  
  
