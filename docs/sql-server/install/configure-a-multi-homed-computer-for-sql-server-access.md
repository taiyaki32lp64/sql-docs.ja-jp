---
title: SQL Server アクセス用のマルチホーム コンピューターの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], multi-homed computer
- multi-homed computer [SQL Server] configuring ports
- firewall systems [Database Engine], multi-homed computer
ms.assetid: ba369e5b-7d1f-4544-b7f1-9b098a1e75bc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4a024707b5fa7ab70394a068ed47110898ae0518
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126220"
---
# <a name="configure-a-multi-homed-computer-for-sql-server-access"></a>SQL Server アクセス用のマルチホーム コンピューターの構成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  サーバーが複数のネットワークまたはネットワーク サブネットへの接続を提供する必要がある場合、一般的なシナリオではマルチホーム コンピューターを使用します。 通常、このコンピューターは、境界ネットワーク (DMZ、非武装地帯、またはスクリーン サブネットとも呼ばれます) にあります。 この記事では、マルチホーム環境内の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへのネットワーク接続用に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とセキュリティが強化された Windows ファイアウォールを構成する方法について説明します。  
  
> [!NOTE]  
>  マルチホーム コンピューターには複数のネットワーク アダプターがあるか、または 1 つのネットワーク アダプターに複数の IP アドレスを使用するように構成されています。 デュアルホーム コンピューターには 2 つのネットワーク アダプターがあるか、または 1 つのネットワーク アダプターに 2 つの IP アドレスを使用するように構成されています。  
  
 この記事を続行する前に、「[SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」の記事の説明をよく理解してください。 この記事には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントがファイアウォールと連携して動作する方法に関する基本的な情報が含まれています。  
  
 **この例の前提条件は、次のとおりです。**  
  
-   コンピューターに 2 つのネットワーク アダプターがインストールされています。 1 つ以上のネットワーク アダプターをワイヤレスにすることができます。 2 つのネットワーク アダプターをシミュレートするには、1 つ目のネットワーク アダプターの IP アドレスを使用してから、2 つ目のネットワーク アダプターとしてループバック IP アドレス (127.0.0.1) を使用します。  
  
-   簡単にするため、この例では IPv4 アドレスを使用します。 IPv6 アドレスを使用しても、同じ手順を実行できます。  
  
    > [!NOTE]  
    >  IPv4 アドレスは、オクテットと呼ばれる一連の 4 つの数字です。 各数字は、ピリオドで区切られた 255 より小さい数字です (127.0.0.1 など)。 IPv6 アドレスは、コロンで区切られた一連の 8 つの 16 進数です (fe80:4898:23:3:49a6:f5c1:2452:b994 など)。  
  
-   ファイアウォール ルールでは、特定のポート (ポート 1433 など) を経由したアクセスを許可できます。 または、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] プログラム (sqlservr.exe) へのアクセスを許可できます。 どちらのメソッドもあまりよくありません。 境界ネットワーク内のサーバーはイントラネット上のサーバーよりも攻撃に対して脆弱なので、この記事では、より正確に制御し、開くポートを個別に選択する場合を前提とします。 そのため、この記事では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が固定ポートでリッスンするように構成することを前提とします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用するポートの詳細については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」をご参照ください。  
  
-   次の例では、TCP ポート 1433 を使用して [!INCLUDE[ssDE](../../includes/ssde-md.md)] へのアクセスを構成します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントが異なる他のポートは、同じ一般的な手順を使用して構成できます。  
  
 **この例の一般的な手順は、次のとおりです。**  
  
-   コンピューターの IP アドレスを特定します。  
  
-   特定の TCP ポートでリッスンするように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を構成します。  
  
-   セキュリティが強化された Windows ファイアウォールを構成します。  
  
## <a name="optional-procedures"></a>省略可能な手順  
 コンピューターで使用可能で、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で使用されている IP アドレスが既にわかっている場合、これらの手順をスキップできます。  
  
#### <a name="to-determine-the-ip-addresses-available-on-the-computer"></a>コンピューターで使用可能な IP アドレスを特定するには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているコンピューターで、 **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックします。次に、 **「cmd」** と入力して、 [!INCLUDE[clickOK](../../includes/clickok-md.md)]。  
  
2.  コマンド プロンプト ウィンドウで、「 **ipconfig,** 」と入力し、Enter キーを押してこのコンピューターで使用可能な IP アドレスを一覧表示します。  
  
    > [!NOTE]  
    >  **ipconfig** コマンドを使用すると、切断されている接続を含む使用可能な多くの接続が一覧表示される場合があります。 **ipconfig** コマンドは、IPv4 アドレスと IPv6 アドレスの両方を一覧表示します。  
  
3.  使用中の IPv4 アドレスおよび IPv6 アドレスに注意してください。 一時アドレス、サブネット マスク、既定のゲートウェイなど一覧内の他の情報は、TCP/IP ネットワークを構成する際の重要な情報です。 ただし、この情報はこの例では使用されません。  
  
#### <a name="to-determine-the-ip-addresses-and-ports-used-by-includessnoversionincludesssnoversion-mdmd"></a>使用される IP アドレスおよびポートを特定するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、[ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]]、 **[構成ツール]** の順にポイントして、 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [構成マネージャー]** をクリックします。  
  
2.  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]構成マネージャー**のコンソール ペインで、 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][ネットワークの構成]** 、 **[\<instance name> のプロトコル]** を順に展開し、 **[TCP/IP]** をダブルクリックします。  
  
3.  **[TCP/IP のプロパティ]** ダイアログ ボックスの **[IP アドレス]** タブに、 **IP1**、 **IP2**という形式で **IPAll**まで IP アドレスが表示されます。 このうちいずれかが、ループバック アダプターの IP アドレス 127.0.0.1 です。 追加の IP アドレスがコンピューターで構成される各 IP アドレスとして表示されます。  
  
4.  IP アドレスについて、 **[TCP 動的ポート]** ダイアログ ボックスに **0**が表示されている場合、これは [!INCLUDE[ssDE](../../includes/ssde-md.md)] が動的ポートでリッスンしていることを示しています。 この例では、再起動時に変わる可能性のある動的ポートではなく、固定ポートを使用します。 したがって、 **[TCP 動的ポート]** ダイアログ ボックスに **0**が表示されている場合は、0 を削除します。  
  
5.  構成する各 IP アドレスについて TCP ポートが一覧表示されます。 この例では、両方の IP アドレスが既定のポート 1433 でリッスンしているとします。  
  
6.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用可能なポートの一部を使用しない場合、 **[プロトコル]** タブで、 **[すべて受信待ち]** 値を **[いいえ]** に変更し、 **[IP アドレス]** タブで、使用しない IP アドレスの **[アクティブ]** 値を **[いいえ]** に変更します。  
  
## <a name="configuring-windows-firewall-with-advanced-security"></a>セキュリティが強化された Windows ファイアウォールの構成  
 コンピューターで使用される IP アドレスと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用されるポートを確認した後、ファイアウォール ルールを作成して、特定の IP アドレス用にそれらのルールを構成できます。  
  
#### <a name="to-create-a-firewall-rule"></a>ファイアウォール ルールを作成するには  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされているコンピューターで、管理者としてログオンします。  
  
2.  **[スタート]** をクリックし、 **[ファイル名を指定して実行]** をクリックします。次に、「 **wf.msc**」と入力して、 **[OK]** をクリックします。  
  
3.  **[ユーザー アカウント制御]** ダイアログ ボックスの **[続行]** をクリックし、管理者資格情報を使用して、セキュリティが強化された Windows ファイアウォールのスナップインを開きます。  
  
4.  **[概要]** ページで、Windows ファイアウォールが有効であることを確認します。  
  
5.  左側のペインで、 **[受信の規則]** をクリックします。  
  
6.  **[受信の規則]** を右クリックし、 **[新しい規則]** をクリックして、 **新規の受信の規則ウィザード**を開きます。  
  
7.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プログラムのルールを作成できます。 ただし、この例では固定ポートを使用しているので、 **[ポート]** を選択して **[次へ]** をクリックします。  
  
8.  **[プロトコルおよびポート]** ページで、 **[TCP]** を選択します。  
  
9. **[指定したローカル ポート]** を選択します。 コンマで区切ったポート番号を入力して、 **[次へ]** をクリックします。 この例では、既定のポートを構成するので、「 **1433**」と入力します。  
  
10. **[アクション]** ページで、オプションを確認します。 この例では、セキュリティで保護された接続を指定するためにファイアウォールを使用しません。 したがって、 **[接続を許可する]** 、 **[次へ]** を順にクリックします。  
  
    > [!NOTE]  
    >  環境で、セキュリティで保護された接続が必要な場合があります。 セキュリティで保護された接続のオプションのいずれかを選択すると、証明書および **[強制的に暗号化]** オプションの構成が必要な場合があります。 セキュリティで保護された接続の詳細については、「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」および「[データベース エンジンへの暗号化接続の有効化 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。  
  
11. **[プロファイル]** ページで、ルールに対して 1 つ以上のプロファイルを選択します。 ファイアウォール プロファイルの詳細を確認するには、ファイアウォール プログラムの **[プロファイルの詳細を表示します]** リンクをクリックします。  
  
    -   コンピューターがサーバーであり、ドメインに接続されているときのみ使用可能な場合は、 **[ドメイン]** を選択して、 **[次へ]** をクリックします。  
  
    -   コンピューターがモバイル コンピューターである場合 (たとえば、ラップトップ)、別のネットワークに接続するとき複数のプロファイルを使用する可能性があります。 モバイル コンピューターの場合、別のプロファイル用に別のアクセス機能を構成できます。 たとえば、コンピューターがドメイン プロファイルを使用する場合はアクセスを許可し、パブリック プロファイルを使用する場合はアクセスを許可しないようにすることができます。  
  
12. **[名前]** ページで、ルールの名前および説明を指定して、 **[完了]** をクリックします。  
  
13. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用する IP アドレスごとに別のルールを作成するには、この手順を繰り返します。  
  
 1 つ以上のルールを作成した後、ルールを使用するコンピューターで各 IP アドレスを構成するには、次の手順を実行します。  
  
#### <a name="to-configure-the-firewall-rule-for-a-specific-ip-addresses"></a>特定の IP アドレス用にファイアウォール ルールを構成するには  
  
1.  **[セキュリティが強化された Windows ファイアウォール]** の **[受信の規則]** ページで、作成したルールを右クリックして、 **[プロパティ]** をクリックします。  
  
2.  **[規則のプロパティ]** ダイアログ ボックスで、 **[スコープ]** タブをクリックします。  
  
3.  **[ローカル IP アドレス]** 領域で **[これらの IP アドレス]** を選択して、 **[追加]** をクリックします。  
  
4.  **[IP アドレス]** ダイアログ ボックスで **[この IP アドレスまたはサブネット]** を選択して、構成する IP アドレスのいずれかを入力します。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  **[リモート IP アドレス]** 領域で **[これらの IP アドレス]** を選択して、 **[追加]** をクリックします。  
  
7.  **[IP アドレス]** ダイアログ ボックスを使用して、コンピューター上の選択した IP アドレス用に接続を構成します。 指定した IP アドレス、IP アドレスの範囲、サブネット全体、または特定のコンピューターからの接続を有効にすることができます。 このオプションを正しく構成するには、ネットワークをよく理解しておく必要があります。 ネットワークの詳細については、ネットワーク管理者にお問い合わせください。  
  
8.  **[IP アドレス]** ダイアログ ボックスを閉じるには、 **[OK]** をクリックします。次に **[OK]** をクリックして **[規則のプロパティ]** ダイアログ ボックスを閉じます。  
  
9. マルチホーム コンピューターで他の IP アドレスを構成するには、別の IP アドレスと別のルールを使用して、この手順を繰り返します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Browser サービス &#40;データベース エンジンと SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)   
 [プロキシ サーバーを介して SQL Server に接続する方法 &#40;SQL Server 構成マネージャー&#41;](../../database-engine/configure-windows/connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager.md)  
  
  
