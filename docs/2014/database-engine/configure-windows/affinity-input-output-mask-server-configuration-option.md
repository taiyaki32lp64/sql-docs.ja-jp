---
title: affinity Input-Output mask サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- affinity I/O mask option
- processor affinity [SQL Server]
- binding processors [SQL Server]
- CPU affinity mask option
ms.assetid: 9950a8c9-9fe0-4003-95df-6f0d1becb0e7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 65e412a3dfdfc71931e6af4d449c5be88ae351b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813680"
---
# <a name="affinity-input-output-mask-server-configuration-option"></a>affinity Input-Output mask サーバー構成オプション
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 と Windows Server 2003 では、マルチタスク処理を実行するために、プロセス スレッドを異なるプロセッサ間で移動させることがあります。 オペレーティング システムにとっては効率的であっても、この操作で各プロセッサのキャッシュに繰り返しデータが再読み込みされるため、システムの負荷が高くなり、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンスが低下する場合があります。 このような状況では、特定のスレッドにプロセッサを割り当てることで、プロセッサの再読み込みを回避してパフォーマンスを向上できます。このようなスレッドとプロセッサ間の関連付けを "プロセッサ関係 (processor affinity)" と言います。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 **affinity mask** (別名 **CPU affinity mask**) と **affinity I/O mask**の 2 つの affinity mask オプションにより、プロセッサ関係をサポートします。 **affinity mask** オプションの詳細については、「 [affinity mask サーバー構成オプション](affinity-mask-server-configuration-option.md)」を参照してください。 プロセッサが 33 から 64 個のサーバーに対して CPU および I/O affinity をサポートするには、 [affinity64 mask サーバー構成オプション](affinity64-mask-server-configuration-option.md) および [affinity64 I/O mask サーバー構成オプション](affinity64-input-output-mask-server-configuration-option.md) がそれぞれ必要になります。  
  
> [!NOTE]  
>  33 から 64 個までのプロセッサを搭載しているサーバーでの関係 (affinity) は、64 ビット オペレーティング システムでのみサポートされます。  
  
 **affinity I/O mask** オプションでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のディスク I/O が、指定した CPU のサブセットに関連付けられます。 ハイエンドな [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン トランザクション処理 (OLTP) 環境では、この拡張機能により、I/O を発行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スレッドのパフォーマンスを向上できます。 この拡張機能では、個別のディスクやディスク コントローラーのハードウェア関係 (hardware affinity) はサポートされません。  
  
 マルチプロセッサ コンピューターでは、 **affinity I/O mask** の値により、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のディスク I/O 操作を処理できる CPU が指定されます。 このマスクはビットマップで、右端のビットによって最も順番の小さい CPU(0) が指定され、そのビットの左隣のビットによって次に順番の小さい CPU(1) が指定され、それ以降も同様に CPU が指定されます。 33 個以上のプロセッサを構成するには、 **affinity I/O mask** と **affinity64 I/O mask**の両方を設定します。  
  
 **affinity I/O mask** の値は、以下のとおりです。  
  
-   1 バイトの **affinity I/O mask** は、マルチプロセッサ コンピューターの最大 8 個の CPU に対応します。  
  
-   2 バイトの **affinity I/O mask** は、マルチプロセッサ コンピューターの最大 16 個の CPU に対応します。  
  
-   3 バイトの **affinity I/O mask** は、マルチプロセッサ コンピューターの最大 24 個の CPU に対応します。  
  
-   4 バイトの **affinity I/O mask** は、マルチプロセッサ コンピューターの最大 32 個の CPU に対応します。  
  
-   33 個以上の CPU に対応するには、最初の 32 個の CPU に 4 バイトの **affinity I/O mask** を構成し、残りの CPU に 4 バイトの **affinity64 I/O mask** を構成します。  
  
 affinity I/O パターンで 1 が設定されているビットは、対応する CPU で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のディスク I/O 操作を実行できることを示します。また、0 が設定されているビットは、対応する CPU に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のディスク I/O 操作のスケジュールを設定できないことを示します。 すべてのビットがゼロに設定されているか、 **affinity I/O mask** が指定されていない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のディスク I/O は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のスレッドを処理できるすべての CPU にスケジュール設定されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **affinity I/O mask** オプションの設定は特殊な操作なので、特に必要な場合にのみこのオプションを使用することをお勧めします。 通常は、Windows 2000 または Windows 2003 の既定の関係 (affinity) で、最適なパフォーマンスが得られます。  
  
 **affinity I/O mask** オプションを指定する場合は、 **affinity mask** 構成オプションと共に使用する必要があります。 **affinity I/O mask** スイッチと **affinity mask** オプションの両方で同じ CPU を有効にしないようにしてください。 各 CPU に対応するビットは、次の 3 つの状態のうちのいずれかに設定します。  
  
-   **affinity I/O mask** オプションと **affinity mask** オプションの両方で 0。  
  
-   **affinity I/O mask** オプションで 0、 **affinity mask** オプションで 1。  
  
-   **affinity I/O mask** オプションで 0、 **affinity mask** オプションで 1。  
  
 **affinity I/O mask** オプションは拡張オプションです。 使用する場合、`sp_configure`システム ストアド プロシージャの設定を変更するのには、変更できます**affinity I/O mask**場合にのみ**詳細オプションの表示**が 1 に設定します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、**affinity I/O mask[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オプションを再構成した場合、** のインスタンスを再起動する必要があります。  
  
> [!CAUTION]  
>  Windows オペレーティング システムでの CPU 関係の構成と、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] での関係マスクの構成は、同時に行わないようにしてください。 この 2 つの設定は、同じ効果をねらったものであり、これらの構成間に一貫性がない場合は、予期しない結果を招く可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU 関係を構成する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の `sp_configure` オプションを使用する方法が最適です。  
  
## <a name="see-also"></a>関連項目  
 [リソースの利用状況の監視 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
