---
title: 廃止されたフルテキスト検索プロパティを使用するストアド プロシージャの変更 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- discontinued properties [Full-Text Search]
- stored procedures [Full-Text Search]
ms.assetid: 8d9392d9-a9ba-4378-84e4-59f516b67ddb
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5204b27fb4745f8005a328dc62503f7db418387d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66093850"
---
# <a name="modify-stored-procedures-that-use-discontinued-full-text-search-properties"></a>廃止されたフルテキスト検索プロパティを使用するストアド プロシージャを変更する
  ストアド プロシージャが正しく実行されるようにするには、既存のプロシージャを編集し、削除または非推奨とされたフルテキスト関連のプロパティおよび設定を削除する必要があります。  
  
## <a name="component"></a>コンポーネント  
 フルテキスト検索  
  
## <a name="description"></a>説明  
 以下のフルテキスト検索関連のプロパティおよび設定が削除されています。  
  
-   **DataTimeout**  
  
-   **ConnectTimeout**  
  
-   **Clean_up**  
  
-   **LogSize**  
  
 以下のフルテキスト検索関連のプロパティおよび設定が削除または非推奨とされています：  
  
-   フルテキスト カタログの "パス"。 フルテキスト カタログは、システムでの特定のファイル パスを持たない論理オブジェクトになります。  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ではデータベースがフルテキスト検索に対して常に既定で有効になっているので、SP_FULLTEXT_DATABASE の有効化/無効化は効力がありません。  
  
## <a name="corrective-action"></a>修正措置  
 お使いのストアド プロシージャを変更して、これらのプロパティを削除してください。  
  
## <a name="see-also"></a>参照  
 [アップグレード アドバイザーの使用](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
