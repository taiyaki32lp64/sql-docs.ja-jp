---
title: Azure BLOB のダウンロード タスク | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobdltask.f1
- sql14.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fc83e4d8e39c5521fd897ceeec07755f62b5765d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294316"
---
# <a name="azure-blob-download-task"></a>Azure BLOB のダウンロード タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Azure BLOB のダウンロード タスクを使うと、SSIS パッケージで Azure BLOB ストレージからファイルをダウンロードできます。

**Azure BLOB のダウンロード タスク**を追加するには、SSIS デザイナーにドラッグ アンド ドロップし、ダブルクリックまたは右クリックして、 **[編集]** をクリックすると、次の **[Azure BLOB ダウンロード タスク エディター]** ダイアログ ボックスが表示されます。  
  
 **Azure BLOB のダウンロード タスク**は、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。  
  
 次の表で、このダイアログ ボックスの各フィールドを説明します。  

|**フィールド**|**[説明]**|  
|---|---|
|AzureStorageConnection|既存の Azure ストレージ接続マネージャーを指定するか、Azure ストレージ アカウントを参照する新しい接続マネージャーを作成します。この接続マネージャーは、BLOB ファイルがホストされている場所をポイントします。|  
|BlobContainer|ダウンロードする BLOB ファイルを含む BLOB コンテナーの名前を指定します。|  
|BlobDirectory|ダウンロードする BLOB ファイルを含む BLOB ディレクトリを指定します。 BLOB ディレクトリは仮想階層構造です。|  
|SearchRecursively|サブディレクトリ内で再帰的に検索するかどうかを指定します。|  
|LocalDirectory|ダウンロードした BLOB ファイルが格納されているローカル ディレクトリを指定します。|  
|FileName|指定した名前のパターンを持つファイルを選択するための名前フィルターを指定します。 たとえば、`MySheet*.xls\*` には `MySheet001.xls` や `MySheetABC.xlsx` などのファイルが含まれます。|  
|TimeRangeFrom/TimeRangeTo|時間範囲フィルターを指定します。 **TimeRangeFrom** から **TimeRangeTo** までの間に変更されたファイルが含まれます。|  
