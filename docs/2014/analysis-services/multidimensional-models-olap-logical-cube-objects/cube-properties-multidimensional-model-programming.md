---
title: キューブのプロパティ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Collation property
- ID property
- ErrorConfiguration property
- cubes [Analysis Services], properties
- Description property
- DefaultMeasure property
- ProcessingMode property
- AggregationPrefix property
- EstimatedRows property
- Visible property
- StorageLocation property
- StorageMode property
- ScriptErrorHandlingMode property
- Source property
- ScriptCacheProcessingMode property
- Language property
- Name property
- properties [Analysis Services], cubes
- ProcessingPriority property
- ProactiveCaching property
ms.assetid: 72ca3387-620d-4473-8e23-7fe1f2b3d5bf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d2b99362f242ff7f815e9ceb9f67db9c80983c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727648"
---
# <a name="cube-properties"></a>キューブ プロパティ
  キューブには、キューブ全体の動作に影響するように設定できる多数のプロパティがあります。 次の表は、これらのプロパティについてまとめたものです。  
  
> [!NOTE]  
>  キューブの作成時に自動的に設定され、変更できないプロパティもあります。  
  
 キューブのプロパティを設定する方法の詳細については、次を参照してください。[キューブ デザイナー &#40;Analysis Services - 多次元データ&#41;](../cube-designer-analysis-services-multidimensional-data.md)します。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|`AggregationPrefix`|集計名に使用する共通のプレフィックスを指定します。|  
|`Collation`|Latin1_General_C1_AS のように、アンダースコアで区切られたロケール識別子 (LCID) と比較フラグを指定します。|  
|`DefaultMeasure`|キューブの既定のメジャーを定義する多次元式 (MDX) 式を保持します。|  
|`Description`|キューブの説明を指定します。クライアント アプリケーションに公開できます。|  
|`ErrorConfiguration`|重複するキー、不明なキー、エラーの制限、エラー検出時のアクション、エラー ログ ファイル、および NULL キーを処理するための、構成可能なエラー処理設定を保持します。|  
|`EstimatedRows`|キューブ内の予測行数を指定します。|  
|`ID`|キューブの一意識別子 (ID) を保持します。|  
|`Language`|キューブの既定の言語識別子を指定します。|  
|`Name`|キューブの表示名を指定します。|  
|`ProactiveCaching`|キューブのプロアクティブ キャッシュ設定を定義します。|  
|`ProcessingMode`|インデックス作成と集計を処理中に行うか、処理後に行うかを指定します。 オプションは**正規**または`lazy`します。|  
|`ProcessingPriority`|レイジー集計やインデックス作成など、バックグラウンド操作中のキューブの処理の優先度を決定します。 既定値は **0**です。|  
|`ScriptCacheProcessingMode`|スクリプト キャッシュのビルドを処理中に行うか、処理後に行うかを指定します。 オプションは**正規**と`lazy`します。|  
|`ScriptErrorHandlingMode`|エラー処理を決定します。 オプションは`IgnoreNone`または `IgnoreAll`|  
|`Source`|キューブに使用するデータ ソース ビューを表示します。|  
|`StorageLocation`|キューブのファイル システムでのストレージ場所を指定します。 指定しない場合は、キューブ オブジェクトが含まれているデータベースから場所が継承されます。|  
|`StorageMode`|キューブのストレージ モードを指定します。 値は`MOLAP`、 `ROLAP`、または `HOLAP``.`|  
|`Visible`|キューブを表示するかどうかを決定します。|  
  
> [!NOTE]  
>  Null 値やその他のデータ整合性の問題を使用する場合は、ErrorConfiguration プロパティの値を設定する方法についての詳細については、次を参照してください。 [Analysis Services 2005 でのデータの整合性問題の処理](https://go.microsoft.com/fwlink/?LinkId=81891)します。  
  
## <a name="see-also"></a>参照  
 [プロアクティブ キャッシュ&#40;パーティション&#41;](partitions-proactive-caching.md)  
  
  
