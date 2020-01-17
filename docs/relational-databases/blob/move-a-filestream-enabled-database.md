---
title: FILESTREAM が有効なデータベースの移動 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], moving a FILESTREAM-enabled database
ms.assetid: dd4d270d-9283-431a-aa6b-e571fced1893
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 33d2f34f9f2ea63f23c570c0b4ada95906649215
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091535"
---
# <a name="move-a-filestream-enabled-database"></a>FILESTREAM が有効なデータベースの移動
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、FILESTREAM が有効なデータベースを移動する方法について説明します。  
  
> [!NOTE]  
>  このトピックの例では、「 [FILESTREAM が有効なデータベースを作成する方法](../../relational-databases/blob/create-a-filestream-enabled-database.md)」で作成した Archive データベースが必要です。  
  
### <a name="to-move-a-filestream-enabled-database"></a>FILESTREAM が有効なデータベースを移動するには  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]で、 **[新しいクエリ]** をクリックしてクエリ エディターを開きます。  
  
2.  次の [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトをクエリ エディターにコピーして、 **[実行]** をクリックします。 このスクリプトは、FILESTREAM データベースで使用される物理データベース ファイルの場所を表示します。  
  
    ```sql  
    USE Archive  
    GO  
    SELECT type_desc, name, physical_name from sys.database_files  
    ```  
  
3.  次の [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトをクエリ エディターにコピーして、 **[実行]** をクリックします。 このコードでは、 `Archive` データベースがオフラインに設定されます。  
  
    ```sql  
    USE master  
    EXEC sp_detach_db Archive  
    GO  
    ```  
  
4.  `C:\moved_location`というフォルダーを作成し、手順 2. で一覧表示されたファイルとフォルダーをそのフォルダーに移動します。  
  
5.  次の [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトをクエリ エディターにコピーして、 **[実行]** をクリックします。 このスクリプトでは、 `Archive` データベースがオンラインに設定されます。  
  
    ```sql  
    CREATE DATABASE Archive ON  
    PRIMARY ( NAME = Arch1,  
        FILENAME = 'c:\moved_location\archdat1.mdf'),  
    FILEGROUP FileStreamGroup1 CONTAINS FILESTREAM( NAME = Arch3,  
        FILENAME = 'c:\moved_location\filestream1')  
    LOG ON  ( NAME = Archlog1,  
        FILENAME = 'c:\moved_location\archlog1.ldf')  
    FOR ATTACH  
    GO  
    ```  
  
## <a name="see-also"></a>参照  
 [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
  
