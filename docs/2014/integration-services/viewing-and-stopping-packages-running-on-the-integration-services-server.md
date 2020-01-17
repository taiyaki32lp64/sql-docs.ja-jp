---
title: サービス サーバーの表示と、統合で実行中のパッケージの停止 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], managing
- managing running packages [Integration Services]
- packages [Integration Services], running
- running package [Integration Services], managing
ms.assetid: 11bf44e6-f6b0-475f-b816-40e914dbac80
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9a53cf3dbd11c87177c725cf246fb4b1016d87ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054596"
---
# <a name="viewing-and-stopping-packages-running-on-the-integration-services-server"></a>Integration Services サーバーで実行中のパッケージの表示と停止
  `SSISDB` データベースでは、ユーザーに表示されない内部テーブルに実行履歴を格納します。 ただし、必要な情報は、パブリック ビューに対してクエリを実行することで公開されます。 また、パッケージに関連した一般的なタスクを実行するために呼び出すことができるストアド プロシージャも用意されています。  
  
 通常、サーバー上の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] オブジェクトは [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]で管理します。 また、データベース ビューに対してクエリを実行し、ストアド プロシージャを直接呼び出すことや、マネージド API を呼び出すカスタム コードを記述することもできます。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] およびマネージド API では、ビューに対してクエリを実行し、多くのタスクを実行するストアド プロシージャを呼び出します。 たとえば、サーバーで現在実行中の [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージの一覧を表示し、必要に応じてパッケージの停止を要求できます。  
  
## <a name="viewing-the-list-of-running-packages"></a>実行中のパッケージの一覧の表示  
 **[アクティブな操作]** ダイアログ ボックスでは、サーバーで現在実行中のパッケージの一覧を表示できます。 詳しくは、「 [Active Operations Dialog Box](../../2014/integration-services/active-operations-dialog-box.md)」をご覧ください。  
  
 実行中のパッケージの一覧を表示するその他の方法については、次のトピックをご覧ください。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] アクセス  
 サーバーで実行中のパッケージの一覧を表示するには、ステータスが 2 のパッケージに対してビュー [catalog.executions (SSISDB データベース)](/sql/integration-services/system-views/catalog-executions-ssisdb-database) をクエリします。  
  
 マネージド API を使用したプログラムによるアクセス  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 名前空間とそのクラスのトピックをご覧ください。  
  
## <a name="stopping-a-running-package"></a>実行中のパッケージの停止  
 **[アクティブな操作]** ダイアログ ボックスでは、実行中のパッケージを停止するよう要求できます。 詳しくは、「 [Active Operations Dialog Box](../../2014/integration-services/active-operations-dialog-box.md)」をご覧ください。  
  
 実行中のパッケージを停止するその他の方法については、次のトピックをご覧ください。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] アクセス  
 サーバーで実行中のパッケージを停止するには、ストアド プロシージャ [catalog.stop_operation (SSISDB データベース)](/sql/integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database) を呼び出します。  
  
 マネージド API を使用したプログラムによるアクセス  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 名前空間とそのクラスのトピックをご覧ください。  
  
## <a name="viewing-the-history-of-packages-that-have-run"></a>実行したパッケージの履歴の表示  
 実行したパッケージの履歴を [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]で確認するには、 **[すべての実行]** レポートを使用します。 **[すべての実行]** レポートとその他の標準レポートの詳細については、「[Integration Services サーバーのレポート](../../2014/integration-services/reports-for-the-integration-services-server.md)」を参照してください。  
  
 実行中のパッケージの履歴を表示するその他の方法については、次のトピックをご覧ください。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] アクセス  
 実行したパッケージに関する情報を表示するには、ビュー [catalog.executions (SSISDB データベース)](/sql/integration-services/system-views/catalog-executions-ssisdb-database) をクエリします。  
  
 マネージド API を使用したプログラムによるアクセス  
 <xref:Microsoft.SqlServer.Management.IntegrationServices> 名前空間とそのクラスのトピックをご覧ください。  
  
## <a name="see-also"></a>参照  
 [プロジェクトとパッケージの実行](packages/run-integration-services-ssis-packages.md)   
 [パッケージ実行のレポートのトラブルシューティング](troubleshooting/troubleshooting-reports-for-package-execution.md)  
  
  
