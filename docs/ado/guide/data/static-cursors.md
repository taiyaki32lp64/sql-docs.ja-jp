---
title: 静的カーソル |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], static
- static cursors [ADO]
ms.assetid: cce93ace-c4ed-4c6c-940c-28a50ff2fd12
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 520c484bdaaa6eb59488900208993a607c5b0f7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924115"
---
# <a name="static-cursors"></a>静的カーソル
静的カーソルは常に、カーソルが最初に開いたときと、結果セットを表示します。 静的カーソルでは、実装によっては、読み取り専用または読み取り/書き込みと前方と後方スクロールを指定します。 静的カーソルでは、メンバーシップ、順序、または、カーソルを開いた後に結果セットの値に加えられた変更は、通常は検出されません。 静的カーソルは、それ自体の更新、削除、挿入を検出してもかまいませんが、必ず行う必要はありません。  
  
 静的カーソルは、その他の更新、削除、および挿入を検出することはありません。 たとえば、静的カーソルが行をフェッチした後で、別のアプリケーションによってその行が更新されるものとします。 アプリケーションで静的カーソルから行を再フェッチした場合、他のアプリケーションによって変更が行われたにも関わらず、認識される値は変更されていません。 すべての種類のスクロールがサポートされますが、プロバイダーの場合がありますまたはブックマークをサポートしていません。  
  
 アプリケーションがデータの変更し、スクロールが必要なを検出する必要がない場合、最適な選択肢は、静的カーソル。 使用して、 **adOpenStatic CursorTypeEnum** ADO では静的カーソルを使用することを指定します。  
  
## <a name="see-also"></a>関連項目  
 [順方向専用カーソル](../../../ado/guide/data/forward-only-cursors.md)   
 [Keyset カーソル](../../../ado/guide/data/keyset-cursors.md)   
 [動的カーソル](../../../ado/guide/data/dynamic-cursors.md)
