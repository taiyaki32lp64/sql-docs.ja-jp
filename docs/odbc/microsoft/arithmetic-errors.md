---
title: 算術エラー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arithmetic errors [ODBC]
- desktop database drivers [ODBC], arithmetic errors
ms.assetid: 1c47bfac-7455-4487-b673-6b47d2a2d756
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e0880e1746b4b65070fb28bf8d83aadec301aa4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138180"
---
# <a name="arithmetic-errors"></a>算術エラー
ODBC ドライバーは、各の行をフェッチするように SELECT ステートメントの WHERE 句を評価します。 行には、0 除算、または数値のオーバーフローなどの算術エラーが発生する値が含まれている場合、ドライバーは、すべての行を返しますが、算術エラーのある列のエラーを返します。 挿入または更新する、ただし、ODBC ドライバー停止を挿入または最初の算術エラーが発生した場合にデータを更新します。
