---
title: フィルターの設定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.filtersettings.f1
ms.assetid: 1b401d7d-db8a-4ba1-acb1-b8dec14e3311
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bd4c6f3729d4d090854a48a65ce6d6a2465a98e2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721211"
---
# <a name="filter-settings"></a>[フィルターの設定]
  **[フィルターの設定]** ダイアログ ボックスを使用すると、レプリケーション モニターのグリッドのフィルターを定義できます。 たとえば、アクティブなサブスクリプションのみを **[すべてのサブスクリプション]** タブに表示するには、 **[列名]** 列から **[状態]** を選択し、 **[演算子]** 列から **[等しい]** を選択し、 **[値 1]** 列から **[アクティブ]** を選択します。 1 つ以上の列に基づくフィルターを定義したら、フィルター条件に一致する行のサブセットのみがグリッドに表示されるようにフィルターが適用されます。  
  
## <a name="options"></a>および  
 **[状態]**  
 フィルター選択する列の名前を選択します。 1 つ以上の列をフィルター処理の基にすることができます。  
  
 **[等しい]**  
 フィルターで使用する演算子 (たとえば、 **[次の値以下]** ) を選択します。  
  
 **[値 1]** および **[値 2]**  
 フィルターの値を入力または選択します。 ほとんどの演算子は **[値 1]** 列に値を入力するだけで済みますが、 **[次の値の間]** と **[次の値の範囲外]** の操作は、 **[値 2]** 列にも値を入力する必要があります。  
  
 **[フィルターのクリア]**  
 このボタンをクリックすると、定義されているすべてのフィルターがクリアされます。 単一のフィルターを削除するには、フィルター行を選択して Del キーを押します。  
  
## <a name="see-also"></a>参照  
 [レプリケーションの監視](monitoring-replication.md)  
  
  
