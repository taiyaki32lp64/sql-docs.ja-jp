---
title: データベース ミラーリング セッションでのトランザクションの安全性の変更 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- transaction safety [SQL Server database mirroring]
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a79010a4fa59eaebfc743543799a1e83cc5e687d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754926"
---
# <a name="change-transaction-safety-in-a-database-mirroring-session-transact-sql"></a>データベース ミラーリング セッションでのトランザクションの安全性の変更 (Transact-SQL)
  トランザクションの安全性は、セッションの動作モードを制御する属性です。 ただし、データベース所有者は、いつでもトランザクションの安全性を変更できます。 既定では、トランザクションの安全性レベルは FULL (同期動作モード) に設定されています。  
  
 トランザクションの安全性を無効にすると、セッションの動作モードが、パフォーマンスを最適にする非同期動作モードに切り替わります。 プリンシパル サーバーを使用できなくなるとミラー サーバーは停止しますが、ミラー サーバーをウォーム スタンバイ サーバーとして使用することができます (フェールオーバーにはサービスの強制が必要ですが、データを損失する可能性があります)。  
  
### <a name="to-turn-on-transaction-safety"></a>トランザクションの安全性を有効にするには  
  
1.  プリンシパル サーバーに接続します。  
  
2.  次の Transact-SQL ステートメントを実行します。  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY FULL  
    ```  
  
     *\<database>* はミラー化されたデータベースの名前です。  
  
### <a name="to-turn-off-transaction-safety"></a>トランザクションの安全性を無効にするには  
  
1.  プリンシパル サーバーに接続します。  
  
2.  次のステートメントを実行します。  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY OFF  
    ```  
  
     *\<database>* はミラー化されたデータベースです。  
  
## <a name="see-also"></a>関連項目  
 [ALTER DATABASE データベース ミラーリング &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [Database Mirroring Operating Modes](database-mirroring-operating-modes.md)  
  
  
