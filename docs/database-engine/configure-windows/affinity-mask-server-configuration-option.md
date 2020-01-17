---
title: affinity mask サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default affinity mask option
- reloading processor cache
- processor cache [SQL Server]
- CPU [SQL Server], licensing
- deferred process call
- affinity mask option
- processor affinity [SQL Server]
- SMP
- DPC
ms.assetid: 5823ba29-a75d-4b3e-ba7b-421c07ab3ac1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 27f6d8f947dc0ad5e25ddf53ac63e5f40b332c2e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013212"
---
# <a name="affinity-mask-server-configuration-option"></a>affinity mask サーバー構成オプション
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) を使用します。  
  
 マルチタスクを実行するため、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows では、プロセス スレッドが別のプロセッサに移動される場合があります。 オペレーティング システムにとっては効率的であっても、この操作で各プロセッサのキャッシュに繰り返しデータが再読み込みされるため、システムの負荷が高くなり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンスが低下する場合があります。 このような状況では、特定のスレッドにプロセッサを割り当てることで、プロセッサの再読み込みを回避し、プロセッサ間でのスレッドの移行回数を少なくできるため、コンテキストの切り替えを減らしてパフォーマンスを改善できます。このようなスレッドとプロセッサ間の関連付けを "プロセッサ関係 (processor affinity)" と言います。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、affinity mask (別名 **CPU affinity mask**) と affinity I/O mask の 2 つの affinity mask オプションにより、プロセッサ関係をサポートします。 affinity I/O mask オプションの詳細については、「 [affinity Input-Output mask サーバー構成オプション](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)」を参照してください。 プロセッサが 33 から 64 個のサーバーに対して CPU および I/O affinity をサポートするには、 [affinity64 mask サーバー構成オプション](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) および [affinity64 I/O mask サーバー構成オプション](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md)がそれぞれ必要になります。  
  
> [!NOTE]  
>  33 から 64 個までのプロセッサを搭載しているサーバーでの関係 (affinity) は、64 ビット オペレーティング システムでのみサポートされます。  
  
 affinity mask オプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の以前のリリースでも提供されており、動的に CPU 関係を制御します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスを再起動しなくても affinity mask オプションを構成できます。 sp_configure を使用する場合は、構成オプションを設定した後、RECONFIGURE または RECONFIGURE WITH OVERRIDE のどちらかを実行する必要があります。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]を使用している場合、affinity mask オプションを変更しても再起動は必要ありません。  
  
 関係マスク (affinity mask) に対する変更は動的に行われるため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内のプロセス スレッドをバインドする CPU スケジューラのオンデマンドでの起動とシャットダウンが可能になります。 この処理は、サーバーの状態の変化に伴って発生する可能性があります。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の新しいインスタンスをサーバーに追加したときに、プロセッサの負荷を再分散するために、affinity mask オプションを調整する必要が生じる場合があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が新しい CPU スケジューラを有効にし、既存の CPU スケジューラを無効にするためには、関係ビットマスク (affinity bitmask) を変更する必要があります。 関係ビットマスクを変更すると、新しいスケジューラまたは継続して使用されているスケジューラで新しいバッチを処理できるようになります。  
  
 新しい CPU スケジューラを起動するために、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により新しいスケジューラが作成され、これが標準のスケジューラのリストに追加されます。 新しいスケジューラは、新しく受信するバッチ専用と見なされます。 現在のバッチは、これまでと同じスケジューラで実行されます。 ワーカーは、ワーカーが解放されたとき、または新しいワーカーが作成されたときに、新しいスケジューラに移行されます。  
  
 スケジューラをシャットダウンするには、スケジューラ上のすべてのバッチが操作を完了し、終了される必要があります。 シャットダウンされたスケジューラは、オフラインとしてマークされ、新しいバッチがこのスケジューラにより処理されないようにします。  
  
 新しいスケジューラが追加または削除されても、ロック モニターやチェックポイント、システム タスク スレッド (DTC の処理)、シグナル プロセスなどの永続的なシステム タスクは、サーバーが稼働している間はスケジューラ上で継続して実行されます。 このような永続的なシステム タスクについては、動的な移行は行われません。 スケジューラ間でこれらのシステム タスクのプロセッサ負荷を再分散するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを再起動する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が永続的なシステム タスクに関連付けられているスケジューラをシャットダウンした場合、タスクはオフラインになったスケジューラ上で引き続き実行されます (移行はされません)。 このスケジューラは、変更された関係マスク内のプロセッサにバインドされているため、変更前に関係付けられていたプロセッサに負荷を分散させることはできません。 オフラインのスケジューラが増えたとしても、システムの負荷には目立った影響はありません。 負荷が大幅に増大した場合は、データベース サーバーを再起動して、これらのタスクを再構成する必要があります。  
  
 I/O 関係タスク (レイジーライターやログライターなど) は、直接 I/O 関係マスクの影響を受けます。 レイジーライターおよびログライター タスクは、関係が設定されていなければ、ロック モニターやチェックポイントなど他の永続タスクに定義されているものと同じルールに従います。  
  
 新しい関係マスクを確実に有効にするために、RECONFIGURE コマンドでは、通常の CPU 関係および I/O 関係が相互に排他的であるかどうかの確認を行います。 相互に排他的でない場合は、そのような設定は推奨されないことを示すエラー メッセージがクライアント セッションと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに報告されます。 RECONFIGURE WITH OVERRIDE を実行すると、相互に排他的ではない CPU 関係および I/O 関係が許可されます。  
  
 存在しない CPU にマップしているような関係マスクを指定した場合、RECONFIGURE コマンドによりクライアント セッションと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログの両方にエラー メッセージが報告されます。 この場合、RECONFIGURE WITH OVERRIDE オプションを使用しても影響がなく、同じ構成エラーが再度報告されます。  
  
 Windows&#xA0;2000 または Windows&#xA0;Server&#xA0;2003 オペレーティング システムにより特定のワークロード割り当てが割り当てられているプロセッサから、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の動作を除外することもできます。 プロセッサを表すビットを 1 に設定している場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンは、このプロセッサをスレッド割り当ての対象として選択します。 **affinity mask** を 0 (既定値) に設定すると、Microsoft Windows 2000 または Windows Server 2003 のスケジューリング アルゴリズムにより、スレッドの関係 (affinity) が設定されます。 **affinity mask** を 0 以外の値に設定すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の関係 (affinity) により、選択可能なプロセッサを指定するビット マスクとしてその値が解釈されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スレッドを特定のプロセッサ上の実行から隔離すると、Microsoft Windows&#xA0;2000 または Windows&#xA0;Server&#xA0;2003 では、システムによる Windows 固有のプロセス処理を評価しやすくなります。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを 2 つ (インスタンス A および B) を実行する 8 CPU サーバーで、システム管理者は affinity mask オプションを使用して最初の 4 個の CPU をインスタンス A に割り当て、残りの 4 個をインスタンス B に割り当てることができます。33 プロセッサ以上を構成する場合は、affinity mask および affinity64 mask の両方を設定します。 **affinity mask** の値は、以下のとおりです。  
  
-   1 バイトの **affinity mask** は、マルチプロセッサ コンピューターの最大 8 個の CPU に対応します。  
  
-   2 バイトの **affinity mask** は、マルチプロセッサ コンピューターの最大 16 個の CPU に対応します。  
  
-   3 バイトの **affinity mask** は、マルチプロセッサ コンピューターの最大 24 個の CPU に対応します。  
  
-   4 バイトの **affinity mask** は、マルチプロセッサ コンピューターの最大 32 個の CPU に対応します。  
  
-   33 個以上の CPU に対応するには、最初の 32 個の CPU に 4 バイトの affinity mask を構成し、残りの CPU に 4 バイトの affinity64 mask を構成します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセッサ関係を設定することは特別な操作なので、特に必要な場合にのみこのオプションを使用することをお勧めします。 通常は、Microsoft Windows&#xA0;20000 または Windows&#xA0;Server&#xA0;2003 の既定の関係 (affinity) で、最適なパフォーマンスが得られます。 また、関係マスクを設定する場合は、他のアプリケーションの CPU 要件も考慮する必要があります。 詳細については、Windows オペレーティング システムのマニュアルを参照してください。  
  
> [!NOTE]  
>  各プロセッサの利用状況を表示して分析するには、Windows のシステム モニターを使用します。  
  
 affinity I/O mask オプションを指定する場合は、affinity mask 構成オプションの設定を考慮して使用する必要があります。 **affinity I/O mask** スイッチと affinity mask オプションの両方で同じ CPU を有効にしないようにしてください。 各 CPU に対応するビットは、次の 3 つの状態のうちのいずれかに設定します。  
  
-   affinity mask オプションと affinity I/O mask オプションの両方で 0。  
  
-   affinity mask オプションでは 1、affinity I/O mask オプションでは 0。  
  
-   affinity mask オプションでは 0、affinity I/O mask オプションでは 1。  
  
> [!CAUTION]  
>  Windows オペレーティング システムでの CPU 関係の構成と、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]での関係マスクの構成は、同時に行わないようにしてください。 この 2 つの設定は、同じ効果をねらったものであり、これらの構成間に一貫性がない場合は、予期しない結果を招く可能性があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CPU 関係を構成する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の sp_configure オプションを使用する方法が最適です。  
  
## <a name="example"></a>例  
 affinity mask オプションの設定例として、たとえば、ビット 1、2、および 5 を 1 に設定し、ビット 0、3、4、6、および 7 を 0 に設定して、プロセッサ 1、2、および 5 を使用可能として選択する場合は、16 進値 0x26 または 10 進値 `38` を指定します。 ビットの番号は右から左に数えます。 affinity mask オプションは、プロセッサを 0 から 31 までカウントします。したがって、次の例のカウンターの `1` は、サーバー上の 2 個目のプロセッサを表しています。  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'affinity mask', 38;  
RECONFIGURE;  
GO  
```  
  
 8 CPU システムでの **affinity mask** の値は以下のようになります。  
  
|10 進値|2 進ビット マスク|SQL Server スレッドを有効にするプロセッサ|  
|-------------------|---------------------|--------------------------------------------|  
|1|00000001|0|  
|3|00000011|0 と 1|  
|7|00000111|0、1、および 2|  
|15|00001111|0、1、2、および 3|  
|31|00011111|0、1、2、3、および 4|  
|63|00111111|0、1、2、3、4、および 5|  
|127|01111111|0、1、2、3、4、5、および 6|  
|255|11111111|0、1、2、3、4、5、6、および 7|  
  
 affinity mask オプションは拡張オプションです。 sp_configure システム ストアド プロシージャを使用して **affinity mask** の設定を変更するには、 **show advanced options** を 1 に設定する必要があります。 [!INCLUDE[tsql](../../includes/tsql-md.md)] の RECONFIGURE コマンドの実行が完了すると、新しい設定は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを再起動しなくてもすぐに有効になります。  
  
## <a name="non-uniform-memory-access-numa"></a>NUMA (Non-uniform Memory Access)  
 NUMA (non-uniform memory access) ベースのハードウェアを使用し、affinity mask を設定する場合、ノード内のすべてのスケジューラがそのノードの CPU に関連付けられます。 affinity mask を設定しない場合、各スケジューラは NUMA ノード内の CPU のグループに関連付けられ、NUMA ノード N1 にマップされたスケジューラはノード内の任意の CPU で作業をスケジュールできますが、他のノードに関連付けられた CPU ではスケジュールできません。  
  
 1 つの NUMA ノードで実行中のすべての操作は、そのノードのバッファー ページのみを使用できます。 操作を複数のノードの CPU で並行して実行する場合、メモリは関連する任意のノードから使用できます。  
  
## <a name="licensing-issues"></a>ライセンスに関する問題点  
 動的関係は、CPU ライセンスにより厳密に制限されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ライセンス ポリシーに違反する関係マスク オプションの構成が許可されていません。  
  
### <a name="startup"></a>起動時  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時またはデータベースのアタッチ時に、指定された関係マスクがライセンス ポリシーに違反する場合、エンジン層により起動処理や、データベースのアタッチおよび復元操作は完了されますが、その後、関係マスクの sp_configure 実行値が 0 にリセットされ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログにエラー メッセージが記録されます。  
  
### <a name="reconfigure"></a>再構成時  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] の RECONFIGURE コマンドの実行時に、指定された関係マスクがライセンス ポリシーに違反する場合は、エラー メッセージがクライアント セッションと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログに報告されます。データベース管理者による関係マスクの再構成作業が必要になります。 この場合、RECONFIGURE WITH OVERRIDE コマンドの実行が許可されません。  
  
## <a name="see-also"></a>参照  
 [リソースの利用状況の監視 &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)  
  
  
