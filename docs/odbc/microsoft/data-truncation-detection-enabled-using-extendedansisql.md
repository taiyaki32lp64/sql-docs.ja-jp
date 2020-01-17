---
title: ExtendedAnsiSQL を使用して有効になっているデータの切り捨ての検出 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d7fb67171a796755bf8d6229b9d562f69bd588ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096510"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>ExtendedAnsiSQL を使用して有効になっているデータの切り捨ての検出
ExtendedAnsiSQL フラグがオンになっていると、アプリケーションが文字またはバイナリ列にデータを挿入すると、データは切り捨てられます、切り捨てが検出されます。 ExtendedAnsiSQL フラグがオフの場合、ODBC のデスクトップ データベース ドライバーの以前のバージョンが、警告なしのデータは切り捨てられます。
