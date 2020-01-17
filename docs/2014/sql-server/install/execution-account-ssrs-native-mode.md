---
title: 実行アカウント (SSRS ネイティブモード) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.executionaccount.F1
ms.assetid: 440b5a09-5fd4-4c3a-b510-f3c33cbf1c82
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 0eff6dca788744b93d2d6d4a0a7175764e263f71
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952543"
---
# <a name="execution-account-ssrs-native-mode"></a>実行アカウント (SSRS ネイティブ モード)
  このページを使用すると、自動処理に使用するアカウントを構成できます。 このアカウントは、他に使用できる資格情報のソースがないという特殊な状況で使用されます。  
  
-   資格情報を必要としないデータ ソースにレポート サーバーが接続する場合。 資格情報を必要としないデータ ソースの例には、XML ドキュメントや一部のクライアント側データベース アプリケーションがあります。  
  
-   外部画像ファイルなど、レポートで参照されるリソースを、レポート サーバーが他のサーバーに接続して取得する場合。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード。  
  
 このアカウントの設定は省略可能ですが、設定しないと、外部画像の使用や一部のデータ ソースへの接続が制限されます。 外部画像ファイルを取得するとき、レポート サーバーでは匿名接続を確立できるかどうかを確認します。 接続がパスワード保護されている場合、レポート サーバーでは自動レポート処理アカウントを使用してリモート サーバーに接続します。 レポート サーバーでレポート用のデータを取得する際には、現在のユーザーの資格情報を借用するか、ユーザーに資格情報を入力するように要求するか、保存されている資格情報を使用するか、またはデータ ソース接続で資格情報の種類として **[なし]** が指定されている場合は自動処理アカウントを使用します。 他のコンピューターに接続する際、レポート サーバーではそのサービス アカウントの資格情報の委任や借用を許可しないので、他の資格情報を使用できない場合は自動処理アカウントを使用する必要があります。  
  
 サービス アカウントの実行に使用するものとは別のアカウントを指定してください。 指定したアカウントを構成すると、値は暗号化されて RSReportServer.config ファイルに保存されます。 スケールアウト配置でレポート サーバーを実行している場合は、各レポート サーバーでこのアカウントを同じように構成する必要があります。  
  
 任意の Windows ユーザー アカウントを使用できます。 最適な結果を得るには、読み取り権限とネットワーク ログオン権限のあるアカウントを選択し、他のコンピューターへの接続がサポートされるようにします。 アカウントには、レポートで使用する外部画像またはデータ ファイルに対する読み取り権限が必要です。 すべてのレポート データ ソースと外部画像がレポート サーバー コンピューターに格納されていない場合は、ローカル アカウントを指定しないでください。 アカウントは自動レポート処理専用に使用してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)] を使用しているときは、レポートで外部画像を参照していて、その画像ファイルにアクセスする権限が必要な場合のみ、このアカウントを構成する必要があります。 SQL Server Express は、リモート サーバーへのデータ ソース接続をサポートしていません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各エディションでサポートされる機能の一覧については、「[SQL Server 2012 の各エディションがサポートする機能](https://go.microsoft.com/fwlink/?linkid=232473)」を参照してください。  
  
 このページを開くには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを起動して、ナビゲーション ウィンドウで **[実行アカウント]** を選択します。 詳細については、「 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)」を参照してください。  
  
## <a name="options"></a>および  
 **[実行アカウントの指定]**  
 アカウントを指定します。  
  
 **アカウント**  
 Windows のドメイン ユーザー アカウントを入力します。 *\<ドメイン>\\<ユーザー アカウント\>* の形式を使用します。  
  
 **パスワード**  
 パスワードを入力します。  
  
 **[パスワードの確認入力]**  
 再度、パスワードを入力します。  
  
## <a name="see-also"></a>参照  
 [Reporting Services Configuration Manager の F1 ヘルプ&#40;トピック SSRS ネイティブ&#41;モード](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [暗号化されたレポート サーバー データの格納 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [自動実行アカウントの構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)  
  
  
