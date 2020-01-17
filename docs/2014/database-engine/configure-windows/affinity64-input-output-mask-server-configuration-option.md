---
title: affinity64 Input-Output mask サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- binding processors [SQL Server]
- affinity64 I/O mask option
ms.assetid: d304eae7-5116-40ee-a0fa-0a3c0bc20c01
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f32c35aabf7d95a31624ca5c507fccac8ba1053e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62811566"
---
# <a name="affinity64-input-output-mask-server-configuration-option"></a>affinity64 Input-Output mask サーバー構成オプション
  **affinity64 I/O mask** オプションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のディスク I/O を指定した CPU のサブセットにバインドします。このオプションは、 **affinity I/O mask** オプションに似ています。 **affinity I/O mask** を使用して最初の 32 プロセッサをバインドし、 **affinity64 I/O mask** を使用してコンピューター上の残りのプロセッサをバインドします。 **affinity64 I/O mask**オプションを再構成した場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスを再起動する必要があります。 このオプションは 64 ビット版の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのみ表示されます。  
  
## <a name="see-also"></a>関連項目  
 [affinity Input-Output mask サーバー構成オプション](affinity-input-output-mask-server-configuration-option.md)   
 [リソースの利用状況の監視 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
