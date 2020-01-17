---
title: 分散再生のインストールの修復 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6fcd8ca8-1ceb-457d-9545-096c74e274d7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca42f1dda184bf5cd99cad7d34f5ae9fce79478b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092961"
---
# <a name="repair-a-distributed-replay-installation"></a>分散再生のインストールの修復
  分散再生コンポーネント (コントローラーまたはクライアント) を修復すると、次の処理が行われます。  
  
1.  ディスク上に関連付けられたすべてのファイルを再インストールし、既存のファイルを置き換えます。  
  
2.  対応するサービス アカウントが削除された場合、Windows サービス アカウントを再作成します。  
  
 修復操作を利用してコンポーネントを追加または削除することはできません。 コンポーネントを追加または削除を確認するかの機能ツリーに対応する要素をオフに、**機能の選択**ページ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]セットアップします。  
  
### <a name="to-repair-a-failed-installation-of-distributed-replay"></a>分散再生のインストールの失敗を修復するには  
  
1.  **開始**] メニューのをクリックして**コントロール パネルの [** 、し、ダブルクリック**プログラム追加と削除**します。  
  
2.  選択[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]で、**のアンインストールまたは変更するプログラム**ウィンドウで、し、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ダイアログ ボックスで、をクリックして**修復**。  
  
3.  手順に従って、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]ウィザード、し、**機能の選択**を修復するには、[分散再生コンポーネントを選択] ページで、 **[次へ]。** 。  
  
4.  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] インストール ウィザードを完了すると、選択した 分散再生の機能が修復されます。  
  
  
