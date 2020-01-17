---
title: Kerberos 接続用のサービス プリンシパル名の登録 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], SPNs
- network connections [SQL Server], SPNs
- registering SPNs
- Server Principal Names
- SPNs [SQL Server]
ms.assetid: e38d5ce4-e538-4ab9-be67-7046e0d9504e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5acd507be99d7ff36245e723d20aebc36f42a917
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62781997"
---
# <a name="register-a-service-principal-name-for-kerberos-connections"></a>Kerberos 接続用のサービス プリンシパル名の登録
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と Kerberos 認証を併用するには、次の両方の条件が満たされる必要があります。  
  
-   クライアント コンピューターとサーバー コンピューターが、同じ Windows ドメインまたは信頼関係のあるドメインの一部であることが必要です。  
  
-   SPN (サービス プリンシパル名) は、Windows ドメインのキー配布センターの役割を担う Active Directory に登録されることが必要です。 SPN は、登録後に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス サービスを起動した Windows アカウントに対してマップされます。 SPN 登録がまだ実行されていないか失敗した場合、Windows セキュリティ レイヤーは、SPN に関連するアカウントを決定することができず、Kerberos 認証は使用されません。  
  
    > [!NOTE]  
    >  サーバーが SPN を自動的に登録できない場合、SPN を手動で登録する必要があります。 「 [SPN の手動登録](#Manual)」を参照してください。  
  
 Kerberos を使用して接続しているかどうかを確認するには、sys.dm_exec_connections 動的管理ビューに対してクエリを実行します。 次のクエリを実行して auth_scheme 列の値を確認します。Kerberos が有効な場合、この値は "KERBEROS" になります。  
  
```  
SELECT auth_scheme FROM sys.dm_exec_connections WHERE session_id = @@spid ;  
```  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と Kerberos に関する接続性の問題のトラブルシューティングに役立つ診断ツールです。 Kerberos 認証の詳細については、「 [Microsoft® Kerberos Configuration Manager for SQL Server®](https://www.microsoft.com/download/details.aspx?id=39046)」をご覧ください。  
  
##  <a name="Role"></a> 認証での SPN の役割  
 アプリケーションが接続されて Windows 認証を使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client が、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンピューター名、インスタンス名、およびオプションで SPN を渡します。 接続の際に SPN が渡される場合、変更せずに使用されます。  
  
 接続の際に SPN が渡されない場合、使用されたプロトコル、サーバー名、およびインスタンス名に基づいて既定の SPN が構築されます。  
  
 前の両方のシナリオでは、SPN はキー配布センターに送信され、接続認証のためのセキュリティ トークンを取得します。 セキュリティ トークンを取得できない場合、NTLM 認証が使用されます。  
  
 サービス プリンシパル名 (SPN) は、クライアントがサービスのインスタンスを一意に識別するための名前です。 Kerberos 認証サービスでは、SPN を使用してサービスが認証されます。 クライアントがサービスに接続するときに、サービスのインスタンスが検索され、そのインスタンスの SPN が構成されます。次に、サービスに接続され、認証のためにサービスの SPN が提示されます。  
  
> [!NOTE]  
>  このトピックで提供する情報は、クラスタリングを使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成にも適用されます。  
  
 Windows 認証は、SQL Server を認証する場合にお勧めする方法です。 Windows 認証を使用するクライアントは、NTLM または Kerberos のどちらかを使用して認証されます。 Active Directory 環境では、常に Kerberos 認証が最初に試みられます。 Kerberos 認証は、名前付きパイプを使用する [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] クライアントには使用できません。  
  
##  <a name="Permissions"></a> Permissions  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスが起動すると、サービス プリンシパル名 (SPN) の登録が試みられます。 SQL Server を開始しているアカウントに、Active Directory Domain Services に SPN を登録する権限がない場合は、この呼び出しは失敗し、アプリケーション イベント ログと SQL Server エラー ログに警告メッセージが記録されます。 SPN を登録するには、ビルトイン アカウント (ローカル システム (非推奨) や NETWORK SERVICE など) または SPN を登録する権限を持つアカウント (ドメイン管理者アカウントなど) で [!INCLUDE[ssDE](../../includes/ssde-md.md)] が実行されている必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が  [!INCLUDE[win7](../../includes/win7-md.md)] または  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] オペレーティング システムで実行されている場合は、仮想アカウントまたは管理されたサービス アカウント (MSA) を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行できます。 仮想アカウントと MSA の両方で SPN を登録できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がこのいずれかのアカウントで実行されていない場合、SPN は起動時には登録されず、ドメイン管理者が SPN を手動で登録する必要があります。  
  
> [!NOTE]  
>  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 機能レベルよりも低い機能レベルで Windows ドメインが実行されるように構成される場合は、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] サービスの SPN を登録するために必要な権限が、管理されたサービス アカウントに与えられません。 Kerberos 認証が必要な場合は、ドメイン管理者が、管理されたサービス アカウントに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の SPN を手動で登録する必要があります。  
  
 ドメイン管理者ではないアカウントに SPN に対する読み取り権限または書き込み権限を許可する方法については、サポート技術情報の資料「 [SQL Server で Kerberos 認証を使用する方法](https://support.microsoft.com/kb/319723)」を参照してください。  
  
 その他の情報については、「 [SQL Server 2008 で Kerberos の制約付き委任を実装する方法](https://technet.microsoft.com/library/ee191523.aspx)」を参照してください。  
  
##  <a name="Formats"></a> SPN の形式  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]以降では、TCP/IP、名前付きパイプ、および共有メモリで Kerberos 認証をサポートするために、SPN の形式が変更されています。 名前付きインスタンスおよび既定のインスタンスでサポートされている SPN の形式は次のとおりです。  
  
 **[名前付きインスタンス]**  
  
-   *MSSQLSvc/FQDN*:[_port_**|**_instancename_]。各要素の説明は次のとおりです。  
  
    -   *MSSQLSvc* は、登録されるサービスです。  
  
    -   *FQDN* は、サーバーの完全修飾ドメイン名です。  
  
    -   *port* は、TCP ポート番号です。  
  
    -   *instancename* は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前です。  
  
 **[既定のインスタンス]**  
  
-   *MSSQLSVC/FQDN*:_port_**|**_MSSQLSVC/FQDN_。各要素の説明は次のとおりです。  
  
    -   *MSSQLSvc* は、登録されるサービスです。  
  
    -   *FQDN* は、サーバーの完全修飾ドメイン名です。  
  
    -   *port* は、TCP ポート番号です。  
  
 新しい SPN の形式では、ポート番号は必要ありません。 つまり、複数ポートのサーバーまたはポート番号を使用しないプロトコルで Kerberos 認証を使用できます。  
  
> [!NOTE]  
>  TCP ポートが SPN に含まれている TCP/IP 接続の場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、Kerberos 認証を使用して接続するユーザー用に TCP プロトコルを有効にする必要があります。  
  
|||  
|-|-|  
|MSSQLSvc/*fqdn:port*|TCP が使用される場合にプロバイダーが生成する既定の SPN。 *port* は、TCP ポート番号です。|  
|MSSQLSvc/*fqdn*|TCP 以外のプロトコルが使用される場合に、既定のインスタンスに対してプロバイダーが生成する既定の SPN。 *fqdn* は、完全修飾ドメイン名です。|  
|MSSQLSvc/*fqdn:InstanceName*|TCP 以外のプロトコルが使用される場合に、名前付きインスタンスに対してプロバイダーが生成する既定の SPN。 *InstanceName* は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの名前です。|  
  
##  <a name="Auto"></a> SPN の自動登録  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスが開始すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスに対する SPN の登録を試みます。 インスタンスが停止すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は SPN の登録解除を試みます。 TCP/IP 接続の場合、SPN は *MSSQLSvc/\<FQDN>*:*\<tcpport>* という形式で登録されます。名前付きインスタンスと既定のインスタンスは、どちらも *MSSQLSvc* として登録され、インスタンスの区別は *\<tcpport>* の値で行われます。  
  
 形式で Kerberos をサポートするその他の接続用の SPN が登録されている*MSSQLSvc/\<FQDN >*:*\<instancename >* 名前付きインスタンス。 既定のインスタンスを登録する場合の形式は、*MSSQLSvc/\<FQDN>* です。  
  
 SPN の登録または登録解除に必要な権限がサービス アカウントにない場合は、これらのアクションを手動で実行することが必要になる場合があります。  
  
##  <a name="Manual"></a> SPN の手動登録  
 SPN を手動で登録するには、管理者は Microsoft [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] サポート ツールに付属する Setspn.exe ツールを使用する必要があります。 詳細については、サポート技術情報の資料「 [Windows Server 2003 Service Pack 1 のサポート ツール](https://support.microsoft.com/kb/892777) 」を参照してください。  
  
 Setspn.exe は、サービス プリンシパル名 (SPN) ディレクトリ プロパティの読み取り、変更、および削除を実行できるようにするコマンド ライン ツールです。 このツールを使用すると、現在の SPN の表示、アカウントの既定の SPN の再設定、および補足 SPN の追加または削除も実行できます。  
  
 TCP/IP 接続の場合に SPN を手動で登録するために使用される構文例を次に示します。  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:1433 accountname  
```  
  
 **注** SPN が既に存在する場合は、再登録する前に削除する必要があります。 削除するには、 `setspn` スイッチを指定して `-D` コマンドを使用します。 次の例は、新しいインスタンス ベースの SPN を手動で登録する方法を示しています。 既定のインスタンスの場合は、次の構文を使用します。  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com accountname  
```  
  
 名前付きインスタンスの場合は、次の構文を使用します。  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:instancename accountname  
```  
  
##  <a name="Client"></a> クライアント接続  
 クライアント ドライバーでは、ユーザー指定の SPN がサポートされています。 ただし、SPN を指定しない場合は、クライアント接続の種類に基づいて SPN が自動的に生成されます。 TCP 接続の場合は、名前付きインスタンスと既定のインスタンスの両方で、 *MSSQLSvc*/*FQDN*:[*port*] という形式の SPN が使用されます。  
  
 名前付きパイプおよび共有メモリ接続の場合は、名前付きインスタンスでは *MSSQLSvc*/*FQDN*:*instancename* 、既定のインスタンスでは *MSSQLSvc*/*FQDN* という形式の SPN が使用されます。  
  
 **SPN としてのサービス アカウントの使用**  
  
 サービス アカウントを SPN として使用できます。 サービス アカウントは、Kerberos 認証の接続属性を使用して次の形式で指定します。  
  
-   **username@domain** または **domain\username** (ドメイン ユーザー アカウントの場合)  
  
-   **machine$@domain** または **host\FQDN** (ローカル システムや NETWORK SERVICES などのコンピューター ドメイン アカウントの場合)  
  
 接続の認証方法を確認するには、次のクエリを実行します。  
  
```sql  
SELECT net_transport, auth_scheme   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
##  <a name="Defaults"></a> 認証の既定  
 次の表では、SPN の登録シナリオに基づいて使用される認証の既定について説明します。  
  
|シナリオ|認証方法|  
|--------------|---------------------------|  
|SPN が正しいドメイン アカウント、仮想アカウント、MSA、またはビルトイン アカウントにマップされている場合 (ローカル システムや NETWORK SERVICE など)<br /><br /> 注:登録済み SPN によってマップされるアカウントは、SQL Server サービスが実行されているアカウントを適切な手段です。|ローカル接続では NTLM が使用され、リモート接続では Kerberos が使用されます。|  
|SPN が正しいドメイン アカウント、仮想アカウント、MSA、またはビルトイン アカウントである場合<br /><br /> 注:登録済み SPN によってマップされるアカウントは、SQL Server サービスが実行されているアカウントを適切な手段です。|ローカル接続では NTLM が使用され、リモート接続では Kerberos が使用されます。|  
|SPN が正しくないドメイン アカウント、仮想アカウント、MSA、またはビルトイン アカウントにマップされている場合|認証は失敗します。|  
|SPN 参照が失敗したか、正しいドメイン アカウント、仮想アカウント、MSA、またはビルトイン アカウントにマップされていないか、正しいドメイン アカウント、仮想アカウント、MSA、またはビルトイン アカウントではない場合|ローカル接続とリモート接続で NTLM が使用されます。|  
  
##  <a name="Comments"></a> コメント  
 専用管理者接続 (DAC) では、インスタンス名ベースの SPN が使用されます。 その SPN が正常に登録されると、Kerberos 認証を DAC で使用できるようになります。 また、ユーザーがアカウント名を SPN として指定することもできます。  
  
 起動中に SPN の登録が失敗した場合は、この失敗が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログに記録されて、起動が続行されます。  
  
 シャットダウン中に SPN の登録解除が失敗した場合は、この失敗が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログに記録されて、シャットダウンが続行されます。  
  
## <a name="see-also"></a>参照  
 [クライアント接続でのサービス プリンシパル名 &#40;SPN&#41; のサポート](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)   
 [クライアント接続 &#40;OLE DB&#41; でのサービス プリンシパル名 &#40;SPNs&#41;](../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)   
 [クライアント接続 &#40;ODBC&#41; でのサービス プリンシパル名 &#40;SPNs&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)   
 [SQL Server Native Client の機能](../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Reporting Services 環境における Kerberos 認証の問題の管理](https://technet.microsoft.com/library/ff679930.aspx)  
  
  
