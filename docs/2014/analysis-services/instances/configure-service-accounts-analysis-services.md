---
title: サービス アカウント (Analysis Services) の構成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services], logon accounts
- logon accounts [Analysis Services]
- accounts [Analysis Services]
- logon accounts [Analysis Services], about logon accounts
ms.assetid: b481bd51-e077-42f6-8598-ce08c1a38716
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8dfde906f7cadc01b9c7a4abbe32be1bd0408986
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080186"
---
# <a name="configure-service-accounts-analysis-services"></a>サービス アカウントの構成 (Analysis Services)
  製品全体のアカウントの準備については、 [を含めて、すべての](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)サービスに関する包括的なサービス アカウントの情報を提供するトピック、「 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows サービス アカウントと権限の構成 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]」を参照してください。 有効なアカウントの種類、セットアップで割り当てられた Windows 特権、ファイル システムの権限、レジストリの権限などについては、前のトピックをご覧ください。  
  
 このトピックでは、テーブルおよびクラスター化インストールに必要な追加の権限など、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]の補足情報を提供します。 また、サーバー操作をサポートするために必要な権限についても説明します。 たとえば、サービス アカウントの下で実行するように処理およびクエリ操作を構成できます。その場合、これを機能させるには追加の権限を付与する必要があります。  
  
-   [Analysis Services に割り当てられる Windows 特権](#bkmk_winpriv)  
  
-   [Analysis Services に割り当てられるファイル システムのアクセス許可](#bkmk_FilePermissions)  
  
-   [特定のサーバー操作に対する追加のアクセス許可の付与](#bkmk_tasks)  
  
 追加の構成手順 (ここでは説明しません) として、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンスおよびサービス アカウントのサービス プリンシパル名 (SPN) を登録します。 この手順によって、ダブルホップ シナリオでクライアント アプリケーションからバックエンド データ ソースへのパススルー認証が有効になります。 この手順は、Kerberos 制約付き委任用に構成されたサービスにのみ適用されます。 詳細な手順については、「 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md) 」を参照してください。  
  
## <a name="logon-account-recommendations"></a>ログオン アカウントに関する推奨事項  
 フェールオーバー クラスターでは、Analysis Services のすべてのインスタンスが Windows ドメイン ユーザー アカウントを使用するように構成する必要があります。 すべてのインスタンスに、同じアカウントを割り当てます。 詳細については、「 [Analysis Services をクラスター化する方法](https://msdn.microsoft.com/library/dn736073.aspx) 」を参照してください。  
  
 スタンドアロンのインスタンスは、既定のインスタンスの場合は既定の仮想アカウント **NT Service\MSSQLServerOLAPService** を使用しなければならず、名前付きインスタンスの場合は **NT Service\MSOLAP$** _instance-name_ を使用します。 この推奨事項は、すべてのサーバー モードの Analysis Services インスタンスに適用されます。オペレーティング システムには Windows Server 2008 R2 以降、Analysis Services には SQL Server 2012 を想定しています。  
  
## <a name="granting-permissions-to-analysis-services"></a>Analysis Services へのアクセス許可の付与  
 このセクションでは、Analysis Services がローカルの内部操作 (実行可能ファイルの開始、構成ファイルの読み取り、データ ディレクトリからのデータベースの読み込みなど) に必要とするアクセス許可を説明します。 必要としているのがその情報ではなく、外部データ アクセスやその他のサービスおよびアプリケーションとの相互運用性のためのアクセス許可の設定のガイダンスである場合は、このトピックで後述する「 [特定のサーバー操作に対する追加のアクセス許可の付与](#bkmk_tasks) 」を参照してください。  
  
 内部操作の場合、Analysis Services の権限保有者はログオン アカウントではなく、セットアップによって作成された、サービスごとの SID が含まれているローカル Windows セキュリティ グループです。 Analysis Services では、以前のバージョンから一貫して、アクセス許可をセキュリティ グループに割り当てるようになっています。 また、ログオン アカウントは時間の経過と共に変更できますが、サービスごとの SID とローカル セキュリティ グループはサーバーのインストールの有効期間にわたって一定です。 そのため、Analysis Services の場合、アクセス許可を保持するための選択肢として、ログオン アカウントよりもセキュリティ グループの方が優れています。 手動でサービス インスタンスに権限を付与するときには、ファイル システム権限と Windows の特権のどちらであっても、必ずサーバー インスタンスのために作成されたローカル セキュリティ グループにアクセス許可を与えます。  
  
 セキュリティ グループの名前は、一定のパターンに従います。 プレフィックスは常に `SQLServerMSASUser$` であり、その後にコンピューター名が続き、最後にインスタンス名が付きます。 既定のインスタンスは `MSSQLSERVER` です。 名前付きインスタンスは、セットアップ時に指定した名前です。  
  
 ローカル セキュリティ設定でこのセキュリティ グループを確認できます。  
  
-   Compmgmt.msc を実行する |**ローカル ユーザーとグループ** | **グループ** | `SQLServerMSASUser$`\<サーバー名 >`$MSSQLSERVER` (の既定のインスタンス)。  
  
-   セキュリティ グループをダブルクリックして、そのメンバーを表示する。  
  
 グループの唯一のメンバーは、サービスごとの SID です。 その隣にログオン アカウントが示されます。 ログオン アカウント名は、サービスごとの SID のコンテキストを示して、分かりやすくする目的で表示されています。 後でログオン アカウントを変更してからこのページに戻ると、セキュリティ グループとサービスごとの SID には変化がないにもかかわらず、ログオン アカウントのラベルが異なっていることが分かります。  
  
##  <a name="bkmk_winpriv"></a> Analysis Services サービス アカウントに割り当てられた Windows 特権  
 Analysis Services では、サービスを開始し、システム リソースを要求するには、オペレーティング システムからの権限が必要です。 要件は、サーバー モードおよびインスタンスがクラスター化されているかどうかによって異なります。 Windows 特権の詳細については、「 [特権](https://msdn.microsoft.com/library/windows/desktop/aa379306\(v=vs.85\).aspx) 」および「 [特権の制約 (Windows)](/windows/desktop/SecAuthZ/privilege-constants) 」を参照してください。  
  
 Analysis Services のすべてのインスタンスには、 **[サービスとしてログオン]** (SeServiceLogonRight) 特権が必要です。 SQL Server セットアップによって、インストール時に指定されたサービス アカウントに特権が割り当てられます。 多次元モードおよびデータ マイニング モードで実行されるサーバーの場合、これは スタンドアロン サーバー インストール環境において Analysis Services サービス アカウントが必要とする唯一の Windows 特権であり、セットアップによって Analysis Services 用に構成される唯一の特権です。 クラスター インスタンスおよび表形式インスタンスの場合、追加の Windows 特権を手動で追加する必要があります。  
  
 フェールオーバー クラスター インスタンスには、表形式モードまたは多次元モードの場合、 **[スケジューリング優先順位の繰り上げ]** (SeIncreaseBasePriorityPrivilege) が必要です。  
  
 表形式インスタンスでは次の 3 つの追加の特権を使用しており、いずれもインスタンスのインストール後に手動で付与する必要があります。  
  
|||  
|-|-|  
|**[プロセス ワーキング セットの増加]** (SeIncreaseWorkingSetPrivilege)|この特権は、既定では **[ユーザー]** セキュリティ グループを介してすべてのユーザーが使用可能です。 サーバーをロックするにはこのグループの権限を削除することで、Analysis Services が、このエラーをログ記録を開始するには、失敗。「必要な特権が保持していませんクライアント。」 このエラーが発生した場合は、特権を適切な Analysis Services セキュリティ グループに付与することで、Analysis Services に特権を復元します。|  
|**[プロセスに対してメモリ クォータを調整する]** (SeIncreaseQuotaSizePrivilege)|この特権は、プロセスのリソースが十分でないためにプロセスの実行を完了できない場合に、さらに多くのメモリを要求するために使用します (メモリ量は、インスタンス用に設定されたメモリしきい値に依存します)。|  
|**[メモリ内のページのロック]** (SeLockMemoryPrivilege)|この特権が必要になるのは、ページングが完全にオフになっているときのみです。 既定では、表形式サーバー インスタンスは Windows ページング ファイルを使用しますが、`VertiPaqPagingPolicy` を 0 に設定して、Windows ページングを使用しないようにすることもできます。<br /><br /> `VertiPaqPagingPolicy` を 1 (既定) にすると、表形式サーバー インスタンスは Windows ページング ファイルを使用します。 割り当てはロックされないため、必要に応じてページ アウトされます。 ページングが使用されているため、メモリ内のページをロックする必要はありません。 したがっての既定の構成 (場所`VertiPaqPagingPolicy`= 1)、付与する必要はありません、**メモリ内のページのロック**特権を表形式インスタンス。<br /><br /> `VertiPaqPagingPolicy` を 0 にした場合。 Analysis Services のページングをオフにした場合は、割り当てがロックされ、 **[メモリ内のページのロック]** 特権が表形式インスタンスに付与されます。 このように設定され、かつ **[メモリ内のページのロック]** 特権がある場合、システムでメモリ不足が発生しているときは、Analysis Services に対して行われたメモリ割り当てをページ アウトできません。 Analysis Services に依存、**メモリ内のページのロック**が適用されているとアクセス許可`VertiPaqPagingPolicy`= 0。 Windows ページングをオフにすることはお勧めしません。 このようにすると、ページングが許可されている場合には正常に処理されるような操作でメモリ不足エラーが発生する率が高まります。 参照してください[メモリ プロパティ](../server-properties/memory-properties.md)の詳細については`VertiPaqPagingPolicy`します。|  
  
#### <a name="to-view-or-add-windows-privileges-on-the-service-account"></a>サービス アカウントに対する Windows 特権を表示または追加するには  
  
1.  GPEDIT.msc を実行し、[ローカル コンピューター ポリシー] | [コンピューターの構成] | [Windows の設定] | [セキュリティの設定] | [ローカル ポリシー] | [ユーザー権利の割り当て] を選択します。  
  
2.  含まれている既存のポリシーを確認`SQLServerMSASUser$`します。 これは、Analysis Services がインストール済みのコンピューター上にあるローカル セキュリティ グループです。 Windows 特権とファイル フォルダー権限の両方が、このセキュリティ グループに付与されています。 **[サービスとしてログオン]** ポリシーをダブルクリックすると、セキュリティ グループがシステムにどのように指定されているかが表示されます。 セキュリティ グループの完全名は、Analysis Services を名前付きインスタンスとしてインストールしたかどうかによって異なります。 アカウントの特権を追加する場合は、実際のサービス アカウントではなく、このセキュリティ グループを使用してください。  
  
3.  GPEDIT でアカウントの特権を追加するには、 **[プロセス ワーキング セットの増加]** を右クリックし、 **[プロパティ]** を選択します。  
  
4.  **[ユーザーまたはグループの追加]** をクリックします。  
  
5.  Analysis Services インスタンスのユーザー グループを入力します。 サービス アカウントはローカル セキュリティ グループのメンバーであり、そのためアカウントのドメインとしてローカル コンピューター名を付加する必要があることに注意してください。  
  
     次の一覧は、"SQL01-WIN12" というコンピューター (コンピューター名はローカル ドメインです) に既定のインスタンスおよび "Tabular" という名前付きインスタンスがある 2 つの例を示しています。  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$MSSQLSERVER  
  
    -   SQL01-WIN12\SQL01-WIN12$SQLServerMSASUser$TABULAR  
  
6.  **[プロセスに対してメモリ クォータを調整する]** のほか、必要に応じて **[メモリ内のページのロック]** または **[スケジューリング優先順位の繰り上げ]** に対しても、この手順を繰り返します。  
  
> [!NOTE]  
>  以前のバージョンのセットアップでは、Analysis Services サービス アカウントが **Performance Log Users** グループに誤って追加されていました。 この欠陥は修正されましたが、既存のインストールにこの不必要なグループ メンバーシップが存在する可能性があります。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サービス アカウントでは **Performance Log Users** グループのメンバーシップを必要としないので、グループから削除できます。  
  
##  <a name="bkmk_FilePermissions"></a> Analysis Services サービス アカウントに割り当てられたファイル システム権限  
  
> [!NOTE]  
>  各プログラム フォルダーに関連付けられている権限の一覧については、「 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) 」を参照してください。  
>   
>  IIS の構成と [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] に関連するファイル権限の詳細については、「[インターネット インフォメーション サービス &#40;IIS&#41; 8.0 上の Analysis Services への HTTP アクセスの構成](configure-http-access-to-analysis-services-on-iis-8-0.md)」を参照してください。  
  
 指定のデータ フォルダーからデータベースをロードおよびアンロードするために必要な権限も含めて、サーバー操作に必要なすべてのファイル システム権限は、インストール時に SQL Server セットアップによって割り当てられます。  
  
 データ ファイル、プログラム実行可能ファイル、構成ファイル、ログ ファイル、および一時ファイルの権限保有者は、SQL Server セットアップによって作成されるローカル セキュリティ グループです。  
  
 インストールするインスタンスごとに作成されるセキュリティ グループが 1 つあります。 セキュリティ グループはインスタンスに基づいて付けられます後か、という名前**SQLServerMSASUser$ MSSQLSERVER**既定のインスタンスまたは`SQLServerMSASUser$` \<servername >$\<instancename > 名前付きインスタンス。 セットアップは、サーバー操作に必要なファイル権限をこのセキュリティ グループに準備します。 \MSAS12.MSSQLSERVER\OLAP\BIN ディレクトリのセキュリティ権限をチェックすると、(サービス アカウントまたはサービスごとの SID ではなく) セキュリティ グループが該当ディレクトリの権限保有者であることがわかります。  
  
 このセキュリティ グループには、1 つのメンバー、つまり [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンス開始アカウントのサービスごとのセキュリティ識別子 (SID) のみが含まれます。 セットアップによって、サービスごとの SID がローカル セキュリティ グループに追加されます。 SQL Server セットアップが Analysis Services を準備する方法において、SID のメンバーシップと共にローカル セキュリティ グループを使用することは、データベース エンジンと比較した場合に、小さくても顕著な相違となります。  
  
 ファイル権限が破損していると考えられる場合は、次の手順に従って、サービスが正しく準備されていることを検証します。  
  
1.  サービス コントロール コマンド ライン ツール (sc.exe) を使用して、既定のサービス インスタンスの SID を取得します。  
  
     `SC showsid MSSqlServerOlapService`  
  
     名前付きインスタンス (インスタンス名が Tabular であるもの) の場合は、次の構文を使用します。  
  
     `SC showsid MSOlap$Tabular`  
  
2.  使用**コンピューター マネージャー** | **ローカル ユーザーとグループ** | **グループ**SQLServerMSASUser$のメンバーシップを検査する\<servername >$\<instancename > セキュリティ グループ。  
  
     メンバーの SID は、手順 1 で示したサービスごとの SID と一致する必要があります。  
  
3.  **[Windows エクスプローラー]**  |  **[Program Files]**  |  **[Microsoft SQL Server]** | Msasxx.mssqlserver | **[OLAP]**  |  **[bin]** を使用して、フォルダーのセキュリティ プロパティが、手順 2 のセキュリティ グループに付与されていることを確認します。  
  
> [!NOTE]  
>  SID は削除したり変更したりしないでください。 誤って削除するサービスごとの SID を復元するを参照してください。 [ https://support.microsoft.com/kb/2620201](https://support.microsoft.com/kb/2620201)します。  
  
 **サービスごとの SID の詳細**  
  
 各 Windows アカウントは関連する [SID](http://en.wikipedia.org/wiki/Security_Identifier)を持ちますが、サービスも SID を持っており、そのためサービスごとの SID と呼ばれます。 サービスごとの SID は、サービス インスタンスのインストール時に、サービスの一意の永続的な機能として作成されます。 サービスごとの SID はコンピューター レベルのローカルな SID であり、サービス名から生成されます。 既定のインスタンスの場合、それには、ユーザー フレンドリな名前として NT SERVICE\MSSQLServerOLAPService という名前が付けられています。  
  
 サービスごとの SID の利点は、広範囲にわたって表示されるログオン アカウントを、ファイル権限に影響を及ぼすことなく自由に変更できることです。 たとえば、共に同じ Windows ユーザー アカウントで実行する Analysis Services の 2 つのインスタンス (既定のインスタンスと名前付きインスタンス) をインストールする場合を考えます。 各サービス インスタンスはログオン アカウントを共有するものの、それぞれ一意のサービスごとの SID を持ちます。 この SID は、ログオン アカウントの SID とは異なります。 サービスごとの SID は、ファイル権限および Windows 特権に使用されます。 これに対し、ログオン アカウント SID は認証と承認のシナリオで使用されます。このように、異なる目的のために異なる SID が使用されます。  
  
 SID は不変であるため、サービスのインストール時に作成されたファイル システム ACL を、サービス アカウントの変更頻度に関係なく、無期限に使用できます。 SID により権限を指定する ACL では、セキュリティのための措置を強化するために、同じアカウントで他のサービスが実行する場合でも、プログラムの実行可能プログラムおよびデータ フォルダーがサービスの単一のインスタンスによってのみアクセスされることが保証されます。  
  
##  <a name="bkmk_tasks"></a> 特定のサーバー操作に対する追加の Analysis Services 権限の付与  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] では、一部のタスクは、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]を開始するために使用されるサービス アカウント (またはログオン アカウント) のセキュリティ コンテキストに従って実行され、他のタスクは、そのタスクを要求しているユーザーのセキュリティ コンテキストに従って実行されます。  
  
 次の表に、サービス アカウントとして実行するタスクをサポートするために必要な追加権限を示します。  
  
|サーバー操作|作業項目|根拠|  
|----------------------|---------------|-------------------|  
|外部リレーショナル データ ソースに対するリモート アクセス|サービス アカウントのデータベース ログインを作成します。|処理とは、外部データ ソース (通常はリレーショナル データベース) からのデータの取得を意味します。これはその後、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] データベースに読み込まれます。 外部データの取得で可能な資格情報に関するオプションの 1 つに、サービス アカウントを使用することがあります。 この資格情報に関するオプションは、サービス アカウントのデータベース ログインを作成し、ソース データベースに対する読み取り権限を付与した場合にのみ選択できます。 このタスクでのサービス アカウント オプションの使用方法の詳細については、「[権限借用オプションの設定s &#40;SSAS - 多次元&#41;](../multidimensional-models/set-impersonation-options-ssas-multidimensional.md)」を参照してください。 同様に、ROLAP をストレージ モードとして使用する場合は、同じ権限借用オプションを選択できます。 この場合、アカウントには、ROLAP パーティションを処理するために (つまり、集計を格納するために)、ソース データに対する書き込みアクセス権も必要です。|  
|DirectQuery|サービス アカウントのデータベース ログインを作成します。|DirectQuery は、表形式モデルに収めるには大きすぎるか、既定のインメモリ ストレージ オプションよりも DirectQuery の適合性が高いその他の特性がある外部データセットをクエリするために使用する表形式の機能です。 DirectQuery モードで使用できる接続オプションの 1 つは、サービス アカウントを使用することです。 ここでもこのオプションは、サービス アカウントにターゲット データ ソースでのデータベースのログイン権限と読み取り権限がある場合にのみ選択できます。 このタスクでのサービス アカウント オプションの使用方法の詳細については、「[権限借用オプションの設定s &#40;SSAS - 多次元&#41;](../multidimensional-models/set-impersonation-options-ssas-multidimensional.md)」を参照してください。 また、データの取得のために、現在のユーザーの資格情報を使用できます。 ほとんどの場合、このオプションではダブル ホップ接続が発生します。したがって、サービス アカウントでダウンストリーム サーバーに ID をデリゲートできるように、Kerberos の制約付き委任のためのサービス アカウントを構成します。 詳細については、「 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md)」を参照してください。|  
|他の SSAS インスタンスへのリモート アクセス|リモート サーバー上に定義された Analysis Services のデータベース ロールへの、サービス アカウントの追加|リモート パーティション、および他のリモート [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] インスタンス上のリンク オブジェクトの参照は共に、リモート コンピューターまたはデバイス上の権限を必要とするシステム機能です。 ユーザーがリモート パーティションを作成および設定するか、リンク オブジェクトを設定すると、現在のユーザーのセキュリティ コンテキストで操作が実行します。 後でこの操作を自動化した場合、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] はそのサービス アカウントのセキュリティ コンテキストでリモート インスタンスにアクセスします。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]のリモート インスタンスにあるリンク オブジェクトにアクセスするには、特定のディメンションに対する読み取りアクセス権など、リモート インスタンス上の適切なオブジェクトを読み取るための権限がログオン アカウントに必要です。 同様に、リモート パーティションを使用するには、サービス アカウントでリモート インスタンス上に管理者権限が必要です。 このような権限は、許可された操作を特定のオブジェクトに関連付けるロールを使用して、リモート Analysis Services インスタンス上で付与されます。 処理およびクエリ操作を許可するフル コントロール権限を付与する方法については、「[データベース権限の付与 &#40;Analysis Services&#41;](../multidimensional-models/grant-database-permissions-analysis-services.md)」を参照してください。 リモート パーティションの詳細については、「[リモート パーティションの作成と管理 &#40;Analysis Services&#41;](../multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)」を参照してください。|  
|[書き戻し]|リモート サーバー上に定義された Analysis Services のデータベース ロールへの、サービス アカウントの追加|書き戻しは、クライアント アプリケーションで有効にされている場合に、データ分析中に新しいデータ値の作成を可能にする多次元モデルの機能です。 ディメンションまたはキューブ内で書き戻しが有効な場合は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サービス アカウントに、ソースの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベースの書き戻しテーブルに対する書き込み権限が必要です。 このテーブルがまだ存在しておらず、作成する必要がある場合は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サービス アカウントに、指定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内でテーブルを作成するための権限も必要です。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リレーショナル データベース内のクエリ ログ テーブルへの書き込み|サービス アカウントのデータベース ログインの作成、およびクエリ ログ テーブルに対する書き込み権限の割り当て|以降の分析用にデータベース テーブル内に使用状況データを収集するために、クエリ ログ記録を有効にできます。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] サービス アカウントには、指定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのクエリ ログ テーブルに対する書き込み権限が必要です。 このテーブルがまだ存在しておらず、作成する必要がある場合は、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ログオン アカウントに、指定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内でテーブルを作成するための権限も必要です。 詳細については、 [使用法に基づく最適化ウィザードによる SQL Server Analysis Services のパフォーマンスの向上 (ブログ)](http://www.mssqltips.com/sqlservertip/2876/improve-sql-server-analysis-services-performance-with-the-usage-based-optimization-wizard/) および [Analysis Services でのクエリのログ記録 (ブログ)](http://weblogs.asp.net/miked/archive/2013/07/31/query-logging-in-analysis-services.aspx)を参照してください。|  
  
## <a name="see-also"></a>関連項目  
 [を含めて、すべての](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [SQL Server サービス アカウントとサービスごとの SID (ブログ)](http://www.travisgan.com/2013/06/sql-server-service-account-and-per.html)   
 [サービス SID を使用してサービスを分離する SQL Server (サポート技術情報の記事)](https://support.microsoft.com/kb/2620201)   
 [アクセス トークン (MSDN)](/windows/desktop/SecAuthZ/access-tokens)   
 [セキュリティ ID (MSDN)](/windows/desktop/SecAuthZ/security-identifiers)   
 [アクセス トークン (Wikipedia)](http://en.wikipedia.org/wiki/Access_token)   
 [アクセス制御リスト (Wikipedia)](http://en.wikipedia.org/wiki/Access_control_list)  
  
  
