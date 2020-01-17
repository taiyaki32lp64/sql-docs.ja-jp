---
title: ネットワーク負荷分散クラスターにおけるレポート サーバーの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], network load balancing
ms.assetid: 6bfa5698-de65-43c3-b940-044f41c162d3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bff66ca0f644f862b7cdcfb534b55c4e8ebdd888
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104088"
---
# <a name="configure-a-report-server-on-a-network-load-balancing-cluster"></a>ネットワーク負荷分散クラスターにおけるレポート サーバーの構成
  レポート サーバーのスケールアウトをネットワーク負荷分散 (NLB) クラスターで実行するように構成する場合は、次の操作を行う必要があります。  
  
-   仮想サーバーの IP アドレスにマップされる仮想サーバー名を使用して NLB クラスターにアクセスできることを確認します。 仮想サーバー名は、NLB クラスターに対して単一のエントリ ポイントを構成できるようにするために必要です。 各レポート サーバー インスタンスの URL を構成するときに、仮想サーバー名をホストとして指定します。  
  
-   対話型レポートを表示できるようにビュー ステート検証を構成します。 対話型レポートは、通常、ユーザーの操作に応じて新しいデータやさまざまなデータをビジュアル化するために単一のユーザー セッション中に何回も表示されます。 ビュー ステート検証を構成すると、どのレポート サーバーで実際の要求を処理するかに関係なく、ユーザー セッション中の継続性が維持されます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、スケールアウト配置の負荷分散機能や共有 URL を使用した単一のアクセス ポイントの定義機能は用意されていません。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] スケールアウト配置をサポートする別のソフトウェアまたはハードウェア NLB クラスター ソリューションを実装する必要があります。  
  
 既に NLB クラスターの一部であるノードに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をインストールするか、まずスケールアウト配置を構成してからクラスター ソフトウェアをインストールすることができます。  
  
## <a name="steps-for-report-server-deployment-on-an-nlb-cluster"></a>NLB クラスターでのレポート サーバー配置の手順  
 配置をインストールして構成するには、次のガイドラインに従ってください。  
  
|手順|説明|詳細情報|  
|----------|-----------------|----------------------|  
|1|NLB クラスター内のサーバー ノードに Reporting Services をインストールする前に、スケールアウト配置の要件を確認します。|[ネイティブ モード レポート サーバーのスケール アウト配置構成&#40;SSRS 構成マネージャー&#41; ](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブック|  
|2|NLB クラスターを構成し、正常に動作することを確認します。<br /><br /> 必ずホスト ヘッダー名を NLB クラスターの仮想サーバー IP にマップしてください。 ホスト ヘッダー名は、レポート サーバーの URL で使用されます。IP アドレスに比べて容易に記憶でき、入力も簡単です。|詳細については、実行する Windows オペレーティング システムのバージョンの Windows Server の製品マニュアルを参照してください。|  
|3|Windows レジストリに格納されている **BackConnectionHostNames** のリストに、ホスト ヘッダーの完全修飾ドメイン名 (FQDN) および NetBIOS 名を追加します。 」の手順に従って**方法 2。ホスト名を指定**で[KB 896861](https://support.microsoft.com/kb/896861) (https://support.microsoft.com/kb/896861) 、次のように調整します。 サポート技術情報の資料の「レジストリ エディターを終了し、IISAdmin サービスを再開します」という**手順 7** の 代わりに、変更が有効になるようにコンピューターを再起動します。<br /><br /> たとえば、ホスト ヘッダー名 \<MyServer> が Windows コンピューター名 "contoso" の仮想名である場合は、FQDN 形式を "contoso.domain.com" として参照できる可能性があります。 ホスト ヘッダー名 (MyServer) と FQDN 名 (contoso.domain.com) の両方を **BackConnectionHostNames**の一覧に追加する必要があります。|この手順は、サーバー環境のローカル コンピューターで NTLM 認証が行われていて、ループ バック接続が作成されている場合に必要になります。<br /><br /> この場合、レポート マネージャーとレポート サーバー間の要求が 401 (権限がありません) で失敗します。|  
|4|既に NLB クラスターの一部であるノードにファイルのみのモードで [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をインストールし、スケールアウト配置のレポート サーバー インスタンスを構成します。<br /><br /> ここで構成したスケールアウトでは、仮想サーバー IP に送信される要求に応答できない場合があります。 仮想サーバー IP を使用するようにスケールアウトを構成する手順は、この後でビュー ステート検証を構成してから行います。|[ネイティブ モード レポート サーバーのスケールアウト配置の構成 (SSRS 構成マネージャー)](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)|  
|5|ビュー ステート検証を構成します。<br /><br /> 最適な結果を得るには、この手順は、スケールアウト配置を構成した後、仮想サーバー IP を使用するようにレポート サーバー インスタンスを構成する前に行います。 ビュー ステート検証を先に構成することによって、ユーザーによる対話型レポートへのアクセス時に、ステート検証の失敗に関する例外を回避できます。|このトピックの「[ビュー ステート検証を構成する方法](#ViewState) 」|  
|6|NLB クラスターの仮想サーバー IP を使用するように `Hostname` と `UrlRoot` を構成します。|このトピックの「[Hostname と UrlRoot を構成する方法](#SpecifyingVirtualServerName) 」|  
|7|指定したホスト名でサーバーにアクセスできることを確認します。|このトピックの「[レポート サーバーへのアクセスの確認](#Verify) 」|  
  
##  <a name="ViewState"></a> ビュー ステート検証を構成する方法  
 NLB クラスターでスケールアウト配置を運用するには、ユーザーが対話型の HTML レポートを表示できるように、ビュー ステート検証を構成する必要があります。 この構成をレポート サーバーとレポート マネージャーについて行う必要があります。  
  
 ビュー ステート検証は、ASP.NET によって制御されます。 既定では、ビュー ステート検証は有効であり、Web サービスの ID を使用して検証を行います。 ただし、NLB クラスターのシナリオでは、異なるコンピューターで実行される複数のサービス インスタンスと Web サービス ID が存在します。 サービス ID はノードにより異なるので、単一のプロセス ID に依存して検証を行うことはできません。  
  
 この問題を回避するために、ビュー ステート検証をサポートする任意の検証キーを生成してから、同じキーを使用するように各レポート サーバー ノードを手動で構成することができます。 ランダムに生成される任意の 16 進数のシーケンスを使用できます。 検証アルゴリズム (SHA1 など) によって、16 進数のシーケンスの必要な長さが決まります。  
  
1.  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]により提供される自動生成機能を使用して、検証キーと暗号化解除キーを生成します。 最後に、1 つがあります <`machineKey`> エントリをスケール アウト配置内の各レポート マネージャー インスタンスの Web.config ファイルに貼り付けることができます。  
  
     次の例は、取得する必要がある値を示しています。 例を構成ファイルにコピーしないでください。このキーの値は有効ではありません。  
  
    ```  
    <machineKey validationKey="123455555" decryptionKey="678999999" validation="SHA1" decryption="AES"/>  
    ```  
  
2.  レポート マネージャーのとでは、Web.config ファイルを開き、<`system.web`> セクションに貼り付けます、<`machineKey`> 生成した要素。 既定では、レポート マネージャーの Web.config ファイルは、\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportManager\Web.config にあります。  
  
3.  ファイルを保存します。  
  
4.  スケールアウト配置内の各レポート サーバーに対し、前の手順を繰り返します。  
  
5.  \Reporting Services\Report Manager フォルダー内のすべての Web.Config ファイルに同一であることを確認 <`machineKey`> 内の要素、<`system.web`> セクション。  
  
##  <a name="SpecifyingVirtualServerName"></a> Hostname と UrlRoot を構成する方法  
 NLB クラスターでレポート サーバー スケールアウト配置を構成するには、サーバー クラスターへの単一のアクセス ポイントとして 1 つの仮想サーバー名を定義する必要があります。 次に、この仮想サーバー名を使用環境のドメイン ネーム サーバー (DNS) に登録します。  
  
 仮想サーバー名を定義したら、レポート サーバーの URL にその仮想サーバー名を含めるよう、RSReportServer.config ファイル内の `Hostname` プロパティと `UrlRoot` プロパティを構成できます。  
  
 レポート環境でワイルドカードの URL 予約を使用している場合は、`Hostname` プロパティを構成します。 `Hostname` プロパティを NLB サーバーの仮想サーバー名になるように指定すると、レポート環境のネットワーク トラフィックが NLB サーバーに送信されます。 NLB はレポート サーバー ノード間に要求を分散します。  
  
 さらに、Excel や PDF などの形式で静的レポートにエクスポートされたレポート、または電子メール サブスクリプションなどのサブスクリプションで生成されるレポートでレポート リンクが動作するよう、`UrlRoot` プロパティを構成します。  
  
 統合する場合[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]で[!INCLUDE[winSPServ](../../includes/winspserv-md.md)]3.0 または[!INCLUDE[offSPServ](../../includes/offspserv-md.md)]2007、またはカスタムの Web アプリケーションでレポートをホストする、のみを構成する必要があります、`UrlRoot`プロパティ。 この場合、`UrlRoot` プロパティを SharePoint サイトまたは Web アプリケーションの URL になるように構成します。 これにより、レポート環境のネットワーク トラフィックが、レポート サーバーまたは NLB クラスターではなく、レポートを処理するアプリケーションに送信されます。  
  
 `ReportServerUrl` は変更しないでください。 この URL を変更すると、内部要求を処理するたびに仮想サーバーとの余分なやり取りが発生します。 詳細については、「[構成ファイル内の URL (SSRS 構成マネージャー)](../install-windows/urls-in-configuration-files-ssrs-configuration-manager.md)」を参照してください。 構成ファイルの編集方法の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「[Reporting Services の構成ファイル (RSreportserver.config) の変更」](modify-a-reporting-services-configuration-file-rsreportserver-config.md)を参照してください。  
  
1.  テキスト エディターで RSReportServer.config を開きます。  
  
2.  検索、 **\<サービス >** セクションし、構成ファイルに次の情報を追加交換、`Hostname`値を NLB サーバーの仮想サーバー名。  
  
    ```  
    <Hostname>virtual_server</Hostname>  
    ```  
  
3.  `UrlRoot` を探します。 要素は、構成ファイルで指定されていませんが、使用される既定値は次の形式で URL: http:// または https://\<*computername*>/\<*reportserver*> ここで、 \< *reportserver*> はレポート サーバー Web サービスの仮想ディレクトリ名です。  
  
4.  値を入力`UrlRoot`この形式で、クラスターの仮想名を含む: http:// または https://\<*virtual_server*>/\<*reportserver*>。  
  
5.  ファイルを保存します。  
  
6.  スケールアウト配置内の各レポート サーバーの RSReportServer.config ファイルごとに、これらの手順を繰り返します。  
  
##  <a name="Verify"></a> レポート サーバーへのアクセスの確認  
 仮想サーバーの名前を使って、スケール アウト配置にアクセスできることを確認します (たとえば、 https://MyVirtualServerName/reportserver と https://MyVirtualServerName/reports) します。  
  
 レポート サーバーのログ ファイルを参照するか、または RS の実行ログを確認して、どのノードが実際にレポートを処理しているのかを確認できます (実行ログ テーブルには、 **InstanceName** という列があり、特定の要求がどのインスタンスによって処理されたのかを示しています)。 詳細については、 [オンライン ブックの「](../report-server/reporting-services-log-files-and-sources.md) Reporting Services のログ ファイルとソース [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
 レポート サーバーに接続できない場合は、NLB を調べて、要求がレポート サーバーに送信されていることを確認し、レポート サーバーの HTTP ログを表示して、サーバーが要求を受信していることを確認します。  
  
#### <a name="troubleshooting-failed-requests"></a>失敗した要求のトラブルシューティング  
 要求がレポート サーバー インスタンスに到達しない場合は、RSReportServer.config ファイルを調べて、仮想サーバー名がレポート サーバーの URL のホスト名として指定されていることを確認します。  
  
1.  テキスト エディターで RSReportServer.config ファイルを開きます。  
  
2.  検索 <`Hostname`>、<`ReportServerUrl`>、および <`UrlRoot`>、各設定のホスト名を確認します。 値が意図したホスト名でない場合は、正しいホスト名に置き換えます。  
  
 これらの変更を行った後、Reporting Services 構成ツールを開始する場合、ツールを変更する可能性があります、<`ReportServerUrl`> 既定値に設定します。 使用する設定を含むバージョンに置き換える必要がある場合に備えて、常にバックアップ コピーを作成しておく必要があります。  
  
## <a name="see-also"></a>参照  
 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../install-windows/configure-a-url-ssrs-configuration-manager.md)   
 [ネイティブ モード レポート サーバーのスケールアウト配置の構成 (SSRS 構成マネージャー)](../install-windows/configure-a-native-mode-report-server-scale-out-deployment.md)   
 [Reporting Services ネイティブ モードのレポート サーバーの管理](manage-a-reporting-services-native-mode-report-server.md)  
  
  
