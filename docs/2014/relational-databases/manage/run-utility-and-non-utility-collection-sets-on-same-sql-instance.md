---
title: ユーティリティを実行していると非ユーティリティ コレクション セット SQL Server の同じインスタンスに関する考慮事項 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ca7ee9b3-ef9a-4ba4-83d0-9ee9f80dab27
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5f2e77a1c4be8462fc509b1a2437329f026d5987
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187175"
---
# <a name="considerations-for-running-utility-and-non-utility-collection-sets-on-the-same-instance-of-sql-server"></a>SQL Server の同じインスタンスでユーティリティ コレクション セットとユーティリティ以外のコレクション セットを実行する場合の考慮事項
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ コレクション セットは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ以外のコレクション セットとサイド バイ サイドで実行できます。 つまり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのメンバーであれば、他のコレクション セットによって監視できます。 ただし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ以外のデータ収集機能は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに登録されている場合は無効にする必要があります。  
  
 インスタンスが UCP に登録されたら、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ以外のコレクション セットを再開できます。 ただし、マネージド インスタンス上のすべてのコレクション セットは、そのデータをユーティリティ管理データ ウェアハウス (UMDW) にアップロードすることに注意してください。UMDW ファイル名は sysutility_mdw です。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ コレクション セットを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ以外のコレクション セットとサイド バイ サイドで実行する場合は、次の点を考慮してください。  
  
-   コレクション セットはサイド バイ サイドで実行できます。  
  
-   インスタンスを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに登録している間は、既存のデータ コレクターを無効にする必要があります。  
  
-   検証要件を満たすには、次のストアド プロシージャを、UCP を作成する前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに登録する前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで実行する必要があります。  
  
    ```  
    exec msdb.dbo.sp_syscollector_set_warehouse_database_name NULL  
    exec msdb.dbo.sp_syscollector_set_warehouse_instance_name NULL  
    ```  
  
     UCP の作成ウィザードまたはマネージド インスタンスの追加ウィザードを起動する前にこれらのストアド プロシージャを実行しないと、操作は失敗します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの UMDW (sysutility_mdw) は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のマネージド インスタンス上のすべてのコレクション セットに対して使用する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQL Server ユーティリティの機能とタスク](sql-server-utility-features-and-tasks.md)   
 [ユーティリティ コントロール ポイント データ ウェアハウスの構成 &#40;SQL Server Utility&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md)  
  
  
