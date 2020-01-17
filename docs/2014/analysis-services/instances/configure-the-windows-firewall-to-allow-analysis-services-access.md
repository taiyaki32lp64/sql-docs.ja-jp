---
title: Analysis Services アクセスを許可するように Windows ファイアウォールを構成する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ports [Analysis Services]
- Windows Firewall [Analysis Services]
- firewall systems [Analysis Services]
ms.assetid: 7673acc5-75f0-4703-9ce2-87425ea39d49
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b74c767c50e8a62c2d65ad089e386a94b9c8a5e
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70151857"
---
# <a name="configure-the-windows-firewall-to-allow-analysis-services-access"></a>Analysis Services のアクセスを許可するための Windows ファイアウォールの構成
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] や [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] をネットワーク上で利用できるようにするための重要な最初の手順は、ファイアウォールのポートのブロックを解除する必要があるかどうかを判断することです。 ほとんどのインストールでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]への接続を許可する受信ファイアウォール ルールを少なくとも 1 つ作成する必要があります。  
  
 ファイアウォールの構成要件は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のインストール方法によって異なります。  
  
-   既定のインスタンスをインストールした場合や、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] フェールオーバー クラスターを作成した場合は、TCP ポート 2383 を開きます。  
  
-   名前付きインスタンスをインストールした場合は、TCP ポート 2382 を開きます。 名前付きインスタンスは、動的なポート割り当てを使用します。 Analysis Services の検出サービスとして、SQL Server Browser サービスは TCP ポート 2382 をリッスンし、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]によって現在使用されているポートに対して接続要求をリダイレクトします。  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を SharePoint モードでインストールし、 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 をサポートしている場合は、TCP ポート 2382 を開きます。 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 では、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスは SharePoint の外部に位置します。 SharePoint Web アプリケーションから発信され、ネットワーク接続を経由して名前付きの 'PowerPivot' インスタンスに至る着信要求では、開かれたポートが必要になります。 他の名前付き [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスと同様に、TCP 2382 で SQL Server Browser サービスに対して [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]へのアクセスを許可する受信ルールを作成します。  
  
-   [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 の場合は、Windows ファイアウォールでポートを開けないでください。 このサービスは SharePoint アドインとして、SharePoint を対象として構成されたポートを使用し、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスへのローカル接続のみを作成します。このインスタンスは、 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] データ モデルの読み込みとそのモデルに対するクエリを実行します。  
  
-   Azure Virtual Machines で実行されている [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスの場合は、サーバーアクセスを構成するための代替手順を使用します。 「 [Azure Virtual Machines でのビジネスインテリジェンスの SQL Server」を](https://msdn.microsoft.com/library/windowsazure/jj992719.aspx)参照してください。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の既定のインスタンスは TCP ポート2383でリッスンしますが、別の固定ポートでリッスンするようにサーバーを構成し、次の形式でサーバーに接続することができます: \<servername >:\<ポート番号 >。  
  
 1 つの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスで使用できるのは、1 つの TCP ポートのみです。 複数のネットワーク カードまたは複数の IP アドレスを使用しているコンピューターでは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] は、そのコンピューターに割り当てられているすべての IP アドレス、または別名を付けられているすべての IP アドレスに対応する 1 つの TCP ポートをリッスンします。 特定のマルチポート要件がある場合は、HTTP アクセス用に [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を構成することを検討してください。 そうすれば、どのポートを選択しても、複数の HTTP エンドポイントを設定できます。 「[インターネット インフォメーション サービス (IIS) 8.0 上の Analysis Services への HTTP アクセスの構成](configure-http-access-to-analysis-services-on-iis-8-0.md)」を参照してください。  
  
 このトピックには、次のセクションが含まれます。  
  
-   [Analysis Services で使用されるポートとファイアウォールの設定](#bkmk_checkport)  
  
-   [Analysis Services の既定のインスタンスに対する Windows ファイアウォールの構成](#bkmk_default)  
  
-   [Analysis Services の名前付きインスタンスに対する Windows ファイアウォール アクセスの構成](#bkmk_named)  
  
-   [Analysis Services クラスターのポートの構成](#bkmk_cluster)  
  
-   [PowerPivot for SharePoint のポート構成](#bkmk_powerpivot)  
  
-   [Analysis Services の既定のインスタンスまたは名前付きインスタンスに対する固定ポートの使用](#bkmk_fixed)  
  
 Windows ファイアウォールの既定の設定の詳細と、データベース エンジン、Analysis Services、Reporting Services、および Integration Services に影響する TCP ポートの説明については、「[SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」をご覧ください。  
  
##  <a name="bkmk_checkport"></a> Analysis Services で使用されるポートとファイアウォールの設定  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]でサポートされる Microsoft Windows オペレーティング システムの場合、既定で Windows ファイアウォールが有効になっており、リモート接続はブロックされます。 Analysis Services への着信要求を許可するために、ファイアウォール内でポートを手動で開く必要があります。 SQL Server セットアップでは、この手順が自動的に実行されません。  
  
 ポートの設定は、msmdsrv.ini ファイルと、SQL Server Management Studio の Analysis Services インスタンスの [全般プロパティ] ページで指定します。 `Port` が正の整数に設定されている場合、Analysis Services は固定ポートでリッスンします。 `Port` が 0 に設定されている場合、Analysis Services が既定のインスタンスであればポート 2383 でリッスンし、名前付きインスタンスであれば動的に割り当てられたポートでリッスンします。  
  
 動的なポート割り当ては、名前付きインスタンスでのみ使用されます。 `MSOLAP$InstanceName` サービスによって、使用されるポートが起動時に決定されます。 名前付きインスタンスによって使用されている実際のポート番号は、次の方法で調べることができます。  
  
-   タスクマネージャーを起動し、 **[サービス]** をクリックして `MSOLAP$InstanceName`の PID を取得します。  
  
-   コマンド ラインから「`netstat -ao -p TCP`」を実行し、その PID に対応する TCP ポート情報を表示します。  
  
-   SQL Server Management Studio を使用してポートを確認し、次の形式で Analysis Services サーバーに接続します。 \<IPAddress >:\<ポート番号 >。  
  
 アプリケーションが特定のポートをリッスンしていても、ファイアウォールによってアクセスがブロックされていれば、接続は失敗します。 Analysis Services の名前付きインスタンスに接続するには、msmdsrv.exe へのアクセスのブロックを解除するか、ファイアウォール内でリッスンしている固定ポートへのアクセスのブロックを解除する必要があります。 以降のセクションで、その手順について説明します。  
  
 Analysis Services に対するファイアウォール設定が既に定義されているかどうかを確認するには、コントロール パネルの [セキュリティが強化された Windows ファイアウォール] を使用します。 [監視] フォルダーの [ファイアウォール] ページに、ローカル サーバーに対して定義されている規則がすべて表示されます。  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]では、すべてのファイアウォール ルールを手動で定義する必要があることに注意してください。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] および SQL Server Browser ではポート 2382 および 2383 が予約されていますが、SQL Server セットアップ プログラムでも、その他の構成ツールでも、ポートまたはプログラム実行可能ファイルへのアクセスを許可するファイアウォールの規則は自動的に定義されません。  
  
##  <a name="bkmk_default"></a> Analysis Services の既定のインスタンスに対する Windows ファイアウォールの構成  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の既定のインスタンスは TCP ポート 2383 でリッスンします。 既定のインスタンスがインストールされている場合にこのポートを使用するには、Windows ファイアウォールで TCP ポート 2383 への受信アクセスを解除し、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の既定のインスタンスへのリモート アクセスを有効にする必要があります。 既定のインスタンスがインストールされているときに、固定ポートでリッスンするようにサービスを構成する場合は、このトピックの「 [Analysis Services の既定のインスタンスまたは名前付きインスタンスに対する固定ポートの使用](#bkmk_fixed) 」を参照してください。  
  
 このサービスが既定のインスタンス (MSSQLServerOLAPService) として動作しているかどうか確認するには、SQL Server 構成マネージャーでサービスの名前を確認します。 Analysis Services の既定のインスタンスは、常に **[SQL Server Analysis Services (MSSQLSERVER)]** という名前で表示されます。  
  
> [!NOTE]  
>  Windows オペレーティング システムの種類によっては、Windows ファイアウォールを構成する別のツールが用意されています。 ほとんどのツールでは、特定のポートとプログラム実行可能ファイルのどちらを開くかを選択できます。 プログラム実行可能ファイルを指定する必要がなければ、ポートを指定することをお勧めします。  
  
 受信の規則を指定するときには、後で探しやすいような名前を付けてください (たとえば、 **SQL Server Analysis Services (TCP-in) 2383**など)。  
  
#### <a name="windows-firewall-with-advanced-security"></a>セキュリティが強化された Windows ファイアウォール  
  
1.  Windows 7 または Windows Vista の場合、コントロール パネルの **[システムとセキュリティ]** をクリックした後、 **[Windows ファイアウォール]** 、 **[詳細設定]** の順にクリックします。 Windows Server 2008 または 2008 R2 の場合、管理ツールを開き、 **[セキュリティが強化された Windows ファイアウォール]** をクリックします。 Windows Server 2012 では、アプリケーション ページを開き、「 **Windows ファイアウォール**」と入力します。  
  
2.  **[受信の規則]** を右クリックし、 **[新しい規則]** をクリックします。  
  
3.  ルールの種類 で、`Port` をクリックし、**次へ** をクリックします。  
  
4.  プロトコルおよびポート で、 **TCP** を選択し、**特定のローカルポート** に「`2383`」と入力します。  
  
5.  [操作] で、 **[接続を許可する]** をクリックし、 **[次へ]** をクリックします。  
  
6.  [プロファイル] で、規則を適用しないネットワークの場所のチェック ボックスをオフにした後、 **[次へ]** をクリックします。  
  
7.  [名前] に、この規則のわかりやすい名前 (`SQL Server Analysis Services (tcp-in) 2383`など) を入力し、 **[完了]** をクリックします。  
  
8.  リモート接続が有効になっているかどうかを検証するには、SQL Server Management Studio または Excel を異なるコンピューター上で開き、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] [サーバー名] **に表示されているサーバーのネットワーク名を指定して**に接続します。  
  
    > [!NOTE]  
    >  他のユーザーは、アクセス許可が与えられるまでこのサーバーにはアクセスできません。 詳細については、「[オブジェクトと操作へのアクセスの承認 (Analysis Services)](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)」を参照してください。  
  
#### <a name="netsh-advfirewall-syntax"></a>Netsh AdvFirewall 構文  
  
-   次のコマンドを実行すると、TCP ポート 2383 での受信要求を許可する受信の規則が作成されます。  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services inbound on TCP 2383" dir=in action=allow protocol=TCP localport=2383 profile=domain  
    ```  
  
##  <a name="bkmk_named"></a> Analysis Services の名前付きインスタンスに対する Windows ファイアウォール アクセスの構成  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の名前付きインスタンスは、指定した固定ポートまたは動的に割り当てられたポートをリッスンできます。動的に割り当てられたポートでは、SQL Server Browser サービスによって接続時現在のサービスの接続情報が提供されます。  
  
 SQL Server Browser サービスは TCP ポート 2382 でリッスンします。 UDP は使用されません。 TCP は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]で使用される唯一の転送プロトコルです。  
  
 次のアプローチのいずれかを使用して、Analysis Services の名前付きインスタンスへのリモート アクセスを有効にします。  
  
-   動的なポート割り当ておよび SQL Server Browser サービスを使用します。 SQL Server Browser サービスが使用するポートのブロックを Windows ファイアウォールで解除します。 次の形式でサーバーに接続します: \<servername >\\< instancename\>。  
  
-   固定ポートおよび SQL Server Browser サービスの両方を連携して使用します。 この方法では、\<servername >\\< instancename\>と同じ形式で接続できます。ただし、この場合、サーバーは固定ポートでリッスンする点が異なります。 このシナリオでは、SQL Server Browser Service は、固定ポートでリッスンしている Analysis Services のインスタンスに名前解決を提供します。 このアプローチを使用するには、サーバーを固定ポートでリッスンするように構成し、そのポートへのアクセスのブロックを解除して、SQL Server Browser サービスが使用するポートへのアクセスのブロックを解除します。  
  
 SQL Server Browser サービスは、名前付きインスタンスでのみ使用されます。既定のインスタンスで使用されることはありません。 サービスは、SQL Server の任意の機能が名前付きインスタンスとしてインストールされるときに、自動的にインストールされ有効になります。 SQL Server Browser サービスが必要なアプローチを選択する場合、サービスが使用するサーバーで有効になっていることと起動されていることを確認してください。  
  
 SQL Server Browser サービスが使用できない場合は、ドメイン名の解決をスキップし、接続文字列内で固定ポートを割り当てる必要があります。 SQL Server Browser サービスを使用しない場合は、すべてのクライアント接続に接続文字列 (AW-SRV01:54321 など) にあるポート番号が含まれている必要があります。  
  
 **オプション 1: 動的なポート割り当てを使用し、SQL Server Browser サービスへのアクセスのブロックを解除する**  
  
 Analysis Services の名前付きインスタンスに対する動的なポート割り当ては、サービスの起動時に、`MSOLAP$InstanceName` によって決定されます。 既定で、使用可能なポートのうち最も小さい番号のポートが要求され、サービスが再起動されるたびに異なるポート番号が使用されます。  
  
 インスタンス名の解決は、SQL Server Browser サービスによって処理されます。 名前付きインスタンスのある動的ポートの割り当てを使用している場合には、必ず、SQL Server Browser サービスの TCP ポート 2382 のブロックを解除する必要があります。  
  
> [!NOTE]  
>  SQL Server Browser サービスは、データベース エンジンに対応する UDP ポート 1434 と、Analysis Services に対応する TCP ポート 2382 をリッスンします。 SQL Server Browser サービス用に UDP ポート 1434 のブロックを既に解除している場合でも、Analysis Services 用に TCP ポート 2382 のブロックを解除する必要があります。  
  
#### <a name="windows-firewall-with-advanced-security"></a>セキュリティが強化された Windows ファイアウォール  
  
1.  Windows 7 または Windows Vista の場合、コントロール パネルの **[システムとセキュリティ]** をクリックした後、 **[Windows ファイアウォール]** 、 **[詳細設定]** の順にクリックします。 Windows Server 2008 または 2008 R2 の場合、管理ツールを開き、 **[セキュリティが強化された Windows ファイアウォール]** をクリックします。 Windows Server 2012 では、アプリケーション ページを開き、「 **Windows ファイアウォール**」と入力します。  
  
2.  SQL Server Browser サービスへのアクセスのブロックを解除するには、 **[受信の規則]** を右クリックし、 **[新しい規則]** をクリックします。  
  
3.  ルールの種類 で、`Port` をクリックし、**次へ** をクリックします。  
  
4.  プロトコルおよびポート で、 **TCP** を選択し、**特定のローカルポート** に「`2382`」と入力します。  
  
5.  [操作] で、 **[接続を許可する]** をクリックし、 **[次へ]** をクリックします。  
  
6.  [プロファイル] で、規則を適用しないネットワークの場所のチェック ボックスをオフにした後、 **[次へ]** をクリックします。  
  
7.  [名前] に、この規則のわかりやすい名前 (`SQL Server Browser Service (tcp-in) 2382`など) を入力し、 **[完了]** をクリックします。  
  
8.  リモート接続が有効になっていることを確認するには、別のコンピューターで SQL Server Management Studio または Excel を開き、サーバーのネットワーク名とインスタンス名を \<servername >\\< instancename\>という形式で指定して Analysis Services に接続します。 たとえば、名前付きインスタンス **Finance** のある **AW-SRV01** という名前の付けられたサーバーでは、サーバー名は **AW-SRV01\Finance** となります。  
  
 **オプション 2: 名前付きインスタンスに固定ポートを使用する**  
  
 または、固定ポートを割り当てた後で、そのポートへのアクセスのブロックを解除します。 このアプローチには、プログラムの実行ファイルへのアクセスを許可するよりも監査を実行しやすいというメリットがあります。 このため、Analysis Services の任意のインスタンスにアクセスする方法としては、固定ポートを使用するアプローチをお勧めします。  
  
 固定ポートを割り当てるには、このトピックの「 [Analysis Services の既定のインスタンスまたは名前付きインスタンスに対する固定ポートの使用](#bkmk_fixed) 」で説明する手順を実行してから、このセクションに戻ってポートのブロックを解除します。  
  
#### <a name="windows-firewall-with-advanced-security"></a>セキュリティが強化された Windows ファイアウォール  
  
1.  Windows 7 または Windows Vista の場合、コントロール パネルの **[システムとセキュリティ]** をクリックした後、 **[Windows ファイアウォール]** 、 **[詳細設定]** の順にクリックします。 Windows Server 2008 または 2008 R2 の場合、管理ツールを開き、 **[セキュリティが強化された Windows ファイアウォール]** をクリックします。 Windows Server 2012 では、アプリケーション ページを開き、「 **Windows ファイアウォール**」と入力します。  
  
2.  Analysis Services へのアクセスのブロックを解除するには、 **[受信の規則]** を右クリックし、 **[新しい規則]** をクリックします。  
  
3.  ルールの種類 で、`Port` をクリックし、**次へ** をクリックします。  
  
4.  [プロトコルおよびポート] で、 **[TCP]** をクリックし、 **[特定のローカル ポート]** に固定ポートの番号を入力します。  
  
5.  [操作] で、 **[接続を許可する]** をクリックし、 **[次へ]** をクリックします。  
  
6.  [プロファイル] で、規則を適用しないネットワークの場所のチェック ボックスをオフにした後、 **[次へ]** をクリックします。  
  
7.  [名前] に、この規則のわかりやすい名前 (`SQL Server Analysis Services on port 54321`など) を入力し、 **[完了]** をクリックします。  
  
8.  リモート接続が有効になっていることを確認するには、別のコンピューターで SQL Server Management Studio または Excel を開き、サーバーのネットワーク名とポート番号を次の形式で指定して Analysis Services に接続します。 \<servername >:\<のポート番号 >。  
  
#### <a name="netsh-advfirewall-syntax"></a>Netsh AdvFirewall 構文  
  
-   次のコマンドにより、SQL Server Browser サービス用の TCP 2382 のブロックを解除する受信の規則と、Analysis Services インスタンス用に指定された固定ポートのブロックを解除する受信の規則が作成されます。 これらのうちのいずれかを実行すると Analysis Services の名前付きインスタンスにアクセスできるようにできます。  
  
     このサンプル コマンドの場合、ポート 54321 が固定ポートです。 実際のシステムで使用する場合、このポートを実際のポート番号に置き換えてください。  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Analysis Services (tcp-in) on 54321" dir=in action=allow protocol=TCP localport=54321 profile=domain  
    ```  
  
    ```  
    netsh advfirewall firewall add rule name="SQL Server Browser Services inbound on TCP 2382" dir=in action=allow protocol=TCP localport=2382 profile=domain  
    ```  
  
##  <a name="bkmk_fixed"></a> Analysis Services の既定のインスタンスまたは名前付きインスタンスに対する固定ポートの使用  
 ここでは、固定ポートをリッスンするように Analysis Services を構成する方法について説明します。 Analysis Services を名前付きインスタンスとしてインストールしている場合、一般的に固定ポートが使用されます。ただし、ビジネス要件またはセキュリティ要件によって既定でないポート割り当てを使用するように指定されている場合、このアプローチを使用することができます。  
  
 固定ポートを使用すると、サーバー名にポート番号を付加する必要があるため、既定のインスタンス用の接続構文が変わることに注意してください。 たとえば、SQL Server Management Studio で、ポート 54321 をリッスンしている Analysis Services のローカルな既定のインスタンスに接続するには、Management Studio の [サーバーへの接続] ダイアログ ボックスにサーバー名として「localhost:54321」と入力する必要があります。  
  
 名前付きインスタンスを使用している場合は、固定ポートを割り当てて、サーバー名の指定方法を変更することはできません (具体的には \<servername\instancename > を使用して、固定ポートでリッスンする名前付きインスタンスに接続できます)。 このアプローチは、SQL Server Browser サービスが実行されており、サービスがリッスンしているポートのブロックが解除されている場合のみに使用できます。 SQL Server Browser サービスは \<servername\instancename > に基づいて固定ポートへのリダイレクトを提供します。 SQL Server Browser サービスと、固定ポートをリッスンする Analysis Services の名前付きインスタンスの両方に対してポートを開いている限り、SQL Server Browser サービスによって名前付きインスタンスへの接続が解決されます。  
  
1.  使用可能な TCP/IP ポートから、使用するポートを決定します。  
  
     使用が禁止されている予約済みポートと登録済みポートの一覧については、IANA の「 [Port Numbers](https://go.microsoft.com/fwlink/?LinkID=198469)」 (ポート番号) を参照してください。 システムで既に使用されているポートを確認するには、コマンド プロンプト ウィンドウを開き、「`netstat -a -p TCP`」と入力すると、システム内で開かれている TCP ポートの一覧が表示されます。  
  
2.  使用するポートを決定した後、msmdsrv.ini ファイルまたは SQL Server Management Studio の Analysis Services インスタンスの [全般プロパティ] ページで、`Port` 構成設定を編集して、ポートを指定します。  
  
3.  サービスを再起動します。  
  
4.  Windows ファイアウォールを構成して、指定した TCP ポートのブロックを解除します。 名前付きインスタンスに固定ポートを使用する場合は、そのインスタンスに指定した TCP ポートと、SQL Server Browser サービスで使用される TCP ポート 2382 の両方のブロックを解除します。  
  
5.  接続を検証します。それには、Management Studio を使用してローカルで接続した後、別のコンピューターのクライアント アプリケーションからリモートで接続します。 Management Studio を使用するには、次の形式でサーバー名を指定して Analysis Services の既定のインスタンスに接続します: \<servername >:\<ポート番号 >。 名前付きインスタンスの場合は、サーバー名を \<servername >\\< instancename\>として指定します。  
  
##  <a name="bkmk_cluster"></a> Analysis Services クラスターのポートの構成  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] フェールオーバー クラスターは、既定のインスタンスまたは名前付きインスタンスとしてインストールされているかどうかにかかわらず、常に TCP ポート 2383 でリッスンします。 動的なポート割り当ては、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では使用されません (Windows フェールオーバー クラスターにインストールされている場合)。 クラスターで [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] を実行しているすべてノードの TCP 2383 を開く必要があります。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のクラスター化の詳細については、「 [SQL Server Analysis Services をクラスター化する方法](https://go.microsoft.com/fwlink/p/?LinkId=396548)」を参照してください。  
  
##  <a name="bkmk_powerpivot"></a>PowerPivot for SharePoint のポート構成  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] に対応するサーバー アーキテクチャは、使用する SharePoint のバージョンによって大きく異なります。  
  
 **SharePoint 2013**  
  
 SharePoint 2013 では、Excel Services が Power Pivot データ モデルに対する要求をリダイレクトし、ついでその要求は、SharePoint 環境外にある [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに読み込まれます。 接続は一般的なパターンに従い、ローカル コンピューター上にある Analysis Services クライアント ライブラリが、同じネットワーク上にあるリモートの [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスに接続要求を送信します。  
  
 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] によって [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] が必ず名前付きインスタンスとしてインストールされるため、SQL Server Browser サービスと動的ポートの割り当てを想定する必要があります。 既に説明したように、SQL Server Browser サービスは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] の名前付きインスタンス宛てに送信される接続要求を TCP ポート 2382 でリッスンし、その要求を現在のポートにリダイレクトします。  
  
 SharePoint 2013 内の Excel Services が、固定ポートを使用した接続構文をサポートしないことに注意して、SQL Server Browser サービスがアクセス可能になるようにしてください。  
  
 **SharePoint 2010**  
  
 SharePoint 2010 を使用している場合は、Windows ファイアウォールのポートを開く必要はありません。 SharePoint は、自らが必要としているポートを開き、また PowerPivot for SharePoint のようなアドインは SharePoint 環境内で動作します。 PowerPivot for SharePoint 2010 のインストールでは、PowerPivot System サービスによって、同じコンピューターにインストールされているローカルの SQL Server Analysis Services (PowerPivot) サービス インスタンスが排他的に使用されます。 ローカルの Analysis Services エンジン サービスへのアクセスには、ネットワーク接続ではなくローカル接続が使用されます。このサービスは、SharePoint サーバー上の PowerPivot データの読み込み、クエリ、および処理を行います。 クライアントアプリケーションから PowerPivot データを要求するには、SharePoint セットアップによって開かれたポートを介して要求がルーティングされます (具体的には、sharepoint-80、SharePoint サーバーの全体管理 v4、SharePoint Web サービスへのアクセスを許可するために受信の規則が定義されています)。、、および SPUserCodeV4)。 PowerPivot Web サービスは SharePoint ファーム内で実行されるため、SharePoint ファーム内の PowerPivot データへのリモート アクセスには SharePoint のファイアウォール規則で十分です。  
  
## <a name="see-also"></a>参照  
 [SQL Server Browser サービス &#40;データベース エンジンと SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)   
 [データベース エンジン、SQL Server エージェント、SQL Server Browser サービスの開始、停止、一時停止、再開、および再起動](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [データベース エンジン アクセスを有効にするための Windows ファイアウォールを構成する](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
  
  
