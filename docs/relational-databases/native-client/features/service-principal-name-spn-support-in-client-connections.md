---
title: 接続でのサービスプリンシパル名
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, SPNs
- ODBC, SPNs
- OLE DB, SPNs
- SPNs [SQL Server]
ms.assetid: 96598c69-ce9a-4090-aacb-d546591e8af7
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dd5de2c8ebb163fce7287f49df35c2bc5e88f438
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247431"
---
# <a name="service-principal-name-spn-support-in-client-connections"></a>クライアント接続でのサービス プリンシパル名 (SPN) のサポート
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  
  [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]以降では、サービス プリンシパル名 (SPN) のサポートが強化されて、あらゆるプロトコルでの相互認証が可能になりました。 以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスの既定の SPN が Active Directory に登録されているときに、Kerberos over TCP に対してのみ SPN がサポートされていました。  
  
 SPN は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが実行されているアカウントを認証プロトコルで特定するために使用されます。 インスタンスのアカウントが判明した場合は、Kerberos 認証を使用したクライアントとサーバーによる相互認証が可能となります。 インスタンスのアカウントが不明である場合は、NTLM 認証を使用して、サーバーによるクライアントの認証のみが行われます。 現時点では、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client がこの認証を参照して、インスタンス名とネットワーク接続のプロパティから SPN を生成します。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが起動時に行いますが、手動で登録することもできます。 ただし、SPN を登録するアカウントのアクセス権が不十分である場合は、登録が失敗します。  
  
 ドメインおよびコンピューター アカウントは、自動的に Active Directory に登録されます。 これらのアカウントを SPN として使用することも、管理者が独自に SPN を定義することもできます。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、使用する SPN をクライアントが直接指定できるようにすることで、セキュリティで保護された認証の管理性と信頼性を高めています。  
  
> [!NOTE]  
>  クライアント アプリケーションで指定された SPN は、Windows 統合セキュリティを使用して接続されている場合にのみ使用されます。  
  
> [!TIP]  
>  の kerberos Configuration Manager は、での kerberos に[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]関連する接続**の[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]問題のトラブルシューティングに役立つ診断ツールです。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ** Kerberos 認証の詳細については、「 [Microsoft® Kerberos Configuration Manager for SQL Server®](https://www.microsoft.com/download/details.aspx?id=39046)」をご覧ください。  
  
 Kerberos の詳細については、次の記事を参照してください。  
  
-   [Windows 向けの Kerberos の技術的な補足](/previous-versions/msp-n-p/ff649429(v=pandp.10))  
  
-   [Microsoft Kerberos](https://go.microsoft.com/fwlink/?LinkID=100758)  
  
## <a name="usage"></a>使用法  
 次の表では、セキュリティで保護された認証をクライアント アプリケーションで使用するための、最も一般的なシナリオについて説明します。  
  
|シナリオ|説明|  
|--------------|-----------------|  
|レガシ アプリケーションで SPN が指定されない。|この互換性のシナリオでは、以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]で作成されたアプリケーションの動作が変更されないことが保証されます。 SPN が指定されていない場合、アプリケーションは生成された SPN を使用し、どの認証方法が使用されるかは認識しません。|  
|現在のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を使用するクライアント アプリケーションで、接続文字列に含まれる SPN が、ドメイン ユーザー アカウント、コンピューター アカウント、インスタンス固有の SPN、またはユーザー定義文字列として指定される。|プロバイダー文字列、初期化文字列、または接続文字列で **ServerSPN** キーワードを使用することで、次の操作が可能になります。<br /><br /> - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが接続に使用するアカウントを指定できます。 これにより、Kerberos 認証へのアクセスが簡単になります。 Kerberos キー配布センター (KDC) が存在し、かつ正しいアカウントが指定された場合は、NTLM よりも Kerberos 認証が使用される可能性が高くなります。 KDC は通常、ドメイン コントローラーと同じコンピューターに存在します。<br /><br /> - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのサービス アカウントを参照するための SPN を指定できます。 この目的で使用できる既定の SPN が、すべての [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに 2 つずつ生成されます。 ただし、これらのキーが Active Directory に存在することは保証されないため、この状況では Kerberos 認証は保証されません。<br /><br /> - [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスのサービス アカウントを参照するために使用される SPN を指定できます。 これは、サービス アカウントにマップされる任意のユーザー定義文字列でかまいません。 この場合は、キーを手動で KDC に登録する必要があり、キーがユーザー定義 SPN の規則を満たしていることも必要です。<br /><br /> 
  **FailoverPartnerSPN** キーワードを使用すると、フェールオーバー パートナー サーバーの SPN を指定できます。 アカウントおよび Active Directory キーの値の範囲は、プリンシパル サーバーに指定できる値と同じです。|  
|ODBC アプリケーションで、SPN がプリンシパル サーバーまたはフェールオーバー パートナー サーバーの接続属性として指定される。|接続属性 **SQL_COPT_SS_SERVER_SPN** を使用して、プリンシパル サーバーへの接続用の SPN を指定できます。<br /><br /> 接続属性 **SQL_COPT_SS_FAILOVER_PARTNER_SPN** を使用して、フェールオーバー パートナー サーバーの SPN を指定できます。|  
|OLE DB アプリケーションで、SPN がプリンシパル サーバーまたはフェールオーバー パートナー サーバーのデータ ソース初期化プロパティとして指定される。|
  **SSPROP_INIT_SERVER_SPN** プロパティ セット内の接続プロパティ **DBPROPSET_SQLSERVERDBINIT** を使用して、接続用の SPN を指定できます。<br /><br /> 
  **SSPROP_INIT_FAILOVER_PARTNER_SPN** 内の接続プロパティ **DBPROPSET_SQLSERVERDBINIT** を使用して、フェールオーバー パートナー サーバーの SPN を指定できます。|  
|ユーザーが、サーバーまたはフェールオーバー パートナー サーバーの SPN を ODBC データ ソース名 (DSN) で指定する。|SPN は、DSN を設定するダイアログ ボックスを使用して ODBC DSN に指定できます。|  
|ユーザーが、サーバーまたはフェールオーバー パートナー サーバーの SPN を、OLE DB の **[データ リンク]** または **[ログイン]** ダイアログ ボックスで指定する。|SPN は、 **[データ リンク]** または **[ログイン]** ダイアログ ボックスで指定できます。 
  **[ログイン]** ダイアログ ボックスは、ODBC または OLE DB で使用できます。|  
|ODBC アプリケーションで、接続の確立に使用された認証方法が特定される。|接続が正常に開いている場合、アプリケーションでは接続属性 **SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD** をクエリして、使用された認証方法を特定できます。 値には **NTLM** や **Kerberos**がありますが、その他の値もあります。|  
|OLE DB アプリケーションで、接続の確立に使用された認証方法が特定される。|接続が正常に開いている場合、アプリケーションでは **SSPROP_AUTHENTICATION_METHOD** プロパティ セット内の接続プロパティ **DBPROPSET_SQLSERVERDATASOURCEINFO** をクエリして、使用された認証方法を特定できます。 値には **NTLM** や **Kerberos**がありますが、その他の値もあります。|  
  
## <a name="failover"></a>フェールオーバー  
 SPN はフェールオーバー キャッシュに保存されないため、接続間で受け渡すことができません。 接続文字列または接続属性に SPN が指定されると、プリンシパルおよびパートナーへの接続が試行されるたびに SPN が使用されます。  
  
## <a name="connection-pooling"></a>接続のプール  
 SPN をすべての文字列ではなく一部の接続文字列で指定すると、プールが断片化する原因となることがあるので、アプリケーションでは注意が必要です。  
  
 アプリケーションでは、接続文字列キーワードを指定する代わりに、プログラムによって SPN を接続属性として指定できます。 こうすると、接続プールの断片化を管理するうえで役立ちます。  
  
 接続文字列内の SPN は対応する接続属性を設定することでオーバーライドできますが、接続のプールで使用される接続文字列は、プールの目的で接続文字列値を使用するので、アプリケーションでは注意が必要です。  
  
## <a name="down-level-server-behavior"></a>下位サーバーの動作  
 新しい接続動作はクライアントで実装されるため、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のバージョンに固有ではありません。  
  
## <a name="linked-servers-and-delegation"></a>リンク サーバーと委任  
 リンクサーバーを作成するときに、 [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)の** \@provstr**パラメーターを使用して、サーバーおよびフェールオーバーパートナーの spn を指定できます。 これを実行するメリットは、クライアント接続文字列で SPN を指定する場合と同じです。つまり、Kerberos 認証を使う接続を確立する方が、より簡単でより信頼性が高くなります。  
  
 リンク サーバーでの委任には、Kerberos 認証が必要です。  
  
## <a name="management-aspects-of-spns-specified-by-applications"></a>アプリケーションによって指定される SPN の管理上の考慮事項  
 SPN をアプリケーションで接続文字列を通じて指定するか、プログラムで接続プロパティを通じて指定するか (プロバイダーが生成した既定の SPN を使用しない) を選択する際には、次の事項を検討してください。  
  
-   セキュリティ : 指定した SPN が保護されている情報を開示する可能性。  
  
-   信頼性 : 既定の SPN を使用できるようにするには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを実行するサービス アカウントに、KDC 上の Active Directory を更新するための十分な権限が必要です。  
  
-   利便性と場所の透過性 : アプリケーションのデータベースを別の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスに移した場合の、アプリケーションの SPN に対する影響。 データベース ミラーリングを使用する場合は、プリンシパル サーバーとそのフェールオーバー パートナーの両方について、この事項を検討する必要があります。 また、サーバーの変更に伴って SPN を変更する場合のアプリケーションに対する影響や、 すべての変更に関する管理の有無についても検討してください。  
  
## <a name="specifying-the-spn"></a>SPN の指定  
 SPN は、ダイアログ ボックスおよびコードで指定できます。 ここでは、SPN を指定する方法について説明します。  
  
 SPN の最大長は 260 文字です。  
  
 接続文字列または接続属性で SPN に使用される構文は次のとおりです。  
  
|構文|説明|  
|------------|-----------------|  
|MSSQLSvc/*fqdn*|TCP 以外のプロトコルが使用される場合に、既定のインスタンスに対してプロバイダーが生成する既定の SPN。<br /><br /> *fqdn*は完全修飾ドメイン名です。|  
|MSSQLSvc/*fqdn*:*port*|TCP が使用される場合にプロバイダーが生成する既定の SPN。<br /><br /> *port*は、TCP ポート番号です。|  
|MSSQLSvc/*fqdn*:*InstanceName*|TCP 以外のプロトコルが使用される場合に、名前付きインスタンスに対してプロバイダーが生成する既定の SPN。<br /><br /> *InstanceName*は[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]インスタンス名です。|  
|HOST/*fqdn*<br /><br /> HOST/*MachineName*|Windows で自動的に登録されるビルトイン コンピューター アカウントにマップされる SPN。|  
|*ユーザー名*@*ドメイン*|ドメイン アカウントの直接指定。<br /><br /> *Username*は Windows ユーザーアカウント名です。<br /><br /> *ドメイン*は、Windows ドメイン名または完全修飾ドメイン名です。|  
|*MachineName*$@*ドメイン*|コンピューター アカウントの直接指定。<br /><br /> (接続先のサーバーが、LOCAL SYSTEM または NETWORK SERVICE アカウントで実行されている場合に Kerberos 認証を使用するには、 **ServerSPN** を *MachineName*$@*Domain* の形式で指定できます。)|  
|*Kdckey*/*MachineName*|ユーザー指定の SPN。<br /><br /> *Kdckey*は、KDC キーの規則に準拠した英数字の文字列です。|  
  
## <a name="odbc-and-ole-db-syntax-supporting-spns"></a>SPN をサポートする ODBC および OLE DB の構文  
 各構文の情報については、次のトピックを参照してください。  
  
-   [クライアント接続 &#40;のサービスプリンシパル名 &#40;Spn&#41; ODBC&#41;](../../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [クライアント接続 &#40;OLE DB のサービスプリンシパル名 &#40;Spn&#41;&#41;](../../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
 この機能を説明するサンプル アプリケーションについては、「 [SQL Server データ プログラミング サンプル](https://msftdpprodsamples.codeplex.com/)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client 機能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
[Kerberos 接続用のサービス プリンシパル名の登録](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)  
  
