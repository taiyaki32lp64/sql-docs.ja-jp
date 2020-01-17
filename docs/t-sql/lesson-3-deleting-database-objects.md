---
title: 'T-SQL のチュートリアル: データベース オブジェクトを削除する | Microsoft Docs'
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting database objects
ms.assetid: ecf26dd5-4535-4ed6-86fc-c73f9d9dedec
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 36b68bb833c5c95beeb65b792b9621f2f9bb9c4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031571"
---
# <a name="lesson-3-delete-database-objects"></a>レッスン 3:データベース オブジェクトの削除
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
この短いレッスンでは、レッスン 1 とレッスン 2 で作成したオブジェクトを削除してから、データベースを削除します。  
  
オブジェクトを削除する前に、適切なデータベースで作業していることを確認します。
  
  ```sql  
  USE TestData;  
  GO  
  ```  

## <a name="revoke-stored-procedure-permissions"></a>ストアド プロシージャの権限を取り消す
  
ストアド プロシージャに対する `REVOKE` の実行権限を削除するには、 `Mary` ステートメントを使用します。
  
  ```sql  
  REVOKE EXECUTE ON pr_Names FROM Mary;  
  GO  
  ```  
  
## <a name="drop-permissions"></a>権限の削除

1. `DROP` データベースに対する `Mary` のアクセス権限を削除するには、 `TestData` ステートメントを使用します。
  
   ```sql  
   DROP USER Mary;  
   GO  
   ```  


2. `DROP` が `Mary` のこのインスタンスにアクセスする権限を削除するには、 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]ステートメントを使用します。
  
   ```sql  
   DROP LOGIN [<computer_name>\Mary];  
   GO   
   ```  
  
3. ストアド プロシージャ `DROP` を削除するには、 `pr_Names`ステートメントを使用します。  
  
   ```sql  
   DROP PROC pr_Names;  
   GO   
   ```  
  
4. ビュー `DROP` を削除するには、 `vw_Names`ステートメントを使用します。  
  
   ```sql  
   DROP VIEW vw_Names;  
   GO  
   ```  

## <a name="delete-table"></a>テーブルの削除
  
1. `DELETE` テーブルからすべての行を削除するには、 `Products` ステートメントを使用します。  
  
    ```sql  
    DELETE FROM Products;  
    GO  
    ```  
  
2.  `DROP` テーブルを削除するには、 `Products` ステートメントを使用します。  
  
    ```sql  
    DROP TABLE Products;  
    GO    
    ```  

## <a name="remove-database"></a>データベースの削除
  
データベースでの作業中は、 `TestData` データベースを削除できません。したがって、まずコンテキストを他のデータベースに切り替えてから、 `DROP` ステートメントを使用して `TestData` データベースを削除します。  
  
  ```sql  
  USE MASTER;  
  GO  
  DROP DATABASE TestData;  
  GO   
  ```  
  
これで、「 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの記述」のチュートリアルを終了します。 このチュートリアルは概要であり、使用できるステートメントのすべてのオプションが記載されているわけではありません。 効率のよいデータベース構造を設計して作成し、セキュリティ保護されたデータ アクセスを構成するには、このチュートリアルで示したデータベースよりも複雑なデータベースが必要です。  

  
  
