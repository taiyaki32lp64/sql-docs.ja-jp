---
title: 固定長のブックマーク |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5877a6cb7a99803f854338321e333c87037c2e90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67913582"
---
# <a name="fixed-length-bookmarks"></a>固定長のブックマーク
場合、ODBC *3.x*ドライバーは ODBC を使用する必要があります*2.x*アプリケーションは固定長のブックマーク、ドライバーが、次をサポートする必要があります。  
  
-   SQL_UB_ON SQL_USE_BOOKMARKS ステートメント オプションの値として。 (SQL_UB_ON が ODBC で非推奨と*3.x*)。  
  
-   SQL_GET_BOOKMARK ステートメント オプション。
