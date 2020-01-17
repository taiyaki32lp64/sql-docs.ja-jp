---
title: ディストリビューションの構成 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- remote Distributors [SQL Server replication]
- transactional replication, configuring distribution
- distribution databases [SQL Server replication], sizing
- Distributors [SQL Server replication], configuring
- distribution databases [SQL Server replication], about distribution databases
- distribution databases [SQL Server replication]
- merge replication [SQL Server replication], configuring distribution
ms.assetid: 94d52169-384e-4885-84eb-2304e967d9f7
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 36e89b7092ea497f3ad2ca0267e7f5dab99056e7
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768673"
---
# <a name="configure-distribution"></a>ディストリビューションの構成
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  ディストリビューターは、ディストリビューション データベースを含むサーバーです。ディストリビューション データベースには、すべての種類のレプリケーションのメタデータと履歴データ、およびトランザクション レプリケーションに対するトランザクションが格納されます。 レプリケーションを設定するには、ディストリビューターを構成する必要があります。 パブリッシャーはそれぞれ 1 つのディストリビューター インスタンスにしか割り当てることができませんが、複数のパブリッシャーで 1 つのディストリビューターを共有できます。 サーバーがディストリビューターとして指定されると、次のようなリソースが新たに消費されることになります。  
  
-   パブリケーションのスナップショット ファイルをディストリビューターに格納する場合 (通常の場合) は、そのためのディスク領域  
  
-   ディストリビューション データベースを格納するためのディスク領域  
  
-   ディストリビューター上で実行されるプッシュ サブスクリプションのために、レプリケーション エージェントによって使用されるプロセッサ時間  
  
 ディストリビューターとして指定するサーバーには、サーバー上でさまざまな機能を果たしながら、レプリケーションの処理を実行できるだけの十分なディスク容量とプロセッサ パワーが必要です。 ディストリビューターを構成するには、以下の設定を行います。  
  
-   ディストリビューターを使用するすべてのパブリッシャーに対して既定で使用されるスナップショット フォルダー。 フォルダーが既に共有されていること、および適切な権限が設定されていることを確認します。 詳細については、「[Secure the Snapshot Folder](../../relational-databases/replication/security/secure-the-snapshot-folder.md)」(スナップショット フォルダーのセキュリティ保護) をご覧ください。  
  
-   ディストリビューション データベースの名前とファイルの場所。 ディストリビューション データベースの名前は、作成後には変更できません。 データベースで別の名前を使用するには、ディストリビューションを無効にして再構成する必要があります。  
  
-   ディストリビューターの使用を許可するパブリッシャー。 ディストリビューターが実行されているインスタンス以外のパブリッシャーを指定する場合は、パブリッシャーがリモート ディストリビューターに接続するためのパスワードも指定する必要があります。  
  
 トランザクション レプリケーションでは、ディストリビューションの構成後に以下の作業を行うことをお勧めします。  
  
-   ディストリビューション データベースのサイズを適切に設定する。 システムの典型的な負荷でレプリケーションをテストし、コマンドを格納するために必要な領域を決定します。 データベースが頻繁に自動拡張しなくてもコマンドを格納できるだけの大きさを備えていることを確認します。 データベースのサイズの変更に関する詳細については、「[ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)」を参照してください。  
  
-   ディストリビューション データベースで " **sync with backup** " オプションを設定する。 詳細については、「[スナップショット レプリケーションおよびトランザクション レプリケーションのバックアップと復元の方式](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)」と「[トランザクション レプリケーションの連携バックアップの有効化 &#40;レプリケーション Transact-SQL プログラミング&#41;](../../relational-databases/replication/administration/enable-coordinated-backups-for-transactional-replication.md)」をご覧ください。  
  
## <a name="local-and-remote-distributors"></a>ローカル ディストリビューターとリモート ディストリビューター  
 既定では、ディストリビューターはパブリッシャーと同じサーバー (ローカル ディストリビューター) になりますが、別のサーバー (リモート ディストリビューター) にすることもできます。 一般に、リモート ディストリビューターは次のような場合に使用されます。  
  
-   処理を別のコンピューターにオフロードする場合 (たとえばパブリッシャーが OLTP サーバーである場合など、パブリッシャーに対するレプリケーションの影響を最小限に抑えたい場合)  
  
-   複数のパブリッシャーを集中管理する単一のディストリビューターを構成する場合  
  
 リモート ディストリビューターは、マージ レプリケーションよりトランザクション レプリケーションでよく使用されます。これには、次の 2 つの理由があります。  
  
-   トランザクション レプリケーションでは、レプリケートされたすべてのトランザクションの書き込みと読み取りがディストリビューション データベースに対して行われるため、ディストリビューターが果たす役割が大きくなります。  
  
-   マージ レプリケーション トポロジでは通常、プル サブスクリプションが使用されるため、ディストリビューターですべてのエージェントが実行されるのではなく、各サブスクライバーでエージェントが実行されます。 詳細については、「[パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)」をご覧ください。 マージ レプリケーションでは、ほとんどの場合、ローカル ディストリビューターを使用します。  
  
 パブリッシングおよびディストリビューションを構成するには、「 [Configure Publishing and Distribution](../../relational-databases/replication/configure-publishing-and-distribution.md)」を参照してください。  
  
 パブリッシャーとディストリビューターのプロパティを変更するには、「 [View and Modify Distributor and Publisher Properties](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [ディストリビューターのセキュリティ保護](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  
