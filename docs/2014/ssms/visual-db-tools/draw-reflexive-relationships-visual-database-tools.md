---
title: 再帰リレーションシップの作成 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- drawing reflexive relationships
- reflexive relationships
- database diagrams [SQL Server], relationships
ms.assetid: e218363f-faec-46d5-9904-a537fbcc994d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c11f414bded0c0b927579eb5dbec4664584a055e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63204955"
---
# <a name="draw-reflexive-relationships-visual-database-tools"></a>再帰リレーションシップの作成 (Visual Database Tools)
  テーブルの 1 つ以上の列を同じテーブルの他の 1 つ以上の列にリンクするには、再帰リレーションシップを作成します。 たとえば、 `employee` テーブルに `emp_id` 列と `mgr_id` 列があるとします。 各管理者は従業員でもあるため、テーブル内のこれらの 2 つの列をリレーションシップの線で関連付けます。 このリレーションシップによって、テーブルに追加された各管理者 ID は、既存の従業員 ID と確実に一致します。  
  
 リレーションシップを作成する前に、まずテーブルに主キー制約または UNIQUE 制約を定義する必要があります。 次に、主キー列を目的の列に関連付けます。 リレーションシップを作成すると、対応する列がテーブルの外部キーになります。  
  
### <a name="to-draw-a-reflexive-relationship"></a>再帰リレーションシップを作成するには  
  
1.  データベース ダイアグラムで、他の列と関連付けるデータベース列の行セレクターをクリックし、ポインターをテーブル外部にドラッグして線を表示させます。  
  
2.  選択したテーブルに線をドラッグします。  
  
3.  マウスのボタンを離します。 **[テーブルと列]** ダイアログ ボックスが表示されます。  
  
4.  リレーションシップを形成する外部キー列、および主キーのテーブルと列を選択します。  
  
5.  **[OK]** を 2 回クリックしてリレーションシップを作成します。  
  
 テーブルに対してクエリを実行するとき、再帰リレーションシップを使用して自己結合を作成できます。 結合を含むテーブル クエリの実行の詳細については、「 [結合を使用したクエリ (Visual Database Tools)](visual-database-tools.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [結合を使用したクエリ (Visual Database Tools)](visual-database-tools.md)  
  
  
