---
title: レッスン 2:別のコンピューターからの接続 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: fd4ddeb8-0cb6-441b-9704-03575c07020f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: eedbde338ad3cc2af5477cc263eac7444707c0d8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63144799"
---
# <a name="lesson-2-connecting-from-another-computer"></a>レッスン 2:別のコンピューターからの接続
  セキュリティを強化するため、 [!INCLUDE[ssDE](../includes/ssde-md.md)] Developer、Express、および Evaluation Editions の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は、最初にインストールした状態では別のコンピューターからアクセスできないようになっています。 このレッスンでは、別のコンピューターから接続するために、プロトコルの有効化、ポートの構成、Windows ファイアウォールの構成を行う方法について学習します。  
  
 このレッスンの内容は次のとおりです。  
  
-   [プロトコルの有効化](#protocols)  
  
-   [固定ポートの構成](#port)  
  
-   [ファイアウォールでポートを開く](#firewall)  
  
-   [別のコンピューターからのデータベース エンジンへの接続](#otherComp)  
  
-   [SQL Server Browser サービスを使用した接続](#browser)  
  
##  <a name="protocols"></a> プロトコルを有効にします。  
 セキュリティを強化するために、 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]、Developer、および Evaluation は、ネットワーク接続が制限された状態でインストールされます。 [!INCLUDE[ssDE](../includes/ssde-md.md)] には、同じコンピューターで実行しているツールから接続できますが、別のコンピューターからは接続できません。 [!INCLUDE[ssDE](../includes/ssde-md.md)]と同じコンピューターで開発作業を行う場合、他のプロトコルを有効にする必要はありません。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] は、共有メモリ プロトコルを使用して [!INCLUDE[ssDE](../includes/ssde-md.md)] に接続します。 このプロトコルは既に有効になっています。  
  
 別のコンピューターから [!INCLUDE[ssDE](../includes/ssde-md.md)] に接続する場合は、TCP/IP などのプロトコルを有効にする必要があります。  
  
#### <a name="how-to-enable-tcpip-connections-from-another-computer"></a>別のコンピューターからの TCP/IP 接続を有効にするには  
  
1.  **[スタート]** メニューで、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[SQL Server 構成マネージャー]** をクリックします。  
  
    > [!NOTE]  
    >  32 ビットと 64 ビットの両方のオプションが利用できる場合もあります。  
  
2.  **SQL Server 構成マネージャー**、展開**SQL Server ネットワーク構成**、 をクリックし、**プロトコル**  _\<InstanceName>_ します。  
  
     既定のインスタンス (名前のないインスタンス) は、 **MSSQLSERVER**として一覧表示されます。 名前付きインスタンスをインストールした場合は、指定した名前が表示されます。 [!INCLUDE[ssExpressEd11](../includes/ssexpressed11-md.md)] は **SQLEXPRESS**としてしてインストールされます (セットアップ中に名前を変更した場合を除く)。  
  
3.  プロトコルの一覧で、有効にするプロトコル ( **[TCP/IP]** ) を右クリックし、 **[有効化]** をクリックします。  
  
    > [!NOTE]  
    >  ネットワーク プロトコルを変更したら [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] サービスを再起動する必要がありますが、これは次の作業で実行されます。  
  
##  <a name="port"></a> 固定ポートの構成  
 セキュリティ強化のために、Windows Server 2008、 [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]、および Windows 7 では Windows ファイアウォールが有効になっています。 別のコンピューターからこのインスタンスに接続する場合は、ファイアウォールで通信ポートを開放する必要があります。 [!INCLUDE[ssDE](../includes/ssde-md.md)] の既定のインスタンスはポート 1433 でリッスンするので、固定ポートを構成する必要はありません。 ただし、 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] の名前付きインスタンスは、動的ポートでリッスンします。 ファイアウォールでポートを開く前に、まず [!INCLUDE[ssDE](../includes/ssde-md.md)] が固定ポートまたは静的ポートと呼ばれる特定のポートでリッスンするように構成する必要があります。このように構成しないと、 [!INCLUDE[ssDE](../includes/ssde-md.md)] は起動のたびに異なるポートでリッスンする可能性があります。 ファイアウォール、Windows ファイアウォールの既定の設定の詳細と、データベース エンジン、Analysis Services、Reporting Services、および Integration Services に影響する TCP ポートの説明については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」を参照してください。  
  
> [!NOTE]  
>  ポート番号の割り当ては、Internet Assigned Numbers Authority によって管理され、[http://www.iana.org](https://go.microsoft.com/fwlink/?LinkId=48844) に一覧が掲載されています。ポート番号には 49152 ～ 65535 の数値を割り当てる必要があります。  
  
#### <a name="configure-sql-server-to-listen-on-a-specific-port"></a>SQL Server が特定のポートでリッスンするよう構成するには  
  
1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーで、 **[SQL Server ネットワークの構成]** を展開し、構成するサーバー インスタンスをクリックします。  
  
2.  右側のペインで、 **[TCP/IP]** をダブルクリックします。  
  
3.  **[TCP/IP のプロパティ]** ダイアログ ボックスの **[IP アドレス]** タブをクリックします。  
  
4.  **[IPAll]** セクションの **[TCP ポート]** ボックスで、使用可能なポート番号を入力します。 このチュートリアルでは使用`49172`します。  
  
5.  **[OK]** をクリックしてダイアログ ボックスを閉じ、サービスを再起動する必要があるという警告が表示されたら **[OK]** をクリックします。  
  
6.  左ペインで、 **[SQL Server のサービス]** をクリックします。  
  
7.  右ペインで、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]インスタンスを右クリックし、 **[再起動]** をクリックします。 ときに、[!INCLUDE[ssDE](../includes/ssde-md.md)]ポートでリッスン再起動すると、`49172`します。  
  
##  <a name="firewall"></a> ファイアウォールでポートを開く  
 ファイアウォール システムは、コンピューター リソースへの不正アクセスを防ぐのに役立ちます。 ファイアウォールが有効になっている場合、別のコンピューターから [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に接続するには、ファイアウォールでポートを開く必要があります。  
  
> [!IMPORTANT]  
>  ファイアウォールのポートを開くと、サーバーが攻撃を受けやすくなります。 ポートを開く前に、ファイアウォール システムに関する理解を深めておいてください。 詳細については、「 [Security Considerations for a SQL Server Installation](../sql-server/install/security-considerations-for-a-sql-server-installation.md)」を参照してください。  
  
 固定ポートを使用するよう [!INCLUDE[ssDE](../includes/ssde-md.md)] を構成した後、次の手順に従って、Windows ファイアウォールで固定ポートを開きます (既定のインスタンスに固定ポートを構成する必要はありません。既定のインスタンスには固定の TCP ポート 1433 が構成済みです)。  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access-windows-7"></a>TCP アクセス用に Windows ファイアウォールのポートを開くには (Windows 7)  
  
1.  **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックして **「WF.msc」** と入力し、 **[OK]** をクリックします。  
  
2.  **[セキュリティが強化された Windows ファイアウォール]** の左ペインの **[受信の規則]** をクリックし、[操作] ペインの **[新規の規則]** をクリックします。  
  
3.  **[規則の種類]** ダイアログ ボックスで、 **[ポート]** をクリックし、 **[次へ]** をクリックします。  
  
4.  **[プロトコルおよびポート]** ダイアログ ボックスで、 **[TCP]** をクリックします。 **[特定のローカル ポート]** を選択し、 [!INCLUDE[ssDE](../includes/ssde-md.md)]のインスタンスのポート番号を入力します。 既定のインスタンスの場合は「1433」と入力してください。 型`49172`名前付きインスタンスを構成して、前の作業で固定ポートを構成する場合。 **[次へ]** をクリックします。  
  
5.  **[操作]** ダイアログ ボックスで、 **[接続を許可する]** をクリックし、 **[次へ]** をクリックします。  
  
6.  **[プロファイル]** ダイアログ ボックスで、 [!INCLUDE[ssDE](../includes/ssde-md.md)]に接続するときのコンピューター接続環境を表すプロファイルをすべて選択し、 **[次へ]** をクリックします。  
  
7.  **[名前]** ダイアログ ボックスで、この規則の名前と説明を入力し、 **[完了]** をクリックします。  
  
 [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)]の指示を含む、ファイアウォールの構成に関する詳細については、「 [データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)」を参照してください。 Windows ファイアウォールの既定の設定の詳細と、データベース エンジン、Analysis Services、Reporting Services、および Integration Services に影響する TCP ポートの説明については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」をご覧ください。  
  
##  <a name="otherComp"></a> 別のコンピューターからデータベース エンジンへの接続  
 固定ポートで受信待ちするように [!INCLUDE[ssDE](../includes/ssde-md.md)] を構成し、ファイアウォールでそのポートを開いたら、別のコンピューターから [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に接続できます。  
  
 サーバー コンピューターで [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser サービスが実行され、ファイアウォールで UDP ポート 1434 が開いている場合は、コンピューター名とインスタンス名を使用して接続を確立できます。 セキュリティ強化のため、今回の例では [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser サービスは使用しません。  
  
#### <a name="to-connect-to-the-database-engine-from-another-computer"></a>別のコンピューターからデータベース エンジンに接続するには  
  
1.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のクライアント ツールがインストールされている別のコンピューターに、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]への接続権限のあるアカウントを使用してログインし、 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]を開きます。  
  
2.  **[サーバーへの接続]** ダイアログ ボックスで、 **[サーバーの種類]** ボックスが **[データベース エンジン]** になっていることを確認します。  
  
3.  **[サーバー名]** ボックスに「**tcp:** 」と入力してプロトコルを指定し、続けてコンピューター名、コンマ、ポート番号の順に入力します。 既定のインスタンスに接続する場合、ポート 1433 が暗黙的に設定されるためポート番号を省略できます。したがって、この場合は「**tcp:** _<computer_name>_ 」と入力します。 今回の名前付きインスタンスの例では、「**tcp:** _<computer_name>_ **,49172**」と入力します。  
  
    > [!NOTE]  
    >  **[サーバー名]** ボックスで **tcp:** を省略した場合、クライアントは、有効になっているすべてのプロトコルをクライアント構成に指定された順番で試行します。  
  
4.  **認証**ボックスに、確認**ウィンドウ認証**、順にクリックします**Connect**します。  
  
##  <a name="browser"></a> SQL Server Browser サービスを使用して接続します。  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser サービスは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の各種リソースに関する着信要求を受信し、このコンピューター上にインストールされている [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスに関する情報を提供します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser サービスが実行されている場合、ユーザーはコンピューター名とポート番号の代わりにコンピューター名とインスタンス名を指定して、名前付きインスタンスに接続できます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser は、認証されていない UDP 要求を受信します。したがって、セットアップで有効にしない場合もあります。 サービスの説明と、有効にする場合の説明については、「[SQL Server Browser サービス (データベース エンジンと SSAS)](../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser を使用するには、前の作業と同じ手順に従い、ファイアウォールの UDP ポート 1434 を開放します。  
  
 これで、基本的な接続に関する簡単なチュートリアルを終了します。  
  
## <a name="return-to-tutorials-portal"></a>チュートリアル ポータルに戻る  
 [チュートリアル:データベース エンジンの概要](tutorial-getting-started-with-the-database-engine.md)  
  
  
