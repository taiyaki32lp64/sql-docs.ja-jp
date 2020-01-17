---
title: Azure HDInsight Create Cluster Task | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpcreatecltask.f1
- sql14.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa9599ae0a4c3a38a409131b3f9f344bd478e15b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294311"
---
# <a name="azure-hdinsight-create-cluster-task"></a>Azure HDInsight Create Cluster Task

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


**Azure HDInsight Create Cluster Task** を使用すると、指定された Azure サブスクリプションとリソース グループの Azure HDInsight クラスターを SSIS パッケージで作成できます。
  
**Azure HDInsight Create Cluster Task** は、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。
  
> [!NOTE]  
> - 新しい HDInsight クラスターの作成には 10 分から 20 分かかる場合があります。  
> - Azure HDInsight クラスターの作成と実行には、料金がかかります。 詳細については、「[HDInsight の価格](https://azure.microsoft.com/pricing/details/hdinsight/)」を参照してください。  
  
**Azure HDInsight Create Cluster Task**を追加するには、SSIS デザイナーにドラッグ アンド ドロップし、ダブルクリックまたは右クリックして、 **[編集]** をクリックします。すると、次の **[Azure HDInsight Create Cluster Task エディター]** ダイアログ ボックスが表示されます。  
  
次の表で、このダイアログ ボックスの各フィールドについて説明します。  
  
|||  
|-|-|  
|**フィールド**|**[説明]**|  
|AzureResourceManagerConnection|既存の Azure Resource Manager 接続マネージャーを選択するか、HDInsight クラスターを作成するために使用する新しいものを作成します。|  
|AzureStorageConnection|既存の Azure ストレージ接続マネージャーを選ぶか、HDInsight クラスターに関連付けられている Azure ストレージ アカウントを参照する新しい接続マネージャーを作成します。|
|SubscriptionId|HDInsight クラスターが作成されるサブスクリプションの ID を指定します。|
|ResourceGroup|HDInsight クラスターが作成される Azure リソース グループを指定します。|
|Location|HDInsight クラスターの場所を指定します。 クラスターは、指定された Azure ストレージ アカウントと同じ場所に作成する必要があります。|  
|ClusterName|作成する HDInsight クラスターの名前を指定します。|  
|ClusterSize|クラスターに作成するノードの数を指定します。|  
|BlobContainer|HDInsight クラスターに関連付けられる既定のストレージ コンテナーの名前を指定します。|  
|UserName|HDInsight クラスターに接続するために使用するユーザー名を指定します。|  
|Password|HDInsight クラスターに接続するために使用するパスワードを指定します。|
|SshUserName|SSH を使用して HDInsight クラスターをリモートでアクセスするために使用するユーザー名を指定します。|
|SshPassword|SSH を使用して HDInsight クラスターをリモートでアクセスするために使用するパスワードを指定します。|
|FailIfExists|クラスターが既に存在する場合に、タスクがエラーになるかどうかを指定します。|  
  
> [!NOTE]  
> HDInsight クラスターと Azure ストレージ アカウントの場所は同じである必要があります。
