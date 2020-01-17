---
title: ウイルス対策ソフトウェア
description: データセンターにウイルス対策ソフトウェアが必要な場合は、次のガイドラインに従って、Analytics Platform System (APS) にウイルス対策ソフトウェアをインストールしてください。 データセンターの要件が十分でない場合は、ウイルス対策ソフトウェアをインストールしないことをお勧めします。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: c3687b839e52e64350591402c3aa19e9c2c54ac7
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401472"
---
# <a name="antivirus-software-for-analytics-platform-system-aps"></a>Analytics Platform System (APS) 用ウイルス対策ソフトウェア
データセンターでウイルス対策ソフトウェアが必要な場合は、次のガイドラインに従って、Analytics Platform System にウイルス対策ソフトウェアをインストールしてください。 データセンターの要件が十分でない場合は、ウイルス対策ソフトウェアをインストールしないことをお勧めします。  
  
> [!WARNING]  
> 各コンピューターのセキュリティリスクと分析プラットフォームシステム全体を個別に評価し、各コンピューターのセキュリティリスクレベルに適したツールを選択することを強くお勧めします。 また、ウイルス対策プロジェクトを展開する前に、システム全体を完全な負荷でテストして、安定性とパフォーマンスの変化を測定することをお勧めします。  
>   
> ウイルス対策ソフトウェアを実行するには、いくつかのシステムリソースが必要です。 分析プラットフォームシステムにパフォーマンス上の影響があるかどうかを判断するには、ウイルス対策ソフトウェアをインストールする前と後にテストを実行する必要があります。  
  
このトピックの内容は、SQL Server および[サポート技術情報の記事 961804](https://support.microsoft.com/kb/961804/en-us)を実行している[コンピューターでウイルス対策ソフトウェアを選択して実行する方法](https://support.microsoft.com/kb/309422)に関するガイドに基づいています。  
  
## <a name="exclusion-list-for-physical-hosts"></a>物理ホストの除外一覧  
物理ホストにウイルス対策ソフトウェアをインストールするには、次のディレクトリとプロセスの一覧を除外します。 ウイルス対策ソフトウェアによってスキャンされないようにする必要があります。  
  
**次のディレクトリを除外:**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V-仮想マシンの構成ディレクトリ  
  
-   C:\Users\Public\Documents\Hyper-V\Virtual ハードディスク-既定の仮想ハードディスクドライブディレクトリ  
  
-   C:\: 記憶域-仮想ハードディスクドライブディレクトリ  
  
**次のプロセスを除外する:**  
  
-   バーチャルマシンの管理 (Vmms)  
  
-   仮想マシンの作業プロセス (Vmwp .exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>Virtual Machines (Vm) の除外一覧  
Vm にウイルス対策ソフトウェアをインストールするには、次のディレクトリとファイルの一覧を除外します。 ウイルス対策ソフトウェアによってスキャンされないようにする必要があります。  
  
**_PDW_region_-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-AD01**および** _appliance_domain_-AD02**  
  
-   制限なし  
  
**コンピューティングノード Vm**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-VMM**  
  
-   制限なし  
  
**_appliance_domain_-WDS**  
  
-   制限なし  
  
**_appliance_domain_-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>参照  
[アプライアンス管理タスク &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
