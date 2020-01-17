---
title: パッケージで使用されるファイルへのアクセス |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- packages [Integration Services], security
- configuration files [Integration Services]
- checkpoint files
- Integration Services packages, security
- logs [Integration Services], security
- files [Integration Services], security
- SQL Server Integration Services packages, security
ms.assetid: 2e3ddea9-5289-4289-a70e-11c018f34977
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c0dbc5c5c72b6c69a6d2d390ac6c2c8920a19332
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66062188"
---
# <a name="access-to-files-used-by-packages"></a>パッケージで使用されるファイルへのアクセス
  パッケージに格納されないファイルは、パッケージ保護レベルでは保護されません。 このようなファイルには、次のファイルが含まれます。  
  
-   [構成ファイル]  
  
-   チェックポイント ファイル  
  
-   ログ ファイル  
  
 特に機密情報が含まれている場合、これらのファイルは個別に保護する必要があります。  
  
## <a name="configuration-files"></a>[構成ファイル]  
 ログイン情報やパスワード情報などの機密情報が構成に含まれている場合は、その構成を [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に保存することを検討するか、アクセス制御リスト (ACL) を使用して、ファイルを保存する場所またはフォルダーへのアクセスを制限し、特定のアカウントにのみアクセスを許可する必要があります。 通常は、パッケージの実行を許可するアカウント、およびパッケージの管理とトラブルシューティング (構成の内容、チェックポイント、およびログ ファイルの確認) を行うアカウントにアクセス権を許可します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、サーバー レベルおよびデータベース レベルでの保護により、さらに堅牢なセキュリティが提供されます。 構成を [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に保存するには、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成の種類を使用します。 ファイル システムに保存するには、XML 構成の種類を使用します。  
  
 詳細については、「 [パッケージ構成](../../2014/integration-services/package-configurations.md)」、「 [パッケージ構成を作成する](../../2014/integration-services/create-package-configurations.md)」、および「 [SQL Server インストールにおけるセキュリティの考慮事項](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)」を参照してください。  
  
## <a name="checkpoint-files"></a>チェックポイント ファイル  
 同様に、パッケージで使用するチェックポイント ファイルに機密情報が含まれている場合も、アクセス制御リスト (ACL) を使用して、ファイルが格納されている場所またはフォルダーを保護する必要があります。 チェックポイント ファイルは、パッケージの進行状況に関する現在の状態情報と変数の現在の値を格納します。 たとえば、電話番号を格納するカスタム変数がパッケージに含まれることがあります。 詳細については、「 [チェックポイントを使用してパッケージを再開する](packages/restart-packages-by-using-checkpoints.md)」を参照してください。  
  
## <a name="log-files"></a>ログ ファイル  
 ファイル システムに書き込まれるログ エントリも、アクセス制御リスト (ACL) を使用して保護する必要があります。 ログ エントリは、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] テーブルに保存して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] セキュリティで保護することもできます。 ログ エントリには機密情報が含まれることがあります。たとえば、パッケージに含まれる SQL 実行タスクによって、電話番号を参照する SQL ステートメントが構築される場合、SQL ステートメントのログ エントリにも電話番号が含まれています。 また、SQL ステートメントにより、データベース内のテーブル名や列名に関するプライベートな情報が明らかにされる場合もあります。 詳細については、「[Integration Services (SSIS) のログ記録](performance/integration-services-ssis-logging.md)」をご覧ください。  
  
  
