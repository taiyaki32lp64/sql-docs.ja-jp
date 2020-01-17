---
title: SET NULL コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9f8addb9b4c7c200ee8f213bdd959067039ccfff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68063671"
---
# <a name="set-null-command"></a>SET NULL コマンド
決定方法によって、ALTER TABLE - SQL、CREATE TABLE - SQL、および INSERT の null 値がサポートされている SQL コマンド。  
  
## <a name="syntax"></a>構文  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>引数  
 ON  
 ドライバーの既定値 (Visual FoxPro の既定値は OFF)。ALTER TABLE と CREATE TABLE で作成されたテーブルのすべての列で null 値を許可することを指定します。 列の定義に NOT NULL 句を含めることにより、テーブルの列に null 値のサポートをオーバーライドできます。  
  
 また、INSERT - SQL は null 値を挿入 INSERT - SQL VALUE 句に含まれていない任意の列を指定します。 INSERT - SQL は、null 値を許容する列にのみ null 値が挿入されます。  
  
 OFF  
 ALTER TABLE と CREATE TABLE で作成されたテーブルのすべての列が null 値を許可しないことを指定します。 列の定義に NULL 句を含めることで、ALTER TABLE と CREATE TABLE で列の null 値のサポートを指定できます。  
  
 またこと INSERT - SQL は空白の値に挿入 INSERT - SQL VALUE 句に含まれていない列を指定します。  
  
## <a name="remarks"></a>コメント  
 NULL に設定の影響のみ方法に null 値は、ALTER TABLE、CREATE TABLE、および INSERT - SQL でサポートされます。 その他のコマンドは、SET NULL による影響を受けません。  
  
## <a name="see-also"></a>関連項目  
 [ALTER TABLE - SQL コマンド](../../odbc/microsoft/alter-table-sql-command.md)   
 [CREATE TABLE - SQL コマンド](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL コマンド](../../odbc/microsoft/insert-sql-command.md)
