---
title: 列ストア インデックスの推奨事項 - データベース エンジン チューニング アドバイザー (DTA)
ms.custom: seo-dt-2019
ms.date: 01/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor, columnstore index
- Database Engine Tuning Advisor, columnstore and rowstore indexes
ms.assetid: 9fba1139-82cb-4244-a41f-4337a7d0c132
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 1d0086a6698c45d5c24d89f8e6a681d14051e11f
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165998"
---
# <a name="columnstore-index-recommendations-in-database-engine-tuning-advisor-dta"></a>データベース エンジン チューニング アドバイザー (DTA) での列ストア インデックスの推奨事項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

 
  データ ウェアハウスと分析ワークロードでは、[列ストア インデックス](../../t-sql/statements/create-columnstore-index-transact-sql.md)および従来の行ストア インデックスから大きな効果を得ることができます。 データベースを構築するために選択する行ストア インデックスおよび列ストア インデックスは、アプリケーションのワークロードに依存します。 SQL Server 2016 では、[データベース エンジン チューニング アドバイザー (DTA)](../../relational-databases/performance/database-engine-tuning-advisor.md) でワークロードを分析し、データベースに構築するために適切な行ストア インデックスと列ストア インデックスの組み合わせが推奨されます。 
  
 この機能は、バージョン **16.4** 以降の SQL Server Management Studio で使用できます。 
  
## <a name="how-to-enable-columnstore-index-recommendations-in-database-engine-tuning-advisor-gui"></a>データベース エンジン チューニング アドバイザー GUI での列ストア インデックスの推奨事項を有効にする方法

  
  1. データベース エンジン チューニング アドバイザーを起動し、新しいチューニング セッションを開きます。
  
  2. **[全般]** ウィンドウで、チューニングを行うデータベースとワークロードを選択します。
  
  3. [チューニング オプション] ウィンドウで、 **[列ストア インデックスを推奨する]** チェック ボックスをオンにします (次の図を参照してください)。
  ![DTA 列ストア インデックスのチューニング オプション](../../relational-databases/performance/media/dta-columnstore-indexes-tuning-option.gif)
 
  4. その他のチューニング オプションを選択し、 **[分析の開始]** ボタンをクリックします。
  
  5. チューニングが完了したら、 **[推奨事項]** ウィンドウに列ストア インデックスを含む、すべての推奨事項が表示されます (次の図を参照してください)。      
  ![DTA 列ストア インデックスの推奨事項](../../relational-databases/performance/media/dta-columnstore-index-recommendation.gif)
  
  6. **[定義]** ハイパーリンクをクリックして、推奨インデックスを作成できる、SQL データ定義言語 (DDL) ステートメントを表示します。 既定では、DTA は、列ストア インデックスを簡単に識別できるように、列ストア インデックスの名前にサフィックス **col** を使用します (次の図を参照してください)。
  ![DTA 列ストア インデックスの定義](../../relational-databases/performance/media/dta-columnstore-index-definition.gif) 
  
  
  ## <a name="how-to-enable-columnstore-index-recommendations-in-dtaexe-utility"></a>dta.exe ユーティリティで列ストア インデックスの推奨事項を有効にする方法

dta.exe コマンド ライン ユーティリティを使用するときに、列ストアの推奨事項を有効にするには、コマンド ライン パラメーター **-fc** を使用します。

dta.exe コマンド ライン ユーティリティの詳細については、「[dta Utility](../../tools/dta/dta-utility.md)」 (dta ユーティリティ) を参照してください。

## <a name="see-also"></a>参照
[列ストア インデックス ガイド](../../relational-databases/indexes/columnstore-indexes-overview.md)       
[データベース エンジン チューニング アドバイザー](../../relational-databases/performance/database-engine-tuning-advisor.md)      
[チュートリアル:データベース エンジン チューニング アドバイザー](Tutorial:%20Database%20Engine%20Tuning%20Advisor.md)



  

