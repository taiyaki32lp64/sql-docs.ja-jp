---
title: ディストリビューション保有期間の設定
description: SQL Server Management Studio (SSMS) で、ディストリビューション データベース内のデータの保有期間を設定します。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: ebbf937388d19b36910bc0d1a029933f500d4715
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321720"
---
# <a name="set-distribution-retention-period-for-transactional-publications"></a>トランザクション パブリケーションのディストリビューションの保有期間の設定
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  **[ディストリビューション データベースのプロパティ - \<DistributionDatabase>]** ダイアログ ボックスで、ディストリビューションの最小保有期間と最大保有期間を指定します。 このダイアログ ボックスは、 **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスの **[全般]** ページから使用できます。 このダイアログ ボックスへのアクセスの詳細については、「[ディストリビューターとパブリッシャーのプロパティの表示および変更](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)」を参照してください。  
  
### <a name="to-specify-the-distribution-retention-period"></a>ディストリビューションの保有期間を指定するには  
  
1.  **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスの **[全般]** ページで、ディストリビューション データベースのプロパティ ボタン **[...]** をクリックします。  
  
2.  ディストリビューションの最小保有期間を指定するには **[最小]** ボックスに値を入力し、ディストリビューションの最大保有期間を指定するには **[最大]** ボックスに値を入力します。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="see-also"></a>参照  
 [[ディストリビューションの構成]](../../relational-databases/replication/configure-distribution.md)   
 [サブスクリプションの有効期限と非アクティブ化](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
