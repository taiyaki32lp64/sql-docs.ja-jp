---
title: ブックマークの比較 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44da652ad1e52934fa48f32b1b2f88b30212ad3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083304"
---
# <a name="comparing-bookmarks"></a>ブックマークの比較
ブックマークがバイトを比較できるため、等値または非等値比較できます。 これを行うには、アプリケーションは、各ブックマークをバイト配列として扱われます、2 つのブックマークのバイトを比較します。 ブックマークは、結果セット内でのみ一意では保証されているため意味がない別の結果セットから取得したブックマークを比較します。
