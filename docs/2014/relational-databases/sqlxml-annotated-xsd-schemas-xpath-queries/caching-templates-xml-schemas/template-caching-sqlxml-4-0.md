---
title: テンプレート キャッシュ (SQLXML 4.0) |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- templates [SQLXML], caching
ms.assetid: 73e151c6-b24e-4422-a116-51e0846bc6f5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0024066a5a687828cc59d5053d62e891bbf198d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013210"
---
# <a name="template-caching-sqlxml-40"></a>テンプレートのキャッシュ (SQLXML 4.0)
  テンプレートをキャッシュすると、パフォーマンスが大幅に向上します。 テンプレートのキャッシュを設定している場合、テンプレートは初回実行時にメモリに残るので、 以降のテンプレート実行でパフォーマンスが向上します。  
  
 テンプレートのキャッシュ サイズは、レジストリに次のキーを追加することで設定できます。  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 テンプレートのサイズは、使用できるメモリと使用しているテンプレートの数に基づいて設定します。 デフォルトの**TemplateCacheSize**サイズは、31 です。 テンプレートのアクセスが遅い場合はキャッシュ サイズを増やし、メモリが少ない場合はキャッシュ サイズを減らします。  
  
 パフォーマンス向上のためお勧め設定する**TemplateCacheSize**通常使用するテンプレートの数よりも高い。 場合**TemlateCacheSize**は、以下のテンプレートの増加数と、あるテンプレートの数よりもパフォーマンスが低下します。 **TemplateCacheSize**最大値は 128 に設定することができます。  
  
 キャッシュされたテンプレートが使用されるときには、毎回テンプレート ファイルの変更回数がチェックされ、更新が必要がどうかが決定されます。 これは、ディスク コピーがキャッシュ コピーより新しいためです。  
  
> [!NOTE]  
>  テンプレートのパラメーターとコマンド プロパティはキャッシュされません。  
  
## <a name="see-also"></a>関連項目  
 [スキーマ キャッシュ&#40;SQLXML 4.0&#41;](schema-caching-sqlxml-4-0.md)   
 [XSL のキャッシュ&#40;SQLXML 4.0&#41;](xsl-caching-sqlxml-4-0.md)  
  
  
