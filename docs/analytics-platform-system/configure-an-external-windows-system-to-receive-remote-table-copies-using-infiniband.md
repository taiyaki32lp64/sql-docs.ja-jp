---
title: リモートテーブルコピーを受信するように Windows を構成する
description: 並列データウェアハウスのリモートテーブルコピー機能で使用するために、InfiniBand ネットワークを使用して接続されているアプライアンス以外の Windows システムを購入して構成する方法について説明します。 Windows システムは、SQL Server PDW データベースからリモートテーブルのコピーを受信する SQL Server データベースをホストします。 アプライアンスとは別に購入し、アプライアンス InfiniBand ネットワークに接続します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 837d41cc929d90b2494682645127f985b5768546
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401314"
---
# <a name="configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband---parallel-data-warehouse"></a>InfiniBand-Parallel Data Warehouse を使用してリモートテーブルコピーを受信するように外部 Windows システムを構成する
SQL Server PDW のリモートテーブルコピー機能で使用するために、InfiniBand ネットワークを使用して接続されているアプライアンス以外の Windows システムを購入して構成する方法について説明します。 Windows システムは、SQL Server PDW データベースからリモートテーブルのコピーを受信する SQL Server データベースをホストします。 アプライアンスとは別に購入し、アプライアンス InfiniBand ネットワークに接続します。  
  
> [!NOTE]  
> リモートテーブルコピーを使用する場合、InfiniBand ネットワーク経由の接続は必要ありません。 イーサネットネットワーク経由の接続は、イーサネット帯域幅がニーズに合っている場合に行うことができます。  
  
このトピックでは、リモートテーブルのコピーを構成するための構成手順の1つについて説明します。 すべての構成手順の一覧については、「[リモートテーブルのコピー](remote-table-copy.md) 」を参照してください。  
  
## <a name="before-you-begin"></a>開始する前に  
外部 Windows システムを構成する前に、次のことを行う必要があります。  
  
1.  リモートコピーを受信する Windows システムを購入または提供します。  
  
2.  コントロールラックの Windows システムをラックに設置します (十分な領域がある場合)。または、アプライアンスに十分に近づけて、アプライアンス InfiniBand ネットワークに接続できるようにします。  
  
3.  InfiniBand ケーブルと InfiniBand ネットワークアダプターを、アプライアンスハードウェアベンダーから購入します。 エクスポートされたデータを受信する場合は、フォールトトレランスのために2つのポートを持つネットワークアダプターを購入することをお勧めします。 2つのポートネットワークアダプターをお勧めしますが、これは必須ではありません。  
  
## <a name="HowToWindows"></a>リモートテーブルコピーを受信するように外部 Windows システムを構成する  
外部 Windows システムを構成するには、次の手順に従います。  
  
1.  Windows システムに InfiniBand ネットワークアダプターをインストールします。  
  
2.  InfiniBand ケーブルを使用して、InfiniBand ネットワークアダプターを、コントロールラックのメイン InfiniBand スイッチに接続します。  
  
3.  InfiniBand ネットワークアダプター用の適切な Windows ドライバーをインストールして構成します。  
  
    InfiniBand drivers for Windows は、InfiniBand ベンダーの業界コンソーシアムである OpenFabrics アライアンスによって開発されています。  正しいドライバーが InfiniBand アダプターと共に配布されている可能性があります。 それ以外の場合は、www.openfabrics.org からドライバーをダウンロードできます。  
  
4.  アダプターのポートごとに IP アドレスを構成します。 SMP システムでは、この目的のために予約されているアドレス範囲の静的 IP アドレスを使用する必要があります。 次のパラメーターに従って、最初のポートを構成します。  
  
    -   IP ネットワークアドレス: 172.16.132  
  
    -   IP サブネットマスク: 255.255.128.0  
  
    -   IP ホストの範囲: 1-254  
  
    2つのポートを持つ InfiniBand ネットワークアダプターについては、次のパラメーターに従って2番目のポートを構成します。  
  
    -   IP ネットワークアドレス: 172.16.132  
  
    -   IP サブネットマスク: 255.255.128.0  
  
    -   IP ホストの範囲: 1-254  
  
5.  2つのポートアダプターが使用されている場合、または複数の外部 Windows システムがアプライアンスに接続されている場合は、各システムにそれぞれの IP サブネット内の異なるホスト番号を割り当てます。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
