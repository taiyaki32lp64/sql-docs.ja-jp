---
title: HDFS ファイル ソース | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfilesrc.f1
ms.assetid: f8cda200-c389-4a2e-8ee9-5d59b326aac1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a06374e2803a5e482e6d5a7a665756e38cb7f2f
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292445"
---
# <a name="hdfs-file-source"></a>HDFS ファイル ソース

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  HDFS ファイル ソース コンポーネントは、SSIS パッケージが HDFS ファイルからデータを読み取ることを可能にします。 サポートされるファイル形式は、テキストと Avro です (ODBC ソースはサポートされません)。  
  
 HDFS ファイル ソースを構成するには、HDFS ファイル ソースをデータ フロー デザイナー上にドラッグ アンド ドロップし、そのコンポーネントをダブルクリックしてエディターを開きます。  
  
 ![HDFS ファイル ソース エディター](../../integration-services/data-flow/media/hdfs-file-source.png "HDFS ファイル ソース エディター")  
  
## <a name="options"></a>オプション  
 **[Hadoop ファイル ソース エディター]** ダイアログ ボックスの **[全般]** タブで、次のオプションを構成します。  
  
|フィールド|[説明]|  
|-----------|-----------------|  
|**Hadoop 接続**|既存の Hadoop 接続マネージャーを指定するか、新しい Hadoop 接続マネージャーを作成します。 この接続マネージャーは、HDFS ファイルがホストされる場所を示します。|  
|**ファイル パス**|HDFS ファイルの名前を指定します。|  
|**ファイル形式**|HDFS ファイルの形式を指定します。 使用できるオプションは [テキスト] と [Avro] です (ODBC ソースはサポートされません)。|  
|**列区切り文字**|テキスト形式を選択した場合は、列区切り文字を指定します。|  
|**先頭データ行を列名として使用する**|テキスト形式を選択した場合は、ファイルの最初の行に列の名前が含まれるかどうかを示します。|  
  
 これらのオプションを構成した後、 **[列]** タブを選択し、データ フローのソース列を変換先列にマップします。  
  
## <a name="see-also"></a>参照  
 [Hadoop 接続マネージャー](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [HDFS ファイル変換先](../../integration-services/data-flow/hdfs-file-destination.md)  
  
  
