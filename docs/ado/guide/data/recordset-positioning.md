---
title: レコード セットの配置 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdce4c7b08a8b15cdb0a9ee1111a216aeef005bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924432"
---
# <a name="recordset-positioning"></a>レコードセットを配置する
使用して、 **AbsolutePosition**内の序数位置に基づいて、レコードに移動するプロパティ、**レコード セット**オブジェクト、または現在のレコードの序数位置を決定します。 プロバイダーは、このプロパティを使用するための適切な機能をサポートする必要があります。  
  
 **AbsolutePosition**は 1 に基づいており、現在のレコードが最初のレコードは 1 に等しい、 **Recordset**します。 前述のように、内のレコードの合計数を取得することができます、 **Recordset**オブジェクトから、 **RecordCount**プロパティ。  
  
 設定すると、 **AbsolutePosition**プロパティ、現在のキャッシュ内のレコードになった場合でも ADO キャッシュに再読み込みを指定したレコードとレコードの新しいグループにします。 **CacheSize**プロパティは、このグループのサイズを決定します。  
  
> [!NOTE]
>  使用しないようにする、 **AbsolutePosition**プロパティ レコード番号の代わりにします。 前のレコードを削除すると、特定のレコードの位置を変更します。 特定のレコードと同じことが保証されていません**AbsolutePosition**場合、 **Recordset**オブジェクトのクエリを再実行または再度開きます。 ブックマークはあらゆる種類の配置の唯一の方法は、保持して、指定した位置に戻るをお勧め**Recordset**オブジェクト。
