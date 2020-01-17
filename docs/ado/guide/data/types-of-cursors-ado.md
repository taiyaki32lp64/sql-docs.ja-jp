---
title: 種類のカーソル (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 00c89272d121898b6ac5af75022344acf1dceb28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923854"
---
# <a name="types-of-cursors-ado"></a>カーソルの種類 (ADO)
一般的な規則として、アプリケーションに必要なデータ アクセスを提供する最も簡単なカーソルを使用する必要があります。 基本の (順方向専用、読み取り専用、static、スクロール、バッファリングされていない) 場合は、各追加カーソル特性には、クライアントのメモリ、ネットワークの負荷、またはパフォーマンスの価格 - があります。 多くの場合は、既定のカーソル オプションは、アプリケーションが実際に必要以上より複雑なカーソルを生成します。  
  
 カーソルの種類の選択とによって異なります、アプリケーションが結果セットを使用する方法も、結果セットでは、使用される可能性のデータの割合、データの変更、およびアプリケーションのパフォーマンスに対する感度のサイズなど、いくつかの設計考慮事項要件。  
  
 基本的では、カーソル選択で変更または単にデータを表示する必要があるかどうかによって異なります。  
  
-   結果がない変更データのセットをスクロールする場合を使用して、[順方向専用](../../../ado/guide/data/forward-only-cursors.md)または[静的](../../../ado/guide/data/static-cursors.md)カーソル。  
  
-   場合は、大きな結果セットと、いくつかの行を選択する必要がある場合を使用して、[キーセット](../../../ado/guide/data/keyset-cursors.md)カーソル。  
  
-   使用してでの設定を最近使用した結果に追加し、変更されると、し、同時実行のすべてのユーザーによって削除を同期する場合、[動的](../../../ado/guide/data/dynamic-cursors.md)カーソル。  
  
 各カーソルの種類別にする見えますは、これらのカーソルの種類がないことほどの多様な単に重複する特性とオプションの結果として留意してください。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [順方向専用カーソル](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [静的カーソル](../../../ado/guide/data/static-cursors.md)  
  
-   [Keyset カーソル](../../../ado/guide/data/keyset-cursors.md)  
  
-   [動的カーソル](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>関連項目  
 [順方向専用カーソル](../../../ado/guide/data/forward-only-cursors.md)   
 [静的カーソル](../../../ado/guide/data/static-cursors.md)   
 [Keyset カーソル](../../../ado/guide/data/keyset-cursors.md)   
 [動的カーソル](../../../ado/guide/data/dynamic-cursors.md)
