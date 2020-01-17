---
title: 最新バージョンとして指定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- version control services [SQL Server], latest version
- latest file version specified
- file versions [SQL Server]
ms.assetid: 407dffb1-3ecf-461e-835d-124781f26ee7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f34631e979ded7a329939c23a758ccc0c9aea959
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773478"
---
# <a name="specify-a-version-as-the-latest-version"></a>特定のバージョンを最新バージョンとして指定する
  ソース管理にファイルをチェックインすると、そのバージョンが最新バージョンになります。つまり、その最新バージョンをチェックアウト (取得) するユーザーは、その最新項目のローカル コピーを受け取ることになります。  
  
 ただし、古いバージョンの項目を最新バージョンとして指定したい状況もあります。 たとえば、ファイルをチェックアウトし、そのファイルを修正してからチェックインした後に、 その修正内容を破棄することにしたとします。 既に項目をチェックインしているので、最初のチェックアウトを元に戻すことはできません。 この場合は、最初にチェックアウトしたバージョンを最新バージョンの項目として指定できます。  
  
 最新バージョンとして指定するには、以下の方法があります。  
  
-   **バージョンのピン留め**します。 ファイルのバージョンにピンを設定しても、そのバージョンよりも新しいバージョンが削除されるわけではありません。 ピンを設定したファイルのピンを解除することもできます。 ピンを解除すると、最後にチェックインしたバージョンのファイルが最新バージョンになります。 ただし、ピンを設定したファイルをチェックアウトすることはできません。  
  
-   **指定されたバージョンにロールバック**します。 あるバージョンにロールバックすると、そのバージョンよりも新しいバージョンはすべてソース管理から削除されます。 その後、残っている最新バージョンをチェックアウトできます。  
  
### <a name="to-pin-a-version"></a>バージョンにピンを設定するには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]ソリューションを開きます。  
  
2.  ソリューション エクスプローラーで、最新バージョンとして指定するファイルを選択します。  
  
3.  **ファイル**メニューで、**ソース管理**クリック**ViewHistory**。  
  
4.  **の履歴**\<ファイル > ダイアログ ボックスで、最新バージョンとして指定し、をクリックするバージョンを選択します。 **Pin**します。  
  
     選択したバージョンの横に、それがファイルの最新バージョンであることを示すピンの記号が表示されます。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] に別のバージョンが読み込まれている場合は、ファイルの再読み込みのための画面が表示されます。  
  
### <a name="to-roll-back-to-a-version"></a>特定のバージョンにロールバックするには  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]ソリューションを開きます。  
  
2.  ソリューション エクスプローラーで、最新バージョンとして指定する項目を選択します。  
  
3.  **ファイル**メニューで、**ソース管理**クリック**履歴**。  
  
4.  **履歴のオプション**ダイアログ ボックスで、をクリックして**OK**を表示する、**ファイルの履歴** ダイアログ ボックス。  
  
5.  **ファイルの履歴**ボックスで、最新のバージョンとして指定し、をクリックするバージョンを選択**ロールバック**します。  
  
     選択したバージョンよりも新しいバージョンがすべて削除されることを知らせるメッセージが表示されます。  
  
6.  クリックして**はい**選択したバージョンにロールバックします。  
  
## <a name="see-also"></a>参照  
 [チェックインを管理します。](../../2014/database-engine/manage-checkins.md)   
 [ファイルのチェックイン](../../2014/database-engine/check-in-files.md)  
  
  
