---
title: Azure Data Lake Store Destination | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSDEST.F1
- sql14.dts.designer.afpadlsdest.f1
ms.assetid: 4c4f504f-dd2b-42c5-8a20-1a8ad9a5d632
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 952dcc604dd99c2563ee0c9ef6dac3b9980ce429
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293396"
---
# <a name="azure-data-lake-store-destination"></a>Azure Data Lake Store Destination

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  **Azure Data Lake Store Destination** コンポーネントは、SSIS パッケージが Azure Data Lake Store にデータを書き込めるようにします。 サポートされるファイル形式は、テキスト、Avro、ORC です。 
  
 **Azure Data Lake Store Destination** は、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。
 
> [!NOTE]
> Azure Data Lake Store 接続マネージャーとこれを使用するコンポーネント (つまり、Azure Data Lake Store Source と Azure Data Lake Store Destination) がサービスに接続できるようにするために、必ず最新バージョンの Azure Feature Pack を [こちら](https://www.microsoft.com/download/details.aspx?id=49492)からダウンロードしてください。 

**Azure Data Lake Store Destination を構成する**

1. **Azure Data Lake Store Destination** をデータ フロー デザイナーにドラッグ アンド ドロップし、ダブルクリックしてエディターを表示します。  

2.  **[Azure Data Lake Store connection manager (Azure Data Lake Store 接続マネージャー)]** フィールドに、既存の Azure Data Lake Store 接続マネージャーを指定するか、Azure Data Lake Store サービスを参照する新しいものを作成します。  
  
    1.  **[ファイル パス]** フィールドには、データを書き込むファイルの名前を指定します。 このファイルが既に存在する場合、その内容は上書きされます。  
  
    2.  **[ファイル形式]** フィールドには、使用するファイル形式を指定します。  
  
       テキスト ファイル形式の場合は、 **[列の区切り文字]** に値を指定する必要があります。 さらに、ファイルの 1 行目に列名が含まれている場合は、 **[先頭データ行を列名として使用する]** も指定する必要があります。  

       ファイル形式が ORC の場合は、Java が必要です。 詳細については、[こちら](../../integration-services/azure-feature-pack-for-integration-services-ssis.md#dependency-on-java)を参照してください。
  
3.  接続情報を指定した後、 **[列]** ページで、SSIS データ フローのマップ元の列をマップ先の列にマップします。  
