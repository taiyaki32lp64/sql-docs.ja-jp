---
title: 暗号化されたデータベースと AlwaysOn 可用性グループ (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption, AlwaysOn Availability Groups
- TDE, AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 09eb6ebc-3051-4fff-86a5-93524507b1fc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5bafd990a7c115a6108b699a61897f9e587e83c4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62814638"
---
# <a name="encrypted-databases-with-alwayson-availability-groups-sql-server"></a>暗号化されたデータベースと AlwaysOn 可用性グループ (SQL Server)
  このトピックでは、 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] で現在暗号化されているデータベースまたは最近暗号化解除されたデータベースと [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]を使用する方法について説明します。  
  
 **このトピックの内容**  
  
-   [制限事項と制約事項](#Restrictions)  
  
-   [関連タスク](#RelatedTasks)  
  
##  <a name="Restrictions"></a> 制限事項と制約事項  
  
-   データベースが暗号化されているか、データベース暗号化キー (DEK) を含んでいる場合、 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] または [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] を使用してそのデータベースを可用性グループに追加することはできません。 暗号化されたデータベースの暗号化を解除した場合でも、そのログ バックアップには暗号化されたデータが含まれていることがあります。 この場合、データベースに対する初期データの完全同期が失敗する可能性があります。 これは、ログの復元操作にはデータベース暗号化キー (DEK) で使用された証明書が必要なことがあり、その証明書を使用できないことがあるためです。  
  
     暗号化解除されたデータベースを、ウィザードを使用して可用性グループに追加できるようにするには、次の操作を行います。  
  
    1.  プライマリ データベースのログ バックアップを作成します。  
  
    2.  プライマリ データベースの完全バックアップを作成します。  
  
    3.  セカンダリ レプリカをホストするサーバー インスタンスでデータベース バックアップを復元します。  
  
    4.  プライマリ データベースから新しいログ バックアップを作成します。  
  
    5.  セカンダリ データベースでこのログ バックアップを復元します。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [可用性グループに対するセカンダリ データベースの手動準備 &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [可用性グループ ウィザードの使用 &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [可用性グループへのデータベース追加ウィザードの使用 &#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>関連項目  
 [AlwaysOn 可用性グループの概要&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [透過的なデータ暗号化 &#40;TDE&#41;](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
  
