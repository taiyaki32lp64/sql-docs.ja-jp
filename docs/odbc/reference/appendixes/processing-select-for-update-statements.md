---
title: UPDATE ステートメントの SELECT 処理 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8ad9a20ab8abd40123ec4e4d7369373e68699205
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68028364"
---
# <a name="processing-select-for-update-statements"></a>SELECT FOR UPDATE ステートメントの処理
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 アプリケーションの相互運用性を最大に、位置指定の update ステートメントで実行することによって更新される結果セットを生成する必要があります、**選択更新**ステートメント。 カーソル ライブラリではこの必要はありません、位置指定の update ステートメントをサポートするほとんどのデータ ソースで必要です。  
  
 カーソル ライブラリ内の列を無視する、 **FOR UPDATE**の句、 **SELECT FOR UPDATE**ステートメントは、ドライバー、ステートメントに渡す前にこの句を削除します。 SQL_ATTR_CONCURRENCY ステートメント属性の前のセクションで説明されている制限事項と、カーソル ライブラリのコントロール セットに結果の列かどうかを更新できます。
