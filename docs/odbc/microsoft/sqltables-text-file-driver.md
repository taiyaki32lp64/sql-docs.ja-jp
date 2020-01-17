---
title: SQLTables (テキスト ファイル ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLTables
- SQLTables function [ODBC], Text File Driver
ms.assetid: f47fd1a4-5bd8-4b2e-8ae3-e595e49f4f95
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7fcdf9cc41a55d1e529001ae7183ef9fa833363b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949011"
---
# <a name="sqltables-text-file-driver"></a>SQLTables (テキスト ファイル ドライバー)
> [!NOTE]  
>  このトピックでは、テキスト ファイル ドライバー固有の情報を提供します。 この関数の詳細については、該当するトピックを参照してください。 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)します。  
  
|引数|コメント|  
|--------------|--------------|  
|*szTableOwner*|唯一の有効な引数*szTableOwner*ドライバーのサポートの所有者名が NULL です。 *SzTableOwner*を NULL に設定すると、すべてのテーブルが返されます。 TABLE_OWNER 列で NULL が返されます。|  
|*szTableQualifier*|TABLE_QUALIFIER 列で、 **SQLTables**ディレクトリへのパスを返します。|  
|*SzTableType*|"TABLE"では、サポートされている唯一のテーブル型です。<br /><br /> テキストのドライバーを使用する場合、によって返されるファイルの一覧**SQLTables**内のファイル拡張子によって決まりますが、**拡張機能の一覧**ボックスに、 **ODBC テキスト セットアップ** ダイアログ ボックス。|
