---
title: ALTER TABLE ステートメントの制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1333cd6cd5946b7a3a70152e12f4d3decfa7fed0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138432"
---
# <a name="alter-table-statement-limitations"></a>ALTER TABLE ステートメントの制限事項
ときに、dBASE ファイルまたは Paradox ドライバーを使って、インデックスが作成され、新しいレコードの追加、インデックスが削除され、テーブルの内容は削除しない限り、ALTER TABLE ステートメントによって、テーブルの構造を変更ことはできません。  
  
 Microsoft Excel またはテキストのドライバーでは、ALTER TABLE ステートメントはサポートされていません。  
  
> [!NOTE]  
>  Borland データベース エンジンを実装することがなく Paradox ドライバーを使用する場合、ALTER TABLE ステートメントはサポートされていません。のみの読み取りし、追加ステートメントを使用できます。
