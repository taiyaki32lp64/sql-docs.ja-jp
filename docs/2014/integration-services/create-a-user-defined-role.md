---
title: ユーザー定義ロールの作成 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: c4128993-2333-48c7-84b1-e51cdcea393d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0277b936ddd4884f8a6b9b47b9184766dac9954b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66060241"
---
# <a name="create-a-user-defined-role"></a>ユーザー定義ロールを作成する
    
### <a name="to-create-a-user-defined-role"></a>ユーザー定義ロールを作成するには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]を開きます。  
  
2.  **[表示]** メニューの **[オブジェクト エクスプローラー]** をクリックします。  
  
3.  オブジェクト エクスプローラー ツール バーで **[接続]** をクリックし、 **[データベース エンジン]** をクリックします。  
  
4.  **[サーバーへの接続]** ダイアログ ボックスで、サーバー名を指定し、認証モードを選択します。 ピリオド (.)、(local)、または `localhost` を使用すると、ローカル サーバーを指定できます。  
  
5.  **[接続]** をクリックします。  
  
6.  [データベース]、[システム データベース]、[msdb]、[セキュリティ]、[ロール] を順に展開します。  
  
7.  [ロール] ノードの [データベース ロール] を右クリックし、 **[新しいデータベース ロール]** をクリックします。  
  
8.  [全般] ページでロール名を指定します。必要に応じて、所有者および所有されているスキーマを指定し、ロール メンバーを追加します。  
  
9. 必要に応じて、 **[権限]** をクリックし、オブジェクトの権限を構成します。  
  
10. 必要に応じて、 **[拡張プロパティ]** をクリックし、任意の拡張プロパティを構成します。  
  
11. **[OK]** をクリックします。  
  
  
