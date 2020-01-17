---
title: OLE DB 用の Microsoft カーソル サービス |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursor service for ole db [ADO]
- cursors [ADO], cursor service for OLE DB
ms.assetid: 1ac3bd9b-2d45-4cc8-88ec-bd8a218cfb49
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aeac8c848f01f01e8969f94c571ad15f5e7f615a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923918"
---
# <a name="the-microsoft-cursor-service-for-ole-db"></a>OLE DB 向けの Microsoft カーソル サービス
クライアント側のカーソルを選択またはに設定した場合、 **CursorLocation**プロパティを**adUseClient**、OLE DB の Microsoft カーソル サービスを呼び出すことができます。 「クライアント カーソル エンジン」、ADO のコンテキストでは基本的に同じであるへの参照も表示があります。 このサービスは、データ プロバイダーのカーソル サポート機能を補完します。 その結果、すべてのデータ プロバイダーから機能の統一感を得ることができます。  
  
 OLE DB のカーソル サービスは、動的プロパティを使用できるようにし、特定のメソッドの動作の向上します。 たとえば、**最適化**動的プロパティなどの特定の操作を容易に一時インデックスの作成ができるように、**検索**メソッド。  
  
 カーソル サービスを使用すると、常にバッチを更新するためのサポート。 データ プロバイダーが劣るカーソル、静的カーソルなどを指定できますのみときも、dynamic カーソルより高機能な種類のカーソルをシミュレートします。  
  
## <a name="see-also"></a>関連項目  
 [OLE DB (ADO サービス コンポーネント) の Microsoft カーソル サービス](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)
