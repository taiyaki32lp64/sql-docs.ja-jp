---
title: 'レッスン 3: Dta コマンド プロンプト ユーティリティの使用 |Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 30f27f4d-8852-4b12-ba62-57f63e496f1d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e2881a2a118306f9d567236516f05bb29ad2d60a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68186568"
---
# <a name="lesson-3-using-the-dta-command-prompt-utility"></a>レッスン 3: DTA コマンド プロンプト ユーティリティの使用
  **dta** コマンド プロンプト ユーティリティは、データベース エンジン チューニング アドバイザーの機能以外にも機能があります。  
  
 データベース エンジン チューニング アドバイザーの XML スキーマを使用すれば、使い慣れた XML ツールで、このユーティリティへの入力ファイルを作成できます。 このスキーマには、インストールするときにインストールされている[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で確認できます。C:\Program Files (x86) \Microsoft SQL Server\110\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd します。  
  
 データベース エンジン チューニング アドバイザーの XML スキーマは、 [Microsoft Web サイト](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)から入手することもできます。  
  
 この XML スキーマにより、チューニング オプションをより柔軟に設定することができます。 たとえば、"what-if" 分析を実行できます。 "what-if" 分析とは、チューニングするデータベースに対して実在の物理設計構造と仮想の物理設計構造のセットを指定し、それをデータベース エンジン チューニング アドバイザーで分析する手法です。これにより、仮想的な物理設計がクエリ処理のパフォーマンスを向上させるかどうかを判断できます。 このタイプの分析には、実際に実装しなくても新しい構成を評価できるという利点があります。 仮想的な物理構造により十分にパフォーマンスが向上しなくとも、十分な結果が得られる構成になるまで再び構造を変えて分析するのは容易です。  
  
 また、データベース エンジン チューニング アドバイザーの XML スキーマと **dta** コマンド プロンプト ユーティリティを使用すると、データベース エンジン チューニング アドバイザーの機能をスクリプトに組み込み、そのスクリプトを他のデータベース設計ツールで使用することもできます。  
  
 データベース エンジン チューニング アドバイザーの XML 入力機能の使用方法は、このレッスンでは扱いません。  
  
 このレッスンでは、 **dta** コマンド プロンプト ユーティリティの基本的な構文を紹介するほか、ヘルプへのアクセス方法を説明し、簡単なワークロードをチューニングします。  
  
 ここで説明する内容は次のとおりです。  
  
-   **dta** コマンド プロンプト ユーティリティの起動とワークロードのチューニング  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [dta コマンド プロンプト ユーティリティの起動とワークロードのチューニング](lesson-1-1-tuning-a-workload.md)  
  
  
