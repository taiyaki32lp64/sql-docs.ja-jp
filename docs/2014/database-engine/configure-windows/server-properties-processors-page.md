---
title: サーバーのプロパティ ([プロセッサ] ページ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.processor.f1
ms.assetid: cc1581a2-492b-41f0-bda5-17909b65c4f7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: aae800226a585f7a29334887829be2a09277a004
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62809278"
---
# <a name="server-properties-processors-page"></a>[サーバーのプロパティ] ([プロセッサ] ページ)
  このページを使用すると、プロセッサ オプションを表示または変更できます。 プロセッサの関係の設定は、複数のプロセッサが実装されている場合のみ有効です。  
  
## <a name="options"></a>および  
 **[プロセッサの関係]**  
 プロセッサの再読み込みを防ぎ、プロセッサ間のスレッドの移行を少なくするために、プロセッサを特定のスレッドに割り当てます。 詳細については、「 [affinity mask サーバー構成オプション](affinity-mask-server-configuration-option.md)」を参照してください。  
  
 **[I/O 関係]**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ディスク I/O を特定の CPU のサブセットにバインドします。 詳細については、「 [affinity Input-Output mask サーバー構成オプション](affinity-input-output-mask-server-configuration-option.md)」を参照してください。  
  
 **[すべてのプロセッサに対して自動的にプロセッサ関係マスクを設定する]**  
 プロセッサの関係が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって設定されます。  
  
 **[すべてのプロセッサに対して自動的に I/O 関係マスクを設定する]**  
 I/O 関係が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって設定されます。  
  
 **[ワーカー スレッドの最大数]**  
 0 を指定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はワーカー スレッドの数を動的に設定します。 この設定は、ほとんどのシステムで最適な設定です。 ただし、システム構成によっては、このオプションに特定の値を設定した方がパフォーマンスが向上することがあります。 詳細については、「 [max worker threads サーバー構成オプションの構成](configure-the-max-worker-threads-server-configuration-option.md)」を参照してください。  
  
 **SQL Server の優先度を上げる**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows スケジュールでの [!INCLUDE[msCoName](../../includes/msconame-md.md)] の優先度を、同じコンピューター内の他のプロセスよりも高くして実行するかどうかを指定します。 詳細については、「 [priority boost サーバー構成オプションの構成](configure-the-priority-boost-server-configuration-option.md)」を参照してください。  
  
 **[Windows ファイバーを使用する (簡易プーリング)]**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに対して、スレッドの代わりに Windows ファイバーを使用します。 このオプションは、Windows 2003 Server Edition でのみ使用できます。 詳細については、「 [lightweight pooling Server Configuration Option](lightweight-pooling-server-configuration-option.md)」を参照してください。  
  
 **[構成した値]**  
 このペインの各オプションに構成されている値を表示します。 これらの値を変更した場合は、 **[実行中の値]** をクリックして、変更後の値が反映されているかどうかを確認してください。 値が反映されていない場合は、最初に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを再起動する必要があります。  
  
 **[実行中の値]**  
 このペイン上のオプションの、現在実行中の値を表示します。 これらの値は読み取り専用です。  
  
## <a name="see-also"></a>参照  
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
