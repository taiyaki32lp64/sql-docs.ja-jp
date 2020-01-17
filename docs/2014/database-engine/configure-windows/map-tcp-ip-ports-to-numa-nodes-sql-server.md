---
title: NUMA ノードへの TCP/IP ポートのマッピング (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- NUMA
- memory [SQL Server], NUMA
- affinity NUMA
- ports [SQL Server], working with NUMA
- CPU [SQL Server], NUMA support
- NUMA, How to map a port to a NUMA node
- NUMA affinity
- TCP/IP [SQL Server], NUMA support
- non-uniform memory access
ms.assetid: 07727642-0266-4cbc-8c55-3c367e4458ca
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 138e5743e18ba6e39aa55aaec6931413dd21175b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781746"
---
# <a name="map-tcp-ip-ports-to-numa-nodes-sql-server"></a>NUMA ノードへの TCP/IP ポートのマッピング (SQL Server)
  このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、TCP/IP ポートを NUMA (non-uniform memory access) ノードにマップする方法について説明します。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、起動時にノード情報をエラー ログに書き込みます。  
  
 使用するノードのノード番号を調べるには、エラー ログまたは **sys.dm_os_schedulers** ビューからノード情報を読み取ります。 1 つのノードまたは複数のノードに対して TCP/IP アドレスとポートを設定するには、ポート番号の後に、ノード ID ビットマップ (関係マスク) を角かっこで囲んで追加します。 ノードは、10 進数形式または 16 進数形式で指定できます。 ビットマップを作成するには、ノードに対して右から左に、76543210 のように 0 から番号を付けます。 使用するノードには 1、使用しないノードには 0 を指定して、ノード リストのバイナリ表記を作成します。 たとえば、0 番、2 番、および 5 番の NUMA ノードを使用するには、00100101 と指定します。  
  
|||  
|-|-|  
|NUMA ノード番号|76543210|  
|右から数えて 0 番、2 番、および 5 番をマスク|00100101|  
  
 バイナリ表記 (00100101) を 10 進数 `[37]`または 16 進数 `[0x25]`に変換します。 すべてのノードでリッスンするには、ノード識別子を指定しません。  
  
 ポートが複数の NUMA ノードにマッピングされている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はノード間での負荷分散を試行することなくラウンド ロビン方式でノードに接続を割り当てます。  
  
> [!NOTE]  
>  各 IP アドレスの複数の TCP ポートでのリッスンを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で有効にするには、「 [複数の TCP ポートでリッスンするデータベース エンジンの構成](configure-the-database-engine-to-listen-on-multiple-tcp-ports.md)」を参照してください。  
  
##  <a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="to-map-a-tcpip-port-to-a-numa-node"></a>NUMA ノードに TCP/IP ポートをマッピングするには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーで、 **[SQL Server ネットワークの構成]** を展開し、 **[\<インスタンス名>** *のプロトコル]* をクリックします。  
  
2.  詳細ペインで、 **[TCP/IP]** をダブルクリックします。  
  
3.  **[IP アドレス]** タブで、構成する IP アドレスに対応するセクションの **[TCP ポート]** ボックスで、ポート番号の後に NUMA ノード識別子を角かっこで囲んで追加します。 たとえば、TCP ポート 1500 とノード 0 番、2 番、5 番の場合、`1500[37]`、または `1500[0x25]` を使用します。  
  
## <a name="see-also"></a>関連項目  
 [ソフト NUMA を使用する SQL Server を構成する&#40;SQL Server&#41;](soft-numa-sql-server.md)  
  
  
