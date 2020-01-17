---
title: Azure HDInsight Create Cluster Task | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpcreatecltask.f1
- sql11.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 88ab6a4e91b98a2e6551f6a01cbca29738513b61
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028631"
---
# <a name="azure-hdinsight-create-cluster-task"></a>Azure HDInsight Create Cluster Task
**Azure HDInsight Create Cluster Task** を使用すると、指定された Azure サブスクリプションとリソース グループの Azure HDInsight クラスターを SSIS パッケージで作成できます。
  
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
