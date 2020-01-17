---
title: 結果生成および結果解放ステートメント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 55b2ff4d428f02b59883b675fde95531366f0b4d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020601"
---
# <a name="result-generating-and-result-free-statements"></a>結果生成および結果解放ステートメント
SQL ステートメントは、疎に次の 5 つのカテゴリに分類できます。  
  
-   **結果セットを生成するステートメント**これらは、結果セットを生成する SQL ステートメント。 たとえば、**選択**ステートメント。  
  
-   **行の数を生成するステートメント**これらは、影響を受ける行の数を生成する SQL ステートメント。 たとえば、 **UPDATE**または**削除**ステートメント。  
  
-   **データ定義言語 (DDL) ステートメント**これらは、データベースの構造を変更する SQL ステートメント。 たとえば、 **CREATE TABLE**または**DROP INDEX**します。  
  
-   **ステートメントのコンテキストを変更する**これらは、データベースのコンテキストを変更する SQL ステートメント。 たとえば、**使用**と**設定**SQL Server でのステートメント。  
  
-   **管理ステートメント**これらは、データベースの管理の目的で使用する SQL ステートメント。 たとえば、 **GRANT**と**取り消す**します。  
  
 最初の 2 つのカテゴリ内の SQL ステートメントと総称されます*ステートメントの結果を生成する*します。 後者の 3 つのカテゴリ内の SQL ステートメントと総称されます*結果解放ステートメント*します。 ODBC では、ステートメントの結果生成のみを含むバッチのセマンティクスを定義します。 これらのセマンティクスは大きく異なるし、データ ソースに固有であるためです。 たとえば、オブジェクトを削除して、参照するか、同じバッチ内で同じオブジェクトを再作成、SQL Server ドライバーはサポートされません。 そのため、用語*バッチ*このマニュアルは結果を生成するのバッチのみを参照で使用されるステートメント。
