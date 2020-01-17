---
title: CREATE INDEX ステートメント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- SQL grammar [ODBC], create index
ms.assetid: 69438247-eef3-44c5-bef2-acef4e146f41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ad15ad436b0f34f00acbd75e371e998183f22d2f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081907"
---
# <a name="create-index-statement"></a>CREATE INDEX ステートメント
CREATE INDEX ステートメントの構文です。  
  
 [UNIQUE] インデックスの作成*インデックス名*ON*テーブル名*(*列識別子*[ASC] [DESC] [、*列識別子*[ASC][DESC]...])\<*インデックス オプションの一覧*>  
  
 場所\<*インデックス オプションのリスト*> することができます。プライマリ&#124;DISALLOW NULL&#124;無視 NULL  
  
 Microsoft Access ドライバーのみでは、NULL を許可しないようにし、NULL を無視のインデックス オプションを使用します。 DBASE および Paradox ドライバーの構文を受け取りますが、いずれかのオプションの存在を無視します。  
  
 Paradox ドライバーを使用すると、CREATE INDEX ステートメントは、Paradox キー ファイルのプライマリとセカンダリ ファイルを作成します。  
  
 このステートメントは、Microsoft Excel またはテキストのドライバーでサポートされていません。
