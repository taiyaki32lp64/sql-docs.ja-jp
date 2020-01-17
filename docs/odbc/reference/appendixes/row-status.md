---
title: 行の状態 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a62bad0e69a8bf8b5365575f97e4791cbbf270d6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057110"
---
# <a name="row-status"></a>行の状態
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 カーソル ライブラリでは、行の状態のキャッシュにバッファーを作成します。 カーソル ライブラリは、このバッファーから行の状態配列 (し、SQL_ATTR_ROW_STATUS_PTR ステートメント属性で指定) の値を取得します。 行ごとに、カーソル ライブラリをこのバッファーを設定します。  
  
-   SQL_ROW_DELETED、位置指定を実行するときは、行のステートメントを削除します。  
  
-   データ ソースから行を取得中にエラーが発生したときに、SQL_ROW_ERROR **SQLFetch**します。  
  
-   持つデータ ソースから行を正常にフェッチ時に SQL_ROW_SUCCESS **SQLFetch**します。  
  
-   SQL_ROW_UPDATED 行位置指定の update ステートメントを実行するとき。
