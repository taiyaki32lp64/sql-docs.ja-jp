---
title: 動的カーソル |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], dynamic
- dynamic cursors [ADO]
ms.assetid: 00460f30-8cf7-494e-82df-41012f40ae51
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86e51b7880004117e8efc96bd310c6de705d43a6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925502"
---
# <a name="dynamic-cursors"></a>動的カーソル
動的カーソルまたはカーソルの外部の他のユーザーがカーソル内から、変更が発生するかどうかに関係なく、結果セット内の行に加えられたすべての変更を検出します。 すべての insert、update、および delete ステートメントのすべてのユーザーによって行われたは、カーソルによって表示されます。 動的カーソルでは、行、順序、および、カーソルを開いた後に結果セット内の値に加えられた変更を検出できます。 (ただし、カーソルのトランザクション分離レベルを「コミット」設定すると) にコミットされるまで、カーソルの外部から行われた更新は表示されません。  
  
 たとえば、動的カーソル別のアプリケーションでは、2 つの行をフェッチしし、それらの行の 1 つの更新し、もう一方を削除します。 その後、動的カーソルでこれらの行がフェッチされた場合、削除された行は検出されませんが、更新された行は新しい値が表示されます。  
  
 動的カーソルは、適切な選択を場合は、アプリケーションが他のユーザーによって行われたすべての同時更新を検出する必要があります。 使用して、 **adOpenDynamic CursorTypeEnum**を ADO では動的カーソルを使用することを示します。  
  
## <a name="see-also"></a>関連項目  
 [順方向専用カーソル](../../../ado/guide/data/forward-only-cursors.md)   
 [静的カーソル](../../../ado/guide/data/static-cursors.md)   
 [Keyset カーソル](../../../ado/guide/data/keyset-cursors.md)
