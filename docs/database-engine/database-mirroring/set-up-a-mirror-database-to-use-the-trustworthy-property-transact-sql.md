---
title: ミラー化されたデータベースの信頼可能プロパティを有効にする
description: 新しくミラー化されたデータベースで信頼可能プロパティを有効にするために必要な手順について説明します。
ms.custom: seo-lt-2019
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- TRUSTWORTHY database option
- mirror database [SQL Server]
- database mirroring [SQL Server], security
ms.assetid: 6993b076-78ef-453e-b0ea-e341b8e5ee3e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 20ee7631b1fd4ca8613191ac67a0e13ee1cb028c
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822381"
---
# <a name="set-up-a-mirror-database-to-use-the-trustworthy-property-transact-sql"></a>TRUSTWORTHY プロパティを使用するようにミラー データベースを設定する方法 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  データベースをバックアップするときに、TRUSTWORTHY データベース プロパティは OFF に設定されます。 したがって、新しいミラー データベースでは TRUSTWORTHY は常に OFF です。 フェールオーバー後にデータベースを信頼可能にする必要がある場合は、ミラーリングを開始した後で追加の設定が必要です。  
  
> [!NOTE]  
>  このデータベース プロパティの詳細については、「 [TRUSTWORTHY データベース プロパティ](../../relational-databases/security/trustworthy-database-property.md)」を参照してください。  
  
## <a name="procedure"></a>手順  
  
#### <a name="to-setup-a-mirror-database-to-use-the-trustworthy-property"></a>TRUSTWORTHY プロパティを使用するようにミラー データベースを設定するには  
  
1.  プリンシパル サーバー インスタンスで、プリンシパル データベースの TRUSTWORTHY プロパティがオンになっていることを確認します。  
  
    ```  
    SELECT name, database_id, is_trustworthy_on FROM sys.databases   
    ```  
  
     詳細については、「[sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)」を参照してください。  
  
2.  ミラーリングが開始された後、データベースが現在プリンシパル データベースであること、セッションが同期動作モードを使用していること、およびセッションが既に同期していることを確認します。  
  
    ```  
    SELECT database_id, mirroring_role, mirroring_safety_level_desc, mirroring_state_desc FROM sys.database_mirroring  
    ```  
  
     詳細については、「[sys.database_mirroring &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)」を参照してください。  
  
3.  ミラーリング セッションが同期されたら、ミラー データベースに手動でフェールオーバーします。  
  
     この操作を行うには、SQL Server Management Studio または Transact-SQL を使用します。  
  
    -   [データベース ミラーリング セッションを手動でフェールオーバーする方法 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)  
  
    -   [データベース ミラーリング セッションを手動でフェールオーバーする方法 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/manually-fail-over-a-database-mirroring-session-transact-sql.md)  
  
4.  次の ALTER DATABASE コマンドを使用して、TRUSTWORTHY データベース プロパティをオンにします。  
  
    ```  
    ALTER DATABASE <database_name> SET TRUSTWORTHY ON  
    ```  
  
     詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。  
  
5.  必要に応じて、手動で再度フェールオーバーし、元のプリンシパルに戻します。  
  
6.  必要に応じて、SAFETY を OFF に設定し、WITNESS も OFF に設定されていることを確認して、非同期の高パフォーマンス モードに切り替えます。  
  
     Transact-SQL での操作  
  
    -   [データベース ミラーリング セッションでのトランザクションの安全性の変更 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)  
  
    -   [データベース ミラーリング セッションからのミラーリング監視サーバーの削除 &#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
     SQL Server Management Studio での操作  
  
    -   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
## <a name="see-also"></a>参照  
 [TRUSTWORTHY データベース プロパティ](../../relational-databases/security/trustworthy-database-property.md)   
 [暗号化されたミラー データベースの設定](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)  
  
  
