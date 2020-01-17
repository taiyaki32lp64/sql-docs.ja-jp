---
title: IPD の自動作成 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- automatically populating ipd [ODBC]
- descriptors [ODBC], automatically populating ipd
- descriptors [ODBC], allocating and freeing
- ipd [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 1184a7d8-d557-4140-843b-6633ae6deacc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1591843667ef01c6c88f5dfafb734f044679b2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909830"
---
# <a name="automatic-population-of-the-ipd"></a>IPD の自動作成
一部のドライバーでは、パラメーター化クエリが準備された後に、IPD のフィールドを設定できます。 記述子フィールドのデータ型、有効桁数、スケール、およびその他の特性などのパラメーターに関する情報が自動的に設定されます。 サポートするのと同じ**SQLDescribeParam**します。 この情報をなど、アプリケーションが認識していないパラメーターを持つアドホック クエリを実行するときにそれを検出するには、他の方法があるないとき、アプリケーションに特に役立ちます。  
  
 アプリケーションは、ドライバーが、呼び出すことによって自動作成をサポートしているかどうかを決定します。 **SQLGetConnectAttr**で、*属性*SQL_ATTR_AUTO_IPD の。 SQL_TRUE が返された場合、ドライバーではサポートし、アプリケーションを使用すると、SQL_ATTR_ENABLE_AUTO_IPD ステートメント属性を SQL_TRUE に設定して有効ことができます。  
  
 呼び出しでパラメーター マーカーを含む SQL ステートメントが準備された後に、ドライバーが、IPD のフィールドを設定します自動作成をサポートして有効にすると、 **SQLPrepare**します。 アプリケーションが呼び出すことでこの情報を取得できます**SQLGetDescField**または**SQLGetDescRec**、または**SQLDescribeParam**します。 パラメーターの最適なアプリケーション バッファーをバインドする、またはデータ変換を指定することに、アプリケーションは、情報を使用できます。  
  
 IPD の自動作成は、パフォーマンスの低下を生じる可能性があります。 アプリケーションは、オフに sql_false になります (既定値) に、SQL_ATTR_ENABLE_AUTO_IPD ステートメント属性をリセットすることで。
