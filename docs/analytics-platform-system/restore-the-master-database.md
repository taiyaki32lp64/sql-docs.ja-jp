---
title: Master データベースの復元
description: Analytics Platform System (APS) で master データベースを復元します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6d122881f5283da86f66494ee2f049756d151551
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400453"
---
# <a name="restore-the-master-database-in-analytics-platform-system-aps"></a>Analytics Platform System (APS) での master データベースの復元
SQL Server PDW Configuration Manager の**復元マスター**ページを使用すると、バックアップから master データベースを復元できます。  
  
## <a name="before-you-begin"></a>開始する前に  
  
> [!IMPORTANT]  
> 復元を実行するには、ユーザーのセキュリティ情報とデータベースカタログを含む現在の master データベースを削除 SQL Server PDW 必要があります。 復元を実行する前に、現在の master データベースのバックアップを作成することをお勧めします。  
  
## <a name="to-restore-the-master-database"></a>master データベースを復元するには  
  
1.  Configuration Manager を起動します。 詳細については、「 [Configuration Manager &#40;Analytics Platform System&#41;の起動](launch-the-configuration-manager.md)」を参照してください。  
  
2.  Configuration Manager の左側のウィンドウで、[ **Master の復元**] をクリックします。  
  
3.  復元するマスターバックアップを選択します。  
  
4.  
  **[適用]** をクリックします。  
  
5.  復元を実行するために、SQL Server PDW によってすべてのアプライアンスサービスがシャットダウンされ、すべてのユーザーが切断されます。 復元が完了すると、SQL Server PDW によってアプライアンスサービスが再開されます。  
  
![DWConfig アプライアンス PDW の master の復元](./media/restore-the-master-database/SQL_Server_PDW_DWConfig_ApplPDWRestore.png "SQL_Server_PDW_DWConfig_ApplPDWRestore")  
  
