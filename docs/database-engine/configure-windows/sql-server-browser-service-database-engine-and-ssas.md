---
title: SQL Server Browser サービス (データベース エンジンと SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- services [SQL Server], security
- SQL Browser service (See SQL Server Browser service)
- Browser Service
- SQL Server Browser service
ms.assetid: 5c236ddc-766d-4a30-af1e-cc6176eca690
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fade5e48340e8cc2b51b354f9717a561c632e4d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028630"
---
# <a name="sql-server-browser-service-database-engine-and-ssas"></a>SQL Server Browser サービス (データベース エンジンと SSAS)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser プログラムは Windows サービスとして実行されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各種リソースに関する着信要求を受信し、このコンピューター上にインストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに関する情報を提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は次の操作に役立ちます。  
  
-   使用可能なサーバーの一覧の参照  
  
-   適切なサーバー インスタンスへの接続  
  
-   専用管理者接続 (DAC) のエンドポイントへの接続  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] Browser サービス (sqlbrowser) は、 [!INCLUDE[ssAS](../../includes/ssas-md.md)]と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各インスタンスに対してインスタンス名とバージョン番号を提供します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と共にインストールされます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は、セットアップ時に、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して構成できます。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスは次の場合に自動的に開始されます。  
  
-   インストールをアップグレードする場合  
  
-   クラスターにインストールする場合  
  
-   SQL Server Express のすべてのインスタンスを含む、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] の名前付きインスタンスをインストールする場合  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の名前付きインスタンスをインストールする場合  
  
## <a name="background"></a>背景情報  
 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]より前は、コンピューターにインストールできる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスは 1 つだけでした。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、公式の Internet Assigned Numbers Authority (IANA) によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に割り当てられたポート 1433 で着信要求を待ちます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 1 つのインスタンスしかポートを使用できないので、 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の複数のインスタンスをサポートするようになったとき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol (SSRP) が開発され、UDP ポート 1434 で受信待ちするようになりました。 このリスナー サービスは、インストールされているインスタンスの名前と、そのインスタンスが使用しているポートまたは名前付きパイプでクライアント要求に応答していました。 SSRP システムの制限を解消するため、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] では SSRP の代わりに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを導入しています。  
  
## <a name="how-sql-server-browser-works"></a>SQL Server Browser のしくみ  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを起動すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に対して TCP/IP プロトコルが有効な場合は、サーバーに TCP/IP ポートが割り当てられます。 名前付きパイプのプロトコルが有効な場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は特定の名前付きパイプでリッスンします。 クライアント アプリケーションとのデータの交換には、このポート、つまり "パイプ" がそのインスタンスで使用されます。 インストール中、TCP ポート 1433 とパイプ `\sql\query` が既定のインスタンスに割り当てられますが、これは後でサーバー管理者が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して変更できます。 ポートまたはパイプを使用できるのは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 1 つのインスタンスだけなので、 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]を含めて、名前付きインスタンスには別のポート番号とパイプ名が割り当てられます。 既定では、名前付きインスタンスと [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] が有効な場合、両方とも動的ポートを使用するように設定されています。つまり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の起動時に使用可能なポートが割り当てられます。 必要であれば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに特定のポートを割り当てることができます。 クライアントは接続時に特定のポートを指定できますが、ポートが動的に割り当てられる場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が再起動されるたびにポート番号が変わる可能性があるので、クライアントは正しいポート番号を特定できません。  
  
 起動時に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser が開始されて UDP ポート 1434 が要求されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser はレジストリを読み取って、コンピューター上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのインスタンスを識別し、使用されているポートと名前付きパイプを確認します。 サーバーに複数のネットワーク カードがある場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser が最初に検出したポートを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に返します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser では ipv6 と ipv4 をサポートしています。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クライアントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースを要求すると、ポート 1434 を使用しているサーバーにクライアント ネットワーク ライブラリが UDP メッセージを送信します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は、要求されたインスタンスの TCP/IP ポートまたは名前付きパイプで応答します。 その後、クライアント アプリケーションのネットワーク ライブラリが、目的のインスタンスのポートまたは名前付きパイプを使用しているサーバーに要求を送って接続を完了します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser では既定のインスタンスのポート情報は返されません。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスの開始と停止の詳細については、「 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)」を参照してください。  
  
## <a name="using-sql-server-browser"></a>SQL Server Browser の使用  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスが実行されていない場合でも、正しいポート番号か名前付きパイプを指定すれば [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続できます。 たとえば、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスがポート 1433 で実行されている場合は、TCP/IP を使用して接続できます。  
  
 ただし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスが実行されていない場合は、次の接続が機能しません。  
  
-   パラメーター (たとえば TCP/IP ポートや名前付きパイプ) を完全に指定せずに名前付きインスタンスに接続しようとするコンポーネント。  
  
-   後で他のコンポーネントが再接続に使用する可能性のあるサーバーまたはインスタンス情報を生成するかまたは渡すコンポーネント。  
  
-   ポート番号やパイプを指定せずに名前付きインスタンスに接続する。  
  
-   TCP/IP ポート 1433 を使用していない場合は、名前付きインスタンスや既定のインスタンスへの DAC。  
  
-   OLAP リダイレクター サービス。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、Enterprise Manager、またはクエリ アナライザーでのサーバーの列挙。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をクライアント/サーバーのシナリオで使用している場合 (たとえば、アプリケーションがネットワーク経由で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にアクセスしている場合)、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスを停止または無効化するには、各インスタンスに特定のポート番号を割り当て、常にそのポート番号が使用されるようにクライアント アプリケーションのコードを記述する必要があります。 この方法には次の問題があります。  
  
-   クライアント アプリケーションが必ず適切なポートに接続するように、コードを更新および管理しておく必要があります。  
  
-   各インスタンスに対して選択したポートがサーバー上の別のサービスまたはアプリケーションによって使用されている場合があります。この場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスは使用できません。  
  
## <a name="clustering"></a>クラスター  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser はクラスター化されたリソースではなく、クラスター ノード間のフェールオーバーはサポートしません。 そのため、クラスターの場合は、クラスターのノードごとに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser をインストールして有効にする必要があります。 クラスターでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は IP_ANY で受信待ちします。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser では最初に検出された IP とポートのペアが返されるため、IP_ANY で受信待ちのときに特定の IP での受信待ちを有効にする場合は、各 IP に同じ TCP ポートを構成する必要があります。  
  
## <a name="installing-uninstalling-and-running-from-the-command-line"></a>コマンド ラインからのインストール、アンインストール、実行  
 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser プログラムは C:\Program Files (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe にインストールされます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の最後のインスタンスを削除すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスがアンインストールされます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は、トラブルシューティングの目的で、コマンド プロンプトから **-c** スイッチを使用して起動できます。  
  
```  
<drive>\<path>\sqlbrowser.exe -c  
```  
  
## <a name="security"></a>Security  
  
### <a name="account-privileges"></a>アカウントの権限  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser は UDP ポートで受信待ちし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Resolution Protocol (SSRP) を使用して、認証されていない要求を受け入れます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser を権限が制限されているユーザーのセキュリティ コンテキストで実行することにより、悪意のある攻撃にさらされる危険性を最小限に抑える必要があります。 ログオン アカウントは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して変更できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser の最小限のユーザー権限は次のとおりです。  
  
-   ネットワークからこのコンピューターへのアクセスを拒否  
  
-   ローカルでのログオンを拒否  
  
-   バッチ ジョブとしてのログオンを拒否  
  
-   ターミナル サービス経由のログオンを拒否  
  
-   サービスとしてログオン  
  
-   ネットワーク通信に関連する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] レジストリ キーの読み取りおよび書き込み (ポートおよびパイプ)  
  
### <a name="default-account"></a>既定のアカウント  
 セットアップ プログラムは、セットアップ中にサービス用に選択したアカウントを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser が使用するように構成します。 他に可能なアカウントは次のとおりです。  
  
-   すべての **domain\local** アカウント  
  
-   **ローカル サービス** アカウント  
  
-   **ローカル システム** アカウント (不要な権限があるので推奨しません)  
  
### <a name="hiding-sql-server"></a>SQL Server の非表示  
 非表示インスタンスは、共有メモリ接続のみをサポートする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の場合は、 `HideInstance` Browser がこのサーバー インスタンスに関する情報を返さないことを示すために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フラグを設定します。  
  
### <a name="using-a-firewall"></a>ファイアウォールの使用  
 ファイアウォールの背後にある [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスと通信するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用される TCP ポート (1433 など) のほかに UDP ポート 1434 も開きます。 ファイアウォールの使用方法については、次をご覧ください。「[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のアクセス用にファイアウォールを構成する」([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブック)  
  
## <a name="see-also"></a>参照  
 [ネットワーク プロトコルとネットワーク ライブラリ](../../sql-server/install/network-protocols-and-network-libraries.md)  
 [SQL Server データベース エンジンのインスタンスの非表示](../../database-engine/configure-windows/hide-an-instance-of-sql-server-database-engine.md)  
  
