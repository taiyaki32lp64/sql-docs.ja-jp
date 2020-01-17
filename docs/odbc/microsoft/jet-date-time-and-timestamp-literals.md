---
title: 'Jet: 日付、時刻、およびタイムスタンプのリテラル |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bb7f0fb02049b6d2f1897c4f495035aee2858f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085490"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: 日付、時刻、およびタイムスタンプのリテラル
相互運用性を最大に、アプリケーションは、エスケープ句の構文を使用して ODBC 正規の形式で日付リテラルを渡す必要があります。  
  
-   日付リテラル値、{d '*値*'} ここで、 *valu*e は"yyyy mm dd"の形式  
  
-   時刻のリテラル値、{t '*値*'} ここで、 *valu*e は"hh:mm:ss"の形式  
  
 タイムスタンプのリテラルの {ts'*値*'} ここで、 *valu*e がフォームでは"- yyyy-mm-dd hh:mm:ss [. f.]"。
