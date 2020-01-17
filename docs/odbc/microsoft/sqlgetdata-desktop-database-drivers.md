---
title: SQLGetData (デスクトップ データベース ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 086c5381f1801baf919508525c17faab93746ca0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003360"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (デスクトップ データベース ドライバー)
この関数は、その後に、列を取得する順序に関係なくバインドされた列があるかどうか、任意の列からデータを取得できます。  
  
> [!NOTE]  
>  \*pcbValue **SQLGetData**返す可能性があります 2 倍の数文字を実際に使用できる Jet 4.0 データベースで 510 文字より長く ANSI データにバインドする場合。 以下の 510 文字値では、実際の cbValue を返します。
