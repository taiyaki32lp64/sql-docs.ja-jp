---
title: 行の状態配列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57b187bf4f14bd5c05f91a433fa331e954fa0fb9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020372"
---
# <a name="row-status-array"></a>行の状態の配列
データに加えて**SQLFetch**と**SQLFetchScroll**行セットの各行のステータスを提供している配列を返すことができます。 この配列を指定し、SQL_ATTR_ROW_STATUS_PTR のステートメント属性を使用します。 この配列は、アプリケーションが割り当てられる、SQL_ATTR_ROW_ARRAY_SIZE ステートメント属性で指定された数の要素を必要とします。 によって、配列内の値が設定されます**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**、および**SQLSetPos します。** 値には、行とその状態が最後にフェッチするために変更されたかどうかの状態について説明します。  
  
|行の状態の配列の値|説明|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|行が正常にフェッチされたれ、最後にフェッチした後は変更されていません。|  
|SQL_ROW_SUCCESS_WITH_INFO|行が正常にフェッチされたれ、最後にフェッチした後は変更されていません。 ただし、行の詳細については、警告が返されました。|  
|SQL_ROW_ERROR|行のフェッチ中にエラーが発生しました。|  
|SQL_ROW_UPDATED|行は正常にフェッチされ、が最後にフェッチされた以降に更新されました。 場合は、行が、再びフェッチまたはによって更新**SQLSetPos**、その状態は、新しい状態に変更されます。<br /><br /> 一部のドライバーはデータへの変更を検出することはできませんし、そのため、この値を返すことはできません。 アプリケーションを呼び出すドライバーが行の再フェッチの更新を検出できるかどうかを判断する**SQLGetInfo** SQL_ROW_UPDATES オプションを使用します。|  
|SQL_ROW_DELETED になります|最後にフェッチしたため、行が削除されました。|  
|SQL_ROW_ADDED|行が挿入された**SQLBulkOperations**します。 行を再度フェッチによって更新されますか**SQLSetPos**、その状態が SQL_ROW_SUCCESS します。<br /><br /> この値が設定されていない**SQLFetch**または**SQLFetchScroll**します。|  
|SQL_ROW_NOROW であって|行セットには、結果セットの末尾がオーバー ラップされ、この要素の行の状態配列に対応する行が返されません。|
