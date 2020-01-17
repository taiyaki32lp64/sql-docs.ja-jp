---
title: メモリ使用率の監視 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- tuning databases [SQL Server], memory
- monitoring server performance [SQL Server], memory usage
- isolating memory [SQL Server]
- paging rate [SQL Server]
- memory [SQL Server], monitoring usage
- monitoring [SQL Server], memory usage
- low-memory conditions
- database monitoring [SQL Server], memory usage
- available memory [SQL Server]
- page faults [SQL Server]
- monitoring performance [SQL Server], memory usage
- server performance [SQL Server], memory
ms.assetid: 1aee3933-a11c-4b87-91b7-32f5ea38c87f
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: b7ec7d6142bae4a6a0ad21a7f68413b257764e06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091007"
---
# <a name="monitor-memory-usage"></a>メモリ使用率の監視
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを定期的に監視し、メモリ使用率が通常の範囲内であることを確認します。  
  
 メモリの少ない状況を監視するには、次のオブジェクト カウンターを使用します。  
  
-   **Memory:Available Bytes**  
  
-   **Memory:Pages/sec**  
  
 **Available Bytes** カウンターは、プロセスで現在使用できるメモリのバイト数を示します。 **Pages/sec** カウンターは、ハード ページ フォールトのためにディスクから取り出されたページ数や、ページ フォールトによって作業セット内の領域を解放するためにディスクに書き込まれたページ数を示します。  
  
 **Available Bytes** カウンターの値が低い場合、コンピューターのメモリが全体的に不足しているか、アプリケーションがメモリを解放していないことが考えられます。 **Pages/sec** カウンターの値が高い場合、ページングが過剰であることが考えられます。 ディスク利用状況がページングによるものかどうかを確認するには、**Memory:Page Faults/sec** カウンターを監視します。  
  
 コンピューターに十分なメモリがある場合でも、ページングとページ フォールトが低い率で発生することは問題ではありません。 Microsoft Windows Virtual Memory Manager (VMM) では、プロセスの作業セットのサイズを小さくするときに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と他のプロセスからページを取得します。 この VMM の動作が、ページ フォールトの原因になる場合があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または他のプロセスが過剰なページングの原因であるかどうかを判断するには、**Process:Page Faults/sec** カウンター ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセス インスタンス) を監視します。  
  
 過剰なページングの解決方法の詳細については、Windows オペレーティング システムのマニュアルを参照してください。  
  
## <a name="isolating-memory-used-by-sql-server"></a>SQL Server が使用するメモリの分離  
 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は使用可能なシステム リソースに基づいて、必要なメモリを動的に変更します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により多くのメモリが必要な場合は、空き物理メモリが使用可能かどうかを調べるためにオペレーティング システムに問い合わせ、使用可能なメモリを使用します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、現在割り当てられているメモリが必要ない場合は、そのメモリをオペレーティング システムに対して解放します。 ただし、**minservermemory** および **maxservermemory** サーバー構成オプションを使用して、オプションをオーバーライドしてメモリを動的に使用できます。 詳細については、「 [サーバー メモリ オプション](../../database-engine/configure-windows/server-memory-server-configuration-options.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用されるメモリの量を監視するには、次のパフォーマンス カウンターを調べます。  
  
-   **Process:Working Set**  
  
-   **SQL Server:Buffer Manager:Buffer Cache Hit Ratio**  
  
-   **SQL Server:Buffer Manager:Database Pages**  
  
-   **SQL Server:Memory Manager:Total Server Memory (KB)**  
  
 **WorkingSet** カウンターは、プロセスが使用しているメモリの量を示します。 この数値が **min server memory** および **max server memory** サーバー オプションで設定したメモリの量を常に下回っている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は過剰なメモリを使用するように構成されています。  
  
 **Buffer Cache Hit Ratio** カウンターは、アプリケーション固有のカウンターです。 適切な値は 90% 以上です。 値が常に 90% より大きくなるまで、メモリを追加してください。 90% より大きい値は、90% を超えるデータ要求がデータ キャッシュで処理できたことを示しています。  
  
 **TotalServerMemory (KB)** カウンターがコンピューターの物理メモリ容量に比べて常に高い場合、より多くのメモリが必要であることを示しています。  
  
## <a name="determining-current-memory-allocation"></a>現在のメモリ割り当ての特定  
 次のクエリでは、現在割り当てられているメモリに関する情報を返します。  
  
```  
SELECT  
(physical_memory_in_use_kb/1024) AS Memory_usedby_Sqlserver_MB,  
(locked_page_allocations_kb/1024) AS Locked_pages_used_Sqlserver_MB,  
(total_virtual_address_space_kb/1024) AS Total_VAS_in_MB,  
process_physical_memory_low,  
process_virtual_memory_low  
FROM sys.dm_os_process_memory;  
```  
  
  
