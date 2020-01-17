---
title: ソフト NUMA (SQL Server) を使用する SQL Server の構成 |Microsoft Docs
ms.custom: ''
ms.date: 07/12/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- NUMA
- non-uniform memory access
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6ad0e30c0db83daf7e0cae4f7353d1f0a96a96d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62809040"
---
# <a name="configure-sql-server-to-use-soft-numa-sql-server"></a>ソフト NUMA を使用するように SQL Server を構成する方法 (SQL Server)
最新のプロセッサでは、1 つのソケットに対して複数のコアが与えられます。 各ソケットは、通常、1 つの NUMA ノードとして表示されます。 SQL Server データベース エンジンは、さまざまな内部構造を分割し、NUMA ノード単位でサービス スレッドを分割します。 1 ソケットにつき 10 個以上のコアを含む、ソフトウェアを使用するプロセッサを搭載したは、一般にハードウェア NUMA ノードに分割する NUMA (ソフト NUMA) は、スケーラビリティとパフォーマンスが向上します。   

> [!NOTE]
> ホット アド プロセッサは、ソフト NUMA ではサポートされていません。
  
## <a name="automatic-soft-numa"></a>自動ソフト NUMA
SQL Server 2014 Service Pack 2 以降、データベース エンジン サーバーが起動時に 8 個を超えるの物理プロセッサを検出するたびに、ソフト NUMA ノードは自動的に作成、スタートアップ パラメーターとしてトレース フラグ 8079 が有効になっている場合。 物理プロセッサを数えるときに、ハイパー スレッド プロセッサ コアはの考慮されません。 検出された物理プロセッサの数がソケットあたり 8 個を超えると、データベース エンジン サービスは 8 コア、含めることが理想的ですが、ノードあたり 5 個、最大 9 個の論理プロセッサがダウンするソフト NUMA ノードを作成します。 ハードウェア ノードのサイズは CPU 関係マスクにより制限されます。 NUMA ノードの数がサポートされる NUMA ノードの最大数を超えることはありません。

トレース フラグを設定しないソフト NUMA は既定で無効になります。 ソフト NUMA を有効にできるトレース フラグ 8079 を使用します。 この設定の値を変更した場合、その変更を適用するには、データベース エンジンを再起動する必要があります。

次の図は、SQL Server を 8 個の論理プロセッサを超えるハードウェア NUMA ノードを検出したときと、トレース フラグ 8079 が有効になっている場合、SQL Server エラー ログに表示されるソフト NUMA に関する情報の種類を示します。

![ssNoVersion](./media/soft-numa-sql-server/soft-numa.PNG)

> [!NOTE]
> この動作は、エンジンとトレース フラグ 8079 によって制御される SQL Server 2016 以降も効果はありません。

## <a name="manual-soft-numa"></a>手動ソフト NUMA
  
構成する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ソフト NUMA を手動で使用する場合は、ノード構成関係マスクを追加するレジストリを編集する必要があります。 ソフト NUMA マスクは、バイナリ、DWORD (16 進数または 10 進数)、または QWORD (16 進数または 10 進数) のレジストリ エントリとして記述できます。 最初の 32 個を超える CPU を構成するには、QWORD またはバイナリのレジストリ値を使用します ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以前では QWORD 値を使用できません。)再起動する必要があります、[!INCLUDE[ssDE](../../includes/ssde-md.md)]ソフト NUMA を構成します。  
  
> [!TIP]  
>  CPU には、0 から始まる番号が付けられます。  
  
 [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 次の例を考えてみましょう。 この 8 個の CPU が搭載されたコンピューターには、ハードウェア NUMA がありません。 3 つのソフト NUMA ノードが構成されています。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンス A は、CPU 0 から 3 を使用するように構成されています。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の 2 つ目のインスタンスがインストールされており、CPU 4 から 7 を使用するように構成されています。 この例は、次のように視覚的に表されます。  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 多くの I/O が発生するインスタンス A には、2 つの I/O スレッドと 1 つのレイジー ライター スレッドが存在するようになります。一方、プロセッサに負荷が集中する操作を実行するインスタンス B には、1 つの I/O スレッドと 1 つのレイジー ライター スレッドしかありません。 異なる量のメモリをこれらのインスタンスに割り当てることができますが、ハードウェア NUMA とは異なり、どちらもオペレーティング システムの同じメモリ ブロックからメモリを受け取るのでメモリおよびプロセッサ間の関係はありません。  
  
 レイジー ライター スレッドは、物理 NUMA メモリ ノードの SQL OS のビューに関連付けられています。 したがって、ハードウェアが物理 NUMA ノードとして表すものは、作成されるレイジー ライター スレッドの数と一致します。 詳細については、「[How It Works:Soft NUMA, I/O Completion Thread, Lazy Writer Workers and Memory Nodes](https://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx)」 (動作方法: ソフト NUMA、I/O 完了スレッド、レイジー ライター ワーカー、およびメモリ ノード) を参照してください。  
  
> [!NOTE]  
>  **のインスタンスをアップグレードするときに** ソフト NUMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]レジストリ キーはコピーされません。  
  
### <a name="set-the-cpu-affinity-mask"></a>CPU affinity mask の設定  
  
1.  インスタンス A で次のステートメントを実行し、CPU affinity mask を設定して CPU 0、1、2、および 3 を使用するように構成します。  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=0 TO 3;  
    ```  
  
2.  インスタンス B で次のステートメントを実行し、CPU affinity mask を設定して CPU 4、5、6、および 7 を使用するように構成します。  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=4 TO 7;  
    ```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>CPU へのソフト NUMA ノードのマッピング  
  
-   レジストリ エディター プログラム (regedit.exe) を使用して、次のレジストリ キーを追加し、ソフト NUMA ノード 0 を CPU 0 および 1 に、ソフト NUMA ノード 1 を CPU 2 および 3 に、ソフト NUMA ノード 2 を CPU 4、 5、6、および 7 にマッピングします。  
  
     次の例では、1 ソケットにつき 18 個のコア (4 ソケットを装備) を備え、各ソケットがそれぞれ独自の K グループに属する DL580 G9 サーバーを使用するとします。 次のようなソフト NUMA の構成を作成できます。 (ノードごとに 6 コア、グループごとに 3 ノード、4 グループ)。  
  
    |複数の K グループを持つ [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] サーバーの例|型|値の名前|値データ|  
    |------------------------------------------------------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|グループ化|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|グループ化|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|グループ化|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|グループ化|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|グループ化|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|グループ化|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|グループ化|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|グループ化|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|グループ化|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|グループ化|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|グループ化|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|グループ化|3|  
  
     その他の例:  
  
    |[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|型|値の名前|値データ|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|グループ化|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|グループ化|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|グループ化|0|  
  
    > [!TIP]  
    >  CPU 60 ～ 63 を指定するには、QWORD 値 F000000000000000 またはバイナリ値 1111000000000000000000000000000000000000000000000000000000000000 を使用します。  
  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|型|値の名前|値データ|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|グループ化|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|グループ化|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|グループ化|0|  
  
    |SQL Server 2008 R2|型|値の名前|値データ|  
    |------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|グループ化|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|グループ化|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|グループ化|0|  
  
    |SQL Server 2008|型|値の名前|値データ|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
    |SQL Server 2005|型|値の名前|値データ|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
## <a name="see-also"></a>関連項目  
 [NUMA ノードへの TCP/IP ポートのマッピング &#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)   
 [affinity mask サーバー構成オプション](affinity-mask-server-configuration-option.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
