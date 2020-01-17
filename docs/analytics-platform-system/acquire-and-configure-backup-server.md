---
title: バックアップサーバーの取得 & 構成
description: この記事では、Analytics Platform System (APS) と Parallel Data Warehouse (PDW) のバックアップおよび復元機能で使用するために、非アプライアンス Windows システムをバックアップサーバーとして構成する方法について説明します。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e160c606b19933934ec844b477ffec08475307d8
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401490"
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>並列データウェアハウスのバックアップサーバーを取得して構成する
この記事では、Analytics Platform System (APS) と Parallel Data Warehouse (PDW) のバックアップおよび復元機能で使用するために、非アプライアンス Windows システムをバックアップサーバーとして構成する方法について説明します。  
  
  
## <a name="Basics"></a>Backup server の基礎  
バックアップサーバー:  
  
-   は、独自の IT チームによって提供および管理されます。  
  
-   PDW 固有のソフトウェアやツールは必要ありません。 PDW では、バックアップサーバーにソフトウェアはインストールされません。  
  
-   はアプライアンス以外のラックに設置されており、APS アプライアンス内に配置することはできません。  
  
-   アプライアンス InfiniBand ネットワークに接続できます。 バックアップは、InfiniBand またはイーサネット経由で実行できます。パフォーマンス上の理由から、InfiniBand をお勧めします。  
  
-   は、アプライアンスドメインではなく、独自の顧客ドメインにあります。 お客様のドメインとアプライアンスドメインとの間に信頼関係はありません。  
  
-   は、サーバーメッセージブロック (SMB) アプリケーションレベルのネットワークプロトコルを使用する Windows ファイル共有であるバックアップファイル共有をホストします。 バックアップファイル共有のアクセス許可は、Windows ドメインユーザー (通常は専用のバックアップユーザー) に対して、共有に対するバックアップ操作と復元操作を実行する機能を提供します。 Windows ドメインユーザーのユーザー名とパスワードの資格情報は PDW に格納されるので、PDW でバックアップファイル共有に対するバックアップおよび復元操作を実行できます。  
  
## <a name="Step1"></a>手順 1: 容量の要件を決定する  
バックアップサーバーのシステム要件は、実際のワークロードにほぼ完全に依存します。 バックアップサーバーを購入またはプロビジョニングする前に、容量の要件を把握しておく必要があります。 バックアップサーバーは、ワークロードのパフォーマンスとストレージの要件を処理できる限り、バックアップ専用である必要はありません。 また、複数のバックアップサーバーを使用して、各データベースを複数のサーバーのいずれかにバックアップおよび復元することもできます。  
  
容量の要件を決定するには、[バックアップサーバーの容量計画ワークシート](backup-capacity-planning-worksheet.md)を使用します。  
  
## <a name="Step2"></a>手順 2: バックアップサーバーを取得する  
容量の要件を十分に理解できるようになったので、購入またはプロビジョニングする必要があるサーバーとネットワークコンポーネントを計画することができます。 次の要件の一覧を購入計画に組み込み、サーバーを購入するか、既存のサーバーをプロビジョニングします。  
  
### <a name="software-requirements"></a>ソフトウェア要件  
Windows ファイル共有 (SMB) プロトコルを使用する任意のファイルサーバー。  
  
次の場合は、Windows Server 2012 以降をお勧めします。  
  
-   SMB 経由でのファイルの事前割り当てのパフォーマンス上の利点を得ます。  
  
-   バックアップ操作には、ファイルの瞬時初期化 (IFI) を使用します。 IT チームは、この設定をバックアップサーバーで管理します。 PDW Configuration Manager (dwconfig .exe) では、バックアップサーバーでの IFI の設定または制御は行われません。 以前のバージョンの Windows には IFI はありませんが、バックアップサーバーとして使用することはできます。  
  
### <a name="networking-requirements"></a>ネットワーク要件  
必須ではありませんが、InfiniBand は、バックアップサーバーに推奨される接続の種類です。 ロードサーバーをアプライアンス InfiniBand ネットワークに接続する準備をするには、次のようにします。  
  
1.  アプライアンスの InfiniBand スイッチに接続できるように、サーバーをアプライアンスに近づけてください。 InfiniBand に関する Mellanox テクノロジの詳細については、ホワイトペーパー「 [InfiniBand の概要](https://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf)」を参照してください。  
  
2.  Mellanox FDR InfiniBand のシングルまたはデュアルポートネットワークアダプターを購入します。 データ転送中は、フォールトトレランスのために2つのポートを備えたネットワークアダプターを購入することをお勧めします。 高可用性を実現するには、2つのポートネットワークアダプターが必要です。  
  
3.  2つのポートカード用の FDR InfiniBand ケーブルを購入するか、単一のポートカードに対して 1 FDR InfiniBand ケーブルを購入します。 FDR InfiniBand ケーブルは、ロードサーバーをアプライアンス InfiniBand ネットワークに接続します。 ケーブルの長さは、使用している環境に応じて、読み込みサーバーとアプライアンス InfiniBand スイッチの距離によって異なります。  
  
## <a name="Step3"></a>手順 3: サーバーを InfiniBand ネットワークに接続する  
ロードサーバーを InfiniBand ネットワークに接続するには、次の手順に従います。 サーバーが InfiniBand ネットワークを使用していない場合は、この手順をスキップします。  
  
1.  アプライアンス InfiniBand ネットワークに接続できるように、サーバーをアプライアンスに近づけます。  
  
2.  InfiniBand Mellanox の FDR InfiniBand ネットワークアダプターを読み込み中のサーバーにインストールします。  
  
3.  FDR ケーブルを使用して、InfiniBand ネットワークアダプターを、1番目のアプライアンスラックの2つの InfiniBand スイッチのいずれかに接続します。  
  
4.  InfiniBand ネットワークアダプター用の適切な Windows ドライバーをインストールして構成します。  
  
    -   InfiniBand drivers for Windows は、InfiniBand ベンダーの業界コンソーシアムである OpenFabrics アライアンスによって開発されています。  正しいドライバーが、InfiniBand ネットワークアダプターと共に配布されている可能性があります。 それ以外の場合は、www.openfabrics.org からドライバーをダウンロードできます。  
  
5.  ネットワークアダプターの InfiniBand と DNS の設定を構成します。 構成の手順については、「 [Configure InfiniBand Network Adapters](configure-infiniband-network-adapters.md)」を参照してください。  
  
## <a name="Step4"></a>手順 4: バックアップファイル共有を構成する  
PDW は UNC ファイル共有を使用してバックアップサーバーにアクセスします。 ファイル共有を設定するには:  
  
1.  バックアップを格納するためのフォルダーをバックアップサーバーに作成します。  
  
2.  バックアップフォルダーに対して、バックアップ共有と呼ばれるファイル共有を作成します。  
  
3.  バックアップと復元を実行する目的で使用する Windows ドメインアカウントを顧客ドメインに指定または作成します。 セキュリティ上の理由から、バックアップユーザーとして専用アカウントを使用することをお勧めします。  
  
4.  信頼されたアカウントとドメインのバックアップアカウントのみが共有の場所にアクセスし、読み取り、書き込みを行えるように、バックアップ共有にアクセス許可を追加します。  
  
5.  バックアップドメインアカウントの資格情報を PDW に追加します。  
  
    例:  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    詳細については、次のストアドプロシージャを参照してください。  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>手順 5: データのバックアップを開始する  
これで、バックアップサーバーへのデータのバックアップを開始する準備ができました。  
  
データをバックアップするには、クエリクライアントを使用して SQL Server PDW に接続し、データベースのバックアップまたはデータベースの復元コマンドを実行します。 DISK = 句を使用して、バックアップサーバーとバックアップの場所を指定します。  
  
> [!IMPORTANT]  
> 必ず、バックアップサーバーの InfiniBand IP アドレスを使用してください。 それ以外の場合、データは InfiniBand ではなくイーサネット経由でコピーされます。  
  
例:  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
詳細については、次のドキュメントを参照してください。 
  
-   [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [データベースの復元](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="Security"></a>セキュリティに関する通知  
バックアップサーバーがアプライアンスのプライベートドメインに参加していません。 独自のネットワーク内にあり、独自のドメインとプライベートのアプライアンスドメインとの間に信頼関係がありません。  
  
PDW のバックアップはアプライアンスに格納されていないため、IT チームはバックアップセキュリティのすべての側面を管理する責任があります。 たとえば、バックアップデータのセキュリティ、バックアップの保存に使用するサーバーのセキュリティ、およびバックアップサーバーを APS アプライアンスに接続するネットワークインフラストラクチャのセキュリティを管理することができます。  
  
### <a name="manage-network-credentials"></a>ネットワーク資格情報の管理  
  
バックアップ ディレクトリへのネットワーク アクセスは、標準 Windows ファイル共有セキュリティに基づきます。 バックアップを実行する前に、PDW をバックアップディレクトリに認証するために使用する Windows アカウントを作成または指定する必要があります。 この Windows アカウントには、バックアップ ディレクトリにアクセスし、作成や書き込みを行うための許可を与える必要があります。  
  
> [!IMPORTANT]  
> データのセキュリティ リスクを緩和するために、バックアップ操作と復元操作を実行する目的のためだけに Windows アカウントを 1 つ用意することをお勧めします。 そのアカウントのアクセス許可をバックアップの場所に限定します。  
  
PDW にユーザー名とパスワードを格納するには、 [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)ストアドプロシージャを使用します。 PDW は、Windows 資格情報マネージャーを使用して、コントロールノードとコンピューティングノードにユーザー名とパスワードを格納および暗号化します。 資格情報は BACKUP DATABASE コマンドでバックアップされません。  
  
PDW からネットワーク資格情報を削除するには、 [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)ストアドプロシージャを使用します。  
  
SQL Server PDW に格納されているすべてのネットワーク資格情報を一覧表示するには、 [dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md)動的管理ビューを使用します。  
  
### <a name="secure-communications"></a>セキュリティで保護された通信  
  
読み込み側サーバーでの操作では、UNC パスを使用して、信頼された内部ネットワークの外部からデータをプルできます。 ネットワーク上の攻撃者または名前解決に影響を与える機能によって、PDW に送信されるデータを傍受または変更することができます。 これにより、改ざんと情報漏えいのリスクが生じます。 改ざんのリスクを軽減するために、次のようにします。

- 接続の署名が必要です。 
- 読み込み側のサーバーで、Security] 権利セキュリティ Options の [Microsoft ネットワーククライアント: デジタル署名通信 (always): 有効] を選択して、次のグループポリシーオプションを設定します。  
  
## <a name="see-also"></a>参照  
[バックアップと復元](backup-and-restore-overview.md)  
  
