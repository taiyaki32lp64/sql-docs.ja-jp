---
title: CREATE TABLE ステートメントで NOT NULL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 808cddbd805db09d1b5c356d5b5af5734a5dcc16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086326"
---
# <a name="not-null-in-create-table-statements"></a>CREATE TABLE ステートメントの NULL 以外
いくつかのデータベース、および特にデスクトップ データベースは、サポートしていません、 **NOT NULL**内の列制約**CREATE TABLE**ステートメント。 詳細についてで SQL_NON_NULLABLE_COLUMNS オプションを参照して、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)関数の説明。
