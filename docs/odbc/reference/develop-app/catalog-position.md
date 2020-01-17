---
title: カタログの位置 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog position
- catalog position [ODBC]
ms.assetid: 5bc5f64b-c75a-43d2-8745-102ec7a49000
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3d7c320521a9948c7968f4f7f5d42fd715f6c03d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062683"
---
# <a name="catalog-position"></a>カタログの位置
識別子および他の識別子を区切る方法でカタログ名の位置は、データ ソースからデータ ソースに変化します。 たとえば、Xbase データソースでカタログ名がディレクトリで、Microsoft® Windows® は分離 (つまり、ファイル名)、テーブル名に円記号 (\\)。 次の図では、この条件を示します。  
  
 ![カタログの位置。Xbase](../../../odbc/reference/develop-app/media/ch0801.gif "ch0801")  
  
 SQL Server データ ソースには、カタログはデータベースでありはスキーマとテーブル名とピリオド (.) で区切られます。  
  
 ![カタログの位置。SQL Server](../../../odbc/reference/develop-app/media/ch0802.gif "ch0802")  
  
 Oracle データ ソースに、カタログもデータベースが、テーブル名に依存して、によって、スキーマとテーブルの名前から分離されて、アット マーク (@)。  
  
 ![カタログの位置。Oracle](../../../odbc/reference/develop-app/media/ch0803.gif "ch0803")  
  
 カタログの区切り記号とカタログ名の場所を決定するには、アプリケーションが呼び出す**SQLGetInfo** SQL_CATALOG_NAME_SEPARATOR および SQL_CATALOG_LOCATION のオプションを使用します。 相互運用可能なアプリケーションでは、これらの値に従って識別子を構築する必要があります。  
  
 1 つ以上の部分を含む識別子を囲むには、アプリケーションは各部分を個別に見積もりし、を識別子を区切る文字を引用符で囲むしないように注意してあります。 カタログ (\XBASE\SALES\CORP) と、テーブル (Parts.dbf) 名がカタログの区切り記号ではないすべての行と Xbase のテーブルの列を選択するには、次のステートメントを引用符でなど (\\)。  
  
```  
SELECT * FROM "\XBASE\SALES\CORP"\"PARTS.DBF"  
```  
  
 すべての行と、Oracle テーブルの列を選択するには、次のステートメントの引用符カタログ (Sales)、(企業) のスキーマおよびテーブル (部分) の名前がカタログではありません (@) またはスキーマ (.) の区切り記号。  
  
```  
SELECT * FROM "Corporate"."Parts"@"Sales"  
```  
  
 識別子を囲む方法の詳細については、次のセクションを参照してください。[引用符で囲まれた識別子](../../../odbc/reference/develop-app/quoted-identifiers.md)します。
