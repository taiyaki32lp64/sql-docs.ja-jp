---
title: SELECT ステートメントの制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, SELECT statement limitations
- SELECT statement limitations [ODBC]
ms.assetid: c6b05955-f8fd-4706-a1a7-a8dbd74870c2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0cde0158e72d1e24c112c8e7955f0d6b317bd729
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987852"
---
# <a name="select-statement-limitations"></a>SELECT ステートメントの制限事項
SELECT ステートメントの非集計列と、集計関数の列を混在させることはできません。  
  
 GROUP BY 句が SELECT ステートメントの選択リストでは、GROUP BY 句の式を持つことができますのみまたは関数を設定します。  
  
 アスタリスク (すべての列の選択) を GROUP BY 句を含む SELECT ステートメントでの使用がサポートされていません。 選択する列の名前を指定する必要があります。  
  
 SELECT ステートメント内の縦棒の使用がサポートされていません。 垂直バーを格納しているデータ値を参照する必要がある場合は、SELECT ステートメントで、パラメーターを使用します。  
  
 を、SELECT ステートメントで列の別名を使用する場合、エイリアス"as"という単語の前にする必要があります。 たとえば、"SELECT col1 として、b から"。 なし、「と」、ステートメントはエラーを返します。  
  
 SELECT ステートメントに、正しくない列名が入力された、SQLSTATE 07001 エラー、「誤った数のパラメーター」が返されます、SQLSTATE S0022 エラーではなく「列が見つかりません」  
  
 Microsoft Excel のドライバーを使用すると、空の文字列が列に挿入する場合は、空の文字列が NULL に変換します。実行すると、WHERE 句で空の文字列を検索した SELECT ステートメントは、その列には成功しません。
