---
title: ネットワーク プロトコルとネットワーク ライブラリ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- protocols [SQL Server]
- configuration options [SQL Server], protocols
- network libraries [SQL Server]
- protocols [SQL Server], about network protocols
- pipes [SQL Server]
- network protocols [SQL Server]
- default SQL Server configurations
- library [SQL Server]
- network protocols [SQL Server], about network protocols
- configuration options [SQL Server], libraries
ms.assetid: 8cd437f6-9af1-44ce-9cb0-4d10c83da9ce
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f4649f6a5abd9726a1b01e3ed30d6cabf88aef9e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067699"
---
# <a name="network-protocols-and-network-libraries"></a>ネットワーク プロトコルとネットワーク ライブラリ
  サーバーは、一度に複数のネットワーク プロトコルでリッスンまたは監視することができます。 ただし、これには各プロトコルを構成する必要があります。 特定のプロトコルが構成されていない場合、サーバーはそのプロトコルでリッスンできません。 インストール後、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、プロトコルの構成を変更できます。  
  
## <a name="default-sql-server-network-configuration"></a>SQL Server の既定のネットワーク構成  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスは、TCP/IP ポート 1433 と名前付きパイプ \\\\.\pipe\sql\query です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前付きインスタンスは TCP 動的ポートに構成され、ポート番号がオペレーティング システムによって割り当てられます。  
  
 動的ポート アドレスを使用できない場合 (たとえば、特定のポート アドレスを通過するように構成されたファイアウォール サーバーを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の接続が通過する必要がある場合) は、 未割り当てのポート番号を選択してください。 ポート番号の割り当ては、Internet Assigned Numbers Authority によって管理され、[http://www.iana.org](https://go.microsoft.com/fwlink/?LinkId=48844) に一覧が掲載されています。  
  
 セキュリティを強化するため、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール時にネットワーク接続は完全には有効になっていません。 セットアップの完了後にネットワーク プロトコルを有効化、無効化、または構成するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ネットワークの構成領域を使用します。  
  
## <a name="server-message-block-protocol"></a>サーバー メッセージ ブロック プロトコル  
 境界ネットワーク内のサーバーでは、サーバー メッセージ ブロック (SMB) を含め、不要なプロトコルをすべて無効にする必要があります。 Web サーバーとドメイン ネーム システム (DNS) サーバーは SMB を必要としません。 ユーザー列挙の脅威に対抗するためには、このプロトコルを無効にする必要があります。  
  
> [!WARNING]
>  サーバー メッセージ ブロックを無効にすると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Windows クラスター サービスからリモート ファイル共有にアクセスできなくなります。 以下のいずれかの作業を行う、または計画している場合は、SMB を無効にしないでください。  
> 
>  -   Windows クラスター ノードおよびファイル共有マジョリティ クォーラム モードを使用する  
> -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインストール時に SMB ファイル共有をデータ ディレクトリとして指定する  
> -   SMB ファイル共有でデータベース ファイルを作成する  
  
#### <a name="to-disable-smb"></a>SMB を無効にするには  
  
1.  **[スタート]** ボタンをクリックし、 **[設定]** をポイントして、 **[ネットワークとダイヤルアップ接続]** をクリックします。  
  
     インターネットに直接つながっている接続を右クリックし、 **[プロパティ]** をクリックします。  
  
2.  **[Microsoft ネットワーク用クライアント]** チェック ボックスをオンにして、 **[アンインストール]** をクリックします。  
  
3.  アンインストールの手順に従います。  
  
4.  **[Microsoft ネットワーク用ファイルとプリンター共有]** チェック ボックスをオンにして、 **[アンインストール]** をクリックします。  
  
5.  アンインストールの手順に従います。  
  
#### <a name="to-disable-smb-on-servers-accessible-from-the-internet"></a>インターネットからアクセス可能なサーバーで SMB を無効にするには  
  
-   [ローカル エリア接続のプロパティ] で、 **[インターネット プロトコル (TCP/IP) のプロパティ]** ダイアログ ボックスを使用して、 **[Microsoft ネットワーク用ファイルとプリンター共有]** と **[Microsoft ネットワーク用クライアント]** を削除します。  
  
## <a name="endpoints"></a>エンドポイント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続に関して新しい概念が導入されました。接続は、 [!INCLUDE[tsql](../../includes/tsql-md.md)]*エンドポイント*によりサーバー エンドで表されます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] エンドポイントに対して、権限の許可、取り消し、および拒否が行われます。 既定では、sysadmin グループのメンバーまたはエンドポイント所有者によって拒否または取り消しが行われない限り、エンドポイントへアクセスする権限はすべてのユーザーにあります。 GRANT、REVOKE、および DENY ENDPOINT 構文では、管理者がエンドポイントのカタログ ビューから取得する必要があるエンドポイント ID を使用します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップを実行すると、専用管理者接続のエンドポイントに加えて、サポートされるすべてのネットワーク プロトコルの [!INCLUDE[tsql](../../includes/tsql-md.md)] エンドポイントが作成されます。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] セットアップで作成される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エンドポイントは次のとおりです。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] ローカル マシン  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 名前付きパイプ  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 既定 TCP  
  
 エンドポイントの詳細については、「[複数の TCP ポートでリッスンするデータベース エンジンの構成](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md)」と「[エンドポイントのカタログ ビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql)」を参照してください。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ネットワーク構成の詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの次のトピックを参照してください。  
  
-   [サーバー ネットワークの構成](../../database-engine/configure-windows/server-network-configuration.md)  
  
## <a name="see-also"></a>関連項目  
 [セキュリティ構成](../../relational-databases/security/surface-area-configuration.md)   
 [SQL Server インストールにおけるセキュリティの考慮事項](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [SQL Server のインストール計画](../../../2014/sql-server/install/planning-a-sql-server-installation.md)  
  
  
