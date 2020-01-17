---
title: マイニング構造に列の追加 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], columns
- columns [data mining], mining structure columns
- adding columns
ms.assetid: 3f879344-9f66-4178-851a-e8c5ccccf4cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85a713bb9da24a67ebe8fdd097535c5a9d5ac98e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66086224"
---
# <a name="add-columns-to-a-mining-structure"></a>マイニング構造への列の追加
  データ マイニング ウィザードで定義したマイニング構造に列を追加するには、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] のデータ マイニング デザイナーを使用します。 マイニング構造の定義に使用したデータ ソース ビューに存在する列はどれでも追加できます。  
  
> [!NOTE]  
>  マイニング構造に列のコピーを複数追加することもできます。ただし、同じモデル内で 1 つの列のインスタンスが複数にならないようにし、ソースと派生列の間に誤った相関関係ができるのを防ぐ必要があります。  
  
### <a name="to-add-a-column-to-a-mining-structure"></a>マイニング構造に列を追加するには  
  
1.  データ マイニング デザイナーで **[マイニング構造]** タブを選択します。  
  
2.  マイニング構造を右クリックして **[列の追加]** を選択します。  
  
     **[列の選択]** ダイアログ ボックスが開きます。  
  
3.  **[基になるテーブル]** で、列が格納されているデータ ソース ビュー内のテーブルを選択します。  
  
4.  **[基になる列]** で、マイニング構造に追加する列を選択します。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  既に存在する列を追加すると、構造にコピーが追加され、その名前に "1" が付加されます。 コピーされた列の名前をわかりやすい名前に変更するには、マイニング構造列の **[名前]** プロパティに新しい名前を入力します。  
  
## <a name="see-also"></a>参照  
 [マイニング構造のタスクと操作方法](mining-structure-tasks-and-how-tos.md)  
  
  
