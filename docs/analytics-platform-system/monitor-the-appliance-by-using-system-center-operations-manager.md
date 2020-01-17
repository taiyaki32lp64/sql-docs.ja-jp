---
title: SCOM で監視する
description: Analytics Platform System (APS) アプライアンスを監視するには、System Center Operations Manager (SCOM) を使用します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 0b244d85e601e46fe778298e723c0a7d01e669bb
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400971"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>System Center Operations Manager 分析プラットフォームシステムを使用した監視
Analytics Platform System (APS) アプライアンスを監視するには、System Center Operations Manager (SCOM) を使用します。
  
## <a name="before-you-begin"></a>開始する前に  
  
### <a name="prerequisites"></a>前提条件  
  
1.  System Center Operations Manager 2007 R2、2012、または 2012 SP1 がインストールされ、実行されている必要があります。  
  
2.  SQL Server 2008 R2 Native Client または SQL Server 2012 Native Client がインストールされている必要があります。  
  
3.  SQL Server PDW を監視する管理パックをインストール、インポート、および構成する必要があります。 これらのタスクを実行する手順については、次の記事を参照してください。  
  
    -   [SCOM 管理パック &#40;Analytics Platform System&#41;をインストールします。](install-the-scom-management-packs.md)  
  
    -   [PDW &#40;Analytics Platform System&#41;用の SCOM 管理パックをインポートします。](import-the-scom-management-pack-for-pdw.md) 
    
    -   [SCOM を構成して Analytics Platform System &#40;Analytics Platform System&#41;を監視する](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>SCOM で SQL Server PDW を監視するには  
SCOM 管理パックを構成したら、SCOM の [監視] ウィンドウをクリックし、 **SQL Server アプライアンス**にドリルダウンして、 **Microsoft SQL Server Parallel Data Warehouse**します。 Microsoft SQL Server Parallel Data Warehouse の下には、アラート、アプライアンス、アプライアンスダイアグラム、ノードの4つの選択肢があります。  
  
### <a name="alerts"></a>アラート  
アラートでは、管理対象の現在のアラートを確認できます。  
  
![コンテンツ](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>アプライアンス  
アプライアンスは、現在環境内で検出および監視されている SQL Server PDW アプライアンスを見つけます。 アプライアンスがここに表示されず、そのための ODBC 接続を作成している場合は、PDWWatcher アカウントで問題が発生している可能性があります。 "監視されていません" と表示されている場合は、PDWMonitor アカウントで問題が発生している可能性があります。 SCOM はリアルタイムで変更されることはないため、定期的に監視する新しいアプライアンスを確認し、監視のために定期的にクエリをアプライアンスに送信します。  
  
![電気](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>アプライアンスの図  
[アプライアンスダイアグラム] ページでは、ツリービューでアプライアンスのヘルスを確認できます。  
  
![アプライアンスの図](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>Nodes  
最後に、ノードビューでは、各ノードでアプライアンスの正常性を確認できます。  
  
![節](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>参照  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[管理コンソールのアラートについて &#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)  
  
