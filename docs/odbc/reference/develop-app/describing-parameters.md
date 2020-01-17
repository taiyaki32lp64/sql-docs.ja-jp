---
title: パラメーターの記述 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d32e5212ba1ba28262d871498f2974485d38233
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040021"
---
# <a name="describing-parameters"></a>パラメーターの記述
**SQLBindParameter**にパラメーターを記述する引数があります。 その SQL 型、有効桁数、およびスケール。 ドライバーは、この情報を使用または*メタデータ、* パラメーター値をデータ ソースで必要な型に変換します。 一見、かもしれませんが、ドライバーが、アプリケーションよりもパラメーター メタデータを認識する最適な位置にあります。結局のところ、結果セット列のドライバーは、メタデータを検出簡単にできます。 結局のところ、これは、当てはまりません。 最初に、ほとんどのデータ ソースには、パラメーターのメタデータを検出するドライバー向けの方法は使えません。 2 つ目は、ほとんどのアプリケーションが既にメタデータを認識します。  
  
 アプリケーションでハード コード化された SQL ステートメントの場合、アプリケーションの作成者は各パラメーターの型を既に知っています。 SQL ステートメントが実行時にアプリケーションによって構築された場合、アプリケーションは、ステートメントを作成する方法と、メタデータを判断できます。 句を構築ときなど、アプリケーション  
  
```  
WHERE OrderID = ?  
```  
  
 呼び出すことができます**SQLColumns** OrderID 列にします。  
  
 アプリケーションに特定できませんのパラメーター メタデータ簡単にのみ状況、ユーザーがパラメーター化されたステートメントを入力したときです。 この場合、アプリケーションが呼び出す**SQLPrepare** 、ステートメントを準備する**SQLNumParams** 、パラメーターの数を決定して**SQLDescribeParam**を記述するには各パラメーター。 ただし、前に説明したようにほとんどのデータ ソースは用意されていない、そのため、パラメーターのメタデータを検出するドライバーの**SQLDescribeParam**広くサポートされていません。
