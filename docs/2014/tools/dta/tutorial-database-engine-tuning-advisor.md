---
title: チュートリアル:データベース エンジン チューニング アドバイザー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor [SQL Server], tutorials
- tutorials [Database Engine Tuning Advisor]
ms.assetid: 3b54cbbe-d8c6-424d-92f1-aa58179f4da8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 484919274e7b7df3c49ce03668950807c3627d30
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63268372"
---
# <a name="tutorial-database-engine-tuning-advisor"></a>チュートリアル:Database Engine Tuning Advisor
  データベース エンジン チューニング アドバイザーのチュートリアルへようこそ。 データベース エンジン チューニング アドバイザーは、指定されたデータベースでクエリがどのように処理されるのかを調査し、インデックス、インデックス付きビュー、パーティション分割などのデータベース構造を更新することによって、クエリ処理のパフォーマンスを強化するようユーザーに提案します。  
  
 データベース エンジン チューニング アドバイザーには、グラフィカル ユーザー インターフェイス (GUI) および **dta** コマンド プロンプト ユーティリティの 2 つのユーザー インターフェイスがあります。 GUI では、チューニング セッションの結果をすばやく簡単に表示できます。一方、 **dta** ユーティリティでは、データベース エンジン チューニング アドバイザーの機能をスクリプトへ簡単に組み込み、チューニングを自動化することができます。 また、XML 入力の取り込みが可能なので、より詳細にチューニング処理を制御できます。  
  
## <a name="what-you-will-learn"></a>学習する内容  
 このチュートリアルでは、データベース エンジン チューニング アドバイザー GUI の操作方法、および基本的な作業を GUI と **dta** ユーティリティの両方で実行する方法を学習します。 ここで学習する内容は次のとおりです。  
  
 [レッスン 1:データベース エンジン チューニング アドバイザーでの基本操作](../../relational-databases/performance/database-engine-tuning-advisor.md)  
 このレッスンでは、データベース エンジン チューニング アドバイザーの新しい GUI に慣れ親しみ、表示オプションとレイアウトの設定方法を学習します。  
  
 [レッスン 2:データベース エンジン チューニング アドバイザーの使用](lesson-2-using-database-engine-tuning-advisor.md)  
 このレッスンでは、データベース エンジン チューニング アドバイザーの GUI を使った基本的なチューニング タスクの実行方法を学習します。  
  
 [レッスン 3:Dta コマンド プロンプト ユーティリティの使用](lesson-3-using-the-dta-command-prompt-utility.md)  
 このレッスンでは、 **dta** コマンド プロンプト ユーティリティを起動する方法と、いくつかの簡単なチューニング コマンドを実行する方法を学習します。  
  
## <a name="requirements"></a>必要条件  
 このチュートリアルは、データベース管理の経験はあるが、データベース エンジン チューニング アドバイザーの GUI または **dta** コマンド プロンプト ユーティリティに不慣れなデータベース管理者を対象としています。インデックスやインデックス付きビューなどデータベースの概念や構造は理解している必要があります。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (または以降のバージョン) および [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースをインストールする必要があります。 セキュリティ強化のため、既定ではサンプル データベースがインストールされません。 サンプル データベースをインストールするには、「 [SQL Server のサンプルとサンプル データベースのインストール](http://sqlserversamples.codeplex.com)」を参照してください。  
  
## <a name="after-you-finish-this-tutorial"></a>このチュートリアルが終了したら  
 このチュートリアルのレッスンが終了したら、次のトピックを参照し、データベース エンジン チューニング アドバイザーの詳細を学習してください。  
  
-   このツールを使用した作業の実行方法の説明については、「[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md) 」を参照してください。  
  
-   コマンド プロンプト ユーティリティおよびユーティリティの動作の制御に使用できるオプションの XML ファイルに関するリファレンス情報については、「[dta Utility](dta-utility.md) 」を参照してください。  
  
## <a name="next-lesson"></a>次のレッスン  
 [レッスン 1:データベース エンジン チューニング アドバイザーでの基本操作](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
