---
title: メモリ最適化テーブルを使用するための要件 | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2a8830fbf4b9418f80cf07c7586e71689001d455
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68109615"
---
# <a name="requirements-for-using-memory-optimized-tables"></a>メモリ最適化テーブルを使用するための要件
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Azure DB でのインメモリ OLTP の使用については、「 [SQL Database でのインメモリ (プレビュー) の使用](https://azure.microsoft.com/documentation/articles/sql-database-in-memory/)」を参照してください。  
  
 インメモリ OLTP を使用する場合、「[SQL Server のインストールに必要なハードウェアおよびソフトウェア](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)」に加え、以下も要件です。  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 (以降) のあらゆるエディション。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] と [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] RTM (SP1 前) の場合、Enterprise、Developer、または Evaluation エディションが必要です。
    
    > [!NOTE]
    > インメモリ OLTP には、64 ビット版の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が必要です。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には、メモリ最適化テーブルおよびインデックス内にデータを保持するために十分なメモリが必要です。また、オンライン ワークロードに対応するには、追加のメモリが必要です。 詳細については、「 [メモリ最適化テーブルのメモリ必要量の推定](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) 」を参照してください。  

-   仮想マシン (VM) で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行する場合、メモリ最適化テーブルとインデックスに必要なメモリに対応できるように、VM に十分なメモリを割り当てる必要があります。 VM ホスト アプリケーションによっては、VM のメモリ割り当てを保証する構成オプションはメモリ予約と呼ばれます。動的メモリを使用する場合は、最小 RAM と呼ばれます。 これらの設定が、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のデータベースのニーズを十分に満たしていることを確認します。
  
-   持続性メモリ最適化テーブルの 2 倍のサイズの空きディスク領域。  
  
-   インメモリ OLTP を使用するための **cmpxchg16b** 命令をサポートするプロセッサ。 最新のすべての 64 ビット プロセッサでは **cmpxchg16b**がサポートされています。  
  
     仮想マシンを使用していて、古いプロセッサが原因のエラーが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって表示される場合は、VM ホスト アプリケーションに **cmpxchg16b**を許可する構成オプションがあるかどうかをご確認ください。 該当する構成オプションがない場合は、Hyper-V を使用できます。Hyper-V では、構成オプションを変更することなく **cmpxchg16b** がサポートされています。  
  
-   インメモリ OLTP は **データベース エンジン サービス**の一部としてインストールされます。  
  
     レポートの生成 (「[テーブルまたはストアド プロシージャをインメモリ OLTP に移植する必要があるかどうかの確認](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)」) と [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] オブジェクト エクスプローラーでインメモリ OLTP を管理する場合) をインストールするには、[SQL Server Management Studio (SSMS) をダウンロード](../../ssms/download-sql-server-management-studio-ssms.md)します。   
  
## <a name="important-notes-on-using-includehek2includeshek-2-mdmd"></a>[!INCLUDE[hek_2](../../includes/hek-2-md.md)] の使用に関する重要な注意事項  
  
-   [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降、メモリ最適化テーブルのサイズには空きメモリのサイズ以外の制限がありません。 

-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] では、データベース内の持続性のあるすべてのテーブルのメモリ内サイズの合計は 250 GB を超えないようにする必要があります。 詳細については、「 [メモリ最適化テーブルのメモリ必要量の推定](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)」を参照してください。  

> [!NOTE]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 より、Standard エディションと Express エディションではインメモリ OLTP がサポートされていますが、所与のデータベースでメモリ最適化テーブルに利用できるメモリ量にクォータが課せられます。 Standard エディションの場合、これはデータベースごとに 32GB です。Express エディションの場合、データベースごとに 352MB です。 
  
-   メモリ最適化テーブルが含まれるデータベースを 1 つ以上作成する場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス開始アカウントに *SE_MANAGE_VOLUME_NAME* ユーザー権を与え、ファイルの瞬時初期化 (IFI) を有効にしてください。 IFI なしの場合、メモリ最適化ストレージ ファイル (データ ファイルとデルタ ファイル) が作成時に初期化されるため、ワークロードのパフォーマンスが低下する場合があります。 有効化方法など、IFI に関する詳細については、「[データベースのファイルの瞬時初期化](../../relational-databases/databases/database-instant-file-initialization.md)」を参照してください。
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP &#40;インメモリ最適化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
 [データベースのファイルの瞬時初期化](../../relational-databases/databases/database-instant-file-initialization.md)  
 [メモリ アーキテクチャ ガイド](../../relational-databases/memory-management-architecture-guide.md)
  
