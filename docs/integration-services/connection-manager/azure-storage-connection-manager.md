---
title: Azure Storage 接続マネージャー | Microsoft Docs
description: Azure Storage 接続マネージャーにより、SSIS パッケージは Azure ストレージ アカウントに接続できます。
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6d3912e2b5cbf8051348191cf3efb6ed2d20d551
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2019
ms.locfileid: "74687191"
---
# <a name="azure-storage-connection-manager"></a>Azure Storage 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Azure Storage 接続マネージャーにより、SQL Server Integration Services (SSIS) パッケージは Azure ストレージ アカウントに接続できます。 接続マネージャーは、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。 
  
**[SSIS 接続マネージャーの追加]** ダイアログ ボックスで、 **[AzureStorage]**  >  **[追加]** を選択します。  
  
使用できるプロパティは次のとおりです。

- **サービス:** 接続先のストレージ サービスを指定します。
- **アカウント名:** ストレージ アカウント名を指定します。
- **認証:** 使用する認証方法を指定します。 AccessKey と ServicePrincipal の認証がサポートされています。
    - **AccessKey:** この認証方法には、**アカウント キー**を指定します。
    - **ServicePrincipal:** この認証方法には、サービス プリンシパルの**アプリケーション ID**、**アプリケーション キー**、**テナント ID** を指定します。
      **テスト接続**が機能するためには、サービス プリンシパルには少なくともストレージ アカウントに対する**ストレージ BLOB データ閲覧者**の役割を割り当てる必要があります。
      詳細については、「[Azure portal で RBAC を使用して Azure BLOB とキューのデータへのアクセスを付与する](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal)」を参照してください。
- **環境:** ストレージ アカウントをホストするクラウド環境を指定します。

## <a name="managed-identities-for-azure-resources-authentication"></a>Azure リソース認証用のマネージド ID
[Azure Data Factory 内の Azure-SSIS 統合ランタイム](https://docs.microsoft.com/azure/data-factory/concepts-integration-runtime#azure-ssis-integration-runtime)上で SSIS パッケージを実行しているときは、お使いのデータ ファクトリに関連付けられている[マネージド ID](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#managed-identity) を Azure Storage 認証に使用できます。 この ID を使用して指定したファクトリからストレージ アカウントにアクセスし、ストレージ アカウントとの間でデータをコピーできます。

一般的な Azure Storage 認証については、[Azure Active Directory を使用した Azure Storage へのアクセスの認証](https://docs.microsoft.com/azure/storage/common/storage-auth-aad)に関する記事をご覧ください。 Azure Storage にマネージド ID 認証を使用するには:

1. [Azure portal でデータ ファクトリのマネージド ID を確認します](https://docs.microsoft.com/azure/data-factory/data-factory-service-identity)。 お使いのデータ ファクトリの **[プロパティ]** に移動します。 (**マネージド ID オブジェクト ID** ではなく) **マネージド ID アプリケーション ID** をコピーします。

1. ストレージ アカウント内でマネージド ID に適切なアクセス許可を付与します。 ロールの詳細については、[RBAC を使用した Azure Storage データへのアクセス権の管理](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal)に関する記事をご覧ください。

    - **ソースとして**、アクセス制御 (IAM) で、少なくとも**ストレージ BLOB データ閲覧者**の役割を付与します。
    - **宛先として**、アクセス制御 (IAM) で、少なくとも**ストレージ BLOB データ共同作成者**の役割を付与します。

次に、Azure Storage 接続マネージャーに対するマネージド ID 認証を構成します。 これを行うには次のオプションがあります。

- **設計時に構成します。** SSIS デザイナーで、Azure Storage 接続マネージャーをダブルクリックして **Azure Storage 接続マネージャー エディター**を開きます。 **[Use managed identity to authenticate on Azure]\(マネージド ID を使用して Azure 上で認証する\)** をオンにします。
    > [!NOTE]
    >  現在、SSIS パッケージを SSIS デザイナーまたは [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server で実行しているときは、このオプションが有効になりません (マネージド ID 認証が機能しないことを示します)。
    
- **実行時に構成します。** パッケージを [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/integration-services/ssis-quickstart-run-ssms) または [Azure Data Factory の SSIS パッケージの実行アクティビティ](https://docs.microsoft.com/azure/data-factory/how-to-invoke-ssis-package-ssis-activity)で実行するときは、Azure Storage 接続マネージャーを探します。 そのプロパティ `ConnectUsingManagedIdentity` を `True` に更新します。
    > [!NOTE]
    >  Azure-SSIS 統合ランタイムでは、ストレージ操作にマネージド ID 認証を使用すると、Azure Storage 接続マネージャーで事前構成済みの他のすべての認証方法 (アクセス キー、サービス プリンシパルなど) はオーバーライドされます。

> [!NOTE]
>  既存のパッケージでマネージド ID 認証を構成するための推奨される方法は、[最新の SSIS デザイナー](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)を使用して SSIS プロジェクトを少なくとも 1 回リビルドすることです。 SSIS プロジェクトのすべての Azure Storage 接続マネージャーに新しい接続マネージャー プロパティ `ConnectUsingManagedIdentity` が自動的に追加されるように、SSIS プロジェクトを Azure-SSIS 統合ランタイムに再配置します。 または、実行時にプロパティ パス **\Package.Connections[<接続マネージャーの名前>].Properties[ConnectUsingManagedIdentity]** を指定して、プロパティのオーバーライドを直接使用します。

## <a name="secure-network-traffic-to-your-storage-account"></a>ストレージ アカウントへのネットワークトラフィックをセキュリティで保護する
Azure Data Factory は、Azure Storage にとって[信頼できる Microsoft サービス](https://docs.microsoft.com/azure/storage/common/storage-network-security#trusted-microsoft-services)になりました。 マネージド ID の認証を使用すると、[選択したネットワークへのアクセスを制限](https://docs.microsoft.com/azure/storage/common/storage-network-security#change-the-default-network-access-rule)することで、ストレージ アカウントをセキュリティで保護することができます。その上、データ ファクトリでご利用のストレージ アカウントに引き続きアクセスすることができます。 手順については、「[例外の管理](https://docs.microsoft.com/azure/storage/common/storage-network-security#managing-exceptions)」を参照してください。

## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; の接続](../../integration-services/connection-manager/integration-services-ssis-connections.md)
