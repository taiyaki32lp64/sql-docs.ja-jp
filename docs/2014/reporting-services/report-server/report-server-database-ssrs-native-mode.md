---
title: レポート サーバー データベース (SSRS ネイティブ モード) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- databases [Reporting Services]
- report servers [Reporting Services], databases
- temporary databases [Reporting Services]
- report server database
- reportservertempdb
- reportserver database
ms.assetid: 0fc5c033-3fe1-4cea-86c7-66ea5e424d65
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 6e0a2d0a723629ae1e9b7e7277ff646c63a86aec
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2019
ms.locfileid: "56043263"
---
# <a name="report-server-database-ssrs-native-mode"></a>レポート サーバー データベース (SSRS ネイティブ モード)
  レポート サーバーは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] を使用してメタデータやオブジェクトの定義を格納するステートレス サーバーです。 ネイティブ モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストールでは、一時データと永続データが 2 つのデータベースに別々に格納されます。 この 2 つのデータベースは同時に作成され、データベース名によってバインドされます。 既定では、データベース名がそれぞれ **reportserver** と **reportservertempdb**になります。  
  
 SharePoint モードの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストールでは、データ警告機能用のデータベースも作成されます。 SharePoint モードの 3 つのデータベースは、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] サービス アプリケーションに関連付けられます。 詳細については、「 [Reporting Services SharePoint サービス アプリケーションの管理](../manage-a-reporting-services-sharepoint-service-application.md)｣を参照してください  
  
 データベースは、ローカルまたはリモートの [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスで実行できます。 十分なシステム リソースがある場合、またはソフトウェア ライセンスを節約したい場合は、ローカル インスタンスを選択します。ただし、データベースをリモート コンピューター上で実行した方がパフォーマンスを向上できます。  
  
 既存のレポート サーバー データベースは、以前のインストールから、または別のレポート サーバー インスタンスを使用した別のインスタンスから、移植または再利用できます。 レポート サーバー データベースのスキーマには、レポート サーバー インスタンスとの互換性が必要です。 データベースが古い形式の場合、現在の形式にアップグレードするように求められます。 新しいバージョンを古いバージョンにダウングレードすることはできません。 新しいレポート サーバー データベースを使用する場合、そのデータベースを以前のバージョンのレポート サーバー インスタンスで使用することはできません。 レポート サーバー データベースを新しい形式にアップグレードする方法の詳細については、「 [レポート サーバー データベースのアップグレード](../install-windows/upgrade-a-report-server-database.md)」を参照してください。  
  
> [!IMPORTANT]  
>  データベースのテーブル構造はサーバー操作用に最適化されているので、変更またはチューニングしないでください。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、リリースごとにテーブル構造を変更することがあります。 ユーザーがデータベースを変更または拡張すると、将来のアップグレードの実行や Service Pack の適用の際に、機能が制限されたり機能を利用できない場合があります。 また、レポート サーバーの処理を損なう変更を行う可能性もあります。 たとえば、ReportServer データベースで READ_COMMITTED_SNAPSHOT をオンにすると、対話的な並べ替え機能が無効になります。  
  
 レポート サーバー データベースへのすべてのアクセスは、レポート サーバー経由で行われる必要があります。 レポート サーバー データベースのコンテンツにアクセスするには、レポート マネージャーや [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]などのレポート サーバー管理ツールを使用するか、または URL アクセス、レポート サーバー Web サービス、Windows Management Instrumentation (WMI) プロバイダーなどの、プログラマティック インターフェイスを使用します。  
  
 レポート サーバー データベースへの接続は、通常、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを使用して定義します。 ただし、既定の構成でインストールする場合は、セットアップ時に定義することもできます。 データベースへのレポート サーバーの接続の詳細については、「[レポート サーバー データベース接続の構成 &#40;SSRS 構成マネージャー&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)」を参照してください。  
  
## <a name="report-server-database"></a>レポート サーバー データベース  
 レポート サーバー データベースは、以下のコンテンツを格納する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースです。  
  
-   レポート サーバーによって管理されるアイテム (../レポートおよびリンク レポート、共有データ ソース、レポート モデル、フォルダー、リソース) およびすべてのプロパティとそれらの項目に関連付けられているセキュリティ設定。  
  
-   サブスクリプションおよびスケジュールの定義  
  
-   レポート スナップショット (クエリ結果も含む) およびレポート履歴  
  
-   システム プロパティおよびシステムレベルのセキュリティ設定  
  
-   レポート実行ログ データ  
  
-   レポート データ ソースに対して使用する対称キー、暗号化された接続情報、および資格情報  
  
 レポート サーバー データベースには、アプリケーションの状態と永続データが格納されるため、このデータベースのバックアップ スケジュールを作成して、データの損失を防ぐ必要があります。 データベースのバックアップ方法に関する推奨事項と説明については、「[別のコンピューターへのレポート サーバー データベースの移動 &#40;SSRS ネイティブ モード&#41;](moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md)」を参照してください。  
  
## <a name="report-server-temporary-database"></a>レポート サーバーの一時データベース  
 各レポート サーバー データベースでは、関連する一時データベースが使用され、セッション データ、実行データ、キャッシュされたレポート、およびレポート サーバーによって生成される作業テーブルが格納されます。 バックグラウンドのサーバー プロセスにより、一時データベースのテーブルから古いアイテムや未使用のアイテムが定期的に削除されます。  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、一時データベースが存在しない場合、一時データベースが再作成されません。また、存在しないテーブルや変更されたテーブルも修復されません。 一時データベースには永続データが格納されませんが、それでもデータベースのコピーをバックアップすることをお勧めします。バックアップを行うことによって、障害復旧時にデータベースを再作成する必要がなくなります。  
  
 一時データベースをバックアップし、続いてデータベースを復元する場合、コンテンツを削除する必要があります。 一般的に、一時データベースのコンテンツは、いつでも安全に削除できます。 ただし、コンテンツを削除した後、レポート サーバー Windows サービスを再起動する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQL Server フェールオーバー クラスターでのレポート サーバー データベースのホスト](../install-windows/host-a-report-server-database-in-a-sql-server-failover-cluster.md)   
 [暗号化されたレポート サーバー データの格納 &#40;SSRS 構成マネージャー&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Reporting Services Report Server](../reporting-services-report-server.md)   
 [レポート サーバー データベースを管理する &#40;SSRS ネイティブ モード&#41;](report-server-database-ssrs-native-mode.md)   
 [レポート サーバー データベースの作成 &#40;SSRS 構成マネージャー&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Reporting Services のバックアップおよび復元操作](../install-windows/backup-and-restore-operations-for-reporting-services.md)  
  
  
