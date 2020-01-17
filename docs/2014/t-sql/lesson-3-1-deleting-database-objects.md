---
title: データベース オブジェクトの削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting database objects
ms.assetid: dbb94fdf-c85b-477b-8e84-f830d259bade
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a23d307cc33e5b8e59111819b245bc9df1df67df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63063121"
---
# <a name="deleting-database-objects"></a>データベース オブジェクトの削除
  このチュートリアルのすべてのトレースを削除するには、データベースを削除します。 ただし、このトピックでは、チュートリアルを進みながら実行したすべての操作を元に戻す手順を実行します。  
  
### <a name="removing-permissions-and-objects"></a>権限とオブジェクトの削除  
  
1.  オブジェクトを削除する前に、適切なデータベースで作業していることを確認します。  
  
    ```  
    USE TestData;  
    GO  
    ```  
  
2.  ストアド プロシージャに対する `REVOKE` の実行権限を削除するには、 `Mary` ステートメントを使用します。  
  
    ```  
    REVOKE EXECUTE ON pr_Names FROM Mary;  
    GO  
  
    ```  
  
3.  `DROP` データベースに対する `Mary` のアクセス権限を削除するには、 `TestData` ステートメントを使用します。  
  
    ```  
    DROP USER Mary;  
    GO  
  
    ```  
  
4.  `DROP` が `Mary` のこのインスタンスにアクセスする権限を削除するには、 [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]ステートメントを使用します。  
  
    ```  
    DROP LOGIN [<computer_name>\Mary];  
    GO  
  
    ```  
  
5.  ストアド プロシージャ `DROP` を削除するには、 `pr_Names`ステートメントを使用します。  
  
    ```  
    DROP PROC pr_Names;  
    GO  
  
    ```  
  
6.  ビュー `DROP` を削除するには、 `vw_Names`ステートメントを使用します。  
  
    ```  
    DROP View vw_Names;  
    GO  
  
    ```  
  
7.  `DELETE` テーブルからすべての行を削除するには、 `Products` ステートメントを使用します。  
  
    ```  
    DELETE FROM Products;  
    GO  
  
    ```  
  
8.  `DROP` テーブルを削除するには、 `Products` ステートメントを使用します。  
  
    ```  
    DROP Table Products;  
    GO  
  
    ```  
  
9. データベースでの作業中は、 `TestData` データベースを削除できません。したがって、まずコンテキストを他のデータベースに切り替えてから、 `DROP` ステートメントを使用して `TestData` データベースを削除します。  
  
    ```  
    USE MASTER;  
    GO  
    DROP DATABASE TestData;  
    GO  
  
    ```  
  
 これで、「 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの記述」のチュートリアルを終了します。 このチュートリアルは概要であり、使用できるステートメントのすべてのオプションが記載されているわけではありません。 効率のよいデータベース構造を設計して作成し、セキュリティ保護されたデータ アクセスを構成するには、このチュートリアルで示したデータベースよりも複雑なデータベースが必要です。  
  
## <a name="return-to-sql-server-tools-portal"></a>SQL Server ツールのポータルに戻る  
 [チュートリアル: Transact-SQL ステートメントの作成](tutorial-writing-transact-sql-statements.md)  
  
## <a name="see-also"></a>関連項目  
 [REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql)   
 [DROP USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-user-transact-sql)   
 [DROP LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-login-transact-sql)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-procedure-transact-sql)   
 [DROP VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-view-transact-sql)   
 [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql)   
 [DROP TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-table-transact-sql)   
 [DROP DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)  
  
  
