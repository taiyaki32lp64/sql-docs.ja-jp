---
title: XML でのレコード セットの動的プロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset dynamic properties in XML [ADO]
ms.assetid: 52f8e379-812a-4db8-9210-94458926301c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a058a2d0c5a808f29807744c6ba01f658bebc120
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924443"
---
# <a name="recordset-dynamic-properties-in-xml"></a>XML でのレコードセットの動的プロパティ
(クライアント カーソル エンジン) から次のレコード セット プロバイダー固有のプロパティは、現在 XML 形式に永続化されます。  
  
-   更新プログラムの再同期  
  
-   Unique Table  
  
-   一意のスキーマ  
  
-   一意のカタログ  
  
-   再同期コマンド  
  
-   IRowsetChange  
  
-   IRowsetUpdate  
  
-   CommandTimeOut  
  
-   BatchSize  
  
-   UpdateCriteria  
  
-   名前を変更します。  
  
-   AutoRecalc  
  
 これらのプロパティは、スキーマのセクションでは永続化されるレコード セットの要素の定義の属性として保存されます。 これらの属性が行セットのスキーマ名前空間で定義され、接頭辞を付ける必要があります"rs:"です。  
  
## <a name="see-also"></a>関連項目  
 [レコードを XML 形式で保持する](../../../ado/guide/data/persisting-records-in-xml-format.md)
