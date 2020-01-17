---
title: インターネットインフォメーションサービス (IIS) 8.0 で Analysis Services への HTTP アクセスを構成します。Microsoft Docs
ms.custom: ''
ms.date: 06/19/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: cf2e2c84-0a69-4cdd-90a1-fb4021936513
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f4f911ebf60852fd4ab11c5813fc567deb2d0c87
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75225399"
---
# <a name="configure-http-access-to-analysis-services-on-internet-information-services-iis-80"></a>インターネット インフォメーション サービス (IIS) 8.0 上の Analysis Services への HTTP アクセスの構成
  この記事では、Analysis Services インスタンスにアクセスするために HTTP エンドポイントを設定する方法について説明します。 HTTP アクセスを有効にするには、MSMDPUMP.dll を構成します。MSMDPUMP.dll は、インターネット インフォメーション サービス (IIS) で実行され、クライアント アプリケーションと Analysis Services サーバーの間で双方向にデータをポンプする ISAPI 拡張機能です。 この方法は、BI ソリューションが次の機能を必要とする場合に、Analysis Services への接続の代わりに使用できます。  
  
-   クライアント アクセスが、有効にできるポートに制限があるインターネット接続またはエクストラネット接続を経由して接続する。  
  
-   クライアント接続が同じネットワーク内の信頼されていないドメインからの接続である。  
  
-   HTTP 接続は許可されているが TCP/IP 接続が許可されていないネットワーク環境でクライアント アプリケーションが実行される。  
  
-   クライアント アプリケーションが Analysis Services クライアント ライブラリを使用できない (UNIX サーバーで実行されている Java アプリケーションなど)。 データ アクセスに Analysis Services クライアント ライブラリを使用できない場合は、Analysis Services インスタンスへの HTTP 直接接続で SOAP および XML/A を使用できます。  
  
-   Windows 統合セキュリティ以外の認証メソッドが必要である。 つまり、HTTP アクセス用に Analysis Services を構成する際に、匿名接続および基本認証を使用できる。 ダイジェスト認証、フォーム認証、および ASP.NET 認証はサポートされていません。 基本認証の要件は、HTTP アクセスを有効にするための主な理由の 1 つです。 詳細については、「 [Microsoft BI 認証と ID 委任](https://go.microsoft.com/fwlink/?LinkId=286576)」を参照してください。  
  
 テーブル モードまたは多次元モードのいずれかを実行する Analysis Services のサポートされているすべてのバージョンまたはエディションで、HTTP アクセスを構成することができます。 ローカル キューブは例外です。 HTTP エンドポイントを介してローカル キューブに接続することはできません。  
  
 HTTP アクセスの設定は、インストール後のタスクです。 HTTP アクセス用に構成する前に、Analysis Services をインストールする必要があります。 Analysis Services 管理者として、HTTP アクセスを可能にする前に、Windows アカウントへのアクセス許可を付与する必要があります。 また、それ以上サーバーを構成する前に、インストールを検証すること (完全に機能することの確認) をお勧めします。 HTTP アクセスを構成したら、HTTP エンドポイントと、TCP/IP 上のサーバーの通常のネットワーク名の両方を使用できます。 HTTP アクセスを設定しても、データ アクセスのためのその他のアプローチは無効にされません。  
  
 MSMDPUMP 構成で先に進む際、client-to-IIS と IIS-to-SSAS の 2 つの接続を考慮する必要があることに注意してください。 この記事の手順では、IIS と SSAS の間の接続を扱います。 IIS に接続するには、クライアント アプリケーションで追加の構成が必要になる場合があります。 SSL を使用するかどうか、バインドをどのように構成するかなどの決定については、この記事では扱いません。 IIS の詳細については、「 [Web サーバー (IIS) の概要](https://technet.microsoft.com/library/hh831725.aspx) 」を参照してください。  
  
 このトピックには、次のセクションが含まれています。  
  
-   [概要](#bkmk_overview)  
  
-   [前提条件](#bkmk_prereq)  
  
-   [MSMDPUMP を Web サーバー上のフォルダーにコピーします。](#bkmk_copy)  
  
-   [IIS でアプリケーションプールと仮想ディレクトリを作成する](#bkmk_appPool)  
  
-   [IIS 認証の構成と拡張機能の追加](#bkmk_auth)  
  
-   [MSMDPUMP を編集します。ターゲットサーバーを設定する INI ファイル](#bkmk_edit)  
  
-   [構成をテストする](#bkmk_test)  
  
##  <a name="bkmk_overview"></a>概要  
 MSMDPUMP は、IIS に読み込まれ、ローカルまたはリモートの Analysis Services インスタンスへのリダイレクトを提供する ISAPI 拡張機能です。 この ISAPI 拡張機能を構成して、Analysis Services インスタンスへの HTTP エンドポイントを作成します。  
  
 HTTP エンドポイントごとに 1 個の仮想ディレクトリを作成し、構成する必要があります。 接続先の Analysis Services インスタンスごとに、各エンドポイントに独自の MSMDPUMP ファイル セットが必要になります。 このファイル セット内の構成ファイルで、各 HTTP エンドポイントに使用される Analysis Services インスタンスの名前を指定します。  
  
 IIS では、MSMDPUMP は、Analysis Services OLE DB プロバイダーを使用して、TCP/IP 経由で Analysis Services に接続します。 クライアントの要求は、ドメインの信頼関係の外部で発生する可能性がありますが、ネイティブ接続を成功させるには、Analysis Services と IIS の両方が同じドメイン内または信頼されたドメイン内に存在する必要があります。  
  
 MSMDPUMP が Analysis Services に接続するときには、Windows のユーザー ID を使用して接続を行います。 このアカウントは、仮想ディレクトリが匿名接続用に構成されている場合は匿名アカウント、それ以外の場合は Windows のユーザー アカウントになります。 アカウントには、Analysis Services サーバーとデータベースでの適切なデータ アクセス権限が与えられている必要があります。  
  
 ![コンポーネント間の接続を示す図](../media/ssas.gif "コンポーネント間の接続を示す図")  
  
 次の表には、さまざまなシナリオで HTTP アクセスを有効にするときに検討する必要がある追加の検討事項が示されています。  
  
|シナリオ|構成|  
|--------------|-------------------|  
|IIS と Analysis Services が同じコンピューター上にある場合|これが、既定の構成 (サーバー名は localhost)、ローカルの Analysis Services OLE DB プロバイダー、および NTLM を使用した Windows 統合セキュリティを使用できるため最も簡単な構成となります。 クライアントも同じドメインにあることを前提としているため、認証はユーザーにはわからないように内部的に行われ、追加の作業も必要ありません。|  
|IIS と Analysis Services が異なるコンピューター上にある場合|このトポロジでは、Web サーバーに Analysis Services OLE DB プロバイダーをインストールする必要があります。 msmdpump.ini ファイルを編集して、リモート コンピューター上の Analysis Services インスタンスの場所を指定する必要もあります。<br /><br /> このトポロジでは、ダブルホップ認証ステップが追加されます。この認証では、資格情報がクライアントから Web サーバーに渡され、バックエンドの Analysis Services サーバーまで到達する必要があります。 Windows 資格情報と NTLM を使用している場合、NTLM では 2 番目のサーバーへのクライアント資格情報の委任が許可されないためにエラーが発生します。 最も一般的なソリューションは、SSL (Secure Sockets Layer) で基本認証を使用する方法です。ただし、この場合、MSMDPUMP 仮想ディレクトリにアクセスするときにユーザー名とパスワードの入力が必要となります。 さらにわかりやすい方法として、Kerberos を有効にし、Analysis Services 制約付き委任を構成することによって認証を内部的に処理して Analysis Services にアクセスできるようにすることもできます。 詳細については、「 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md) 」を参照してください。<br /><br /> Windows ファイアウォールでどのポートのブロックを解除するかを検討してください。 両方のサーバー上のポートのブロックを解除して IIS 上の Web アプリケーションと、リモート サーバー上の Analysis Services にアクセスできるようにする必要があります。|  
|信頼されていないドメインからのクライアント接続、またはエクストラネット接続の場合|信頼されていないドメインからのクライアント接続の場合、認証はさらに制限されます。 既定では、Analysis Services は、Windows 統合認証を使用します。この認証では、ユーザーは、サーバーと同じドメインにいる必要があります。 既定の設定を使用するようにサーバーが構成されている場合に、エクストラネット ユーザーがドメインの外から IIS に接続しようとすると接続エラーが表示されます。<br /><br /> 対処方法には、エクストラネット ユーザーがドメインの資格情報を使用して VPN 経由で接続する方法があります。 ただし、IIS Web サイト上で基本認証と SSL を有効にする方法が適している場合もあります。|  
  
##  <a name="bkmk_prereq"></a>応募  
 この記事の手順では、IIS が既に構成され、また Analysis Services が既にインストールされていることを想定しています。 Windows Server 2012 には、システムで有効にできるサーバーの役割として IIS 8.x が付属しています。  
  
 **IIS 8.0 の追加構成**  
  
 IIS 8.0 の既定の構成では、Analysis Services への HTTP アクセスに必要なコンポーネントが不足しています。 それらのコンポーネントは **[Web サーバー (IIS)]** ロールの **[セキュリティ]** と **[アプリケーション開発]** 機能領域にあり、以下のものが含まれます。  
  
-   **セキュリティ** | **Windows 認証**、**基本認証**、およびデータアクセスのシナリオに必要なその他のセキュリティ機能。  
  
-   **アプリケーション開発** | の**CGI**  
  
-   **アプリケーション開発用** | **ISAPI 拡張機能**  
  
 これらのコンポーネントを確認または追加するには、**サーバーマネージャー** | **管理** | ]**[役割と機能の追加**] を使用します。 [ **サーバー ロール**] が表示されるまで、ウィザードを進みます。 
  **[Web サーバー (IIS)]** が表示されるまで下へスクロールします。  
  
1.  [ **Web サーバー** | の**セキュリティ**] を開き、認証方法を選択します。  
  
2.  **Web サーバー** | **アプリケーション開発**を開き、[ **CGI**と**ISAPI 拡張**] を選択します。  
  
     ![Web サーバー ロールの機能ページの追加](../media/ssas-httpaccess-isapicgi.png "Web サーバー ロールの機能ページの追加")  
  
 **IIS がリモートサーバー上にある場合**  
  
 IIS と Analysis Services の間のリモート接続では、Analysis Services OLE DB プロバイダー (MSOLAP) を、IIS を実行する Windows サーバーにインストールする必要があります。  
  
1.  
  [SQL Server 2014 Feature Pack](https://www.microsoft.com/download/details.aspx?id=42295)のダウンロード ページに移動します。  
  
2.  赤い [ダウンロード] ボタンをクリックします。  
  
3.  ENU\x64\SQL_AS_OLEDB.msi が見つかるまで下にスクロールします。  
  
4.  ウィザードの指示に従って、インストールを完了させます。  
  
> [!NOTE]  
>  クライアントがリモートの Analysis Services サーバーに接続できるようにするために、Windows ファイアウォールでポートのブロックを忘れずに解除してください。 詳細については、「 [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md)」をご参照ください。  
  
##  <a name="bkmk_copy"></a>手順 1: MSMDPUMP ファイルを Web サーバー上のフォルダーにコピーする  
 作成した各 HTTP エンドポイントに、独自の MSMDPUMP ファイル セットを用意する必要があります。 この手順では、Analysis Services プログラム フォルダーの MSMDPUMP 実行可能ファイル、構成ファイル、およびリソース フォルダーを、IIS が実行されているコンピューターのファイル システム上に作成する新しい仮想ディレクトリ フォルダーにコピーします。  
  
 ドライブは、NTFS ファイル システム用にフォーマットされている必要があります。 作成するフォルダーへのパスには、スペースを使用することはできません。  
  
1.  ドライブ> SQL Server \<\\ : MSMDPUMP の<インスタンス\>\OLAP\bin\isapi: にある次のファイルをコピーします。DLL、MSMDPUMP。INI とリソースフォルダーを参照してください。  
  
     ![コピーするファイルを表示するファイル エクスプローラー](../media/ssas-httpaccess-msmdpumpfilecopy.PNG "コピーするファイルを表示するファイル エクスプローラー")  
  
2.  Web サーバーで、ドライブ>: \inetpub\wwwroot \<\\**OLAP**の新しいフォルダーを作成します。  
  
3.  この新しいフォルダーに、コピーしておいたファイルを貼り付けます。  
  
4.  Web サーバー上の \inetpub\wwwroot\OLAP フォルダーに、MSMDPUMP.DLL、MSMDPUMP.INI、および Resources フォルダーがあることを確認します。 フォルダー構造は次のようになります。  
  
    -   \<ドライブ>: \inetpub\wwwroot\OLAP\MSMDPUMP.dll  
  
    -   \<ドライブ>: \inetpub\wwwroot\OLAP\MSMDPUMP.ini  
  
    -   \<ドライブ>: \inetpub\wwwroot\OLAP\Resources  
  
##  <a name="bkmk_appPool"></a>手順 2: IIS でアプリケーションプールと仮想ディレクトリを作成する  
 次に、アプリケーション プールと、ポンプへのエンドポイントを作成します。  
  
#### <a name="create-an-application-pool"></a>アプリケーション プールの作成  
  
1.  IIS マネージャーを起動します。  
  
2.  サーバーのフォルダーを開き、 **[アプリケーション プール]** を右クリックし、 **[アプリケーション プールの追加]** をクリックします。 マネージド パイプライン モードを **[クラシック]** に設定し、.NET Framework を使用して、 **OLAP**という名前のアプリケーション プールを作成します。  
  
     ![[アプリケーション プールの追加] ダイアログのスクリーンショット](../media/ssas-httpaccess.PNG "[アプリケーション プールの追加] ダイアログのスクリーンショット")  
  
3.  既定では、IIS はセキュリティ ID として **ApplicationPoolIdentity** を使用してアプリケーション プールを作成します (これは、Analysis Services への HTTP アクセスの有効な選択肢です)。 ID を変更しなければならない特別な理由があれば、 **[OLAP]** を右クリックし **[詳細設定]** を選択します。 [ **ApplicationPoolIdentity**] を選択します。 このプロパティの **[変更]** をクリックして、ビルトイン アカウントを目的のカスタム アカウントに置き換えます。  
  
     ![[詳細設定] プロパティ ページのスクリーンショット](../media/ssas-httpaccess-advsettings.PNG "[詳細設定] プロパティ ページのスクリーンショット")  
  
4.  既定では、64 ビット オペレーティング システムの IIS では、 **[32 ビット アプリケーションの有効化]** プロパティは **false**に設定されています。 Analysis Services の 64 ビット インストールから msmdpump.dll をコピーした場合、64 ビット IIS サーバーの MSMDPUMP 拡張機能の設定はこの設定で合っています。 MSMDPUMP バイナリを 32 ビット インストールからコピーした場合は、このプロパティを **true**に設定します。 [ **詳細設定** ] でこのプロパティをチェックして、設定が適切かどうか確認します。  
  
#### <a name="create-an-application"></a>アプリケーションの作成  
  
1.  IIS マネージャで、[ **サイト**] を開き、[ **既定の Web サイト**] を開きます。 
  **Olap**という名前のフォルダーが表示されます。 これは \inetpub\wwwroot の下に作成した OLAP フォルダーへの参照です。  
  
     ![既定の Web サイトの下の OLAP フォルダー](../media/ssas-httpaccess-convertfolderbefore.png "既定の Web サイトの下の OLAP フォルダー")  
  
2.  フォルダーを右クリックし、 **[アプリケーションに変換]** を選択します。  
  
3.  [アプリケーションの追加] でエイリアスの **OLAP** を入力します。 [ **選択** ] をクリックして、OLAP アプリケーション プールを選択します。 C:\inetpub\wwwroot\OLAP に物理パスを設定する必要があります。  
  
     ![[アプリケーションの追加] ダイアログ ボックス](../media/ssas-httpaccess-convertedapp.png "[アプリケーションの追加] ダイアログ ボックス")  
  
4.  [**OK**] をクリックすると、 Web サイトを更新し、OLAP フォルダーが既定の Web サイトでアプリケーションになっていることを確認します。 これで、MSMDPUMP ファイルへの仮想パスが確立されました。  
  
     ![アプリ変換後の OLAP フォルダー](../media/ssas-httpaccess-convertfolderafter.png "アプリ変換後の OLAP フォルダー")  
  
> [!NOTE]  
>  以前のバージョンのこれらの手順には、仮想ディレクトリを作成する手順が含まれていました。 その手順は必要なくなりました。  
  
##  <a name="bkmk_auth"></a>手順 3: IIS 認証を構成し、拡張機能を追加する  
 この手順では、作成した SSAS 仮想ディレクトリの詳細を進めます。 認証方法を指定してから、スクリプト マップを追加します。 HTTP を使用した Analysis Services でサポートされている認証方法は次のとおりです。  
  
-   Windows 認証 (Kerberos または NTLM)  
  
-   基本認証  
  
-   匿名認証  
  
 **Windows 認証**は最も安全であると見なされ、Active Directory を使用するネットワークの既存のインフラストラクチャを活用します。 Windows 認証を効果的に使用するには、すべてのブラウザー、クライアント アプリケーション、およびサーバー アプリケーションが Windows 認証をサポートする必要があります。 これは最も安全性が高く推奨されるモードですが、接続を要求しているユーザーの ID を認証できる Windows ドメイン コントローラーに IIS がアクセスできる必要があります。  
  
 Analysis Services と IIS が別々のコンピューターに配置されているトポロジの場合、ユーザー ID をリモート コンピューターの 2 番目のサービスに委任するために、一般的には Analysis Services で Kerberos 制約付き委任を有効にしますが、その際に発生するダブルホップ問題を解決する必要があります。 詳細については、「 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md)」を参照してください。  
  
 **基本認証**は、Windows id があるものの、ユーザー接続が信頼されていないドメインからのものであり、委任された接続や偽装された接続の使用を禁止する場合に使用されます。 基本認証では、接続文字列でユーザー ID とパスワードを指定することができます。 現在のユーザーのセキュリティ コンテキストを使用せず、接続文字列の資格情報を使用して、Analysis Services に接続します。 Analysis Services サービスでは Windows 認証のみがサポートされるため、Analysis Services サービスに渡される資格情報はすべて、Analysis Services がホストされているドメインのメンバーである Windows ユーザーまたは Windows グループであることが必要です。  
  
 **匿名認証**は、初期テスト中によく使用されます。これは、構成の容易さが Analysis Services への HTTP 接続をすばやく検証するのに役立ちます。 わずか数回の操作で、一意のユーザー アカウントを ID として割り当て、そのアカウントに Analysis Services の権限を付与し、そのアカウントを使用してクライアント アプリケーション内のデータ アクセスを検証した後、テストの完了時に匿名認証を無効にすることができます。  
  
 運用環境でユーザーが Windows ユーザー アカウントを持っていない場合でも匿名認証を使用することができますが、「 [匿名認証を有効にする (IIS 7)](https://technet.microsoft.com/library/cc731244\(v=ws.10\).aspx)」の記事で示されているベスト プラクティスに従って、ホスト システムに対する権限をロックしてください。 認証は仮想ディレクトリに対して設定し、親 Web サイトには設定しないでください。アカウント アクセスのレベルをさらに下げるためです。  
  
 匿名認証を有効にした場合、HTTP エンドポイントに接続するすべてのユーザーが匿名ユーザーとして接続できるようになります。 個々のユーザー接続を監査したり、ユーザー id を使用してモデルのデータを選択したりすることはできません。 このように、匿名認証を使用すると、モデル デザインからデータ更新、データ アクセスに至るまで、広範囲に影響が及びます。 ただし、ユーザーにまだ Windows ユーザー ログインがない状況では、匿名アカウントを使用せざるを得ない場合があります。  
  
#### <a name="set-the-authentication-type-and-add-a-script-map"></a>認証の種類の設定とスクリプト マップの追加  
  
1.  IIS マネージャーで、 **[サイト]** を開き、 **[既定の Web サイト]** を開いて、 **OLAP** 仮想ディレクトリを選択します。  
  
2.  メイン ページの [IIS] セクションで、 **[認証]** をダブルクリックします。  
  
     ![IIS マネージャー メイン ページのスクリーンショット](../media/ssas-httpaccess-iis.png "IIS マネージャー メイン ページのスクリーンショット")  
  
3.  Windows 統合セキュリティを使用している場合は、 **[Windows 認証]** を有効にします。  
  
     ![Vdir 認証設定のスクリーンショット](../media/ssas-httpaccess-iisauth.png "Vdir 認証設定のスクリーンショット")  
  
4.  または、クライアント アプリケーションとサーバー アプリケーションが異なるドメインにある場合、 **[基本認証]** を有効にします。 このモードでは、ユーザーがユーザー名とパスワードを入力する必要があります。 ユーザー名とパスワードは HTTP 接続経由で IIS に送信されます。 IIS は MSMDPUMP に接続するときに、指定された資格情報を使用してユーザーの権限を借用しようとしますが、その資格情報は Analysis Services に委任されません。 代わりに、このドキュメントの手順 6. で説明するように、接続の有効なユーザー名とパスワードを渡す必要があります。  
  
    > [!IMPORTANT]  
    >  パスワードを送信するシステムを構築する場合は、通信チャネルをセキュリティで保護する手段が必要不可欠であることに注意してください。 IIS には、チャネルをセキュリティで保護できる一連のツールが用意されています。 詳細については、「 [IIS 7 で SSL を設定する方法](https://go.microsoft.com/fwlink/?LinkId=207562)」を参照してください。  
  
5.  Windows 認証または基本認証を使用する場合は、 **匿名認証** を無効にします。 匿名認証が有効な場合、他の認証方法が有効になっていても、IIS はこの認証方法を最初に使用します。  
  
     匿名認証では、匿名ユーザーに対して確立したユーザー アカウントとしてポンプ (msmdpump.dll) が実行されます。 IIS に接続しているユーザーと Analysis Services に接続しているユーザーは区別されません。 既定では、IIS は IUSR アカウントを使用しますが、ネットワークの権限を持つドメイン ユーザー アカウントに変更することもできます。 IIS と Analysis Services が異なるコンピューター上にある場合は、この機能が必要になります。  
  
     匿名認証用に資格情報を構成する方法については、「 [匿名認証](http://www.iis.net/configreference/system.webserver/security/authentication/anonymousauthentication)」を参照してください。  
  
    > [!IMPORTANT]  
    >  通常、匿名認証は、ファイル システムのアクセス制御リストによってユーザーのアクセスが許可または拒否される、厳密に制御された環境で使用されます。 ベスト プラクティスについては、「 [匿名認証 (IIS 7) を有効にする](https://technet.microsoft.com/library/cc731244\(v=ws.10\).aspx)」を参照してください。  
  
6.  
  **OLAP** 仮想ディレクトリをクリックして、メイン ページを開きます。 
  **[ハンドラー マッピング]** をダブルクリックします。  
  
     ![機能ページのハンドラー マッピング アイコン](../media/ssas-httpaccess-handlermapping.png "機能ページのハンドラー マッピング アイコン")  
  
7.  ページ上の任意の場所を右クリックし、 **[スクリプト マップの追加]** を選択します。 [スクリプトマップの追加] ダイアログボックス** \*** で、要求パスとして「.dll」と指定し、実行可能ファイルとして「c:\inetpub\wwwroot\olap\msmdpump.dll」を指定して、名前として「 **OLAP** 」と入力します。 このスクリプト マップに関連付けられている既定のすべての制限を維持します。  
  
     ![[スクリプト マップの追加] ダイアログ ボックスのスクリーンショット](../media/ssas-httpaccess-addscript.png "[スクリプト マップの追加] ダイアログ ボックスのスクリーンショット")  
  
8.  ISAPI 拡張機能を許可するように求めるメッセージが表示されたら、 **[はい]** をクリックします。  
  
     ![ISAPI 拡張機能追加の確認のスクリーンショット](../media/ssas-httpaccess-isapiprompt.png "ISAPI 拡張機能追加の確認のスクリーンショット")  
  
##  <a name="bkmk_edit"></a>手順 4: MSMDPUMP を編集します。ターゲットサーバーを設定する INI ファイル  
 MSMDPUMP.INI ファイルを使用して、MSMDPUMP.DLL が接続する Analysis Services インスタンスを指定します。 これには、ローカルまたはリモートの、既定のインスタンスまたは名前付きのインスタンスとしてインストールされているインスタンスを指定できます。  
  
 C:\inetpub\wwwroot\OLAP フォルダーにある msmdpump.ini ファイルを開いて、このファイルの内容を確認します。 この要素は次のようになります。  
  
```  
<ConfigurationSettings>  
<ServerName>localhost</ServerName>  
<SessionTimeout>3600</SessionTimeout>  
<ConnectionPoolSize>100</ConnectionPoolSize>  
</ConfigurationSettings>  
  
```  
  
 HTTP アクセスを構成している Analysis Services インスタンスがローカル コンピューター上にあり、既定のインスタンスとしてインストールされている場合は、この設定を変更する理由はありません。 それ以外の場合は、サーバー名を指定する必要\<があります (たとえば、servername\<>ADWRKS-SRV01/servername>)。 名前付きインスタンスとしてインストールされているサーバーの場合は、必ずインスタンス名を追加し\<てください (\<たとえば、ServerName>ADWRKS-SRV01\Tabular/servername>)。  
  
 Analysis Services の既定のインスタンスは TCP/IP ポート 2383 をリッスンします。 Analysis Services を既定のインスタンスとしてインストールした場合は、ポート2383で自動的\<にリッスンする方法が Analysis Services であるため、ServerName> でポートを指定する必要はありません。 ただし、Windows ファイアウォールでそのポートへの着信接続を許可する必要があります。 詳細については、「 [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md)」をご参照ください。  
  
 固定ポートでリッスンする Analysis Services の名前付きインスタンスまたは既定のインスタンスを構成した場合は、ポート番号をサーバー名に追加する必要\<があります (たとえば、SERVERNAME\<>AW-SRV01: 55555/ServerName>)。また、Windows ファイアウォールでそのポートへの着信接続を許可する必要があります。  
  
## <a name="step-5-grant-data-access-permissions"></a>手順 5: データ アクセス権限を付与する  
 前に説明したように、Analysis Services インスタンスの権限を付与する必要があります。 各データベース オブジェクトには特定レベルの権限 (読み取り、または読み取り/書き込み) を付与するロールがあり、各ロールに Windows ユーザー ID で構成されるメンバーが割り当てられます。  
  
 権限を設定するには、SQL Server Management Studio を使用します。 [**データベース** | **ロール**] フォルダーでは、ロールの作成、データベースのアクセス許可の指定、Windows ユーザーアカウントまたはグループアカウントへのメンバーシップの割り当て、特定のオブジェクトに対する読み取り権限または書き込み権限の付与を行うことができます。 モデル データを使用するが更新しないクライアント接続の場合、一般的には、キューブに対する権限は **"読み取り"** で十分です。  
  
 ロールの割り当ては、認証の構成方法によって変わります。  
  
|||  
|-|-|  
|Anonymous|IIS の **[匿名認証資格情報の編集]** で指定されたアカウントをメンバーシップ一覧に追加します。 詳細については、「 [匿名認証](http://www.iis.net/configreference/system.webserver/security/authentication/anonymousauthentication)」を参照してください。|  
|Windows 認証|借用または委任によって Analysis Services データを要求する Windows ユーザー アカウントまたはグループ アカウントをメンバーシップ一覧に追加します。<br /><br /> Kerberos の制約付き委任を使用し、権限が必要なアカウントは、アクセスを要求する Windows ユーザー アカウントとグループ アカウントのみであることを想定しています。 アプリケーション プール ID のために必要な権限はありません。|  
|基本認証|接続文字列で渡される Windows ユーザー アカウントまたはグループ アカウントをメンバーシップ一覧に追加します。<br /><br /> また、接続文字列で `EffectiveUserName` を使用して資格情報を渡している場合、アプリケーション プール ID には、Analysis Services インスタンスでの管理者権限が必要になります。 SSMS**で &#124; の**インスタンスを右クリックし、[**セキュリティ**&#124;**追加**] &#124; ます。 アプリケーション プール ID を入力します。 組み込みの既定の id を使用した場合、アカウントは**IIS AppPool\DefaultAppPool**として指定されます。<br /><br /> ![](../media/ssas-httpaccess-iisapppoolidentity.png)|  
  
 アクセス許可の設定の詳細については、「 [オブジェクトと操作へのアクセスの承認 &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)」を参照してください。  
  
##  <a name="bkmk_test"></a>手順 6: 構成をテストする  
 MSMDPUMP の接続文字列構文は、MSMDPUMP.dll ファイルへの URL です。  
  
 Web アプリケーションが固定ポートでリッスンしている場合`http://my-web-srv01:8080/OLAP/msmdpump.dll`は、ポート番号をサーバー名または IP アドレス (や`http://123.456.789.012:8080/OLAP/msmdpump.dll`など) に追加します。  
  
 接続をすばやくテストするために、Microsoft Excel または SQL Server Management Studio を使用して接続を開くことができます。  
  
 **SQL Server Management Studio を使用した接続のテスト**  
  
1.  Management Studio の [サーバーへの接続] ダイアログ ボックスで、サーバーの種類として **[Analysis Services]** を選択します。 [サーバー名] に、msmdpump 拡張機能の HTTP アドレス ( `http://my-web-srv01/OLAP/msmdpump.dll`) を入力します。  
  
     オブジェクト エクスプ ローラーには、次の HTTP 接続が表示されます:  
  
     ![SSAS への http 接続を示したオブジェクト エクスプ ローラー](../media/ssas-httpaccess-ssms.PNG "SSAS への http 接続を示したオブジェクト エクスプ ローラー")  
  
2.  認証には Windows 認証を使用し、Management Studio を使用するユーザーが Analysis Services 管理者であることが必要です。 管理者は、さらに権限を付与して、他のユーザーがアクセスできるようにすることができます。  
  
 **Excel を使用した接続のテスト**  
  
1.  Excel の [データ] タブの [外部データの取り込み] で、 **[その他のデータ ソース]**、 **[Analysis Services]** の順にクリックして、データ接続ウィザードを起動します。  
  
2.  [サーバー名] に、msmdpump 拡張機能の HTTP アドレス ( `http://my-web-srv01/OLAP/msmdpump.dll`) を入力します。  
  
3.  ログオン資格情報については、Windows 統合セキュリティ、NTLM、または匿名ユーザーを使用する場合は **[Windows 認証を使用する]** を選択します。  
  
     基本認証の場合は、 **[以下のユーザー名とパスワードを使用する]** を選択し、サインオンに使用する資格情報を指定します。 指定した資格情報が接続文字列として Analysis Services に渡されます。  
  
 **AMO を使用して接続をテストする**  
  
 AMO を使用したプログラムによる HTTP アクセスをテストできます。それには、サーバー名の代わりにエンドポイントの URL を使用します。 詳細については、 [フォーラムの投稿 (ドメイン/フォレストとファイアウォールの境界を越えて HTTPS で SSAS 2008 R2 データベースを同期する方法)](https://social.msdn.microsoft.com/Forums/en/sqlanalysisservices/thread/c4249d55-914d-4c81-9980-44d0b8df9c3e)を参照してください。  
  
 次の接続文字列の例では、基本認証を使用した HTTP(S) アクセスに使用する構文を示しています。  
  
 `Data Source=https://<servername>/olap/msmdpump.dll; Initial Catalog=AdventureWorksDW2012; Integrated Security=Basic; User ID=XXXX; Password=XXXXX;`  
  
 プログラムからの接続の設定の詳細については、「 [Establishing Secure Connections in ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections)」を参照してください。  
  
 最後に、接続が開始されるネットワーク環境内で実行されているクライアント コンピューターを使用して、より厳密な事後テストを必ず実行するようにしてください。  
  
## <a name="see-also"></a>参照  
 [フォーラムの投稿 (msmdpump と基本認証を使用した http アクセス)](https://social.msdn.microsoft.com/Forums/en/sqlanalysisservices/thread/79d2f225-df35-46da-aa22-d06e98f7d658)   
 [Analysis Services アクセスを許可するように Windows ファイアウォールを構成する](configure-the-windows-firewall-to-allow-analysis-services-access.md)   
 [オブジェクトと操作へのアクセスの承認 &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [IIS の認証方法](https://go.microsoft.com/fwlink/?LinkdID=208461)   
 [IIS 7 で SSL を設定する方法](https://go.microsoft.com/fwlink/?LinkId=207562)  
  
