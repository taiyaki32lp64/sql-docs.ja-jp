---
title: Azure Blob Destination | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobdest.f1
- sql14.dts.designer.afpblobdest.f1
ms.assetid: 820a1e7a-7182-4c7b-ab56-5b4097a7e042
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7ec0d571fe219719a22e841c43dedd0716ef5a4a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293445"
---
# <a name="azure-blob-destination"></a>Azure Blob Destination

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


 **Azure Blob Destination** コンポーネントは、SSIS パッケージが Azure Blob にデータを書き込めるようにします。 サポートされるファイル形式は、CSV と AVRO です。 
   
 **Azure Blob Destination** をデータ フロー デザイナーにドラッグ アンド ドロップし、ダブルクリックしてエディターを表示します。  
  
 **Azure Blob Destination** は、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。  
  
1.  **[Azure storage connection manager]** (Azure Storage 接続マネージャー) フィールドに、既存の Azure Storage 接続マネージャーを指定するか、または Azure Storage アカウントを参照する新しい Azure Storage 接続マネージャーを作成します。  
  
2.  **[Blob container name]** (BLOB コンテナー名) フィールドに、ソース ファイルを含む BLOB コンテナーの名前を指定します。  
  
3.  **[Blob name]** (BLOB 名) フィールドに、BLOB のパスを指定します。  
  
4.  **[Blob file format]** (BLOB ファイル形式) フィールドに、使用する形式を指定します。  
  
5.  CSV 形式の場合は、 **[Column delimiter character]** (列区切り文字) に値を指定する必要があります。 さらに、ファイルの 1 行目に列名が含まれている場合は、 **[先頭データ行を列名として使用する]** も指定する必要があります。  
  
6.  接続情報を指定した後、 **[列]** ページで、SSIS データ フローのマップ元の列をマップ先の列にマップします。  
  
  
