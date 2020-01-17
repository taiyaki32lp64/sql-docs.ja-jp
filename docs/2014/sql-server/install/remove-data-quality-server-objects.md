---
title: Data Quality Server オブジェクトの削除 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 1b7c6dbb-b40e-4822-9caa-608e1056af8e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f273823825cf94da6269a58389f04207ad1c2707
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68190667"
---
# <a name="remove-data-quality-server-objects"></a>Data Quality Server オブジェクトの削除
  [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] インスタンスから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアンインストールしても、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を持つ [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] インスタンスを完全に削除しても、DQS データベースを含む一部の [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] オブジェクトは削除されません。 これは、SQL Server セットアップを使用して [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] をアンインストールする場合、DQS データが失われないことを意味します。 このような [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] オブジェクトは、アンインストール プロセスの完了後に手動で削除する必要があります。  
  
> [!NOTE]
>  -   [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]をアンインストールする前に、既存のすべてのナレッジ ベースを .dqsb ファイルにエクスポートしてバックアップするよう検討します。後からそのファイルを使用して、すべてのナレッジ ベースを [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] の新しいインストールにインポートします。 DQS のすべてのナレッジ ベースのエクスポートとインポートを行うには、コマンド プロンプトから適切なコマンド ライン パラメーターを使用して DQSInstaller.exe を実行する必要があります。 詳細については、「 [DQSInstaller.exe を使用した DQS ナレッジ ベースのエクスポートとインポート](../../data-quality-services/install-windows/export-and-import-dqs-knowledge-bases-using-dqsinstaller-exe.md)」を参照してください。  
> -   データベースを保持して後からデータの復元に使用する必要がある場合は、DQS データベースを削除する前にデータベースのバックアップを検討します。 詳細については、「 [DQS データベースの管理](../../../2014/data-quality-services/manage-dqs-databases.md)」を参照してください。  
  
## <a name="uninstall-data-quality-server-from-a-sql-server-instance"></a>SQL Server インスタンスからの Data Quality Server のアンインストール  
 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] インスタンスから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をアンインストールするだけの場合、 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] のアンインストール プロセスの完了後に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの次の [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] オブジェクトを手動で削除する必要があります。  
  
-   DQS_MAIN、DQS_PROJECTS、および DQS_STAGING_DATA データベース。  
  
-   \##MS_dqs_db_owner_login## と ##MS_dqs_service_login## ログイン。  
  
-   master データベースの DQInitDQS_MAIN ストアド プロシージャ。  
  
 SQL Server Management Studio でこれらのオブジェクトを削除するには、オブジェクトを右クリックして、ショートカット メニューの **[削除]** をクリックします。  
  
> [!IMPORTANT]  
>  コマンド プロンプトで [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] コマンド ライン パラメーターを使用して SQL サーバー インスタンスから `-uninstall` をアンインストールするだけで、アンインストール プロセスの一部としてすべての DQS オブジェクトが削除されます。 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)]のアンインストール後に手動でそれらを削除する必要はありません。 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] をコマンド プロンプトからアンインストールするには、コマンド プロンプトで次のコマンドを入力し、Enter キーを押します。   
> `dqsinstaller.exe -uninstall`  
  
## <a name="uninstall-sql-server-instance-containing-data-quality-server"></a>Data Quality Server を含む SQL Server インスタンスのアンインストール  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を含む [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] インスタンスを完全にアンインストールする場合、アンインストール プロセスの完了後に、コンピューターから DQS_MAIN データベース、DQS_PROJECTS データベース、および DQS_STAGING_DATA データベースを手動で削除する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインストールでは、DQS_MAIN、DQS_PROJECTS、および DQS_STAGING_DATA のデータベース ファイルは C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA にあります。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server の既存のインスタンスのアンインストール &#40;セットアップ&#41;](../../../2014/sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)   
 [SQL Server 2014 のアンインストール](uninstall-sql-server.md)  
  
  
