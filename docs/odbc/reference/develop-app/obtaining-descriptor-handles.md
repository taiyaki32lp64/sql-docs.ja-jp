---
title: 記述子ハンドルの取得 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8bfa0b36ecca3af655efde84c3ce3f22ab0c1f88
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086314"
---
# <a name="obtaining-descriptor-handles"></a>記述子ハンドルの取得
アプリケーションへの呼び出しの出力引数としての任意の明示的に割り当てられた記述子ハンドルを取得する**SQLAllocHandle**します。 呼び出すことによって、暗黙的に割り当てられた記述子ハンドルが取得した**SQLGetStmtAttr**します。
