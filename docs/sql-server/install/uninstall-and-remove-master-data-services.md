---
title: マスター データ サービスのアンインストールと削除 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: efc2431c-588b-42e7-b23b-c875145a33f6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a0ed3134e26bc2ed0f581a722de50526a49fb9e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126037"
---
# <a name="uninstall-and-remove-master-data-services"></a>マスター データ サービスのアンインストールと削除
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスから [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] 機能をアンインストールするには、「[SQL Server の既存のインスタンスのアンインストール &#40;セットアップ&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)」の手順に従って [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] を **[機能の選択]** ページで削除する機能として指定します。 アンインストール プロセスによって [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] のフォルダーおよびファイルが削除され、ローカル コンピューターから [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]がアンインストールされます。  
  
 データの損失またはシステム内の他のコンピューターへの影響を回避するために、削除されない項目、またはアンインストール プロセスによって変更される項目もあります。 次の表を参考にして、項目を残すか削除するかを決定します。  
  
|アイテム|[説明]|  
|----------|-----------------|  
|フォルダーとファイル|アンインストール プロセスによって、ほとんどのフォルダーとファイルがインストール パスから削除されます。<br /><br /> アンインストール プロセスでは、Master Data Services フォルダーおよび MDSTempDir フォルダーはインストール場所から削除されません。 これらのフォルダーのファイル システムからの削除は、アンインストール プロセスの完了後に手動で実行できます。 詳細については、「[フォルダーとファイルの権限 &#40;マスター データ サービス&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md)」を参照してください。|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] アセンブリ|アンインストール プロセスによって、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] アセンブリがグローバル アセンブリ キャッシュ (GAC) から削除されます。|  
|データベース|アンインストール プロセスは、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベースには影響を及ぼしません。 データベースは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンス内にそのまま残ります。つまり、マスター データ、モデル オブジェクト、ユーザーおよびグループの権限、ビジネス ルールなどを含めて、データは損失しません。<br /><br /> データベースを必要とせず、別の [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] Web サイトまたはアプリケーションに将来接続する予定がない場合、データベースをホストする [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスからデータベースを削除することもできます。 詳細については、「 [データベースの削除](../../relational-databases/databases/delete-a-database.md)」を参照してください。|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] と Web.config|WebApplication フォルダーは、アンインストール プロセスによってファイル システムから削除されます。 WebApplication フォルダーには、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]の Web アプリケーション ファイルと Web.config ファイルがあります。<br /><br /> **\*\* 重要 \*\*** アンインストールを実行する前に、ファイル内に保存されているカスタム設定やその他の情報を維持するために Web.config ファイルを別の場所にコピーする必要がある場合があります。 アンインストール プロセスが完了すると、Web.config ファイルは回復できません。|  
|インターネット インフォメーション サービス (IIS) の項目|アンインストール プロセスは、ローカル コンピューター上の IIS にあるアプリケーション プール、Web サイト、Web アプリケーションには影響を及ぼしません。 アンインストール プロセスによって、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]の WebApplication フォルダーと Web.config ファイルが削除されるため、これらのファイルを使用する [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションでは、コンテンツが表示されなくなります。 ユーザーが Web アプリにアクセスしようとすると、HTTP エラー 500.19-内部サーバーエラーが発生します:"ページに関連する構成データが無効であるため、要求されたページにアクセスできません。"<br /><br /> Web サイトまたはアプリケーション、および Web サイトまたはアプリケーションで使用されているアプリケーション プールを今後必要としない場合は、IIS ツールを使用してそれらを削除できます。 詳細については、 [TechNet の『](https://go.microsoft.com/fwlink/?LinkId=184885) IIS 7 Operations Guide [!INCLUDE[msCoName](../../includes/msconame-md.md)] 』を参照してください。|  
|**MDS_ServiceAccounts** グループ|アンインストール プロセスが完了しても、 **MDS_ServiceAccounts** Windows グループおよびそのグループに追加されたサービス アカウントはそのまま残ります。 グループおよびアカウントを今後必要としない場合、削除できます。|  
|レジストリ|アンインストール プロセスによって、すべての [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] レジストリ キーが Windows レジストリから削除されます。|  
  
## <a name="see-also"></a>参照  
 [マスター データ サービスのインストール](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
