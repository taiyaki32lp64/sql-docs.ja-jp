---
title: CREATE INDEX ステートメントの制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX statement limitations [ODBC]
- ODBC SQL grammar, CREATE INDEX statement limitations
ms.assetid: 832dcda1-e452-48e6-8adb-7fb33c4fb4ff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0ddb695d996cdd40b7fde4087799e5c1ec84224c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081929"
---
# <a name="create-index-statement-limitations"></a>CREATE INDEX ステートメントの制限事項
CREATE INDEX ステートメントは、Microsoft Excel またはテキストのドライバーではサポートされていません。  
  
 最大 10 個の列にインデックスを定義できます。 CREATE INDEX ステートメントでは、10 個を超える列が含まれている、インデックスは認識されませんし、テーブルとして処理するインデックスは作成されませんでした。  
  
 DBASE ドライバーは、論理列にインデックスを作成することはできません。  
  
 DBASE ドライバーを使用する場合は、SELECT ステートメントの WHERE 句で指定された列 (フィールド) の .mdx (または .ndx) インデックスを作成することにより大きなファイルの応答時間を改善できます。 既存のインデックスを .mdx は =、自動的に適用されます >、 \<、> =、= <、および LIKE 述語、および結合述語でも、WHERE 句での演算子の間。  
  
 DBASE ドライバーを使用する場合は、CREATE UNIQUE INDEX ステートメントによって作成されたインデックスが実際には一意でないと重複する値は、インデックス付きの列に挿入することができます。 インデックスには、同一のキー値を持つセットから 1 つのレコードを追加できます。  
  
 Paradox ドライバーを使用すると場合、は、最初の列を含め、テーブル内の列の連続したサブセットに一意のインデックスを定義する必要があります。 テーブルまたは Borland データベース エンジンの実装を持たない Paradox ドライバーを使用すると、一意のインデックスが定義されていない場合、Paradox ドライバーによって、テーブルを更新できません。
