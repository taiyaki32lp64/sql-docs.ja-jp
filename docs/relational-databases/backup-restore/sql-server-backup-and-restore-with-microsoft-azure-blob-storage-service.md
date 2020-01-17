---
title: Azure BLOB ストレージを使用したバックアップと復元
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ba2574b4468742414d60c1f4e7db4a93380fba0e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75251135"
---
# <a name="sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service"></a>Windows Azure BLOB ストレージ サービスを使用した SQL Server のバックアップと復元
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  ![Azure BLOB へのバックアップのグラフィック](../../relational-databases/backup-restore/media/backup-to-azure-blob-graphic.png "Azre BLOB へのバックアップのグラフィック")  
  
 このトピックでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft Azure Blob ストレージ サービス [への](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)のバックアップと Microsoft Azure Blob ストレージ サービスからの復元について説明します。 また、Microsoft Azure BLOB Service を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップを格納する利点の概要についても説明します。  
  
 SQL Server では、次の方法で Microsoft Azure Blob ストレージ サービスにバックアップを格納できます。  
  
-   **Microsoft Azure へのバックアップを管理する方法:** ディスクまたはテープにバックアップする場合と同じ方法を使用して、バックアップ先として URL を指定することにより、Microsoft Azure ストレージにバックアップできます。 この機能を使用すると、手動でバックアップすることも、ローカル ストレージまたはその他のオフサイト オプションの場合と同じように独自のバックアップ方法を構成することもできます。 この機能は、 **SQL Server Backup to URL**とも呼ばれます。 詳細については、「 [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)」を参照してください。 この機能は、SQL Server 2012 SP1 CU2 以降で使用できます。 この機能は [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] で強化され、ブロック BLOB、Shared Access Signature、ストライピングを使用してパフォーマンスと機能が向上しました。  
  
    > [!NOTE]  
    >  SQL Server 2012 SP1 CU2 より前の SQL Server バージョンでは、Microsoft Azure への SQL Server バックアップ ツール アドインを使用して、Microsoft Azure Storage へのバックアップをすばやく簡単に作成できます。 詳細については、 [ダウンロード センター](https://go.microsoft.com/fwlink/?LinkID=324399)を参照してください。  
  
-   **Azure BLOB Storage 内のデータベース ファイルのファイル スナップショット バックアップ** : [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ファイル スナップショット バックアップでは、Azure のスナップショットを利用することで、Azure BLOB Storage サービスで格納されているデータベース ファイルのバックアップと復元をほぼ即時に実行できます。 この機能を利用すると、バックアップと復元のポリシーを簡素化し、ポイントインタイム リストアをサポートできます。 詳細については、「 [Azure でのデータベース ファイルのファイル スナップショット バックアップ](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)」を参照してください。 この機能は、SQL Server 2016 以降で使用できます。  
  
-   **SQL Server で Microsoft Azure へのバックアップを管理する方法:** SQL Server を構成することにより、単一データベースまたは複数データベースのバックアップ方法やスケジュールを管理することも、インスタンス レベルでの既定値を設定することもできます。 この機能は、 **[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]** と呼ばれるものです。 詳細については、「[Microsoft Azure への SQL Server マネージド バックアップ](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)」を参照してください。 この機能は、SQL Server 2014 以降で使用できます。  
  
## <a name="benefits-of-using-the-microsoft-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップに Microsoft Azure BLOB Service を使用する利点  
  
-   柔軟で信頼性が高く、制限のないオフサイト ストレージ:Microsoft Azure Blob service へのバックアップの保存は、アクセスしやすく便利で柔軟なオフサイトのオプションです。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップ用にオフサイト ストレージを作成するのは、既存のスクリプトやジョブを変更するのと同様に簡単です。 オフサイト ストレージは、通常、災害発生時にオフサイトと運用データベース両方の場所に影響しないように、運用データベースの場所から十分に離れた場所に設置する必要があります。 BLOB ストレージを地理的に離れた場所にレプリケートすることによって、地域全体に影響する可能性がある災害が発生した場合の保護レベルが強化されます。 また、バックアップは場所や時間を問わず使用でき、復元のために簡単にアクセスできます。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]でブロック BLOB を使用すると、バックアップ セットをストライプし、最大 12.8 TB のバックアップ ファイル サイズに対応できます。  
  
-   バックアップ アーカイブ:Microsoft Azure Blob Storage サービスは、バックアップのアーカイブ手段として、よく使用されるテープ オプションより優れています。 テープ ストレージでは、オフサイトの施設への物理的な輸送手段とメディアを保護する手段が必要になります。 Microsoft Azure BLOB ストレージへのバックアップの格納は、すぐに使用でき、可用性が高く、持続性を備えたアーカイブ オプションです。  
  
-   ハードウェア管理のオーバーヘッドなし: Microsoft Azure サービスを使用したハードウェア管理にはオーバーヘッドが生じません。 Microsoft Azure サービスでは、ハードウェアが管理され、ハードウェア障害に対する冗長性と保護を目的として地理的に離れた場所へのレプリケーションが提供されます。  
  
-   現在、Microsoft Azure 仮想マシンで実行されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスでは、アタッチされたディスクを作成することで、BLOB Azure BLOB ストレージ サービスへのバックアップを実行できます。 ただし、Microsoft Azure 仮想マシンにアタッチできるディスク数には制限があります。 ディスク数の上限は、XL インスタンスでは 16 台、サイズの小さいインスタンスではこれより少なくなります。 Microsoft Azure BLOB ストレージに直接バックアップできるようにすることで、16 台のディスク制限がなくなります。  
  
     また、Microsoft Azure BLOB ストレージ サービスに格納されているバックアップ ファイルは、オンプレミスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、または Microsoft Azure 仮想マシンで実行している別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で直接使用できます。その際、データベースのアタッチ/デタッチや、VHD のダウンロードとアタッチは必要ありません。  
  
-   コスト面での利点:使用するサービスにのみ料金がかかります。 オフサイトのバックアップ アーカイブ オプションとして、優れたコスト効果を得ることができます。 詳細とリンクについては、「 [Microsoft Azure の課金に関する注意点](#Billing) 」を参照してください。  
  
##  <a name="Billing"></a> Microsoft Azure の課金に関する注意点:  
 Microsoft Azure ストレージのコストを把握しておくと、Microsoft Azure でバックアップを作成および格納するコストを予測できます。  
  
 [Microsoft Azure 料金計算ツール](https://go.microsoft.com/fwlink/?LinkId=277060) を使用すると、コストを見積もることができます。  
  
 **ストレージ:** 料金は使用領域に基づいており、段階的に、また、冗長性のレベルに応じて計算されます。 詳細と最新情報については、「 **料金の詳細** 」の「 [データ管理](https://go.microsoft.com/fwlink/?LinkId=277059) 」を参照してください。  
  
 **データ転送:** Microsoft Azure への受信データ転送は無料です。 送信転送は、帯域幅の使用量に対して課金され、段階的な地域固有の区分に基づいて計算されます。 詳細については、「 [料金の詳細](https://go.microsoft.com/fwlink/?LinkId=277061) 」の「データ転送」を参照してください。  
  
## <a name="see-also"></a>参照  

[SQL Server Backup to URL に関するベスト プラクティスとトラブルシューティング](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)   

[システム データベースのバックアップと復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)   

[チュートリアル:Azure Blob Storage サービスと SQL Server 2016 データベースの使用](../tutorial-use-azure-blob-storage-service-with-sql-server-2016.md)

[SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)  
  
  
