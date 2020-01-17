---
title: Azure Feature Pack |Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL11.SSIS.AZURE.F1
- SQL12.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 536dce64880c1e70b1b8a0c4b419811c1b32a975
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62772136"
---
# <a name="azure-feature-pack"></a>Azure Feature Pack
SQL Server Integration Services (SSIS) Feature Pack for Azure は、このページにリストされている SSIS のコンポーネントを提供して、Azure サービスへの接続、Azure とオンプレミスのデータ ソース間でのデータ転送、および Azure に格納されたデータの処理を行うための拡張機能です。

## <a name="components-in-the-feature-pack"></a>Feature Pack のコンポーネント
  
-   接続マネージャー  
  
    -   [Azure Storage 接続マネージャー](connection-manager/azure-storage-connection-manager.md)  
  
    -   [Azure サブスクリプション接続マネージャー](connection-manager/azure-subscription-connection-manager.md)  
    
    -   [Azure Data Lake Store 接続マネージャー](../../2014/integration-services/azure-data-lake-store-connection-manager.md)
    
    -   [Azure Resource Manager の接続マネージャー](../../2014/integration-services/azure-resource-manager-connection-manager.md)
    
    -   [Azure HDInsight 接続マネージャー](../../2014/integration-services/azure-hdinsight-connection-manager.md)
  
-   処理手順  
  
    -   [Azure BLOB のアップロード タスク](control-flow/azure-blob-upload-task.md)  
  
    -   [Azure BLOB のダウンロード タスク](control-flow/azure-blob-download-task.md)  
  
    -   [Azure HDInsight Hive タスク](control-flow/azure-hdinsight-hive-task.md)  
  
    -   [Azure HDInsight Pig タスク](https://msdn.microsoft.com/library/mt146781(v=sql.120).aspx)
  
    -   [Azure HDInsight クラスターの作成タスク](control-flow/azure-hdinsight-create-cluster-task.md)  
  
    -   [Azure HDInsight クラスターの削除タスク](control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure SQL DW のアップロード タスク](../../2014/integration-services/azure-sql-dw-upload-task.md)    
    
    -   [Azure Data Lake Store ファイル システム タスク](control-flow/file-system-task.md)    
  
-   データ フロー コンポーネント  
  
    -   [Azure BLOB Source](https://msdn.microsoft.com/library/mt146775(v=sql.120).aspx)  
  
    -   [Azure Blob Destination](data-flow/azure-blob-destination.md)  
    
    -   [Azure Data Lake Store Source](../../2014/integration-services/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store Destination](../../2014/integration-services/azure-data-lake-store-destination.md)
  
-   Azure Blob 列挙子と ADLS File 列挙子。 「 [Foreach Loop Container](control-flow/foreach-loop-container.md)」を参照してください。  
  
 
## <a name="download-the-feature-pack"></a>Feature Pack のダウンロード  
SQL Server Integration Services (SSIS) Feature Pack for Azure をダウンロードします。  
  
-   [Microsoft SQL Server 2014 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=47366)  

## <a name="prerequisites"></a>前提条件  
この機能パックをインストールする前に、次の前提条件をインストールする必要があります。  
  
-   SQL Server Integration Services  
-   .NET Framework 4.5  
  
## <a name="scenarios"></a>シナリオ  
  
### <a name="big-data-processing"></a>ビッグ データ処理  
 Azure コネクタを使用して、次のビッグ データの処理を完了します。  
  
1.  Azure Blob Upload Task を使用して、入力データを Azure Blob ストレージにアップロードします。  
  
2.  Azure HDInsight Create Cluster Task を使用して、Azure HDInsight のクラスターを作成します。 独自のクラスターを使用する場合は、この手順は省略できます。  
  
3.  Azure HDInsight Hive Task か Azure HDInsight Pig Task を使用して、Azure HDInsight クラスターで Pig または Hive ジョブを呼び出します。  
  
4.  手順 2 でオンデマンドの HDInsight クラスターを作成した場合は、使用後の HDInsight クラスターを Azure HDInsight Delete Cluster Task で削除します。  
  
5.  Azure HDInsight Blob Download Task を使用して、Azure Blob ストレージから Pig/Hive の出力データをダウンロードします。  
  
 ![SSIS-AzureConnector-BigDataScenario](media/ssis-azureconnector-bigdatascenario.png "SSIS-AzureConnector-BigDataScenario")  
  
### <a name="cloud-data-archiving"></a>クラウド データのアーカイブ  
 SSIS パッケージ内の Azure Blob Destination を使用して、出力データを Azure Blob ストレージに書き込みむか、または Azure Blob Source を使用して、Azure Blob ストレージからデータを読み取ります。  
  
 ![SSIS-AzureConnector-CloudArchive-1](media/ssis-azureconnector-cloudarchive-1.png "SSIS-AzureConnector-CloudArchive-1")  
  
 ![SSIS-AzureConnector-CloudArchive-2](media/ssis-azureconnector-cloudarchive-2.png "SSIS-AzureConnector-CloudArchive-2")  
  
 また、Azure Blob 列挙子とともに Foreach ループ コンテナーを使用して、複数の bob ファイルのデータを処理します。  
  
 ![SSIS-AzureConnector-CloudArchive-3](media/ssis-azureconnector-cloudarchive-3.png "SSIS-AzureConnector-CloudArchive-3")  
  
  
