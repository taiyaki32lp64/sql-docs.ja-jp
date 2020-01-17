---
title: 内のテーブル ヒントにインデックス付きビューの定義は、互換性モード 80 では無視され、モードが 90 以上では許可されません |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- query hints [SQL Server]
- indexed views [SQL Server], query hints
ms.assetid: 405dfcff-a3a6-4e6d-a53a-ed77bbacdd13
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 69a6bae06b1cb5d7a727ff2582f10bccf1e21ca8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091807"
---
# <a name="table-hints-in-indexed-view-definitions-are-ignored-in-80-compatibility-mode-and-are-not-allowed-in-90-mode-or-later"></a>インデックス付きビュー定義のテーブル ヒントが互換性モード 80 では無視され、互換性モード 90 以上では許可されない
  互換性モード 90 以上では、インデックス付きビューの定義のテーブル ヒントは使用できません。 詳細については、次のトピックを参照してください。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オンライン ブック。「インデックス付きビューのデザイン」、「を作成するインデックス付きビュー、」と"クエリ ヒント ([!INCLUDE[tsql](../../includes/tsql-md.md)])."  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>修正措置  
 テーブル ヒントは、インデックス付きビューの定義から削除する必要があります。 どの互換性モードを使用しているかにかかわらず、アプリケーションをテストすることをお勧めします。 アプリケーションをテストすることによって、インデックス付きビューがクエリに一致した場合など、インデックス付きビューが作成、更新、アクセスされたときに想定どおりに実行されるかどうかを確認できます。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
