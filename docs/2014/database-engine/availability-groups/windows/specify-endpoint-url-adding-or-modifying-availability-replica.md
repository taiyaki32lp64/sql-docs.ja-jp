---
title: 可用性レプリカを追加または変更するときにエンドポイント URL を指定する (SQL Server) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- endpoints [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], endpoint
- Endpoint URLs (HADR)
ms.assetid: d7520c13-a8ee-4ddc-9e9a-54cd3d27ef1c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 524f9d4b3173a70d3491f2efc0f00f4061c4d6b4
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797970"
---
# <a name="specify-the-endpoint-url-when-adding-or-modifying-an-availability-replica-sql-server"></a>可用性レプリカを追加または変更する場合のエンドポイント URL の指定 (SQL Server)
  可用性グループの可用性レプリカをホストするには、サーバー インスタンスにデータベース ミラーリング エンドポイントが存在する必要があります。 サーバー インスタンスでは、このエンドポイントを使用して、他のサーバー インスタンスによってホストされる可用性レプリカから [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] のメッセージをリッスンします。 可用性グループの可用性レプリカを定義するには、そのレプリカをホストするサーバー インスタンスのエンドポイント URL を指定する必要があります。 *エンドポイント URL* は、データベース ミラーリング エンドポイントのトランスポート プロトコル (TCP)、サーバー インスタンスのシステム アドレス、およびエンドポイントに関連付けられているポート番号を識別します。  
  
> [!NOTE]  
>  "エンドポイント URL" という用語は、データベース ミラーリングのユーザー インターフェイスとドキュメントで使用される "サーバー ネットワーク アドレス" という用語と同義です。  
  
-   [エンドポイント URL の構文](#SyntaxOfURL)  
  
-   [システムの完全修飾ドメイン名の検索](#Finding_FQDN)  
  
-   [関連タスク](#RelatedTasks)  
  
-   [関連コンテンツ](#RelatedContent)  
  
##  <a name="SyntaxOfURL"></a> エンドポイント URL の構文  
 エンドポイント URL の構文は、次のような形式になります。  
  
 TCP<strong>://</strong> *\<system-address>* <strong>:</strong> *\<port>*  
  
 パラメーターの説明  
  
-   *\<system-address&gt;* は、ターゲット コンピューター システムを明確に識別する文字列です。 通常、サーバー アドレスは、システム名 (システムが同じドメインに存在する場合)、完全修飾ドメイン名、または IP アドレスになります。  
  
    -   Windows Server フェールオーバー クラスタリング (WSFC) クラスターのノードが同じドメイン内にある場合、コンピューター システムの名前 ( `SYSTEM46`など) を使用できます。  
  
    -   IP アドレスを使用するには、それが環境内で一意である必要があります。 IP アドレスが静的である場合にのみ、IP アドレスを使用することをお勧めします。 IP アドレスには、IP Version 4 (IPv4) または IP Version 6 (IPv6) を使用できます。 IPv6 アドレスは、 **[** _<IPv6_address>_ **]** のように、角かっこで囲む必要があります。  
  
         システムの IP アドレスを参照するには、Windows コマンド プロンプトで、 **ipconfig** コマンドを入力します。  
  
    -   完全修飾ドメイン名は動作が保証されています。 これは、場所によって異なる形式を使用するローカルに定義されたアドレス文字列です。 常にではありませんが多くの場合、完全修飾ドメイン名は、次の形式のようにコンピューター名、およびピリオド区切りの一連のドメイン セグメントを含む複合名になります。  
  
         _computer_name_ **など) を使用できます。** _domain_segment_[... **.** _domain_segment_]  
  
         *computer_name*はサーバー インスタンスを実行しているコンピューターのネットワーク名、および *domain_segment*[... **.** _domain_segment_] はサーバーのその他のドメイン情報です。たとえば、 `localinfo.corp.Adventure-Works.com`のようになります。  
  
         ドメイン セグメントの内容と数は、会社内または組織内で決定されます。 詳細については、このトピックの「 [完全修飾ドメイン名の検索](#Finding_FQDN)」を参照してください。  
  
-   *\<port>* は、パートナー サーバー インスタンスのデータベース ミラーリング エンドポイントによって使用されるポート番号です。  
  
     データベース ミラーリング エンドポイントは、コンピューター システム上の使用可能な任意のポートを使用できます。 各ポート番号は 1 つのエンドポイントだけに関連付けられている必要があります。また、各エンドポイントは 1 つのサーバー インスタンスに関連付けられています。そのため、1 台のサーバー上に複数のサーバー インスタンスがある場合、各サーバー インスタンスは、ポートが異なる別のエンドポイントでリッスンします。 したがって、可用性レプリカを指定するときにエンドポイント URL で指定するポートにより、必ず、エンドポイントがそのポートに関連付けられているサーバー インスタンスに受信メッセージがリダイレクトされます。  
  
     エンドポイント URL で、ターゲット コンピューターのミラーリング エンドポイントに関連付けられているサーバー インスタンスを識別するのは、ポートの番号だけです。 次の図は、1 台のコンピューターにある 2 つのサーバー インスタンスのエンドポイント URL を示しています。 既定のインスタンスではポート `7022` が使用され、名前付きインスタンスではポート `7033`が使用されます。 これら 2 つのサーバー インスタンスのエンドポイント URL は、それぞれ `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7022` と `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7033`です。 アドレスにサーバー インスタンス名が含まれていないことに注意してください。  
  
     ![既定のインスタンスのサーバーネットワークアドレス](../../media/dbm-2-instances-ports-1-system.gif "既定のインスタンスのサーバーネットワークアドレス")  
  
     サーバー インスタンスのデータベース ミラーリング エンドポイントに現在関連付けられているポートを識別するには、次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```sql
    SELECT type_desc, port FROM sys.TCP_endpoints  
    ```  
  
     **type_desc** の値が "DATABASE_MIRRORING" の行を検索し、対応するポート番号を使用します。  
  
### <a name="examples"></a>使用例  
  
#### <a name="a-using-a-system-name"></a>A. システム名を使用する  
 次のエンドポイント URL では、システム名 `SYSTEM46`およびポート `7022`を指定しています。  
  
 `TCP://SYSTEM46:7022`  
  
#### <a name="b-using-a-fully-qualified-domain-name"></a>b. 完全修飾ドメイン名を使用する  
 次のエンドポイント URL では、完全修飾ドメイン名 `DBSERVER8.manufacturing.Adventure-Works.com`およびポート `7024`を指定しています。  
  
 `TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024`  
  
#### <a name="c-using-ipv4"></a>C. IPv4 を使用する  
 次のエンドポイント URL では、IPv4 アドレス `10.193.9.134`およびポート `7023`を指定しています。  
  
 `TCP://10.193.9.134:7023`  
  
#### <a name="d-using-ipv6"></a>D. IPv6 を使用する  
 次のエンドポイント URL では、IPv6 アドレス `2001:4898:23:1002:20f:1fff:feff:b3a3`およびポート `7022`を指定しています。  
  
 `TCP://[2001:4898:23:1002:20f:1fff:feff:b3a3]:7022`  
  
##  <a name="Finding_FQDN"></a> システムの完全修飾ドメイン名の検索  
 システムの完全修飾ドメイン名を検索するには、そのシステムの Windows コマンド プロンプトで次のように入力します。  
  
 **IPCONFIG /ALL**  
  
 完全修飾ドメイン名を作成するには、次に示すように、 *<host_name>* と *<Primary_Dns_Suffix>* の値を連結します:  
  
 _<host_name>_ **.** _<Primary_Dns_Suffix>_  
  
 たとえば、次のような IP 構成があるとします。  
  
 `Host Name  .  .  .  .  .  .  : MYSERVER`  
  
 `Primary Dns Suffix  .  .  .  : mydomain.Adventure-Works.com`  
  
 この場合、完全修飾ドメイン名は次のようになります。  
  
 `MYSERVER.mydomain.Adventure-Works.com`  
  
> [!NOTE]  
>  完全修飾ドメイン名に関する情報が必要な場合は、システム管理者に問い合わせてください。  
  
##  <a name="RelatedTasks"></a> 関連タスク  
 **データベース ミラーリング エンドポイントを構成するには**  
  
-   [AlwaysOn 可用性グループ&#40;SQL Server PowerShell のデータベースミラーリングエンドポイントを作成する&#41;](database-mirroring-always-on-availability-groups-powershell.md)  
  
-   [Windows 認証でのデータベース ミラーリング エンドポイントを作成する &#40;Transact-SQL&#41;](../../database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [データベース ミラーリング エンドポイントでの証明書の使用 &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [データベース ミラーリング エンドポイントで発信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [データベース ミラーリング エンドポイントで着信接続に証明書を使用できるようにする &#40;Transact-SQL&#41;](../../database-mirroring/database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [サーバー ネットワーク アドレスの指定 &#40;データベース ミラーリング&#41;](../../database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [AlwaysOn 可用性グループ構成&#40;SQL Server&#41;削除された問題のトラブルシューティング](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
 **データベース ミラーリング エンドポイントに関する情報を表示するには**  
  
-   [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
 **可用性レプリカを追加するには**  
  
-   [可用性グループへのセカンダリ レプリカの追加 &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
-   [可用性グループへのセカンダリ レプリカの参加 &#40;SQL Server&#41;](join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> 関連コンテンツ  
  
-   [高可用性とディザスターリカバリーのための AlwaysOn ソリューションガイドの Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
## <a name="see-also"></a>参照  
 [可用性グループの作成と構成 &#40;SQL Server&#41;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [AlwaysOn 可用性グループ&#40;SQL Server&#41;の概要](overview-of-always-on-availability-groups-sql-server.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)  
