---
title: InfiniBand を構成する
description: 非アプライアンスクライアントサーバー上の InfiniBand ネットワークアダプターを構成して、並列データウェアハウス (PDW) のコントロールノードに接続する方法について説明します。 読み込み、バックアップ、およびその他のプロセスがアクティブな InfiniBand ネットワークに自動的に接続するように、基本的な接続と高可用性については、次の手順を使用します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 583d7617c0620d5d1ec24d60fbf10435a547616d
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401290"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>Analytics Platform System の InfiniBand ネットワークアダプターを構成する
非アプライアンスクライアントサーバー上の InfiniBand ネットワークアダプターを構成して、並列データウェアハウス (PDW) のコントロールノードに接続する方法について説明します。 読み込み、バックアップ、およびその他のプロセスがアクティブな InfiniBand ネットワークに自動的に接続するように、基本的な接続と高可用性については、次の手順を使用します。  
  
## <a name="Basics"></a>記述  
次の手順では、InfiniBand 接続サーバーで正しい InfiniBand IP アドレスとサブネットマスクを見つけて設定する方法について説明します。 また、接続がアクティブな InfiniBand ネットワークに解決されるように、APS アプライアンス DNS を使用するようにサーバーを設定する方法についても説明します。  
  
高可用性を実現するために、APS には2つの InfiniBand ネットワーク (アクティブとパッシブ) があります。 各 InfiniBand ネットワークには、制御ノードに対して異なる IP アドレスがあります。 Active InfiniBand ネットワークがダウンした場合、パッシブ InfiniBand ネットワークがアクティブなネットワークになります。 この場合、スクリプトまたはプロセスは、スクリプトのパラメーターを変更せずに、アクティブな InfiniBand ネットワークに自動的に接続します。  
  
具体的には、この記事の内容は次のとおりです。  
  
1.  APS DNS サーバー (appliance_domain-AD01 および appliance_domain *-AD02) の InfiniBand IP アドレスを検索します。 これを行うには、AD01 および AD02 サーバーにログインし、各 InfiniBand ネットワークの IP アドレスを取得します。 AD ノードの InfiniBand IP アドレスは、DNS IP アドレスです。  
  
2.  各ネットワークアダプターで、APS InfiniBand ネットワーク上の使用可能な IP アドレスを使用するように構成します。  
  
    1.  2つの InfiniBand ネットワークアダプターがある場合は、TeamIB1 という最初の InfiniBand ネットワークで使用可能な IP アドレスを使用して1つのアダプターを構成し、もう一方のアダプターには TeamIB2 という2番目の InfiniBand ネットワークで使用可能な IP アドレスを設定します。 優先 DNS サーバーとして appliance_domain-AD01 TeamIB1 IP アドレスを使用し、TeamIB1 ネットワークアダプターの代替 DNS サーバーとして appliance_domain-AD02 TeamIB1 IP アドレスを使用します。 優先 DNS サーバーとして appliance_domain-AD01 TeamIB2 IP アドレスを使用し、TeamIB2 ネットワークアダプターの代替 DNS サーバーとして appliance_domain-AD02 TeamIB2 IP アドレスを使用します。  
  
    2.  InfiniBand ネットワークアダプターが1つしかない場合は、いずれかの InfiniBand ネットワークから使用可能な IP アドレスを使用してアダプターを構成します。 次に、appliance_domain-AD01 TeamIB1 と appliance_domain-AD02 TeamIB1 を使用するか、または appliance_domain-AD01 TeamIB2 と appliance_domain-AD02 TeamIB2 のどちらかを使用して、このアダプターの優先 DNS サーバーと代替 DNS サーバーを構成します。優先 DNS サーバーおよび代替 DNS サーバーとして構成されたアダプターとしてネットワークを使用します。  
  
3.  APS DNS サーバーを使用して active InfiniBand ネットワークへの接続を解決するように、InfiniBand ネットワークアダプターを構成します。  
  
    1.  これを構成するには、TCP/IP の詳細設定を使用して、クライアントサーバーの DNS サフィックスの一覧の先頭にアプライアンスドメインの DNS サフィックスを追加します。 これは、ネットワークアダプターの1つでのみ構成する必要があります。この設定は、両方のアダプターに適用されます。  
  
InfiniBand ネットワークアダプターを構成すると、クライアントプロセスは、サーバーのアドレスに対してを使用`PDW_region-SQLCTL01`して、InfiniBand ネットワーク上のコントロールノードに接続できるようになります。 サーバーは Analytics Platform System DNS サフィックスを追加し`PDW_region-SQLCTL01.appliance_domain.pdw.local`ます。または、完全なアドレスを入力することもできます。  
  
たとえば、PDW のリージョン名が MyPDW で、アプライアンス名が MyAPS の場合、データを読み込むための dwloader サーバーの仕様は次のいずれかになります。  
  
-   `dwloader -S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader -S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>開始する前に  
  
### <a name="requirements"></a>要件  
AD01 ノードにログインするには、APS アプライアンスドメインアカウントが必要です。 たとえば、F12345 * \ アドミニストレーターのようになります。  
  
ネットワークアダプターを構成するアクセス許可を持つクライアントサーバーの Windows アカウントが必要です。  
  
### <a name="prerequisites"></a>前提条件  
この手順では、クライアントサーバーが既にラックに収納され、アプライアンス InfiniBand ネットワークにケーブルで接続されていることを前提としています ラックとケーブル接続の手順については、「[読み込みサーバーの取得と構成](acquire-and-configure-loading-server.md)」を参照してください。  
  
### <a name="general-remarks"></a>全般的な解説  
SQLCTL01 を使用すると、Analytics Platform System DNS は active InfiniBand ネットワークを使用して、クライアントサーバーをコントロールノードに接続します。 これは、接続を取得する場合にのみ適用されます。ロードまたはバックアップ中に InfiniBand ネットワークがダウンした場合は、プロセスを再起動する必要があります。  
  
独自のビジネス要件を満たすために、クライアントサーバーをアプライアンス以外のワークグループまたは Windows ドメインに参加させることもできます。  
  
## <a name="Sec1"></a>手順 1: アプライアンス InfiniBand のネットワーク設定を取得する  
*アプライアンス InfiniBand のネットワーク設定を取得するには*  
  
1.  Appliance_domain \Administrator アカウントを使用して、アプライアンスの AD01 ノードにログインします。  
  
2.  [アプライアンスの AD01] ノードで、コントロールパネルを開き、[ネットワークとインターネット] を選択し、[ネットワークと共有センター] * を選択して、[アダプターの設定の変更] を選択します。  
  
3.  [ネットワーク接続] ウィンドウで、[Team IB1] を右クリックし、[プロパティ] を選択します。  
  
    ![管理ノードの InfiniBand 接続](media/network-teamib.png "管理ノードの InfiniBand 接続")  
  
4.  インターネットプロトコルバージョン 4 (TCP/IPv4) プロパティウィンドウから、 **IP アドレス**と**サブネットマスク**の値を書き留めます。  **_アプライアンス\_のドメイン_-AD01**ノードの Ip アドレスは、ANALYTICS Platform System DNS サーバーの ip アドレスです。  
  
5.  **_アプライアンス\_ドメイン_AD02**サーバーの TeamIB1 アダプターに対して上記の手順1-5 を繰り返します。  
  
    ![PDW 管理ノード InfiniBand 1 のプロパティ](media/network-ip1-properties.png "PDW 管理ノード InfiniBand 1 のプロパティ")  
  
6.  [キャンセル] をクリックして、ウィンドウを閉じます。  
  
7.  TeamIB1 ネットワークで使用されていない IP アドレスを見つけて、それを書き留めます。  
  
    使用されていない IP アドレスを検索するには、コマンドウィンドウを開き、アプライアンスのアドレスの範囲内で IP アドレスに対して ping を実行します。 この例では、TeamIB1 ネットワークの IP アドレスは172.16.14.30 です。 使用されていない172.16.14 で始まる IP アドレスを検索します。 たとえば、コマンドラインから、「ping 172.16.14.254」と入力します。 Ping 要求が失敗した場合は、IP アドレスを使用できます。  
  
8.  TeamIB2 についても同じことを行います。 [ネットワーク接続] ウィンドウで、[Team IB2] を右クリックし、[プロパティ] を選択します。  
  
9. Internet Protocol Version 4 (TCP/IPv4) プロパティウィンドウで、TeamIB2 の IP アドレスとサブネットマスクの値を書き留めます。  
  
10. Appliance_domain-AD02 サーバーの TeamIB2 アダプターについて、上記の手順8-9 を繰り返します。  
  
    ![TeamIB2 のプロパティ](media/network-ip2-properties.png "TeamIB2 のプロパティ")  
  
11. **TeamIB2**ネットワークで使用されていない IP アドレスを見つけて、それを書き留めます。  
  
    使用されていない IP アドレスを検索するには、コマンドウィンドウを開き、アプライアンスのアドレスの範囲内で IP アドレスに対して ping を実行します。 この例では、TeamIB2 ネットワークの IP アドレスは172.16.18.30 です。 使用されていない172.16.18 で始まる IP アドレスを検索します。 たとえば、コマンドラインから、「ping 172.16.18.254」と入力します。 Ping 要求が失敗した場合は、IP アドレスを使用できます。  
  
## <a name="Sec2"></a>手順 2: クライアントサーバーで InfiniBand ネットワークアダプターの設定を構成する  

### <a name="notes"></a>メモ  
  
-   次の手順は、サーバーを APS DNS サーバーに登録する方法を示しています。  
  
-   独自のネットワークニーズに対応するために、クライアントサーバーをアプライアンス以外のワークグループまたは Windows ドメインに参加させることもできます。  
  
-   手順では、各サーバーで2つのネットワークアダプターを構成する手順を説明します。  ネットワークアダプターが1つしかない場合は、ネットワークアダプターで構成するネットワークを1つ選択し、代替 DNS サーバーとして2番目の DNS IP アドレスを追加します。  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>クライアントサーバーで InfiniBand ネットワークアダプターの設定を構成するには  
  
1.  Windows 管理者として、アプライアンス InfiniBand ネットワーク上の読み込み、バックアップ、またはその他のクライアントサーバーにログインします。  
  
2.  コントロールペインを開き、[ネットワークと共有センター] を選択し、[アダプターの設定の変更] を選択します。  
  
### <a name="to-configure-the-first-network-adapter"></a>最初のネットワークアダプターを構成するには  
  
1.  [ネットワーク接続] ウィンドウで、Mellanox アダプターの識別されていないネットワークスロットの1つを右クリックし、[プロパティ] を選択します。  
  
    ![InfiniBand ネットワークの選択](media/network-connections.png "InfiniBand ネットワークの選択")  
  
2.  プロパティウィンドウ  
  
    1.  [全般] タブで、IP アドレスを、TeamIB1 の ping テストで [空き] として確認した IP アドレスに設定します。 この記事で使用されている値の例については、「172.16.14.254」と入力します。  
  
    2.  サブネットマスクを、TeamIB1 に対して書き留めたサブネットマスクに設定します。  
  
    3.  優先 DNS サーバーを appliance_domain *-AD01 ノードから前に書き込んだ TeamIB1 の IP アドレスに設定します。  
  
    4.  代替 DNS サーバーを、前に appliance_domain *-AD02 ノードから書き留めた TeamIB1 の IP アドレスに設定します。  
  
        ![InfiniBand 1 ネットワークアダプターのプロパティ](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  [OK] をクリックして変更を適用します。  
  
### <a name="to-configure-the-second-network-adapter"></a>2番目のネットワークアダプターを構成するには  
  
1.  ネットワークアダプターが1つしかない場合は、このセクションをスキップします。  
  
2.  [ネットワーク接続] ウィンドウで、Mellanox アダプターの2番目の識別されていないネットワークスロットを右クリックし、[プロパティ] を選択します。  
  
    ![InfiniBand ネットワークの選択](media/network-connections.png "InfiniBand ネットワークの選択")  
  
3.  プロパティウィンドウ  
  
    1.  [全般] タブで、IP アドレスを、TeamIB2 の ping テストで [空き] として確認した IP アドレスに設定します。 この記事で使用されている値の例については、「172.16.18.254」と入力します。  
  
    2.  サブネットマスクを、TeamIB2 に対して書き留めたサブネットマスクに設定します。  
  
    3.  優先 DNS サーバーを appliance_domain *-AD01 ノードから前に書き込んだ TeamIB2 の IP アドレスに設定します。  
  
    4.  代替 DNS サーバーを、前に appliance_domain *-AD02 ノードから書き留めた TeamIB2 の IP アドレスに設定します。  
  
        > [!NOTE]  
        > ネットワークアダプターが1つしかない場合は、優先 dns サーバーと代替 dns サーバーの両方を優先 dns サーバーまたは代替 DNS サーバーとして使用して、優先 DNS サーバーと代替 DNS サーバーをそれぞれ構成します。または、アプライアンス AD01 TeamIB2 と TeamIB1 を使用します。アプライアンス AD02 は、AD 仮想マシンがフェールオーバーされたかどうかに応じて、優先 DNS サーバーおよび代替 DNS サーバーとして TeamIB2 します。  
  
        ![InfiniBand 1 ネットワークアダプターのプロパティ](media/network-ib1-properties.png "InfiniBand 1 ネットワークアダプターのプロパティ")  
  
    5.  [OK] をクリックして変更を適用します。  
  
### <a name="to-configure-the-dns-suffix"></a>DNS サフィックスを構成するには  
  
1.  [ネットワーク接続] ウィンドウで、Mellanox アダプターのネットワークスロットのいずれかを右クリックし、[プロパティ] を選択します。  
  
2.  [詳細] をクリックします。;.  
  
3.  [TCP/IP の詳細設定] ウィンドウで、[これらの DNS サフィックスを順に追加する] オプションがグレーで表示されていない場合は、[次の DNS サフィックスの追加 (順序)] チェックボックスをオンにして、アプライアンスドメインサフィックスを選択し、[追加] をクリックします。アプライアンスドメインサフィックスは、`appliance_domain.local`  
  
4.  [次の DNS サフィックスを順に追加する] オプションがグレーで表示されている場合は、レジストリキー HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows NT\DNSClient. を変更して、このサーバーに APS ドメインを追加できます。  
  
    ![TCP/IP 設定](media/network-tcpip.png "TCP/IP 設定")  
  
5.  アドレスの解決を高速化するために、アプライアンスのサフィックスを一覧の一番上に移動することをお勧めします。  
  
6.  [OK] をクリックします。  
  
7.  これで、、、またはを使用`PDW_region-SQLCTL01.appliance_domain.local`して、アプライアンス Infiniband ネットワーク`appliance_domain-SQLCTL01`に接続できるようになりました。 完全名と DNS サフィックスを使用して接続すると、接続が高速に確立される可能性があります。  
  
    MyPDW PDW 領域を持つ MyAPS という名前のアプライアンスの例を次に示します。  
  
    -   MyPDW-SQLCTL01. ローカル  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>参照  
[読み込みサーバーの取得と構成](acquire-and-configure-loading-server.md)  
  
