---
title: ソフト NUMA (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- NUMA
- soft-NUMA
helpviewer_keywords:
- NUMA
- non-uniform memory access
- soft-NUMA
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 68232821ac186aa63d113319373b8326dae987a4
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165177"
---
# <a name="soft-numa-sql-server"></a>ソフト NUMA (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

最新のプロセッサには、1 つのソケットに対して複数のコアがあります。 各ソケットは、通常、1 つの NUMA ノードとして表示されます。 SQL Server データベース エンジンは、さまざまな内部構造を分割し、NUMA ノード単位でサービス スレッドを分割します。  1 つのソケットに対してコアを 10 個以上含むプロセッサの場合、ソフトウェア NUMA を使用してハードウェア NUMA ノードを分割すると、一般的に、拡張性と性能が向上します。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 より前の場合、ソフトウェア ベースの NUMA (ソフト NUMA) ではレジストリを編集し、ノード構成関係マスクを追加する必要がありました。また、ソフト NUMA は、インスタンス単位ではなく、ホスト レベルで構成されていました。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 および [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、ソフト NUMA は、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] サービスの起動時にデータベース/インスタンス レベルで自動的に構成されます。  
  
> [!NOTE]  
> ホット アド プロセッサは、ソフト NUMA ではサポートされていません。  
  
## <a name="automatic-soft-numa"></a>自動ソフト NUMA  
[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] では、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]が起動時に NUMA ノードまたはソケットあたり 8 個を超える物理コアを検出するたびに、ソフト NUMA ノードが既定で自動的に作成されます。 ハイパースレッドのプロセッサ コアは、ノードの物理プロセッサを数えるときに区別されません。  物理コアの検出数がソケットあたり 8 個を超えると、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] でソフト NUMA ノードが作成されます。その場合、8 個のコアが含まれていることが理想的ですが、ノードあたり 5 個から 9 個の論理コアを含めることができます。 ハードウェア ノードのサイズは CPU 関係マスクにより制限されます。 NUMA ノードの数がサポートされる NUMA ノードの最大数を超えることはありません。  
  
[ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) ステートメントと `SET SOFTNUMA` 引数を使用し、ソフト NUMA を無効化したり、再有効化したりすることができます。 この設定の値を変更した場合、その変更を適用するには、データベース エンジンを再起動する必要があります。  
  
下の図は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、ノードまたはソケットあたり 8 個を超える物理コアが含まれるハードウェア NUMA ノードが検出されたときに SQL Server エラー ログに表示される、ソフト NUMA に関する情報の種類を示しています。  


```
2016-11-14 13:39:43.17 Server      SQL Server detected 2 sockets with 12 cores per socket and 24 logical processors per socket, 48 total logical processors; using 48 logical processors based on SQL Server licensing. This is an informational message; no user action is required.     
2016-11-14 13:39:43.35 Server      Automatic soft-NUMA was enabled because SQL Server has detected hardware NUMA nodes with greater than 8 physical cores.     
2016-11-14 13:39:43.63 Server      Node configuration: node 0: CPU mask: 0x0000000000555555:0 Active CPU mask: 0x0000000000555555:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.    
2016-11-14 13:39:43.63 Server      Node configuration: node 1: CPU mask: 0x0000000000aaaaaa:0 Active CPU mask: 0x0000000000aaaaaa:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.    
2016-11-14 13:39:43.63 Server      Node configuration: node 2: CPU mask: 0x0000555555000000:0 Active CPU mask: 0x0000555555000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.     
2016-11-14 13:39:43.63 Server      Node configuration: node 3: CPU mask: 0x0000aaaaaa000000:0 Active CPU mask: 0x0000aaaaaa000000:0. This message provides a description of the NUMA configuration for this computer. This is an informational message only. No user action is required.   
```   

> [!NOTE]
> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 以降では、トレース フラグ 8079 を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が自動ソフト NUMA を使用できるようにします。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降では、この動作はエンジンによって制御されるようになり、トレース フラグ 8079 に効力はありません。 詳細については、「[DBCC TRACEON - トレース フラグ](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)」を参照してください。

## <a name="manual-soft-numa"></a>手動ソフト NUMA  
ソフト NUMA を使用できるように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を手動で構成するには、自動のソフト NUMA を無効化し、レジストリを編集してノード構成関係マスクを追加します。 この方法を利用すると、ソフト NUMA マスクは、バイナリ、DWORD (16 進数または 10 進数)、または QWORD (16 進数または 10 進数) のレジストリ エントリとして記述できます。 最初の 32 個を超える CPU を構成するには、QWORD またはバイナリのレジストリ値を使用します ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] より前では QWORD 値を使用できません)。 レジストリの変更後、ソフト NUMA 構成を適用するには [!INCLUDE[ssDE](../../includes/ssde-md.md)] を再起動する必要があります。  
  
> [!TIP]
> CPU には、0 から始まる番号が付けられます。  

> [!WARNING]
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
たとえば、8 個の CPU が搭載されたコンピューターにハードウェア NUMA がないとします。 3 つのソフト NUMA ノードが構成されています。   
[!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンス A は、CPU 0 から 3 を使用するように構成されています。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の 2 つ目のインスタンスがインストールされており、CPU 4 から 7 を使用するように構成されています。 この例は、次のように視覚的に表されます。  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 多くの I/O が発生するインスタンス A には、現在、2 つの I/O スレッドと 1 つのレイジー ライター スレッドがあります。 プロセッサに負荷が集中する操作を実行するインスタンス B には、1 つの I/O スレッドと 1 つのレイジー ライター スレッドしかありません。 異なる量のメモリをこれらのインスタンスに割り当てることができますが、ハードウェア NUMA とは異なり、どちらもオペレーティング システムの同じメモリ ブロックからメモリを受け取るのでメモリおよびプロセッサ間の関係はありません。  
  
 レイジー ライター スレッドは、物理 NUMA メモリ ノードの SQLOS ビューに関連付けられています。 したがって、ハードウェアが物理 NUMA ノード数として表すものは、作成されるレイジー ライター スレッドの数になります。 詳細については、「[How It Works:Soft NUMA, I/O Completion Thread, Lazy Writer Workers and Memory Nodes](https://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx)」 (動作方法: ソフト NUMA、I/O 完了スレッド、レイジー ライター ワーカー、およびメモリ ノード) を参照してください。  
  
> [!NOTE]
> **のインスタンスをアップグレードするときに** ソフト NUMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]レジストリ キーはコピーされません。  
  
### <a name="set-the-cpu-affinity-mask"></a>CPU affinity mask の設定  
 インスタンス A で次のステートメントを実行し、CPU affinity mask を設定して CPU 0、1、2、および 3 を使用するように構成します。  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=0 TO 3;  
```  
  
インスタンス B で次のステートメントを実行し、CPU affinity mask を設定して CPU 4、5、6、および 7 を使用するように構成します。  
  
```sql  
ALTER SERVER CONFIGURATION   
SET PROCESS AFFINITY CPU=4 TO 7;  
```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>CPU へのソフト NUMA ノードのマッピング  
 レジストリ エディター プログラム (regedit.exe) を使用して、次のレジストリ キーを追加し、ソフト NUMA ノード 0 を CPU 0 および 1 に、ソフト NUMA ノード 1 を CPU 2 および 3 に、ソフト NUMA ノード 2 を CPU 4、5、6、および 7 にマッピングします。  
  
> [!TIP]
> CPU 60 ～ 63 を指定するには、QWORD 値 F000000000000000 またはバイナリ値 1111000000000000000000000000000000000000000000000000000000000000 を使用します。  
  
 次の例では、1 ソケットにつき 18 個のコア (4 ソケットを装備) を備え、各ソケットがそれぞれ独自の K グループに属する DL580 G9 サーバーを使用するとします。 作成する可能性のあるソフト NUMA 構成は、ノードごとに 6 コア、グループごとに 3 ノード、および 4 グループのようになります。  
  
|複数の K グループを持つ [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] サーバーの例|種類|値の名前|値データ|  
|-----------------------------------------------------------------------------------------------------------------|----------|----------------|----------------|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node0|DWORD|Group|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node1|DWORD|Group|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node2|DWORD|Group|0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node3|DWORD|Group|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node4|DWORD|Group|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node5|DWORD|Group|1|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node6|DWORD|Group|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node7|DWORD|Group|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node8|DWORD|Group|2|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node9|DWORD|Group|3|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node10|DWORD|Group|3|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\NodeConfiguration\Node11|DWORD|Group|3|  
  
## <a name="metadata"></a>メタデータ  
 次の DMV を使用して、ソフト NUMA の現在の状態と構成を表示できます。  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md): SOFTNUMA の現在の値 (0 または 1) を表示します。  
  
-   [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md): *softnuma_configuration* 列と *softnuma_configuration_desc* 列には、現在の構成値が表示されます。  
  
> [!NOTE]
> [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) を利用することにより、自動ソフト NUMA の実行中の値を表示できますが、 **sp_configure** でその値を変更することはできません。 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md) ステートメントは `SET SOFTNUMA` 引数と共に使用する必要があります。  
  
## <a name="see-also"></a>参照  
[NUMA ノードへの TCP/IP ポートのマッピング &#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)    
[affinity mask サーバー構成オプション](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)    
[ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-configuration-transact-sql.md)     
[sys.dm_os_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-nodes-transact-sql.md)   
  
