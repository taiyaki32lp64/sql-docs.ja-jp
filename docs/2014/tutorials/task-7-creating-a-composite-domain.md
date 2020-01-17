---
title: タスク 7:複合ドメインを作成する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ae778647-1df0-4952-9a69-0ef6177eea9c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: bbc00117e10e48adbde37b9f0561610feff8f87e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65488963"
---
# <a name="task-7-creating-a-composite-domain"></a>タスク 7:複合ドメインを作成する
  このタスクで、複合ドメインを作成する**Address Validation**で構成される**Address Line**、**市区町村**、**状態**、および**Zip**ドメイン。 複合ドメインでは、ルール内の複数のドメインに関するクロスドメイン ルールを定義できます。 複合ドメインには、フィールド値を複数のドメインに解析できるなどの利点があります。  たとえば、氏名フィールドの値を、名、ミドル ネーム、および姓の個別のドメインに解析できます。 このチュートリアルでは、クロスドメイン ルールのみを定義します。 参照してください[複合ドメインの管理](https://msdn.microsoft.com/library/hh510399.aspx)の詳細。  
  
1.  左側のウィンドウで次のようにクリックします。**複合ドメインの作成**ツールバーのボタンをクリックします。  
  
     ![複合ドメインのツール バー ボタンを作成する](../../2014/tutorials/media/et-creatingacompositedomain-01.jpg "複合ドメインのツール バー ボタンの作成")  
  
2.  入力**住所の確認に**の**複合ドメイン名**します。  
  
     ![アドレス検証複合ドメイン](../../2014/tutorials/media/et-creatingacompositedomain-02.jpg "アドレス検証複合ドメイン")  
  
3.  ドメインの一覧から選択**Address Line**、**City**、**State**、および**Zip**  をクリック**右矢印**追加する、**複合ドメイン内の**一覧。  
  
4.  **[OK]** をクリックしてダイアログ ボックスを閉じます。  
  
## <a name="next-step"></a>次の手順  
 [タスク 8:複合ドメイン ルールを作成します。](../../2014/tutorials/task-8-creating-a-composite-domain-rule.md)  
  
  
