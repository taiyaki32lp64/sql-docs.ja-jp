---
title: カーソル ライブラリのキャッシュ |Microsoft Docs
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
- cache [ODBC]
ms.assetid: d6a91cd6-3905-4e3a-98ab-37fce893dbe1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 597abe268979852d754e2e3e86ae81daa8f3fed8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019067"
---
# <a name="cursor-library-cache"></a>カーソル ライブラリのキャッシュ
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 結果セット内のデータの各行については、カーソル ライブラリは、各列のデータ バインド、バインドされた各列のデータの長さと行の状態をキャッシュします。 カーソル ライブラリでは、キャッシュの両方に値を使用して経由して返される**SQLFetch**と**SQLFetchScroll**と位置指定操作の検索対象のステートメントを作成します。 詳細については、次を参照してください。[検索ステートメントの構築](../../../odbc/reference/appendixes/constructing-searched-statements.md)します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [列のデータ](../../../odbc/reference/appendixes/column-data.md)  
  
-   [列データの長さ](../../../odbc/reference/appendixes/length-of-column-data.md)  
  
-   [行の状態](../../../odbc/reference/appendixes/row-status.md)  
  
-   [キャッシュの場所](../../../odbc/reference/appendixes/location-of-cache.md)
