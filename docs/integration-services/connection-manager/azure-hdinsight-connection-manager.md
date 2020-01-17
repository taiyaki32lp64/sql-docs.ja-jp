---
title: Azure HDInsight 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPHDICM.F1
- SQL14.DTS.DESIGNER.AFPHDICM.F1
ms.assetid: 29d01bd9-8b38-43b1-b937-67f8aea57c0f
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: c57abdf2cd6fbdf5cbb0953f1604440d714e1e7e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67968259"
---
# <a name="azure-hdinsight-connection-manager"></a>Azure HDInsight 接続マネージャー

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


**Azure HDInsight 接続マネージャー**により、SSIS パッケージは Azure HDInsight クラスターに接続できます。

**Azure HDInsight 接続マネージャー**は、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。

**Azure HDInsight 接続マネージャー**を作成して構成するには、以下の手順のようにします。

1. **[SSIS 接続マネージャーの追加]** ダイアログ ボックスで **[AzureHDInsight]** を選び、 **[追加]** をクリックします。
2. **[Azure HDInsight Connection Manager Editor]\(Azure HDInsight 接続マネージャー エディター\)** ダイアログ ボックスで、接続先の HDInsight クラスターの **[Cluster DNS name]\(クラスター DNS 名\)** (プロトコル プレフィックスなし)、 **[ユーザー名]** 、 **[パスワード]** を指定します。
3. **[OK]** をクリックして、ダイアログ ボックスを閉じます。
4. 作成した接続マネージャーのプロパティは、 **[プロパティ]** ウィンドウに表示されます。
