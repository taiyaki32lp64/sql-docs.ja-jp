---
title: Azure BLOB のダウンロード タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobdltask.f1
- sql11.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: af99d5ba79919920b2fb1ff3dde8d0a134a8ef0c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62832927"
---
# <a name="azure-blob-download-task"></a>Azure BLOB のダウンロード タスク
  Azure BLOB のダウンロード タスクを使うと、SSIS パッケージで Azure BLOB ストレージからファイルをダウンロードできます。   
**Azure BLOB のダウンロード タスク**を追加するには、SSIS デザイナーにドラッグ アンド ドロップし、ダブルクリックまたは右クリックして、 **[編集]** をクリックすると、次の **[Azure BLOB ダウンロード タスク エディター]** ダイアログ ボックスが表示されます。  
  
 次の表で、このダイアログ ボックスの各フィールドを説明します。  
  
|||  
|-|-|  
|**フィールド**|**[説明]**|  
|AzureStorageConnection|既存の Azure ストレージ接続マネージャーを指定するか、Azure ストレージ アカウントを参照する新しい接続マネージャーを作成します。この接続マネージャーは、BLOB ファイルがホストされている場所をポイントします。|  
|BlobContainer|ダウンロードする BLOB ファイルを含む BLOB コンテナーの名前を指定します。|  
|BlobDirectory|ダウンロードする BLOB ファイルを含む BLOB ディレクトリを指定します。 BLOB ディレクトリは仮想階層構造です。|  
|LocalDirectory|ダウンロードした BLOB ファイルが格納されるローカル ディレクトリを指定します。|  
|FileName|指定した名前のパターンを持つファイルを選択するための名前フィルターを指定します。 例: MySheet*.xls\* には、MySheet001.xls や MySheetABC.xlsx などのファイルが含まれます。|  
|TimeRangeFrom/TimeRangeTo|時間範囲フィルターを指定します。 **TimeRangeFrom** から **TimeRangeTo** までの間に変更されたファイルが含まれます。|  
  
  
