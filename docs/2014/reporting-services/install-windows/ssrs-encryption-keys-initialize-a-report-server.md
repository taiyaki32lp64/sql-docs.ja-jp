---
title: レポート サーバーの初期化 (SSRS 構成マネージャー) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], initializing
- initialization process [Reporting Services]
- checking report server initializations
- scale-out deployments [Reporting Services]
- initializing report servers [Reporting Services]
- verifying report server initializations
ms.assetid: 861d4ec4-1085-412c-9a82-68869a77bd55
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f9bcb5e7818c4125b81d715d7e74f120a07449d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108736"
---
# <a name="initialize-a-report-server-ssrs-configuration-manager"></a>レポート サーバーの初期化 (SSRS 構成マネージャー)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] では、初期化されたサーバーとは、レポート サーバー データベース内のデータの暗号化および暗号化解除を実行できるサーバーのことです。 レポート サーバーを操作するには、初期化が必要です。 初期化は、レポート サーバー サービスを最初に開始するときに行われます。 また、既存の配置にレポート サーバーを追加するときや、復旧処理の一環としてキーを手動で再作成するときにも、初期化が行われます。 暗号化キーを使用する方法と理由の詳細については、「[暗号化キーの構成と管理 (構成マネージャー)](ssrs-encryption-keys-manage-encryption-keys.md)」および「[暗号化されたレポート サーバー データの格納 (SSRS 構成マネージャー)](ssrs-encryption-keys-store-encrypted-report-server-data.md)」を参照してください。  
  
 暗号化キーは、レポート サーバー サービスのプロファイル情報に一部基づいています。 レポート サーバー サービスの実行に使用されるユーザー ID を変更する場合は、それに応じてキーを更新する必要があります。 Reporting Services 構成ツールを使用して ID を変更すると、この手順が自動的に実行されます。  
  
 何らかの理由で初期化が失敗すると、ユーザーおよびサービスからの要求に応じて、レポート サーバーから `RSReportServerNotActivated` エラーが返されます。 この場合、システムまたはサーバーの構成のトラブルシューティングが必要になります。 詳細については、次を参照してください[SSRS:。Reporting Services での問題とエラーのトラブルシューティング](https://social.technet.microsoft.com/wiki/contents/articles/1633.aspx)(https://social.technet.microsoft.com/wiki/contents/articles/1633.aspx) Technet Wiki にします。  
  
## <a name="overview-of-the-initialization-process"></a>初期化処理の概要  
 初期化処理では、暗号化に使用する対称キーが作成され、格納されます。 対称キーは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Cryptographic Services で作成された後、レポート サーバー サービスで暗号化と暗号化解除に使用されます。 対称キー自体も、非対称キーを使って暗号化されます。  
  
 次に、初期化処理の手順を説明します。  
  
1.  初回起動時に、レポート サーバー サービスが RSReportServer.config ファイルを読み取り、インストール識別子とデータベース接続情報を取得します。  
  
2.  レポート サーバー サービスが暗号化サービスに公開キーを要求します。 Windows は秘密キーと公開キーを作成し、レポート サーバー サービスに公開キーを送信します。  
  
3.  レポート サーバー サービスがレポート サーバー データベースに接続し、インストール識別子と公開キーの値を格納します。  
  
4.  レポート サーバー サービスが暗号化サービスを再度呼び出し、今回は対称キーを要求します。 Windows が対称キーを作成します。  
  
5.  レポート サーバー サービスがレポート サーバー データベースに再接続し、手順 3 で格納された公開キーとインストール識別子の値に対称キーを追加します。 対称キーを格納する前に、レポート サーバー サービスはその公開キーを使用して対称キーを暗号化します。 対称キーが格納されると、レポート サーバーは初期化されたと見なされて、使用可能になります。  
  
## <a name="initializing-a-report-server-for-scale-out-deployment"></a>スケールアウト配置用のレポート サーバーの初期化  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 1 つのレポート サーバー データベースを複数のレポート サーバー インスタンスで共有するスケールアウト配置モデルがサポートされています。 スケールアウト配置に参加するには、レポート サーバーは、対称キーのコピーを作成して共有データベースに格納する必要があります。 そのデータベースを使用する複数のサーバーで使用される対称キーは 1 つですが、各レポート サーバーはその対称キーのコピーを持っています。 各コピーは、その所有者の公開キーを使用して一意に暗号化されるため、それぞれ異なります。  
  
 スケールアウト配置のためにレポート サーバーを初期化する際の最初の数手順は、1 つのサーバーと 1 つのデータベースの初期化で行う最初の 3 つの手順と同じです。  
  
 スケールアウト配置用の初期化で異なる点は、レポート サーバーが対称キーを取得する方法です。 最初のサーバーが初期化されるときに、そのサーバーが Windows から対称キーを取得します。 スケールアウト配置の構成時に 2 番目のサーバーが初期化される際、このサーバーは既に初期化されているレポート サーバー サービスから対称キーを取得します。 最初のレポート サーバー インスタンスは、2 番目のインスタンスの公開キーを使用して、2 番目のレポート サーバー インスタンス用に対称キーの暗号化されたコピーを作成します。 この処理では、対称キーはプレーンテキストとして公開されることはありません。  
  
## <a name="how-to-initialize-a-report-server"></a>レポート サーバーを初期化する方法  
  
-   レポート サーバーを初期化するには、Reporting Services 構成ツールを使用します。 初期化は、レポート サーバー データベースを作成および構成するときに自動的に行われます。 詳細については、「 [レポート サーバー データベース接続の構成 &#40;SSRS構成マネージャー&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)」で確認します。  
  
-   レポート サーバーをスケールアウト配置用に初期化するには、Reporting Services 構成ツールの [初期化] ページまたは **RSKeymgmt** ユーティリティを使用します。 実行手順については、「[ネイティブ モード レポート サーバーのスケールアウト配置の構成 (SSRS 構成マネージャー)](configure-a-native-mode-report-server-scale-out-deployment.md)」を参照してください。  
  
> [!NOTE]  
>  **RSKeymgmt** は、既にスケールアウト配置に含まれているレポート サーバー インスタンスをホストするコンピューター上のコマンド ラインから実行するコンソール アプリケーションです。 ユーティリティを実行するとき、初期化するリモートのレポート サーバー インスタンスを選択するための引数を指定します。  
  
 レポート サーバーは、インストール識別子と公開キーが一致する場合のみ初期化されます。 正しく一致すると、暗号化の解除を許可する対称キーが作成されます。 一致しないと、レポート サーバーが無効になります。このとき、バックアップ キーの適用、またはバックアップ キーが利用できない場合や有効でない場合に暗号化データの削除が必要になることがあります。 レポート サーバーによる暗号化キーの使用の詳細については、「[暗号化キーの構成と管理 (SSRS 構成マネージャー)](ssrs-encryption-keys-manage-encryption-keys.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の Windows Management Instrumentation (WMI) プロバイダーを使用して、レポート サーバーをプログラムで初期化することもできます。 詳細については、 [オンライン ブックの「](../tools/access-the-reporting-services-wmi-provider.md) Reporting Service WMI プロバイダーへのアクセス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
## <a name="how-to-confirm-a-report-server-initialization"></a>レポート サーバーの初期化の確認方法  
 レポート サーバーの初期化を確認するには、コマンド ウィンドウで「**http://\<サーバー名>/reportserver**」と入力し、レポート サーバー Web サービスに対して ping を実行します。 `RSReportServerNotActivated` エラーが発生した場合は、初期化が失敗しています。  
  
## <a name="see-also"></a>関連項目  
 [暗号化されたレポート サーバー データの格納 &#40;SSRS 構成マネージャー&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
