---
title: PDW のファイアウォールの構成
description: SQL Server PDW Configuration Manager の [ファイアウォール] ページでは、Analytics Platform System appliance の特定のポートへのアクセスを許可または禁止するファイアウォール規則を有効または無効にすることができます。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4ed739ce12170aa6d0ab79b996de0075cd6723ee
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400883"
---
# <a name="parallel-data-warehouse-firewall-configuration-in-analytics-platform-system"></a>Analytics Platform System の並列データウェアハウスファイアウォール構成

SQL Server PDW Configuration Manager の [**ファイアウォール**] ページでは、Analytics Platform System appliance の特定のポートへのアクセスを許可または禁止するファイアウォール規則を有効または無効にすることができます。  
  
## <a name="to-manage-ports-and-firewall-rules-for-appliance-nodes"></a>アプライアンスノードのポートとファイアウォールルールを管理するには  
  
1.  Configuration Manager を起動します。 詳細については、「 [Configuration Manager &#40;Analytics Platform System&#41;の起動](launch-the-configuration-manager.md)」を参照してください。  
  
2.  Configuration Manager の左側のウィンドウで、[**並列データウェアハウストポロジ**] を展開し、[**ファイアウォール**] をクリックします。  
  
3.  [構成] ボックスの一覧で、更新するポートまたはファイアウォール規則を見つけて、その項目の横にあるチェックボックスをオンまたはオフにします。 この一覧には、SQL Server PDW 管理者が構成可能なオプションのみが表示されます。外部に接続しているノードのポートを開いたり閉じたりすることもできます。  
  
4.  [**適用**] をクリックして変更を保存します。  
  
![DWConfig アプライアンス PDW のファイアウォール](./media/pdw-firewall-configuration/SQL_Server_PDW_DWConfig_ApplPDWFirewall.png "SQL_Server_PDW_DWConfig_ApplPDWFirewall")  
  
## <a name="external-ports"></a>外部ポート  
次のポートは、PDW の外部からのクライアント接続用に開かれています。  
  
|目的|ポート#|Nodes|  
|-----------|-----------|---------|  
|PDW 用 SQL クライアントアクセス (TDS)|17001|CTL|  
|ローダークライアントアクセス (dwloader & SSIS)|8001|CTL|  
|リモート デスクトップ アクセス|3389|CTL、CMP|  
|SSIS BinaryLoaderDataChannel|16551|CTL|  
|dwloader BinaryLoaderDataChannel|16551|CMP|  
|SSL で暗号化された接続 (内部通信の場合は、管理コンソールにアクセスする場合)|443|すべてのノード|  
|SQL Server PDW のロード制御フロー-Windows 資格情報|8002|CTL|  
|_Kerberos|88|AD01 と AD02、|  
|_ldap|389|AD01 と AD02|  
| &nbsp; | &nbsp; | &nbsp; |
  
## <a name="internal-ports"></a>内部ポート  
次のポートは、PDW が内部通信に使用しますが、PDW アプライアンスの外部からの接続に対しては開かれません。  
  
|目的|ポート#|Nodes|  
|-----------|-----------|---------|  
|DMS 制御チャネルトラフィック|16450|CTL、CMP|  
|DMS データチャネルトラフィック|16550|CTL、CMP|  
|内部診断|16650|CTL、CMP|  
|フェールオーバーの状態 (DMS)|15000|CTL、CMP|  
|フェールオーバーの状態 (エンジン)|15001|CMP|  
|動的 (短期) ポート範囲|20000-65535|CTL、CMP|  
|ポート範囲の SQL Server (TDS)|1433、1500-1508|CTL、CMP|  
| &nbsp; | &nbsp; | &nbsp; |
  
> [!NOTE]  
> 外部テーブルまたは外部データソースの作成では、既定で TCP ポート8020が使用されます。 これらのステートメントは、代わりに他のポートを使用するように構成できます。 Hortonworks JOB_TRACKER_LOCATION の既定のポートは50300です。 他のシステムやツールとの統合には、追加のポートが必要になる場合があります。  
  
<!-- MISSING LINKS ## See Also  
[HDInsight Firewall Configuration &#40;Analytics Platform System&#41;](hdinsight-firewall-configuration.md)
-->
  
