---
title: Azure Blob Storage サービスを使用したバックアップと復元の SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 6a0c9b6a-cf71-4311-82f2-12c445f63935
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 38c92e397c971f6e9976bb857c63410fa60b7e85
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75232430"
---
# <a name="sql-server-backup-and-restore-with-azure-blob-storage-service"></a>Azure Blob Storage サービスを使った SQL Server のバックアップと復元
  このトピックで[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は、 [Azure Blob ストレージサービス](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/)に対するバックアップと復元について説明します。 また、Azure Blob service を使用してバックアップを格納[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]する利点の概要についても説明します。  
  
 SQL Server は、次の方法で Azure Blob ストレージサービスへのバックアップの格納をサポートしています。  
  
-   **Azure へのバックアップを管理します。** ディスクとテープへのバックアップに使用したのと同じ方法を使用して、バックアップ先として URL を指定することで、Azure storage にバックアップできるようになりました。  この機能を使用すると、手動でバックアップすることも、ローカル ストレージまたはその他のオフサイト オプションの場合と同じように独自のバックアップ方法を構成することもできます。 この機能は、 **SQL Server Backup to URL**とも呼ばれます。 詳細については、「 [SQL Server Backup to URL](sql-server-backup-to-url.md)」をご覧ください。 この機能は、SQL Server 2012 SP1 CU2 以降で使用できます。  
  
    > [!NOTE]  
    >  SQL Server 2014 より前の SQL Server バージョンでは、Azure ツールへのバックアップ SQL Server を使用して、Azure storage へのバックアップをすばやく簡単に作成できます。 詳細については、 [ダウンロード センター](https://go.microsoft.com/fwlink/?LinkID=324399)を参照してください。  
  
-   **Azure へのバックアップを SQL Server 管理するには、次のようにします。** 1つのデータベースまたは複数のデータベースのバックアップ方法とスケジュールバックアップを管理し、インスタンスレベルで既定値を設定するように SQL Server を構成します。 この機能はと**[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]** 呼ばれます。 詳細については[、「Azure へのマネージバックアップの SQL Server](sql-server-managed-backup-to-microsoft-azure.md)」を参照してください。 この機能は、SQL Server 2014 以降で使用できます。  
  
## <a name="benefits-of-using-the-azure-blob-service-for-includessnoversionincludesssnoversion-mdmd-backups"></a>バックアップに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Azure Blob サービスを使用する利点  
  
-   柔軟で信頼性が高く、無制限のオフサイトストレージ: Azure Blob service へのバックアップの格納は、便利で柔軟性が高く、簡単にアクセスできるオフサイトのオプションです。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バックアップ用にオフサイト ストレージを作成するのは、既存のスクリプトやジョブを変更するのと同様に簡単です。 社外ストレージは通常、運用データベースから十分に離れた場所に設置して、一度の災害によって社外ストレージと運用データベースの両方が影響を受けないようにする必要があります。 BLOB ストレージを地理的に離れた場所にレプリケートすることによって、地域全体に影響する可能性がある災害が発生した場合の保護レベルが強化されます。 また、バックアップは場所や時間を問わず使用でき、復元のために簡単にアクセスできます。  
  
-   バックアップアーカイブ: Azure Blob Storage サービスは、バックアップをアーカイブするために頻繁に使用されるテープオプションに代わる優れた手段を提供します。 テープ ストレージでは、場合によって社外設備への物理的な搬送やメディア保護の対策が必要です。 Azure Blob Storage へのバックアップの保存では、可用性と持続性に優れた高速アーカイブが可能です。  
  
-   ハードウェア管理のオーバーヘッドなし: Azure サービスを使用したハードウェア管理のオーバーヘッドはありません。 Azure サービスのハードウェア管理では、ハードウェア障害に対する冗長性実現と保護のためにgeo レプリケーションが行われます。  
  
-   現在、Azure 仮想[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]マシンで実行されているのインスタンスでは、アタッチされたディスクを作成することによって、azure Blob ストレージサービスへのバックアップを実行できます。 ただし、Azure 仮想マシンに接続できるディスクの数には制限があります。 この制限はインスタンス サイズが XL の場合は 16 ディスクです。インスタンス サイズが小さくなるほど、このディスク数は少なくなります。 Azure Blob Storage に直接バックアップを有効にすることで、16ディスク制限を回避できます。  
  
     さらに、Azure Blob ストレージサービスに格納されているバックアップファイルは、オンプレミス[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または Azure 仮想マシンで実行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]されている別ので直接使用できます。データベースのアタッチ/デタッチや、VHD のダウンロードとアタッチは必要ありません。  
  
-   コスト面での利点: 使用するサービスにのみ料金がかかります。 社外ストレージやバックアップ アーカイブ用にこのサービスを選択することで、高い費用対効果を得られます。 詳細とリンクについては、「 [Azure の課金に関する注意点](#Billing)」を参照してください。  
  
##  <a name="Billing"></a>Azure の課金に関する考慮事項:  
 Azure storage のコストを把握することで、Azure でのバックアップの作成と保存にかかるコストを予測することができます。  
  
 [Azure 料金計算ツール](https://go.microsoft.com/fwlink/?LinkId=277060)を使用すると、コストを見積もることができます。  
  
 **ストレージ:** 料金は、使用された領域に基づいており、段階的なスケールと冗長性のレベルで計算されます。 詳細と最新情報については、「 **料金の詳細** 」の「 [データ管理](https://go.microsoft.com/fwlink/?LinkId=277059) 」を参照してください。  
  
 **データ転送:** Azure への受信データ転送は無料です。 送信転送は、帯域幅の使用量に対して課金され、段階的な地域固有の区分に基づいて計算されます。 詳細については、「 [料金の詳細](https://go.microsoft.com/fwlink/?LinkId=277061) 」の「データ転送」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Backup to URL のベストプラクティスとトラブルシューティング](sql-server-backup-to-url-best-practices-and-troubleshooting.md)   
 [システムデータベースのバックアップと復元 &#40;SQL Server&#41;](back-up-and-restore-of-system-databases-sql-server.md)   
 [チュートリアル: SQL Server Azure Blob Storage サービスへのバックアップと復元](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)   
 [SQL Server Backup to URL](sql-server-backup-to-url.md)  
  
