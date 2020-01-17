---
title: レッスン 4:データベースの完全バックアップからの復元を実行する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 580f76e6-9802-4abc-9043-db6de592c733
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: de9a356589ac6bceb532ed4cecf509f957e3c337
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153402"
---
# <a name="lesson-4-perform-a-restore-from-a-full-database-backup"></a>レッスン 4:データベースの完全バックアップからの復元の実行
  このレッスンでは、TSQL ステートメントを使用して、前のレッスンで作成したデータベースの完全バックアップからの復元を実行する方法を紹介します。  
  
## <a name="perform-a-restore-of-a-database-backup"></a>データベース バックアップの復元の実行  
 データベースの完全バックアップを復元するには、次の手順を実行します。  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]に接続します。  
  
2.  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]のインスタンスに接続します。  
  
3.  [標準] メニュー バーの **[新しいクエリ]** をクリックします。  
  
4.  次の例をコピーしてクエリ ウィンドウに貼り付け、必要に応じて変更します。  
  
    ```  
    RESTORE DATABASE AdventureWorks2012   
    FROM URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    WITH CREDENTIAL = 'mycredential';  
    , STATS = 5 - use this to see monitor the progress  
    GO  
  
    ```  
  
5.  T-sql ステートメントを確認し、 **[実行]** をクリックします。  
  
### <a name="return-to-tutorials-portal"></a>チュートリアル ポータルに戻る  
 [チュートリアル: SQL Server のバックアップと復元を Azure Blob Storage](../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)サービスに対して行います。  
  
  
