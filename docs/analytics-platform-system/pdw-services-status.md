---
title: PDW のサービス状態
description: 分析プラットフォームシステムの並列データウェアハウス (PDW) サービスの状態。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2789c8b74420a56a32d08a0339d4ee6d3cc112d1
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400856"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>分析プラットフォームシステムの並列データウェアハウスサービスの状態
Microsoft Analytics Platform System Configuration Manager の [並列データウェアハウス**サービスの状態**] ページには、すべての SQL Server PDW サービスの現在の状態が表示され、PDW サービスを停止および開始することができます。 これは、PDW サービスを開始および停止する唯一のサポートされている方法です。 個々のコンポーネントまたはサービスは個別に起動できないことに注意してください。  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>アプライアンスサービスを開始または停止するには  
  
1.  アプライアンスサービスを開始するには、[**アプライアンスの開始**] をクリックします。  
  
2.  アプライアンスサービスを停止するには、[**アプライアンスの停止**] をクリックします。  
  
[**アプライアンスの開始**] と [**アプライアンスの停止**] を使用してアプライアンスサービスを開始および停止する場合は、[**適用**] をクリックする必要はありません。  
  
![DWConfig アプライアンス PDW サービス](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> PDW 領域を停止すると、ノード上の PDW エージェント (sqldwagent) も停止します。 PDW エージェントでは、正常性の監視をレポートするために PDW コントロールノードが必要です。  
  
## <a name="see-also"></a>参照  
[APS アプライアンスの電源をオンまたはオフ &#40;Analytics Platform System&#41;](power-the-aps-appliance-on-or-off.md)  
  
