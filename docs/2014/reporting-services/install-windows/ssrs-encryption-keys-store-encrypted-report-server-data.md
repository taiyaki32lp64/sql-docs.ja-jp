---
title: 暗号化されたレポート サーバー データの格納 (SSRS 構成マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], encryption
- credentials [Reporting Services]
- cryptography [Reporting Services]
- confidential reports [Reporting Services]
- encryption [Reporting Services]
- databases [Reporting Services], encryption
ms.assetid: ac0f4d4d-fc4b-4c62-a693-b86e712e75f2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8156e3d62e8aac027499ad1e267e1f6e14f5ef9a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108689"
---
# <a name="store-encrypted-report-server-data-ssrs-configuration-manager"></a>暗号化されたレポート サーバー データの格納 (SSRS 構成マネージャー)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、暗号化された値がレポート サーバー データベースおよび構成ファイルに保存されます。 暗号化された値の大部分は資格情報です。これらの資格情報は、レポートにデータを提供する外部データ ソースへのアクセスに使用されます。 このトピックでは、暗号化される値、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]で使用される暗号化機能、および理解が必要な他の種類の保存された機密データについて説明します。  
  
## <a name="encrypted-values"></a>暗号化された値  
 次の一覧に、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 環境に格納される値を示します。  
  
-   内部サーバー データを格納するレポート サーバー データベースに接続するために、レポート サーバーで使用される接続情報および資格情報。  
  
     これらの値は、セットアップ中またはレポート サーバー構成中に指定および暗号化されます。 Reporting Services 構成ツールまたは **rsconfig** ユーティリティを使用すると、いつでも接続情報を更新できます。 構成設定の暗号化には、ローカル コンピューターのマシン レベル キーが使用されます。このキーは、すべてのユーザーが使用できます。 暗号化されたレポート サーバーの接続情報は rsreportserver.config ファイルに保存されます (他の構成ファイルには、暗号化された設定が保存されません)。 詳細については、「 [レポート サーバー データベース接続の構成 &#40;SSRS構成マネージャー&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)」で確認します。  
  
-   レポートにデータを提供する外部データ ソースに接続するためにレポート サーバーで使用される保存された資格情報。  
  
     これらの値は、レポートのデータ ソース情報を構成する際に定義され、暗号化された値としてレポート サーバー データベースに保存されます。 レポート サーバーは対称キーを使用して、このデータの暗号化および暗号化解除を行います。 保存された資格情報の詳細については、 [オンライン ブックの「](../../integration-services/connection-manager/data-sources.md) レポート データ ソースに関する資格情報と接続情報を指定する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
-   レポートで使用される外部画像ファイルまたは外部データを取得するために、レポート サーバーが他のコンピューターに接続するときに使用する自動実行用ユーザー アカウント。  
  
     このアカウントは、リモート コンピューターへの接続が必要で、接続には他の資格情報が利用できない場合に使用されます。 このアカウントは、主にデータ ソースへのアクセスに資格情報を使用しないレポートの自動実行をサポートするために使用されます。 データのアクセスに資格情報を必要としない、または使用しないデータ ソースを基にしたレポートを作成する場合、このアカウントを構成してレポート サーバーで使用する必要があります。  
  
     このアカウントは特定の状況で必要であり、Reporting Services 構成ツールまたは **rsconfig**でのみ作成できます。 この値も rsreportserver.config ファイルに保存されます。 このアカウントは手動で作成する必要があります。 このアカウントとその使用方法の詳細については、「[自動実行アカウントの構成 &#40;SSRS 構成マネージャー&#41;](configure-the-unattended-execution-account-ssrs-configuration-manager.md)」を参照してください。  
  
-   暗号化に使用する対称キー。  
  
     この値はセットアップ中またはサーバー構成中に作成され、暗号化された値としてレポート サーバー データベースに保存されます。 レポート サーバーの Windows サービスはこのキーを使用して、レポート サーバー データベースに保存されているデータの暗号化および暗号化解除を行います。  
  
## <a name="encryption-functionality-in-reporting-services"></a>Reporting Services での暗号化機能  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、Windows オペレーティング システムの一部になっている暗号化関数を使用します。 対称暗号化と非対称暗号化の両方が使用されます。  
  
 レポート サーバー データベース内のデータは、対称キーを使用して暗号化されます。 レポート サーバー データベースごとに 1 つの対称キーがあります。 この対称キー自体が、Windows によって生成される非対称キー ペアの公開キーを使用して暗号化されています。 秘密キーはレポート サーバー Windows サービス アカウントが持っています。  
  
 レポート サーバーのスケールアウト配置では、複数のレポート サーバー インスタンスが同じレポート サーバー データベースを共有しています。この配置では、1 つの対称キーをすべてのレポート サーバー ノードが使用します。 各ノードは共有する対称キーのコピーを持つ必要があります。 対称キーのコピーは、スケールアウト配置が構成されると自動的にノードごとに作成されます。 各ノードは、Windows サービス アカウント固有のキー ペアの公開キーを使用して、対称キーのコピーを暗号化します。 単一インスタンスおよびスケールアウト配置用に作成される対称キーの詳細については、「[レポート サーバーの初期化 &#40;SSRS 構成マネージャー&#41;](ssrs-encryption-keys-initialize-a-report-server.md)」を参照してください。  
  
> [!NOTE]  
>  レポート サーバー Windows サービス アカウントを変更した場合、非対称キーは無効になり、サーバーの操作が中断される可能性があります。 この問題を回避するには、常に Reporting Services 構成ツールを使用して、サービス アカウントの設定を変更してください。 構成ツールを使用する場合、キーは自動的に更新されます。 詳細については、 [レポート サーバー サービス アカウントの構成 &#40;SSRS 構成マネージャー&#41;](configure-the-report-server-service-account-ssrs-configuration-manager.md)」を参照してください。  
  
## <a name="other-sources-of-confidential-data"></a>機密データの各種のソース  
 レポート サーバーには暗号化されていない各種のデータが保存されますが、その中には保護が必要な重要な情報が含まれていることがあります。 特に、レポート履歴スナップショットおよびレポート実行スナップショットには、クエリ結果が含まれています。このクエリ結果には、権限を持つユーザー向けのデータが含まれることがあります。 機密データを含むレポートのスナップショット機能を使用している場合、レポート サーバー データベースでテーブルを開くことができるユーザーは、テーブルの内容を調べることで、保存されたレポートの一部を参照できる可能性があるという点に注意してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、ユーザーのセキュリティ ID に基づくパラメーターを使用するレポートのキャッシュおよびレポート履歴がサポートされません。  
  
## <a name="see-also"></a>参照  
 [暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
