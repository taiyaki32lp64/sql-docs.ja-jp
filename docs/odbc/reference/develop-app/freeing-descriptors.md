---
title: 記述子の解放 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeHandle function [ODBC]
- descriptors [ODBC], allocating and freeing
- freeing descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 317213f4-0ebb-4bf8-a37a-4d6b1313823f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fe489222c026c1499135b716f0485bb04f51bad9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069770"
---
# <a name="freeing-descriptors"></a>記述子の解放
明示的に割り当てられた記述子は、いずれかを呼び出すことによって、明示的に解放**SQLFreeHandle**で*HandleType* SQL_HANDLE_DESC、または暗黙的にすると、接続ハンドルが解放されます。 明示的に割り当てられた記述子を解放する場合、それらを暗黙的に割り当てられた記述子を元に戻す、解放された記述子を自動的に適用されるすべてのステートメント ハンドル。  
  
 暗黙的に割り当てられた記述子を呼び出すことによってのみ解放できる**SQLDisconnect**、すべてのステートメントを削除するまたは記述子または呼び出すことによって、接続を開く**SQLFreeHandle**で、 *HandleType*の無料のステートメント ハンドルと、ステートメントに関連付けられたすべての暗黙的に割り当てられた記述子を sql_handle_stmt として。 呼び出すことによって、暗黙的に割り当てられた記述子を解放できません**SQLFreeHandle**で、 *HandleType* SQL_HANDLE_DESC の。  
  
 暗黙的に割り当てられた記述子が有効、解放されると場合でも、 **SQLGetDescField**そのフィールドで呼び出すことができます。
