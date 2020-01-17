---
title: WQL を使用して構成管理用 WMI プロバイダーへのアクセス |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
ms.assetid: 26499530-d93b-452b-bbe4-217ef1d11e68
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: adec01de84122552812e5b1b28277d0d399fee56
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68195872"
---
# <a name="access-wmi-provider-for-configuration-management-using-wql"></a>WQL を使用して構成管理の WMI プロバイダーにアクセスする
  このセクションでは、WMI Provider for Computer Management に対して [!INCLUDE[msCoName](../../includes/msconame-md.md)] WQL (Windows Management Instrumentation Query Language) ステートメントを実行する方法について説明します。  
  
 この例では、WQL エディター、WBEMtest.exe を使用して、WMI プロバイダーに対して WQL クエリを実行し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス、ネットワーク プロトコル、および別名を列挙します。  
  
### <a name="querying-services-using-wbemtest"></a>WBEMtest を使用したサービスの照会  
  
1.  **開始** メニューのをクリックして**実行**、し、入力`WBEMtest`します。  
  
2.  WBEMtest.exe のダイアログ ボックスが表示されます。 **[接続]** をクリックします。  
  
3.  最初のテキスト フィールドに、WMI Provider for Computer Management の名前空間 (「root\Microsoft\SqlServer\ComputerManagement11」) を入力します。 **[接続]** をクリックします。  
  
4.  クリックして**クエリ**します。 ローカル コンピューターで実行されている現在のサービスを返すクエリを入力します。**選択\*SqlService から。** **[適用]** をクリックします。  
  
5.  「`WHERE ServiceName = "MSSQLSERVER"`」を追加することで、クエリを絞り込みます。  
  
  
