---
title: 変更の種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5f43dbf75754a16b3163bbb8e268400f34d372b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087813"
---
# <a name="types-of-changes"></a>変更の種類
ODBC で 3 種類の変更が行われた*3.x* (および ODBC の任意のバージョン)。 これらの異なる方法で旧バージョンとの互換性に影響し、さまざまな方法で処理されます。 これらの変更は、次の表で説明します。  
  
|変更の種類|説明|  
|--------------------|-----------------|  
|新しい機能|これらは、ODBC に新しく追加された機能*3.x*、アウトオブ ライン バインドまたは記述子など。 バージョンのアプリケーションおよびドライバーだけでなく、ドライバー マネージャーがいる場合にのみ、これらは実装*3.x*ので、しようとしてこれらの旧バージョンと互換性があることはありません。|  
|重複する機能|ODBC に存在する機能は*2.x*および ODBC *3.x*がそれぞれ異なる方法で実装されます。 関数は、 **SQLAllocHandle**と**SQLAllocStmt**例があります。 これらの旧バージョンとの互換性の問題し、重複しているその他の機能は、ドライバー マネージャーのマッピングによって処理されるほとんどの場合。|  
|動作の変更|これらは、ODBC では異なる方法で処理される機能*2.x*および ODBC *3.x*します。 Datetime **#define**例を示します。 これらの機能は、ODBC によって処理される*3.x*環境属性の設定に基づいて、ドライバー。 (を参照してください[動作が変更される](../../../odbc/reference/develop-app/behavioral-changes.md)詳細についてはします)。|
