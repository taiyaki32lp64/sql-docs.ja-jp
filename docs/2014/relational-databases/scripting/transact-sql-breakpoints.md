---
title: Transact-SQL ブレークポイント
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoints
ms.assetid: c234430f-bd94-4d0d-9e74-2bf11681fa50
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 024f079d28c5ce144282bf09fff675fd308a8173
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75243139"
---
# <a name="transact-sql-breakpoints"></a>Transact-SQL ブレークポイント
  ブレークポイントは、特定の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーの実行の一時停止を指定し、その時点のコード要素の状態を確認できます。  
  
## <a name="breakpoints"></a>ブレークポイント  
 
  [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーの実行時に、特定のステートメントでブレークポイントを切り替えることができます。 ブレークポイントが含まれているステートメントに到達すると、デバッガーの実行は一時停止され、変数やパラメーターに存在する値などの情報を表示できます。  
  
 ブレークポイントの管理は、個別にエディター ウィンドウで、またはまとめて **[ブレークポイント]** ウィンドウで行うことができます。 ブレークポイントを編集することにより、実行を一時停止する条件や、ブレークポイント実行時の動作を指定できます。  
  
## <a name="breakpoint-tasks"></a>ブレークポイントのタスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|デバッガーを一時停止する [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを指定する方法について説明します。|[ブレークポイントの切り替え](../spatial/point.md)|  
|ブレークポイントを一時的に非アクティブ化し、後で再アクティブ化する方法について説明します。 ブレークポイントを削除する方法についても説明します。|[ブレークポイントの有効化、無効化、および削除](enable-disable-and-delete-breakpoints.md)|  
|指定した Transact-SQL 式の評価に基づいてブレークポイントがブレークするかどうかを決定する条件を指定する方法について説明します。|[ブレークポイント条件の指定](specify-a-breakpoint-condition.md)|  
|ブレークポイントを含むステートメントが指定の回数実行されたときにのみ、ブレークポイントがブレークするように、ヒット カウントを指定する方法について説明します。|[ヒット カウントの指定](specify-a-hit-count.md)|  
|指定されたプロセスまたはスレッドでのみブレークポイントがブレークするように、フィルターを指定する方法について説明します。|[ブレークポイント フィルターの指定](specify-a-breakpoint-filter.md)|  
|ブレークポイント ステートメントが実行されるときに行われるカスタム操作である、 **ヒット時** アクションを指定する方法について説明します。 例としては、メッセージの出力などが考えられます。|[ブレークポイント アクションの指定](specify-a-breakpoint-action.md)|  
|ブレークポイントの場所を編集する方法について説明します。|[ブレークポイントの位置の編集](edit-a-breakpoint-location.md)|  
  
## <a name="see-also"></a>参照  
 [Transact-sql デバッガー情報](transact-sql-debugger-information.md)  
  
  
