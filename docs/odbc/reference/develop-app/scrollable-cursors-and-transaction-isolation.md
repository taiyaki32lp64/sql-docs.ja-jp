---
title: スクロール可能なカーソルとトランザクションの分離 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92e3694690ef1cba210da29766e7528762e691f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061599"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>スクロール可能なカーソルとトランザクション分離
次の表は、変更の可視性を規定する要因を一覧表示します。  
  
|によって行われた変更:|可視性によって異なります。|  
|----------------------|----------------------------|  
|カーソル|カーソルの種類、カーソルの実装|  
|同じトランザクション内で他のステートメント|カーソルの種類|  
|他のトランザクション内のステートメント|カーソルの種類、トランザクション分離レベル|  
  
 これらの要因は、次の図に表示されます。  
  
 ![変更の可視性を規定する要因](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 次の表は、単独で、独自のトランザクションで他の操作によって、および他のトランザクションによって加えられた変更を検出するカーソルの種類ごとの機能をまとめたものです。 後者の変更の可視性は、カーソルの種類と、カーソルを含むトランザクションの分離レベルによって異なります。  
  
|カーソル type\action|self|所有<br /><br /> トランザクション|どうやって<br /><br /> トランザクション<br /><br /> (RU[a])|どうやって<br /><br /> トランザクション<br /><br /> (RC[a])|どうやって<br /><br /> トランザクション<br /><br /> (RR[a])|どうやって<br /><br /> トランザクション<br /><br /> (S[a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|スタティック|||||||  
|Insert|おそらく [b]|いいえ|いいえ|いいえ|いいえ|いいえ|  
|更新|おそらく [b]|いいえ|いいえ|いいえ|いいえ|いいえ|  
|DELETE|おそらく [b]|いいえ|いいえ|いいえ|いいえ|いいえ|  
|キーセット ドリブン|||||||  
|Insert|おそらく [b]|いいえ|いいえ|いいえ|いいえ|いいえ|  
|更新|はい|[はい]|[はい]|[はい]|いいえ|いいえ|  
|DELETE|おそらく [b]|はい|[はい]|[はい]|いいえ|いいえ|  
|動的|||||||  
|Insert|[はい]|[はい]|[はい]|[はい]|[はい]|いいえ|  
|更新|はい|[はい]|[はい]|[はい]|いいえ|いいえ|  
|DELETE|はい|[はい]|[はい]|[はい]|いいえ|いいえ|  
  
 [a] かっこで囲まれた文字は、カーソルを含むトランザクションの分離レベルを示します(これで、変更が行われた)、その他のトランザクションの分離レベルは関係ありません。  
  
 RU:READ UNCOMMITTED  
  
 RC:READ COMMITTED  
  
 RR:REPEATABLE READ  
  
 %S:Serializable  
  
 [b]、カーソルの実装方法に依存します。 SQL_STATIC_SENSITIVITY オプションを使用して、カーソルがこのような変更を検出するかどうかは報告**SQLGetInfo**します。
