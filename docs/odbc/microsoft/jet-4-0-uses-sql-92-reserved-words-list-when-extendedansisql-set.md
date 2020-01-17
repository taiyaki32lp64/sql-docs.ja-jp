---
title: Jet 4.0 は、sql-92 の予約語のリスト ExtendedAnsiSQL_Set |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], reserved words
ms.assetid: 7645187e-7777-4c07-9686-0a80d5c5834d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 93d23216db950ed861449061f3e35e5e88a637fb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68058795"
---
# <a name="jet-40-uses-sql-92-reserved-words-list-when-extendedansisqlset"></a>Jet 4.0 は ExtendedAnsiSQL_Set で SQL-92 の予約語リストを使用
ExtendedAnsiSQL フラグがオンになっている場合、Jet 4.0 は、sql-92 の予約語の一覧を使用します。 構文エラーで、引用符なしのオブジェクト名の結果として、予約語、sql-92 を使用しようとしています。 ExtendedAnsiSQL フラグがオフの場合、新しい予約語として前に、のオブジェクト名として使用できます。
