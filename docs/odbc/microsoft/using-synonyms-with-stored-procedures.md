---
title: シノニムを使用してストアド プロシージャ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8620b039-a086-4534-8710-cc8b1787dc80
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6e798a9c7fa3365082a2e6dab562596d56649ec4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088021"
---
# <a name="using-synonyms-with-stored-procedures"></a>ストアド プロシージャでのシノニムの使用
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 Microsoft ODBC Driver for Oracle のバージョン 2.0 および 2.5 ではストアド プロシージャの呼び出し元の Oracle とシノニムはサポートされません。 シノニムは、テーブルなどの他の Oracle データベース オブジェクトで使用する場合に期待どおりに動作します。
