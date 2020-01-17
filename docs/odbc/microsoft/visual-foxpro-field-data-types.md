---
title: Visual FoxPro フィールドのデータ型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 217058bf328677bf375d346ae7201c6eb81efa4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087955"
---
# <a name="visual-foxpro-field-data-types"></a>Visual FoxPro フィールドのデータ型
次の表の値、 *FieldType* ALTER TABLE と CREATE TABLE で引数を示し、かどうか*nFieldWidth*と*nPrecision*引数必須。  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|説明|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|c|N|-|文字のフィールドの幅の*n*|  
|D|-|-|date|  
|F|N|d|数値フィールドの幅を浮動*n*で*d*小数点以下桁数|  
|G|-|-|全般|  
|I|-|-|整数型|  
|L|-|-|論理|  
|M|-|-|メモ|  
|N|N|d|数値フィールドの幅の*n*で*d*小数点以下桁数|  
|T|-|-|DateTime|  
|Y|-|-|通貨|
