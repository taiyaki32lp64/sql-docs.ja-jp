---
title: サーバー ネットワーク アドレスの指定 (データベース ミラーリング) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- database mirroring [SQL Server], endpoint
- endpoints [SQL Server], database mirroring
- server network addresses [SQL Server]
ms.assetid: a64d4b6b-9016-4f1e-a310-b1df181dd0c6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f197eef6369281001359969bf1d92bd0390bedc8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62755058"
---
# <a name="specify-a-server-network-address-database-mirroring"></a>サーバー ネットワーク アドレスの指定 (データベース ミラーリング)
  データベース ミラーリング セッションを設定するには、サーバー インスタンスごとにサーバー ネットワーク アドレスが必要です。 サーバー インスタンスのサーバー ネットワーク アドレスは、システム アドレス、およびインスタンスがリッスンしているポート番号を指定することにより、明確にインスタンスを識別する必要があります。  
  
 サーバー ネットワーク アドレスでポートを指定するには、サーバー インスタンスにデータベース ミラーリング エンドポイントが存在する必要があります。 詳細については、「 [Windows 認証でのデータベース ミラーリング エンドポイントを作成する &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)」を参照してください。  
  
  
  
##  <a name="Syntax"></a> サーバー ネットワーク アドレスの構文  
 サーバー ネットワーク アドレスの構文は、次のような形式になります。  
  
 TCP<strong>://</strong> *\<system-address>* <strong>:<strong> *\<port>* 
  
 パラメーターの説明  
  
-   *\<system-address>* は、ミラーリング先のコンピューター システムを明確に識別する文字列です。 通常、サーバー アドレスは、システム名 (システムが同じドメインに存在する場合)、完全修飾ドメイン名、または IP アドレスになります。  
  
    -   システムが同じドメイン内にある場合、 `SYSTEM46`などのコンピューター システムの名前を使用できます。  
  
    -   IP アドレスを使用するには、それが環境内で一意である必要があります。 IP アドレスが静的である場合にのみ、IP アドレスを使用することをお勧めします。 IP アドレスには、IP Version 4 (IPv4) または IP Version 6 (IPv6) を使用できます。 IPv6 アドレスは、 **[** _<IPv6_address>_ **]** のように、角かっこで囲む必要があります。  
  
         システムの IP アドレスを参照するには、Windows コマンド プロンプトで、 **ipconfig** コマンドを入力します。  
  
    -   完全修飾ドメイン名は動作が保証されています。 これは、場所によって異なる形式を持つローカルに定義されたアドレス文字列です。 常にではありませんが多くの場合、完全修飾ドメイン名は、次の形式のようにコンピューター名、およびピリオド区切りの一連のドメイン セグメントを含む複合名になります。  
  
         _computer_name_ **など) を使用できます。** _domain_segment_[... **.** _domain_segment_]  
  
         *computer_name*はサーバー インスタンスを実行しているコンピューターのネットワーク名、および *domain_segment*[... **.** _domain_segment_] はサーバーのその他のドメイン情報です。たとえば、 `localinfo.corp.Adventure-Works.com`のようになります。  
  
         ドメイン セグメントの内容と数は、会社内または組織内で決定されます。 使用しているサーバーの完全修飾ドメイン名がわからない場合は、システム管理者に問い合わせてください。  
  
        > [!NOTE]  
        >  完全修飾ドメイン名の検索方法の詳細については、このトピックの「完全修飾ドメイン名の検索」を参照してください。  
  
-   *\<port>* は、パートナー サーバー インスタンスのデータベース ミラーリング エンドポイントによって使用されるポート番号です。 エンドポイントの指定の詳細については、「 [Windows 認証でのデータベース ミラーリング エンドポイントを作成する &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)」を参照してください。  
  
     データベース ミラーリング エンドポイントは、コンピューター システム上の使用可能な任意のポートを使用できます。 コンピューター システム上の各ポート番号は 1 つのエンドポイントだけに関連付けられている必要があります。また、各エンドポイントは 1 つのサーバー インスタンスに関連付けられています。そのため、1 台のサーバー上に複数のサーバー インスタンスがある場合、各サーバー インスタンスは、ポートが異なる別のエンドポイントでリッスンします。 したがって、データベース ミラーリング セッションを設定するときにサーバー ネットワーク アドレスで指定するポートにより、必ず、エンドポイントがそのポートに関連付けられているサーバー インスタンスにセッションがリダイレクトされます。  
  
     サーバー インスタンスのサーバー ネットワーク アドレスでは、そのミラーリング エンドポイントに関連付けられているポートの番号によってのみ、そのインスタンスがコンピューター上のその他のインスタンスと区別されます。 次の図は、1 台のコンピューターにある 2 つのサーバー インスタンスのサーバー ネットワーク アドレスを示しています。 既定のインスタンスではポート `7022` が使用され、名前付きインスタンスではポート `7033`が使用されます。 これら 2 つのサーバー インスタンスのサーバー ネットワーク アドレスは、それぞれ `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7022` と `TCP://MYSYSTEM.Adventure-works.MyDomain.com:7033`です。 アドレスにサーバー インスタンス名が含まれていないことに注意してください。  
  
     ![既定のインスタンスのサーバー ネットワーク アドレス](../media/dbm-2-instances-ports-1-system.gif "既定のインスタンスのサーバー ネットワーク アドレス")  
  
     サーバー インスタンスのデータベース ミラーリング エンドポイントに現在関連付けられているポートを識別するには、次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを使用します。  
  
    ```  
    SELECT type_desc, port FROM sys.tcp_endpoints  
    ```  
  
     **type_desc** の値が "DATABASE_MIRRORING" の行を検索し、対応するポート番号を使用します。  
  
### <a name="examples"></a>使用例  
  
#### <a name="a-using-a-system-name"></a>A. システム名を使用する  
 次のサーバー ネットワーク アドレスでは、システム名 `SYSTEM46`およびポート `7022`を指定しています。  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://SYSTEM46:7022';  
```  
  
#### <a name="b-using-a-fully-qualified-domain-name"></a>B. 完全修飾ドメイン名を使用する  
 次のサーバー ネットワーク アドレスでは、完全修飾ドメイン名 `DBSERVER8.manufacturing.Adventure-Works.com`およびポート `7024`を指定しています。  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://DBSERVER8.manufacturing.Adventure-Works.com:7024';  
```  
  
#### <a name="c-using-ipv4"></a>C. IPv4 を使用する  
 次のサーバー ネットワーク アドレスでは、IPv4 アドレス `10.193.9.134`およびポート `7023`を指定しています。  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://10.193.9.134:7023';  
```  
  
#### <a name="d-using-ipv6"></a>D. IPv6 を使用する  
 次のサーバー ネットワーク アドレスでは、IPv6 アドレス `2001:4898:23:1002:20f:1fff:feff:b3a3`およびポート `7022`を指定しています。  
  
```  
ALTER DATABASE AdventureWorks SET PARTNER ='tcp://[2001:4898:23:1002:20f:1fff:feff:b3a3]:7022';  
```  
  
## <a name="finding-the-fully-qualified-domain-name"></a>完全修飾ドメイン名の検索  
 システムの完全修飾ドメイン名を検索するには、そのシステムの Windows コマンド プロンプトで次のように入力します。  
  
 **IPCONFIG /ALL**  
  
 完全修飾ドメイン名を作成するには、次に示すように、 *<host_name>* と *<Primary_Dns_Suffix>* の値を連結します:  
  
 _<host_name>_ **.** _<Primary_Dns_Suffix>_  
  
 たとえば、次のような IP 構成があるとします。  
  
 `Host Name  .  .  .  .  .  .  : MYSERVER`  
  
 `Primary Dns Suffix  .  .  .  : mydomain.Adventure-Works.com`  
  
 この場合、完全修飾ドメイン名は次のようになります。  
  
 `MYSERVER.mydomain.Adventure-Works.com`  
  
##  <a name="Examples"></a> 使用例  
 次の例では、別のドメイン内の `REMOTESYSTEM3` という名前のコンピューター システム上にあるサーバー インスタンスのサーバー ネットワーク アドレスを示します。 ドメイン情報は `NORTHWEST.ADVENTURE-WORKS.COM`であり、データベース ミラーリング エンドポイントのポートは `7025`です。 これらのコンポーネントから、サーバー ネットワーク アドレスは次のようになります。  
  
 `TCP://REMOTESYSTEM3.NORTHWEST.ADVENTURE-WORKS.COM:7025`  
  
 次の例では、 `DBSERVER1`という名前のコンピューター システム上にあるサーバー インスタンスのサーバー ネットワーク アドレスを示します。 このシステムはローカル ドメイン内にあり、システム名によって明確に識別されています。 データベース ミラーリング エンドポイントのポートは `7022`です。  
  
 `TCP://DBSERVER1:7022`  
  
##  <a name="RelatedTasks"></a> 関連タスク  
  
-   [Windows 認証でのデータベース ミラーリング エンドポイントを作成する &#40;Transact-SQL&#41;](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
## <a name="see-also"></a>関連項目  
 [データベース ミラーリング &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](the-database-mirroring-endpoint-sql-server.md)  
  
  
