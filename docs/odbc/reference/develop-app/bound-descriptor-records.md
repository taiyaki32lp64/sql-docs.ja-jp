---
title: バインドされた記述子レコード |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d0016a2849feb5656cb3cd6dd46eff444f37058
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118761"
---
# <a name="bound-descriptor-records"></a>バインドされた記述子レコード
アプリケーションでは、null 値が含まれないように記述子レコードの SQL_DESC_DATA_PTR フィールドが設定、レコードがあると言います。*バインド*します。  
  
 記述子が、APD の場合は、バインドされた各レコードは、バインドされたパラメーターを構成します。 入力パラメーターには、アプリケーションは、ステートメントを実行する前に、SQL ステートメントで各動的パラメーター マーカーのパラメーターをバインドする必要があります。 出力パラメーター、アプリケーションは、パラメーターをバインドしない必要があります。  
  
 記述子が、ARD では、データベースのデータの行を記述する場合は、バインドされた各レコードは、バインドされた列を構成します。
