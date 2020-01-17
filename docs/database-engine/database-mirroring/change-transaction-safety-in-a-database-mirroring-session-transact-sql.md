---
title: トランザクションの安全性の変更 (ミラー化されたデータベース)
description: Transact-SQL を使用して、SQL Server データベース ミラーリング セッションでのトランザクションの安全性属性を変更します。
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- transaction safety [SQL Server database mirroring]
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3ba0b574fea1974ab93c5cecf4346942df6c4a2c
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247492"
---
# <a name="change-transaction-safety-in-a-database-mirroring-session-transact-sql"></a>データベース ミラーリング セッションでのトランザクションの安全性の変更 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE データベース ミラーリング &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  
