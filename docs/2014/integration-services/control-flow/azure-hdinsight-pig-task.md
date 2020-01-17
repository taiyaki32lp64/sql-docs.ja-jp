---
title: Azure HDInsight Pig Task | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afppigtask.f1
- sql11.dts.designer.afppigtask.f1
ms.assetid: 26f34f64-f344-486e-9190-acf71aef29a8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3da6ce80cc9e7bff25614e8589b4bf85dfc68e81
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832710"
---
# <a name="azure-hdinsight-pig-task"></a>Azure HDInsight Pig Task
Azure HDInsight クラスターで Pig スクリプトを実行するには、 **Azure HDInsight Pig Task** を使用します。
     
**Azure HDInsight Pig Task**を追加するには、SSIS デザイナーにドラッグ アンド ドロップし、ダブルクリックまたは右クリックして、 **[編集]** をクリックします。すると、次の **[Azure HDInsight Pig Task Editor]** (Azure HDInsight Pig Task エディター) ダイアログ ボックスが表示されます。  
  
 次の一覧で、このダイアログ ボックスのフィールドについて説明します。  
  
1.  **[HDInsightConnection]** フィールドで、既存の Azure HDInsight 接続マネージャーを選択するか、スクリプトを実行するために使用される Azure HDInsight クラスターを参照する新しいものを作成します。
  
2.  **[AzureStorageConnection]** フィールドで、既存の Azure ストレージ接続マネージャーを選択するか、クラスターに関連付けられている Azure ストレージ アカウントを参照する新しいものを作成します。 これは、スクリプト実行の出力とエラー ログをダウンロードする場合にのみ必要です。
 
3.  **[BlobContainer]** フィールドでは、クラスターに関連付けられているストレージ コンテナー名を指定します。 これは、スクリプト実行の出力とエラー ログをダウンロードする場合にのみ必要です。
  
4.  **[LocalLogFolder]** フィールドでは、スクリプト実行の出力およびエラー ログのダウンロード先となるフォルダーを指定します。 これは、スクリプト実行の出力とエラー ログをダウンロードする場合にのみ必要です。   
  
5.  実行する Pig スクリプトを指定するには、次の 2 つの方法があります。
  
    1.  **インライン スクリプト**: **[スクリプトの入力]** ダイアログ ボックスに実行するスクリプトをインラインで入力して、 **[Script]** フィールドを指定します。
  
    2.  **スクリプト ファイル**: Azure Blob Storage にスクリプト ファイルをアップロードして、 **[BlobName]** フィールドを指定します。 BLOB が HDInsight クラスターに関連付けられている既定のストレージ アカウントまたはコンテナーにない場合は、 **[ExternalStorageAccountName]** と **[ExternalBlobContainer]** フィールドを指定する必要があります。 外部 BLOB の場合は、パブリックにアクセス可能として構成されていることを確認します。  
  
     両方が指定されている場合、スクリプト ファイルが使用され、インライン スクリプトは無視されます。
