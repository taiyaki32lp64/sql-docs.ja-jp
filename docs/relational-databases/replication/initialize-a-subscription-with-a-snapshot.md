---
title: スナップショットを使用したサブスクリプションの初期化 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 68be2c5a44777bb62a594cf2ab612e46a078d0eb
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68767854"
---
# <a name="initialize-a-subscription-with-a-snapshot"></a>スナップショットを使用したサブスクリプションの初期化
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  パブリケーションを作成すると、通常は初期スナップショットが作成され、スナップショット フォルダーにコピーされます (この動作は、パブリケーションの新規作成ウィザードを使用して作成されたマージ パブリケーションに対して既定で実行されます)。 その後スナップショットは、サブスクリプションの最初の同期時に、ディストリビューション エージェント (トランザクション パブリケーションおよびスナップショット パブリケーションの場合) またはマージ エージェント (マージ パブリケーションの場合) によってサブスクライバーに適用されます。 スナップショット処理は、パブリケーションの種類によって変わります。  
  
-   パラメーター化されたフィルターを使用しないスナップショット パブリケーション、トランザクション パブリケーション、またはマージ パブリケーションに対するスナップショットの場合、スナップショットにはスキーマとデータが含まれ、一括コピー プログラム (bcp) ファイルとして作成されます。また、レプリケーションで必要な制約、拡張プロパティ、インデックス、トリガー、およびシステム テーブルも含まれます。 スナップショットの作成と適用の詳細については、「[Create and Apply the Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」(スナップショットの作成と適用) を参照してください。  
  
-   パラメーター化されたフィルターを使用するマージ パブリケーションに対するスナップショットの場合は、2 段階の処理でスナップショットが作成されます。 まず、パブリッシュされたオブジェクトのレプリケーション スクリプトとスキーマが含まれるスキーマ スナップショットが作成されます。ただしデータは含まれません。 次に、スキーマ スナップショットからコピーしたスクリプトとスキーマが含まれるスナップショットと、サブスクリプションのパーティションに属するデータを使用して、各サブスクリプションが初期化されます。 詳細については、「 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」を参照してください。  
  
 スナップショットは、レプリケーションの種類やパブリケーションのアーティクルに応じて異なるファイルで構成されます。 これらのファイルは、ディストリビューターの構成時に指定した既定のスナップショット フォルダーか、パブリケーションを作成する際に指定した代替スナップショット フォルダーにコピーされます。  
  
|レプリケーションの種類|通常のスナップショット ファイル|  
|-------------------------|---------------------------|  
|スナップショット レプリケーションまたはトランザクション レプリケーション|スキーマ (.sch)、データ (.bcp)、制約とインデックス (.dri)、制約 (.idx)、トリガー (.trg) (サブスクライバーの更新専用)、圧縮スナップショットファイル (.cab)|  
|マージ レプリケーション|スキーマ (.sch)、データ (.bcp)、制約とインデックス (.dri)、トリガー (.trg)、システム テーブル データ (.sys)、競合テーブル (.cft)、圧縮スナップショットファイル (.cab)|  
  
 ある時点でスナップショットの転送が中断された場合、転送は自動的に再開され、既に転送が完了したファイルは再送されません。 スナップショット エージェントの配信単位は、各パブリケーション アーティクルに対する bcp ファイルであるため、部分的に配信されたファイルは再度全体を配信する必要があります。 しかし、スナップショットの再開機能を使うことで、転送されるデータ量が大幅に削減され、接続が不安定な場合でもタイムリーにスナップショットを配信できます。  
  
## <a name="snapshot-options"></a>スナップショット オプション  
 スナップショットを使用してサブスクリプションを初期化する際には、いくつかのオプションがあります。 可能な代替手段としては以下の方法があります。  
  
-   既定のスナップショット フォルダーを代替または追加する場所として、代替スナップショット フォルダーの場所を指定できます。 詳細については、[スナップショット オプションの変更](../../relational-databases/replication/snapshot-options.md)に関する記事を参照してください。  
  
-   リムーバブル メディア上に格納するためや低速なネットワーク上で転送するための圧縮スナップショットを使用できます。 詳細については、「 [Compressed Snapshots](../../relational-databases/replication/snapshot-options.md#compressed-snapshots)」を参照してください。 

-   スナップショットを適用する前または後に Transact-SQL スクリプトを実行できます。 詳細については、「[スナップショットが適用される前および後のスクリプトの実行](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)」を参照してください。  
  
-   ファイル転送プロトコル (FTP) を使用してスナップショット ファイルを転送できます。 詳細については、「[FTP によるスナップショットの転送](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [サブスクリプションの初期化](../../relational-databases/replication/initialize-a-subscription.md)   
 [スナップショット フォルダーのセキュリティ保護](../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
