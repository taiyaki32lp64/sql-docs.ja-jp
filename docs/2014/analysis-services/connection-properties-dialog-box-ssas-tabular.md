---
title: 接続プロパティ ダイアログ ボックス (SSAS - テーブル) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssmsimbi.ConnectionProperties.F1
ms.assetid: 17bae8ae-2ba0-4978-be70-61c687f59d54
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 26fa80cc770d4bee9163ec18c21b35bd8c807bde
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086991"
---
# <a name="connection-properties-dialog-box-ssas---tabular"></a>[接続プロパティ] ダイアログ ボックス (SSAS - テーブル)
  このページを使用すると、SQL Server Management Studio で、テーブル モデル データベースによって使用されるデータ ソースの接続プロパティを表示または変更できます。  
  
 このダイアログ ボックスは、タイムスタンプとその他の情報に加え、接続の特性を決定するカスタマイズ可能なプロパティを提供します。  
  
## <a name="options"></a>および  
  
|項目|定義|  
|----------|----------------|  
|**名前**|データ ソース名前を指定します。|  
|**ID**|データ ソース オブジェクトの識別子を表示します。|  
|**[説明]**|データ ソース オブジェクトの説明を表示します。|  
|**[タイムスタンプの作成]**|データベースが作成された日時が表示されます。|  
|**[スキーマの最終更新]**|データベースのメタデータが最後に更新されたときの日時が表示されます。|  
|**接続文字列**|データをモデルに提供するデータ ソースへの接続に使用する接続文字列を指定します。|  
|**接続の最大数**|このデータベースへのクライアント接続の最大数を指定します。|  
|**分離性**|有効な値は、ReadCommitted または Snapshot です。 詳細については、「[Isolation 要素 (ASSL)](https://docs.microsoft.com/bi-reference/assl/properties/isolation-element-assl)」を参照してください。|  
|**[クエリ タイムアウト]**|データの取得を試みたときにタイムアウトまでの時間を指定します (秒単位)。|  
|**マネージド プロバイダー**|マネージド プロバイダーの名前を指定します。 データ ソース接続にネイティブ OLE DB プロバイダーを使用する場合、この値は空です。|  
|**[権限借用情報]**|リレーショナル データ ストア (DirectQuery による) に対して実行されるクエリ、不一致バインド、リモート パーティション、およびターゲットからソースへのデータベース同期で、データを処理または更新するときにデータベース接続で使用される権限借用アカウントを指定します。<br /><br /> 有効な値には、Analysis Services サービス アカウントまたは Windows 資格情報の特定のセットが含まれます。 **[現在のユーザーの資格情報を使用する]** または **[継承する]** を指定しないでください。 これらの資格情報オプションは、テーブル モデル データベースではサポートされません。|  
  
  
