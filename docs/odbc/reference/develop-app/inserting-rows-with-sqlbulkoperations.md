---
title: SQLBulkOperations による行の挿入 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], inserting rows
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: ed585ea7-4d56-4df9-8dc3-53ca82382450
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05b8f71d6f4c885c7dc64887dd92b1f600005ca7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138923"
---
# <a name="inserting-rows-with-sqlbulkoperations"></a>SQLBulkOperations による行の挿入
データを挿入する**SQLBulkOperations**でデータを更新するような**SQLBulkOperations**バインドされたアプリケーション バッファーからデータを使用しているためです。  
  
 新しい行の各列の値を持つ、ように SQL_COLUMN_IGNORE の長さまたはインジケーターの値を持つ列をすべてバインドとバインドされていないすべての列の NULL 値を受け入れるか、既定値がある必要があります。  
  
 行を挿入する**SQLBulkOperations**アプリケーションは次の処理します。  
  
1.  SQL_ATTR_ROW_ARRAY_SIZE ステートメント属性を挿入する行の数に設定し、新しいデータ値をバインドされたアプリケーションのバッファーに配置します。 長い形式のデータを送信する方法については**SQLBulkOperations**を参照してください[長い形式のデータ、SQLSetPos および SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)します。  
  
2.  必要に応じて、各列の長さ/インジケーター バッファーの値を設定します。 これは、SQL_NTS またはデータのバイト長のバイナリのバッファーを NULL に設定する列の SQL_NULL_DATA バインドされている列のデータのバイト長の文字列のバッファーにバインドされている列です。 アプリケーションでは、(存在する場合、既定値に設定するのにはそれらの列または SQL_COLUMN_IGNORE を NULL (1 つでない場合) の長さ/インジケーター バッファーの値を設定します。  
  
3.  呼び出し**SQLBulkOperations**で、*操作*引数 SQL_ADD に設定します。  
  
 後**SQLBulkOperations**返します、現在の行は変更されません。 ブックマーク列 (列 0) がバインドされている場合**SQLBulkOperations**その列にバインドされている行セットのバッファーに挿入された行のブックマークを返します。
