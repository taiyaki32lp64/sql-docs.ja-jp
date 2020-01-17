---
title: アプライアンスノードへの接続
description: この記事では、Analytics Platform System appliance の各ノードに接続するさまざまな方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e1182d174e3281fda944c0b6490b114d4b6f2244
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401245"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>Analytics Platform System のアプライアンスノードへの接続
この記事では、Analytics Platform System appliance の各ノードに接続するさまざまな方法について説明します。  
  
## <a name="connecting-with-hadoop"></a>Hadoop を使用した接続  
SQL Server PDW で Hadoop を使用する前に、SQL Server PDW に Java Runtime Environment をインストールするようアプライアンス管理者に依頼してください。 手順については、「アプライアンス操作ガイド」の「[外部データへの PolyBase 接続の構成 &#40;Analytics Platform System&#41;](configure-polybase-connectivity-to-external-data.md) 」を参照してください。  
  
## <a name="ConnectingToIndividualNodes"></a>アプライアンスノードへの接続  
各アプライアンスノードは、特定の使用シナリオおよび特定のユーザーの種類によってのみ直接アクセスされます。 次の表は、各アプライアンスノードと、ユーザーがそのノードに直接接続するシナリオを示しています。  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  

> [!WARNING]  
> 製品チームまたは APS カスタマーサポートチームに明示的に同意せずに、コントロールまたは計算ノードのデータベースまたはテーブルの設定を変更すると、APS アプライアンスがサポートされなくなる可能性があります。
  
|||  
|-|-|  
|**ノード**|**アクセスシナリオ**|  
|制御ノード|コントロールノードで実行される管理コンソールにアクセスするには、web ブラウザーを使用します。 詳細については、「[管理コンソールを使用したアプライアンスの監視 &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)」を参照してください。<br /><br />すべてのクライアントアプリケーションとツールは、接続がイーサネットまたは InfiniBand のどちらを使用しているかに関係なく、コントロールノードに接続します。<br /><br />制御ノードへのイーサネット接続を構成するには、制御ノードのクラスター IP アドレスとポート**17001**を使用します。 たとえば、"192.168.0.1, 17001" のようになります。<br /><br />コントロールノードへの InfiniBand 接続を構成するには、 <strong> *appliance_domain*-SQLCTL01</strong>とポート**17001**を使用します。 SQLCTL01 を<strong> *appliance_domain*</strong>使用すると、アプライアンスの DNS サーバーは、サーバーを active InfiniBand ネットワークに接続します。 これを使用するようにアプライアンス以外のサーバーを構成するには、「 [Configure InfiniBand Network Adapters](configure-infiniband-network-adapters.md)」を参照してください。<br /><br />アプライアンス管理者は、制御ノードに接続して管理操作を実行します。 たとえば、アプライアンス管理者は、制御ノードから次の操作を実行します。<br /><br />**Dwconfig**構成ツールを使用して、Analytics Platform System を構成します。|  
|コンピューティング ノード|コンピューティングノードの接続は、制御ノードによって指示されます。 コンピューティングノードの IP アドレスは、アプリケーションコマンドにパラメーターとして入力されることはありません。<br /><br />読み込み、バックアップ、リモートテーブルコピー、Hadoop の場合、SQL Server PDW は、コンピューティングノードと非アプライアンスノードまたはサーバーとの間で直接データを送受信します。 これらのアプリケーションは、コントロールノードに接続することによって SQL Server PDW に接続し、制御ノードが SQL Server PDW に指示して、コンピューティングノードと非アプライアンスサーバー間の通信を確立します。<br /><br />たとえば、次のようなデータ転送操作は、コンピューティングノードへの直接接続と並行して行われます。<br /><br />読み込み元のサーバーから SQL Server PDW に読み込んでいます。<br /><br />SQL Server PDW からバックアップサーバーにデータベースをバックアップします。<br /><br />バックアップサーバーから SQL Server PDW にデータベースを復元します。<br /><br />SQL Server PDW から Hadoop データを照会しています。<br /><br />SQL Server PDW から外部 Hadoop テーブルにデータをエクスポートしています。<br /><br />リモート SMP SQL Server データベースに SQL Server PDW テーブルをコピーする。|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>イーサネットネットワークと InfiniBand ネットワークへの接続  
リモートサーバーは、アプライアンス InfiniBand ネットワークまたはイーサネットネットワークのいずれかを介して接続できます。 パフォーマンス上の理由により、 **SELECT ステートメントとして CREATE REMOTE TABLE**を使用して、サーバー、バックアップサーバー、およびデータを受信するサーバーを読み込むことは、通常、アプライアンス InfiniBand ネットワークを介してデータを転送します。  
  
自分のユーザーのワークグループまたはドメインに属しているアプライアンス以外のサーバーを構成し、独自の顧客ネットワークを使用してそれらのサーバーに接続し、データを転送することができます。 また、アプライアンス InfiniBand に接続されている非アプライアンスサーバーには、アプライアンス InfiniBand ネットワークを介して相互にデータを転送するオプションがあります。SQL Server PDW のパフォーマンスが低下する可能性があるため、この点に注意してください。  
  
たとえば、このステートメントでは、InfiniBand IP アドレスが192.168.0.1 のバックアップサーバーに InfiniBand 経由でバックアップを実行するためのネットワーク資格情報を追加します。 アプライアンスドメインは*mypdw*で、ステートメントはバックアップサーバーから実行されます。 このステートメントを実行する前に、独自のパラメーターを入力する必要があります。  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
たとえば、読み込みコマンドの先頭は次のようになります。  
  
```  
dwloader -S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
