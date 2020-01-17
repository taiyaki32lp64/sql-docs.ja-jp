---
title: 追加およびスケール アウト配置 (SSRS 構成マネージャー) の暗号化キーの削除 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- encryption keys [Reporting Services]
- deleting encryption keys
- removing encryption keys
- adding encryption keys
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 2da86fb3-4b4d-407f-9825-74dcc42486f5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b935a74dba93596e734537f62f2ccafd192f3523
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108922"
---
# <a name="add-and-remove-encryption-keys-for-scale-out-deployment-ssrs-configuration-manager"></a>スケールアウト配置に関する暗号化キーの追加と削除 (SSRS 構成マネージャー)
  1 つのレポート サーバー データベースを複数のレポート サーバーで共有するように構成すると、[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をスケールアウト配置モデルで実行できます。 スケールアウト配置でのメンバーシップは、レポート サーバーがレポート サーバー データベースに暗号化キーを格納するかどうかに基づいています。 特定のレポート サーバー インスタンスの暗号化キーを追加および削除することで、スケールアウト配置のメンバーシップを制御できます。 配置からノードを削除する場合は、それらを任意の順序で削除できます。 配置にノードを追加する場合は、既に配置の一部になっているレポート サーバーのすべての新しいインスタンスを結合する必要があります。  
  
## <a name="using-the-reporting-services-configuration-tool-to-configure-scale-out-deployment"></a>Reporting Services 構成ツールを使用したスケールアウト配置の構成  
 スケールアウト配置を最も簡単に構成するには、Reporting Services 構成ツールを使用します。 詳細情報と手順については、「[ネイティブ モード レポート サーバーのスケールアウト配置の構成 &#40;SSRS 構成マネージャー&#41;](configure-a-native-mode-report-server-scale-out-deployment.md)」を参照してください。  
  
## <a name="using-rskeymgmt-to-configure-scale-out-deployment"></a>rskeymgmt を使用したスケールアウト配置の構成  
 共有レポート サーバー データベースを使用するようにレポート サーバー インスタンスを初期化するには、 **rskeymgmt** ユーティリティを使用します。 レポート サーバーをスケールアウト配置に追加するには、レポート サーバーを初期化する必要があります。 初期化には管理者権限が必要です。 配置に結合するレポート サーバーをホストするリモート コンピューターの管理者資格情報も必要です。  
  
#### <a name="how-to-join-a-report-server-to-a-scale-out-deployment-rskeymgmt"></a>レポート サーバーをスケールアウト配置に結合する方法 (rskeymgmt)  
  
1.  レポート サーバー スケールアウト配置のメンバーであるレポート サーバーをホストするコンピューターで、 **rskeymgmt.exe** をローカルに実行します。  
  
2.  `-j` 引数を使用して、レポート サーバーをレポート サーバー データベースに結合します。 `-m` 引数と `-n` 引数を使用して、配置に追加するリモート レポート サーバー インスタンスを指定します。 `-u` 引数と `-v` 引数を使用して、リモート コンピューター上の管理者アカウントを指定します。 同じコンピューター上の複数のレポート サーバー インスタンスを使用してスケールアウト配置を作成する場合、使用する構文は若干異なります。 使用する必要がある構文の詳細については、「[rskeymgmt ユーティリティ &#40;SSRS&#41;](../tools/rskeymgmt-utility-ssrs.md)」を参照してください。  
  
     次の例は、リモート レポート サーバーをスケールアウト配置に結合する場合に指定する必要がある引数を示しています (リモート コンピューターでの管理者権限がある場合は、資格情報を省略できます)。  
  
    ```  
    rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
    ```  
  
#### <a name="how-to-remove-a-report-server-from-a-scale-out-deployment-rskeymgmt"></a>レポート サーバーをスケールアウト配置から削除する方法 (rskeymgmt)  
  
1.  削除するレポート サーバーの rsreportserver.config ファイルを開き、インストール ID を見つけます。 既定では、このファイルは Program Files\Microsoft SQL Server\MSSQL.*n*\Reporting Services\ReportServer にあります。  
  
     単一のインスタンスをインストールした場合、rsreportserver.config ファイルはコンピューター上に 1 つしかありません。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の複数のインスタンスがインストールされている場合は、Reporting Services 構成ツールの [サーバーの状態] ページを使用し、削除するレポート サーバーのインスタンス識別子 (たとえば、MSSQL.2) を検索します。 レポート サーバー インスタンスのプログラム ファイルを格納するフォルダーの名前は、インスタンス識別子に基づきます (たとえば、Program Files\Microsoft SQL Server\MSSQL.2)。  
  
2.  **rskeymgmt.exe**を実行します。 これは、レポート サーバー スケールアウト配置に含まれているどのレポート サーバーでも実行できます。  
  
3.  `-r` 引数を使用して、スケールアウト配置からレポート サーバー インスタンスを解放します。 指定する必要がある引数の例を次に示します。  
  
    ```  
    rskeymgmt -r <installation ID>  
    ```  
  
 これらの手順によってスケール アウト配置からレポート サーバーが削除されますが、レポート サーバーの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] インスタンスはアンインストールされません。 スケール アウト配置からレポート サーバーを削除した後、サーバー上で [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] が不要になった場合は、そのサーバーから [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をアンインストールできます。 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「[SQL Server の既存のインスタンスのアンインストール &#40;セットアップ&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [暗号化キーの構成と管理 &#40;SSRS 構成マネージャー&#41;](ssrs-encryption-keys-manage-encryption-keys.md)   
 [レポート サーバーの初期化 &#40;SSRS 構成マネージャー&#41;](ssrs-encryption-keys-initialize-a-report-server.md)  
  
  
