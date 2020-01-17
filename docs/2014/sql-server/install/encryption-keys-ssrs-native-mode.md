---
title: 暗号化キー (SSRS ネイティブモード) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.encryptionkeypanel.F1
ms.assetid: cc7e6f84-80e1-4b5e-9409-d0e074edd147
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 540cf25a150349c7b6399975d20d10bc202ed935
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952174"
---
# <a name="encryption-keys-ssrs-native-mode"></a>暗号化キー (SSRS ネイティブ モード)
  [暗号化キー] ページを使用すると、レポート サーバーでデータの暗号化と暗号化解除に使用される対称キーを管理できます。 暗号化キーの管理は、レポート サーバーの構成で重要な位置を占めています。 対称キーはレポート サーバー データベースを作成する際に自動的に作成されて適用されますが、 定期的なメンテナンス操作を実行できるように、対称キーのバックアップ コピーを作成しておく必要があります。 次に示すメンテナンス タスクを実行するには、対称キーの有効なコピーが必要です。  
  
-   レポート サーバー サービスのサービス アカウントを変更する。  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インストールを別のコンピューターに移行する。  
  
-   既存のレポート サーバー データベースを共有または使用するように、新しいレポート サーバー インスタンスを構成する。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード。  
  
> [!IMPORTANT]  
>  セキュリティを高めるために、Reporting Services の暗号化キーは定期的に変更することをお勧めします。 キーを変更する推奨されるタイミングは、Reporting Services のメジャー バージョンのアップグレードの直後です。 アップグレード後であれば、アップグレード サイクル以外での Reporting Services の暗号化キーの変更に伴う他のサービスの中断を最小限に抑えることができます。  
  
 レポート サーバー サービスのユーザー アカウントを更新し、アカウントの変更に [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャー以外のツールを使用した場合、またはインストールしたレポート サーバーを新しいサーバーに移行しようとしている場合は、対称キーの復元が必要です。  
  
 不正なアクセスを防ぐために、対称キーはレポート サーバー サービスの秘密キーを使用して暗号化されており、 レポート サーバー サービスのみが、機密データをレポート サーバー データベースに格納する目的で、対称キーをロック解除して使用できます。 レポート サーバー サービスの ID を変更した場合や、レポート サーバーを新しいコンピューターに移行した場合は、レポート サーバー サービスの秘密キーで対称キーをロック解除できなくなります。 対称キーへのアクセスを復元するには、新しいレポート サーバー サービス ID の秘密キーを使用して対称キーを再暗号化します。 対称キーの復元処理によって、再暗号化が行われます。  
  
 対称キーを復元するのは、レポート サーバー データベース内のデータの暗号化と暗号解除に現在使用されているキーと同じキーである場合だけです。 不適切な対称キーを復元すると、機密データにアクセスできなくなります。 そのような場合は、対称キーを削除して再作成します。  
  
> [!IMPORTANT]  
>  対称キーの削除と再作成の操作は、取り消したり元に戻したりすることはできません。 キーを削除または再作成すると、現在のインストールに重大な影響を及ぼす可能性があります。 対称キーを削除すると、その対称キーを使用して暗号化されている既存のデータも削除されます。 たとえば、外部のレポート データ ソースへの接続文字列、保存されている接続文字列、サブスクリプション情報の一部が削除されることがあります。  
  
 このページを開くには、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを起動して、ナビゲーション ウィンドウでリンクを選択します。 詳細については、「 [Reporting Services 構成マネージャー &#40;ネイティブ モード&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)」を参照してください。  
  
## <a name="options"></a>および  
 **Backup**  
 指定したファイルに対称キーをコピーします。 対称キーはプレーン テキストのまま保存しないでください。 パスワードを入力してファイルを保護する必要があります。  
  
 **[復元]**  
 以前に保存された対称キーのコピーを、レポート サーバー データベースに適用します。 ファイルのロックを解除するパスワードを入力する必要があります。  
  
 現在接続しているレポート サーバー インスタンスの以前の対称キーは、復元された対称キーによって上書きされます。 対称キーを復元した後、そのレポート サーバー データベースを利用するレポート サーバーをすべて初期化する必要があります。 レポートサーバーの初期化の詳細については、「[レポート&#40;サーバーの&#41;SSRS Configuration Manager の初期化](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)」を参照してください。  
  
 **変更**  
 対称キーを再作成し、レポート サーバー データベース内の暗号化された値を再暗号化します。 対称キーを再作成する前に、レポート サーバー サービスを必ず停止してください。  
  
 スケールアウト配置では、すべての対称キーが新しいバージョンに置き換えられます。 対称キーを変更する前に、スケールアウト配置に含まれているサーバーの一覧を確認して、有効なレポート サーバー インスタンスにのみ、新しいキーへのアクセスが許可されていることを確認してください。 スケールアウト配置に含まれるサーバーは、 **[スケールアウト配置]** ページに一覧表示されます。 キーを再作成する前に、配置に含まれる各レポート サーバーのサービスを停止してください。  
  
 データ ソースとサブスクリプションが多数存在する場合、対称キーの再作成に長い時間がかかることがあります。  
  
 **[削除]**  
 接続文字列や保存されている資格情報を含むすべての暗号化コンテンツと、対称キーを削除します。 対称キーは、復元できない場合にのみ削除してください。  
  
 対称キーを削除すると、レポートおよび共有データ ソース内に接続文字列や保存されている資格情報が存在しなくなるため、その値を再入力する必要があります。 さらに、暗号化データを保存する配信拡張機能が使用されるサブスクリプションをすべて更新する必要があります。 これには、ファイル共有配信拡張機能や、暗号化された値を使用するサード パーティの拡張機能が含まれます。  
  
 この情報を自動的に更新する方法はありません。 保存されている資格情報や接続文字列を使用する各レポート、サブスクリプション、共有データ ソースを、一度に 1 つずつ更新する必要があります。  
  
## <a name="see-also"></a>参照  
 [Reporting Services Configuration Manager の F1 ヘルプ&#40;トピック SSRS ネイティブ&#41;モード](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Reporting Services の暗号化キーのバックアップと復元](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [暗号化キーの削除と再作成 &#40;SSRS構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [レポート サーバーの初期化 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [暗号化されたレポート サーバー データの格納 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
