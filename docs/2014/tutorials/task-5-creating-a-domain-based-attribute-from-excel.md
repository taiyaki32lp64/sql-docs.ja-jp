---
title: タスク 5:Excel からドメイン ベースの属性を作成する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 07cbc624-2c6b-4568-96e4-f18663a05d80
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: f7e88065ff66ea953d0a91ed080fc3d7159ab794
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489107"
---
# <a name="task-5-creating-a-domain-based-attribute-from-excel"></a>タスク 5:Excel からドメイン ベースの属性を作成する
  変換するこのタスクで、**状態**の属性、**サプライヤー**としてエンティティを**ドメイン ベースの属性**します。 ドメイン ベースの 1 つとして指定し、MDS、という名前の新しいエンティティに発行する State 属性を構成した後**状態**列のすべての値と共に MDS サーバーに作成されます、**状態**の属性、**Supplier**エンティティからの値が表示されます、**状態**エンティティ。 ここで、 **Suppliers**モデルには 2 つのエンティティには。**サプライヤー**と**状態**場所、**状態**の属性、 **Supplier**エンティティに依存するドメイン ベースの属性は、 **の状態**エンティティ。  
  
1.  切り替える**Excel**を持つウィンドウ**Cleansed and Matched Suppliers.xlsx**を開きます。  
  
2.  クリックして**更新**MDS から最新の更新プログラムを取得するには、リボン ボタンをクリックします。 省略可能な実行している場合、2 つのレコードが表示**タスク 4**します。  
  
3.  列名をクリックします。**状態**(セル**I1**) で、**ヘッダー行**します。  
  
     ![Excel - 属性のプロパティ ボタン](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-01.jpg "Excel - [属性プロパティ] ボタン")  
  
4.  クリックして**属性プロパティ**リボン上。  
  
5.  **属性プロパティ**ダイアログ ボックスで、**制約付き一覧 (ドメイン ベース)** の**属性の型**します。  
  
6.  型**状態**の**新しいエンティティ名** をクリック**OK**します。  
  
     ![Excel - [属性プロパティ] ダイアログ ボックス](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-02.jpg "Excel - [属性プロパティ] ダイアログ ボックス")  
  
7.  ここで、Excel では、ことがわかります**下向きの矢印**の任意の値をクリックすると、**状態**列。 必要に応じてドロップダウン リストを使用して値を変更できます。  
  
     ![Excel - ドロップダウン リストの状態を持つ](../../2014/tutorials/media/et-creatingadomainbasedattributefromexcel-03.jpg "Excel - ドロップダウン リストの状態を持つ")  
  
## <a name="next-step"></a>次の手順  
 [タスク 6:マスター データ マネージャーを使用してドメイン ベースの属性を作成することを確認します。](../../2014/tutorials/task-6-verify-domain-based-attribute-master-data-manager.md)  
  
  
