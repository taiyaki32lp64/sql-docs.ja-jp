---
title: XSL のキャッシュ (SQLXML 4.0) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 79683626400f9ef9b410a182ffd81c862575e57d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013231"
---
# <a name="xsl-caching-sqlxml-40"></a>XSL のキャッシュ (SQLXML 4.0)
  XSL スタイル シートをキャッシュすると、パフォーマンスが向上します。 XSL のキャッシュを ON に設定している場合、XSL スタイル シートは初回実行時にメモリに残るので、以降の処理でパフォーマンスが向上します。 既定の設定は ON です。  
  
 XSL のキャッシュ サイズは、レジストリに次のキーを追加することで設定できます。  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\XSLCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 XSL のキャッシュ サイズは、使用できるメモリと使用している XSL スタイル シートの数に基づいて設定します。 既定値は**XSLCacheSize**サイズは 31 です。 XSL のアクセスが遅い場合はキャッシュ サイズを増やし、メモリが少ない場合はキャッシュ サイズを減らします。  
  
 パフォーマンスの向上のためお勧め設定した**XSLCacheSize**通常使用する XSL スタイル シートの数より大きい。 場合**XSLCacheSize**は数よりも小さい XSL スタイル シートのある場合は、XSL スタイル シートの増加の数にパフォーマンスが低下します。 **XSLCacheSize** 128 までの値に設定することができます。  
  
 キャッシュされた XSL スタイル シートが使用されるときには、毎回 XSL ファイルの変更回数がチェックされ、更新が必要かどうかが決定されます。 これは、ディスク コピーがキャッシュ コピーより新しいためです。  
  
## <a name="see-also"></a>参照  
 [テンプレートのキャッシュ&#40;SQLXML 4.0&#41;](template-caching-sqlxml-4-0.md)   
 [スキーマ キャッシュ&#40;SQLXML 4.0&#41;](schema-caching-sqlxml-4-0.md)  
  
  
