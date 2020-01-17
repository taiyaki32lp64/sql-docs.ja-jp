---
title: ネットワーク プロトコルの選択 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
- Named Pipes [SQL Server]
- TCP [SQL Server]
- network protocols [SQL Server], choosing
- protocols [SQL Server], choosing
- NWLink IPX/SPX [SQL Server]
- client configuration [SQL Server], protocols
- VIA
- Multiprotocol Net-Library [SQL Server]
- IPX/SPX [SQL Server]
- Banyan VINES
- protocols [SQL Server], client configuration
ms.assetid: 6565fb7d-b076-4447-be90-e10d0dec359a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 9c167994c7145bce348b6959a57533e398e1d6bb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63035289"
---
# <a name="choosing-a-network-protocol"></a>ネットワーク プロトコルの選択
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]に接続するには、ネットワーク プロトコルを有効にする必要があります。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同時にいくつかのプロトコルで要求を処理することができます。 クライアントは、1 つのプロトコルを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がどのプロトコルでリッスンしているかをクライアント プログラムによって判別できない場合は、複数のプロトコルを順に試みるようにクライアントを構成してください。 ネットワーク プロトコルを有効化、無効化、または構成するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用します。  
  
## <a name="shared-memory"></a>共有メモリ  
 共有メモリは、使用できる最も単純なプロトコルであり、構成可能な設定はありません。 共有メモリ プロトコルを使用するクライアントは、同じコンピューター上で実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスにしか接続できないため、ほとんどのデータベース操作にとって実用的ではありません。 共有メモリ プロトコルは、他のプロトコルが正しく構成されていない可能性がある場合に、トラブルシューティングを行うために使用できます。  
  
> [!NOTE]  
>  MDAC 2.8 以前を使用しているクライアントでは、共有メモリ プロトコルを使用できません。 このようなクライアントで共有メモリ プロトコルの使用を試みた場合は、自動的に名前付きパイプ プロトコルに切り替わります。  
  
## <a name="tcpip"></a>TCP/IP  
 TCP/IP は、インターネットで広く使われている一般的なプロトコルです。 このプロトコルは、多様なハードウェア アーキテクチャやオペレーティング システムを備えたコンピューターが相互に接続されているネットワーク上の通信を実現します。 TCP/IP には、ネットワーク トラフィックをルーティングするための標準や、高度なセキュリティ機能も含まれています。 TCP/IP は、今日の業務で最も一般的に使用されているプロトコルです。 TCP/IP を使用するためにコンピューターを構成する作業は複雑になることもありますが、ほとんどのネットワーク コンピューターには適切な構成が既に適用されています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーで表示されない TCP/IP 設定を構成するには、[!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows のドキュメントを参照してください。  
  
## <a name="named-pipes"></a>名前付きパイプ  
 名前付きパイプは、ローカル エリア ネットワークのために開発されたプロトコルです。 このプロトコルでは、1 つのプロセスが、メモリの一部を使用して別のプロセスに情報を渡します。このとき、1 つ目のプロセスの出力が 2 つ目のプロセスの入力になります。 2 つ目のプロセスは、ローカル (1 つ目のプロセスと同じコンピューター上にある) またはリモート (ネットワーク コンピューター上にある) のどちらでもかまいません。  
  
## <a name="named-pipes-vs-tcpip-sockets"></a>名前付きパイプとします。TCP/IP ソケット  
 高速ローカル エリア ネットワーク (LAN) 環境の場合、TCP/IP ソケットを使用するクライアントと、名前付きパイプを使用するクライアントには、パフォーマンスの点でほとんど差はありません。 ただし、両者のパフォーマンスの違いは、ワイド エリア ネットワーク (WAN) やダイヤルアップ ネットワークなどの低速のネットワークの場合に明らかになります。 これは、プロセス間通信 (IPC) メカニズムによるピア間の通信方法が異なるためです。  
  
 名前付きパイプの場合、ネットワーク通信は通常、より対話的なものになります。 ピアは、別のピアから read コマンドによる要求があるまでデータを送信しません。 ネットワークでの読み取りでは通常、データの読み取りを開始する前に、一連の名前付きパイプ メッセージを処理する必要があります。 これらは低速のネットワークにとって大きなコストとなり、過剰なネットワーク トラフィックを引き起こすので、他のネットワーク クライアントに影響を及ぼします。  
  
 また、ローカル パイプとネットワーク パイプのどちらを指しているのかを区別することも重要です。 サーバー アプリケーションが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを実行しているコンピューター上でローカルに実行されている場合、ローカルの名前付きパイプ プロトコルを選択できます。 ローカルの名前付きパイプはカーネル モードで実行され、非常に高速です。  
  
 TCP/IP ソケットの場合、データ伝送はより効率的でオーバーヘッドも少なくて済みます。 また、データ伝送にウィンドウ化や遅延確認応答など、TCP/IP ソケットのパフォーマンス向上メカニズムを利用できます。 これは、低速ネットワークの場合に非常に役立ちます。 アプリケーションの種類によっては、このようなパフォーマンスの違いが大きく影響します。  
  
 TCP/IP ソケットは、バックログ キューもサポートしています。 名前付きパイプでは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への接続試行時にパイプがビジー状態になるエラーが生じる可能性があるので、それに比べると、接続をある程度スムーズにできる効果があります。  
  
 一般に、TCP/IP は低速の LAN、WAN、またはダイヤルアップ ネットワークに適しています。一方、ネットワークの速度に関する問題がない場合は、名前付きパイプの方が多くの機能を備えており、使いやすく、構成できるオプションも多いので適している可能性があります。  
  
## <a name="enabling-the-protocol"></a>プロトコルの有効化  
 プロトコルを使用するには、クライアントとサーバーの両方で有効にする必要があります。 サーバーは、有効なすべてのプロトコルで同時に要求をリッスンできます。 クライアントは、プロトコルを選択することも、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーの一覧の順でプロトコルを試すこともできます。  
  
 プロトコルを構成して [!INCLUDE[ssDE](../../includes/ssde-md.md)]に接続する方法に関する簡単なチュートリアルについては、「[チュートリアル:データベース エンジンの概要](../../relational-databases/tutorial-getting-started-with-the-database-engine.md)」を参照してください。  
  
  
