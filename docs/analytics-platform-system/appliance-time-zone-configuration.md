---
title: タイムゾーンの構成
description: '[タイムゾーン] ページでは、Analytics Platform System (APS) アプライアンスのすべてのノードのタイムゾーンを設定できます。'
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1da16790d011a628bc2536de051eb1181f06b8cf
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401393"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>アプライアンスのタイムゾーンの構成-分析プラットフォームシステム
[**タイムゾーン**] ページでは、Analytics Platform SYSTEM (APS) アプライアンスのすべてのノードのタイムゾーンを設定できます。  
  
## <a name="to-set-the-time-zone"></a>タイムゾーンを設定するには  
  
1.  Configuration Manager を起動します。 詳細については、「 [Configuration Manager &#40;Analytics Platform System&#41;の起動](launch-the-configuration-manager.md)」を参照してください。  
  
2.  Configuration Manager の [**サービスの状態**] ページを使用して、アプライアンスサービスを停止します。 手順については、「 [PDW サービスの状態 &#40;Analytics Platform System&#41;](pdw-services-status.md) 」を参照してください。  
  
3.  Configuration Manager の左側のウィンドウで、[**タイムゾーン**] をクリックします。 [**タイムゾーン**] ドロップダウンメニューから目的のタイムゾーンを選択します。 場所によっては、[**夏時間を自動的に調整**する] の横にあるボックスを選択することもできます。  
  
4.  [**適用**] をクリックして変更を保存します。  
  
5.  Configuration Manager の [**サービスの状態**] ページを使用して、アプライアンスサービスを再開します。 また、特権を変更することも計画している場合は、アプライアンスを再起動する前にその操作を行うことができます。  
  
![DWConfig アプライアンスの時刻](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>参照  
[Configuration Manager &#40;Analytics Platform System&#41;を起動します。](launch-the-configuration-manager.md)  
  
