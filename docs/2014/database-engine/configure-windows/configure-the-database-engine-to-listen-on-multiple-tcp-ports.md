---
title: 複数の TCP ポートでリッスンするデータベース エンジンの構成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], multiple
- TDS
- listen on multiple ports
- endpoints [SQL Server], TDS
- adding ports
- tabular data stream
- multiple ports
ms.assetid: 8e955033-06ef-403f-b813-3d8241b62f1f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c5f3c354a36f5a3a62120ecc40a815420393648c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62811546"
---
# <a name="configure-the-database-engine-to-listen-on-multiple-tcp-ports"></a>複数の TCP ポートでリッスンするデータベース エンジンの構成
  このトピックでは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] で SQL Server 構成マネージャーを使用して、複数の TCP ポートをリッスンするように [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を構成する方法について説明します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で TCP/IP を有効にしている場合、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は、IP アドレスと TCP ポート番号で構成される接続ポイントで着信接続をリッスンします。次の手順では、表形式のデータ ストリーム (TDS) エンドポイントを作成し、追加の TCP ポートを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がリッスンするように設定します。  
  
 2 つ目の TDS エンドポイントを作成する理由として考えられる点を次に示します。  
  
-   特定のサブネットに存在するローカル クライアント コンピューターの既定のエンドポイントへのアクセスを制限するようにファイアウォールを構成することによって、セキュリティを強化することができます。 サポート チーム向けに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] へのインターネット アクセスを保持する場合は、ファイアウォールからインターネットに公開する新しいエンドポイントを作成し、このエンドポイントへの接続の権利をサーバー サポート チームに制限します。  
  
-   NUMA (Non-Uniform Memory Access) を使用する場合に、特定のプロセッサに接続を関係付けることができます。  
  
 TDS エンドポイントの構成手順は次のとおりです。実行する順序は問いません。  
  
-   TCP ポートに対して TDS エンドポイントを作成し、必要に応じて既定のエンドポイントへのアクセスを復元します。  
  
-   対象のサーバー プリンシパルにエンドポイントへのアクセス権を与えます。  
  
-   選択された IP アドレス用の TCP ポート番号を指定します。  
  
 Windows ファイアウォールの既定の設定の詳細と、データベース エンジン、Analysis Services、Reporting Services、および Integration Services に影響する TCP ポートの説明については、「 [SQL Server のアクセスを許可するための Windows ファイアウォールの構成](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)」をご覧ください。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-create-a-tds-endpoint"></a>TDS エンドポイントを作成するには  
  
-   次のステートメントを実行し、サーバー上の利用できるすべての TCP アドレスのポート 1500 に対して **CustomConnection** という名前のエンドポイントを作成します。  
  
    ```  
    USE master;  
    GO  
    CREATE ENDPOINT [CustomConnection]  
    STATE = STARTED  
    AS TCP  
       (LISTENER_PORT = 1500, LISTENER_IP =ALL)  
    FOR TSQL() ;  
    GO  
    ```  
  
 新しい [!INCLUDE[tsql](../../includes/tsql-md.md)] エンドポイントを作成すると、既定の TDS エンドポイントに対する **public** の接続権限は取り消されます。 既定のエンドポイントに対して **public** グループへのアクセスが必要な場合は、 `GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] to [public];` ステートメントを使用してこの権限を再適用します。  
  
#### <a name="to-grant-access-to-the-endpoint"></a>エンドポイントへのアクセスを許可するには  
  
-   次のステートメントを実行し、corp ドメイン内の SQLSupport グループに対して **CustomConnection** エンドポイントへのアクセスを許可します。  
  
    ```  
    GRANT CONNECT ON ENDPOINT::[CustomConnection] to [corp\SQLSupport] ;  
    GO  
    ```  
  
#### <a name="to-configure-the-sql-server-database-engine-to-listen-on-an-additional-tcp-port"></a>追加の TCP ポートでリッスンするように SQL Server データベース エンジンを構成するには  
  
1.  SQL Server 構成マネージャーで **[SQL Server ネットワークの構成]** を展開し、 _[<instance_name>_ **のプロトコル**] をクリックします。  
  
2.  **[ _<instance_name>_ のプロトコル]** を展開し、 **[TCP/IP]** をクリックします。  
  
3.  右ペインで、無効になっている IP アドレスのうち、有効にする IP アドレスをそれぞれ右クリックし、 **[有効化]** をクリックします。  
  
4.  **[IPAll]** を右クリックし、 **[プロパティ]** をクリックします。  
  
5.  **[TCP ポート]** ボックスで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] がリッスンするポートを入力します。複数のポートを指定する場合はコンマで区切ります。 例では、既定のポート 1433 が表示されている場合に入力`,1500`ボックス`1433,1500`、順にクリックします**OK**します。  
  
    > [!NOTE]  
    >  一部の IP アドレスのポートだけを有効にする場合、[プロパティ] ダイアログ ボックスで、必要なアドレスに対してのみ追加のポートを構成します。 次に、コンソール ペインで、 **[TCP/IP]** を右クリックし、 **[プロパティ]** をクリックします。 **[すべて受信待ち]** ボックスで、 **[いいえ]** を選択します。  
  
6.  左ペインで、 **[SQL Server のサービス]** をクリックします。  
  
7.  右ペインで、 **[SQL Server _<instance_name>_ ]** を右クリックし、 **[再起動]** をクリックします。  
  
     [!INCLUDE[ssDE](../../includes/ssde-md.md)]が再起動すると、エラー ログには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がリッスンしているポートが記録されています。  
  
#### <a name="to-connect-to-the-new-endpoint"></a>新しいエンドポイントに接続するには  
  
-   次のステートメントを実行し、ACCT という名前のサーバー上にある、既定の SQL Server インスタンスの **CustomConnection** エンドポイントに接続します。このとき、信頼関係接続を使用します。ユーザーは [corp\SQLSupport] グループのメンバーであると想定しています。  
  
    ```  
    sqlcmd -SACCT,1500  
    ```  
  
## <a name="see-also"></a>関連項目  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)   
 [DROP ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-endpoint-transact-sql)   
 [GRANT Endpoint Permissions &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)   
 [NUMA ノードへの TCP/IP ポートのマッピング &#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)  
  
  
