---
title: Analysis Services インスタンスに対する SPN の登録 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9e78dc37-a3f0-415d-847c-32fec69efa8c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee52be5eb8c9110e4486a1fa199e3e00572081f3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079568"
---
# <a name="spn-registration-for-an-analysis-services-instance"></a>Analysis Services インスタンスの SPN 登録
  クライアントとサービス ID の相互認証に Kerberos が使用されている場合、サービス プリンシパル名 (SPN) は、Active Directory ドメイン内のサービス インスタンスを一意に識別します。 SPN は、サービス インスタンスを実行するログオン アカウントに関連付けられます。  
  
 Kerberos 認証を通じて Analysis Services に接続するクライアント アプリケーションの場合、Analysis Services クライアント ライブラリは、接続文字列のホスト名と、Analysis Services のどのリリースでも固定されているその他のよく知られている変数 (サービス クラスなど) を使用して、SPN を構築します。  
  
 相互認証が行われるようにするには、クライアントによって構築された SPN が Active Directory ドメイン コントローラー (DC) 上の対応する SPN オブジェクトと一致する必要があります。 つまり、ユーザーが接続文字列でホスト名を指定するすべての方法に対応するには、1 つの Analysis Services インスタンスに複数の SPN の登録が必要になる場合があります。 たとえば、サーバーの完全修飾ドメイン名 (FQDN) と短いコンピューター名の両方に対応するには、2 つの SPN が必要になると思われます。 接続を成功させるには、Analysis Services SPN を正しく登録することが重要です。 SPN が存在しなかったり、形式が不適切だったり、重複していたりすると、接続は失敗します。  
  
 SPN の登録作業は、Analysis Services 管理者が手動で行います。 SQL Server データベース エンジンとは異なり、Analysis Services がサービス開始時に SPN を自動登録することはありません。 手動登録は、Analysis Services が、既定の仮想アカウント、ドメイン ユーザー アカウント、またはビルトイン アカウント (サービスごとの SID を含む) で実行される場合に必要です。  
  
 ドメイン管理者によって作成された定義済みの "管理されたサービス アカウント" でサービスが実行されている場合、SPN の登録は不要です。 ドメインの機能レベルによっては、SPN の登録にドメイン管理者権限が必要になることに注意してください。  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と Kerberos に関する接続性の問題のトラブルシューティングに役立つ診断ツールです。 Kerberos 認証の詳細については、「 [Microsoft® Kerberos Configuration Manager for SQL Server®](https://www.microsoft.com/download/details.aspx?id=39046)」をご覧ください。  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と Kerberos に関する接続性の問題のトラブルシューティングに役立つ診断ツールです。 Kerberos 認証の詳細については、「 [Microsoft® Kerberos Configuration Manager for SQL Server®](https://www.microsoft.com/download/details.aspx?id=39046)」をご覧ください。  
  
 このトピックには、次のセクションが含まれます。  
  
 [SPN の登録が必要な場合](#bkmk_scnearios)  
  
 [Analysis Services 用の SPN の形式](#bkmk_SPNSyntax)  
  
 [仮想アカウントに対する SPN の登録](#bkmk_virtual)  
  
 [ドメイン アカウントに対する SPN の登録](#bkmk_domain)  
  
 [ビルトイン アカウントに対する SPN の登録](#bkmk_builtin)  
  
 [名前付きインスタンスのための SPN の登録](#bkmk_spnNamed)  
  
 [SSAS クラスターのための SPN の登録](#bkmk_spnCluster)  
  
 [HTTP アクセス用に構成された SSAS インスタンスのための SPN の登録](#bkmk_spnHTTP)  
  
 [固定ポートをリッスンしている SSAS インスタンスのための SPN の登録](#bkmk_spnFixedPorts)  
  
##  <a name="bkmk_scnearios"></a> SPN の登録が必要な場合  
 指定する任意のクライアント接続"SSPI = Kerberos"文字列の接続で Analysis Services インスタンスの SPN 登録の要件が導入されます。  
  
 SPN の登録は、次の場合に必要になります。 詳細については、「 [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md)」をご覧ください。  
  
-   ID 委任は、ユーザーの ID をクライアント アプリケーションまたは中間層サービスから Analysis Services に引き渡す際に必要となります。 ID 委任は通常、特定のオブジェクトにユーザーごとの権限 (つまりフィルター) が定義されているときに使用されます。  
  
     Excel Services、Reporting Services などの中間層サービスは、ユーザー ID の権限借用によって、Analysis Services からデータを取得しますが、その際の制約付き委任の構成で ID 委任が関係します。 この動作をサポートするには、Excel Services や Reporting Services の制約付き委任を構成する際に、接続先のサービスとして Analysis Services の SPN を指定する必要があります。  
  
-   Analysis Services が、DirectQuery モードを使用して表形式データベースのために SQL Server リレーショナル データベースのデータを取得するときに、ユーザー ID を委任する。 これは、Analysis Services がユーザー ID を別のサービスに委任する唯一のシナリオです。  
  
##  <a name="bkmk_SPNSyntax"></a> Analysis Services 用の SPN の形式  
 SPN の登録には **setspn** を使用します。 最近のオペレーティング システムでは、 **setspn** はシステム ユーティリティとしてインストールされます。 詳細については、「 [SetSPN](https://technet.microsoft.com/library/cc731241\(WS.10\).aspx)」をご覧ください。  
  
 次の表では、Analysis Services SPN の各部分について説明します。  
  
|要素|説明|  
|-------------|-----------------|  
|Service クラス|MSOLAPSvc.3 は、サービスを Analysis Services インスタンスとして識別します。 .3 は、Analysis Services 伝送で使用される XMLA-over-TCP/IP プロトコルのバージョンへの参照です。 製品リリースとは無関係です。 つまり、MSOLAPSvc.3 は、プロトコル自体が改訂されない限り、SQL Server 2005、2008、2008 R2、2012、および Analysis Services の今後のリリースで正しいサービス クラスです。|  
|ホスト名|サービスが実行されているコンピューターを識別します。 完全修飾ドメイン名にすることも、NetBIOS 名にすることもできます。 どちらも SPN の登録が必要です。<br /><br /> サーバーの NetBIOS 名の SPN を登録する際は必ず、登録の重複がないか `SetupSPN -S` を使ってご確認ください。 フォレストでは NetBIOS 名の一意性が保証されません。重複する SPN が登録されていると接続エラーが発生します。<br /><br /> 負荷分散された Analysis Services クラスターの場合、ホスト名はクラスターに割り当てられた仮想名にする必要があります。<br /><br /> IP アドレスを使用して SPN を作成しないでください。 Kerberos は、ドメインの DNS 解決機能を使用します。 IP アドレスを指定すると、この機能がバイパスされます。|  
|ポート番号|ポート番号は SPN 構文の一部ですが、Analysis Services SPN を登録する際にポート番号を指定することはありません。 通常は標準 SPN 構文でポート番号を提供するために使用されるコロン (:) 文字が、Analysis Services によってインスタンス名を指定するために使用されます。 Analysis Services インスタンスでは、ポートは既定のポート (TCP 2383) であるか、SQL Server Browser サービスによって割り当てられるポート (TCP 2382) であると見なされます。|  
|インスタンス名|Analysis Services は、同じコンピューター上に複数回インストールできる、レプリケート可能なサービスです。 各インスタンスは、インスタンス名によって識別されます。<br /><br /> インスタンス名の先頭には、コロン (:) 文字が付いています。 たとえば、ホスト コンピューター名が SRV01 で、名前付きインスタンスが SSAS-Tabular である場合、SPN は SRV01:SSAS-Tabular になります。<br /><br /> 名前付き Analysis Services インスタンスを指定するための構文は、他の SQL Server インスタンスによって使用される構文とは異なることに注意してください。 他のサービスは、SPN にインスタンス名を追加するために、円記号 (\) を使用します。|  
|サービス アカウント|これは、 **MSSQLServerOLAPService** Windows サービスの開始アカウントです。 アカウントには、Windows ドメイン ユーザー アカウント、仮想アカウント、管理されたサービス アカウント (MSA)、またはサービスごとの SID、NetworkService、LocalSystem などのビルトイン アカウントを使用できます。 Windows ドメイン ユーザー アカウントを domain \user として書式設定できますかuser@domainします。|  
  
##  <a name="bkmk_virtual"></a> 仮想アカウントに対する SPN の登録  
 仮想アカウントは、SQL Server サービスの既定のアカウント タイプです。 仮想アカウントは**NT service \msolapservice**の既定のインスタンスと**NT service \msolap$** \<インスタンス名 >、名前付きインスタンス。  
  
 "仮想" という名前が示すとおり、Active Directory にはこれらのアカウントが存在しません。 仮想アカウントは、ローカル コンピューター上にのみ存在します。 外部のサービス、アプリケーション、またはデバイスに接続するときは、ローカル コンピューターのアカウントを使って接続が行われます。 したがって、仮想アカウントで実行されている Analysis Services には、実際にはコンピューターのアカウントに対する SPN が登録されていることになります。  
  
 **NT Service\MSOLAPService として実行されている既定のインスタンスの構文例**  
  
 この例に示した **setspn** の構文は、Analysis Services の既定のインスタンスが既定の仮想アカウントで実行されていることを想定しています。 この例で使用されているコンピューターのホスト名は **AW-SRV01**です。 SPN の登録では、仮想アカウント ( *NT Service\MSOLAPService* ) ではなく、 **コンピューターのアカウント**を指定する必要があります。  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
> [!NOTE]  
>  NetBIOS ホスト名用と、ホストの完全修飾ドメイン名用に、必ず 2 つの SPN 登録を作成してください。 Analysis Services に接続するクライアント アプリケーションが、すべて同じホスト名規約を使用しているとは限りません。 SPN 登録を 2 つ作成することによって、両方の形式のホスト名に対応することができます。  
  
 **NT service \msolap$ として実行されている名前付きインスタンスの構文例\<インスタンス名 >**  
  
 この例に示した **setspn** の構文は、名前付きインスタンスが既定の仮想アカウントで実行されていることを想定しています。 この例のコンピューターのホスト名は **AW-SRV02**、インスタンス名は **AW-FINANCE** です。 仮想アカウントではなく、spn に指定されているマシン アカウント**NT service \msolap$** \<インスタンス名 >。  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV02.AdventureWorks.com:AW-FINANCE AW-SRV02  
```  
  
##  <a name="bkmk_domain"></a> ドメイン アカウントに対する SPN の登録  
 Analysis Services インスタンスの実行にはドメイン アカウントを使用するのが一般的です。  
  
 ネットワークまたはハードウェアの負荷分散クラスターで実行される Analysis Services インスタンスにはドメイン アカウントが必要です。クラスター内の各インスタンスが、同じドメイン アカウントで実行される必要があります。  
  
 **ドメイン ユーザーとして実行されている既定のインスタンスの構文例**  
  
 この例に示した **setspn** の構文は、Analysis Services の既定のインスタンスが、AdventureWorks ドメイン内のドメイン ユーザー アカウント **SSAS-Service**で実行されていることを想定しています。  
  
```  
Setspn -s msolapsvc.3\AW-SRV01.Adventureworks.com AdventureWorks\SSAS-Service  
```  
  
> [!TIP]  
>  Analysis Services サーバーに対して SPN が作成されたかどうかは、SPN の登録方法に応じて `Setspn -L <domain account>` または `Setspn -L <machinename>`を実行してご確認ください。 MSOLAPSVC.3/を表示する必要があります\<ホスト名 > 一覧にします。  
  
##  <a name="bkmk_builtin"></a> ビルトイン アカウントに対する SPN の登録  
 この方法はお勧めできませんが、従来の Analysis Services インストールは、Network Service、Local Service、Local System などのビルトイン アカウントで実行されるように構成されていることもあります。  
  
 **ビルトイン アカウントで実行されている既定のインスタンスの構文例**  
  
 ビルトイン アカウントまたはサービスごとの SID で実行されるサービスの SPN 登録は、仮想アカウントに使用される SPN 構文と同じです。 使用するのは仮想アカウント名ではなく、コンピューターのアカウントです。  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnNamed"></a> 名前付きインスタンスのための SPN の登録  
 Analysis Services の名前付きインスタンスには、SQL Server Browser サービスによって検出される動的なポート割り当てが使用されます。 名前付きインスタンスを使用するときは、SQL Server Browser サービスと Analysis Services の名前付きインスタンスの両方の SPN を登録します。 詳細については、「 [SQL Server Analysis Services または SQL Server の名前付きインスタンスへの接続を確立するときに、SQL Server Browser サービスの SPN が必要](https://support.microsoft.com/kb/950599)」をご覧ください。  
  
 **LocalService として実行される SQL Browser サービスの SPN 構文の例**  
  
 サービス クラスは **MSOLAPDisco.3**です。 既定では、このサービスは NT AUTHORITY\LocalService として実行されます。つまり、SPN 登録はコンピューターのアカウントに対して設定されます。 この例では、コンピューターのアカウントは **AW-SRV01**(コンピューター名に対応) です。  
  
```  
Setspn -S MSOLAPDisco.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnCluster"></a> SSAS クラスターのための SPN の登録  
 Analysis Services フェールオーバー クラスターの場合、ホスト名はクラスターに割り当てられた仮想名にする必要があります。 これは、既存の WSFC の上に Analysis Services をインストールしたときに、SQL Server のセットアップ中に指定された、SQL Server のネットワーク名です。 Active Directory で、この名前を見つけることができます。 また、 **[フェールオーバー クラスター マネージャー]**  |  **[ロール]**  |  **[リソース]** タブにも表示されます。[リソース] タブにあるサーバー名は、SPN コマンドで '仮想名' として使用する必要があります。  
  
 **Analysis Services クラスターの SPN 構文**  
  
```  
Setspn -s msolapsvc.3/<virtualname.FQDN > <domain user account>  
```  
  
 Analysis Services クラスターのノードは、各ノードが同じ SID を持つように、既定のポート (TCP 2383) を使用し、同じドメイン ユーザー アカウントで実行する必要があることに注意してください。 詳細については、「 [SQL Server Analysis Services をクラスター化する方法](https://msdn.microsoft.com/library/dn736073.aspx) 」をご覧ください。  
  
##  <a name="bkmk_spnHTTP"></a> HTTP アクセス用に構成された SSAS インスタンスのための SPN の登録  
 ソリューションの要件によっては、Analysis Services を HTTP アクセス用に構成してある場合があります。 ソリューションに中間層コンポーネントとして IIS が含まれ、Kerberos 認証がソリューションの要件である場合は、IIS のために手動で SPN を登録しなければならないことがあります。 詳細についてを参照してください「IIS を実行しているコンピューターで設定を構成する」 [Kerberos 認証を使用するには、SQL Server 2008 Analysis Services と SQL Server 2005 Analysis Services を構成する方法](https://support.microsoft.com/kb/917409)します。  
  
 Analysis Services インスタンスのための SPN の登録という点では、TCP 用に構成されたインスタンスと HTTP 用に構成されたインスタンスとの間に違いはありません。 IIS から Analysis Services への接続は、MSMDPUMP ISAPI 拡張機能を使用して、常に TCP です。  
  
 つまり、既定のインスタンスまたは名前付きインスタンスのために SPN を登録する、前のセクションの手順を使用できます。 ホスト名を指定する際には、HTTP アクセス用にサービスを構成したときに msmdpump.ini ファイルで指定したホスト名を使用してください。  
  
 HTTP アクセスの詳細については、「[インターネット インフォメーション サービス &#40;IIS&#41; 8.0 上の Analysis Services への HTTP アクセスの構成](configure-http-access-to-analysis-services-on-iis-8-0.md)」を参照してください。  
  
##  <a name="bkmk_spnFixedPorts"></a> 固定ポートをリッスンしている SSAS インスタンスのための SPN の登録  
 Analysis Services の SPN 登録では、ポート番号は指定できません。 Analysis Services を既定のインスタンスとしてインストールし、固定ポートでリッスンするように構成した場合は、ここで既定のポート (TCP 2383) でリッスンするように構成する必要があります。 名前付きインスタンスの場合は、SQL Server Browser サービスと動的ポート割り当てを使用する必要があります。  
  
 1 つの Analysis Services インスタンスは、1 つのポートでしかリッスンできません。 複数のポートの使用はサポートされていません。 ポートの構成の詳細については、「 [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [Microsoft BI 認証と ID 委任](https://go.microsoft.com/fwlink/?LinkID=286576)   
 [Kerberos を使用した相互認証](https://go.microsoft.com/fwlink/?LinkId=299283)   
 [Kerberos 認証を使用するように SQL Server 2008 Analysis Services および SQL Server 2005 Analysis Services を構成する方法](https://support.microsoft.com/kb/917409)   
 [サービス プリンシパル名 (SPN) SetSPN の構文 (Setspn.exe)](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [使用する SPN とその理由](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [SetSPN](https://technet.microsoft.com/library/cc731241\(WS.10\).aspx)   
 [サービス アカウントのステップ バイ ステップ ガイド](https://technet.microsoft.com/library/dd548356\(WS.10\).aspx)   
 [Windows サービス アカウントと権限の構成](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [インターネット インフォメーション サービスでホストされている Web アプリケーションを構成するときに SPN を使用する方法](https://support.microsoft.com/kb/929650)   
 [サービス アカウントの新機能新機能](https://technet.microsoft.com/library/dd367859\(WS.10\).aspx)   
 [SharePoint 2010 製品向けの Kerberos 認証の構成 (ホワイト ペーパー)](https://technet.microsoft.com/library/ff829837.aspx)  
  
  
