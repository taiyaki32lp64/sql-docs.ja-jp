---
title: データベース ファイルから別のデバイスにバックアップ ファイルがある必要があります |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7039bebb-1f25-4cf3-81f1-393dfb78da12
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 09c54c8229351cf27e0f42c8895f2633b8aa7ccb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62812626"
---
# <a name="backup-files-must-be-on-separate-devices-from-the-database-files"></a>バックアップ ファイルはデータベース ファイルとは別のデバイスに配置する
  このルールでは、データベース ファイルがバックアップ ファイルとは異なるデバイス上にあるかどうかを確認します。 データベース ファイルとバックアップ ファイルが同じデバイスにある場合、デバイスに障害が発生すると、データベースとバックアップの両方が使用できなくなります。 また、データベースとバックアップ ファイルを異なるデバイスに置くと、データベースの運用でもバックアップの書き込みでも I/O パフォーマンスが最適化されます。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 データベースとバックアップは異なるデバイスに置くことを強くお勧めします。  
  
> [!NOTE]  
>  このポリシーでは、マウント ポイントを介して別個の物理デバイスを検出することはできません。  
  
## <a name="for-more-information"></a>詳細情報  
 [バックアップ デバイス &#40;SQL Server&#41;](../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
 [SQL Server データベースのバックアップと復元](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したベスト プラクティスの監視と実行](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
