---
title: ExtendedAnsiSQL を設定して新しいデータ型の有効化 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 88f11adcab09dbe6964bfd67a944912fc185bccb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031118"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>ExtendedAnsiSQL を設定して新しいデータ型の有効化
ExtendedAnsiSQL フラグがオンにすると、2 つの新しいデータ型は Jet 4.0 データベースで使用できます。SQL_DECIMAL SQL_NUMERIC. 既定の有効桁数と小数点 18 と 0 をそれぞれされます。 SQL_DECIMAL または SQL_NUMERIC として型指定された ODBC 経由でアクセスされるデータは、Microsoft Jet を decimal 型に通貨の代わりにマップされます。  
  
 ExtendedAnsiSQL フラグがオフの場合は、10 進数または数値の型を持つテーブルを作成することはできず、SQLGetTypeInfo() にこれらの型が表示されません。 ただし、テーブルに新しいデータ型が含まれている場合は、適切なデータ型が使用できます。
