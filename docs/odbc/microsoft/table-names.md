---
title: テーブル名 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5dd8de055521f4a1831d20a9a34bedb9309d1de6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67939788"
---
# <a name="table-names"></a>テーブル名
ときに、dBASE、Excel、Paradox、またはドライバーが使用されるテキスト、テーブル名で発生するは、SELECT や DELETE FROM 句と更新の後、insert INTO 句の後に CREATE TABLE、および DROP TABLE には、有効なパスを含めることができます、プライマリ名およびファイルの名前の拡張機能.  
  
 SQL ステートメントの他の場所でテーブル名の使用は、パスまたは拡張機能の使用をサポートしていませんがプライマリの名前 (たとえば、EMP から C:\ABC\EMP) のみを受け入れます。  
  
 相関名 (別名) を使用できます。 例:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
