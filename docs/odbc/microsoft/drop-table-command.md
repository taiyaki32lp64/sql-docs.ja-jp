---
title: DROP TABLE コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 278950bac7589b8a6b02d894c8133a699c3bd1ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071804"
---
# <a name="drop-table-command"></a>DROP TABLE コマンド
データ ソースで指定されたデータベースからテーブルを削除し、ディスクから削除されます。  
  
 Visual FoxPro ODBC ドライバーでは、このコマンドのネイティブの Visual FoxPro 言語の構文をサポートしています。 ドライバー固有の情報は、「解説」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>設定  
 *TableName*  
 データ ソースで指定されたデータベースから削除して、ディスクから削除するテーブルを指定します。  
  
 *FileName*  
 ディスクから削除する無料のテーブルを指定します。  
  
 ?  
 データ ソースで指定されたデータベースから削除して、ディスクから削除するテーブルを選択できる [削除] ダイアログが表示されます。  
  
## <a name="remarks"></a>コメント  
 DROP TABLE が発行されると、すべてのプライマリ インデックス、既定値、およびテーブルに関連付けられている検証規則も削除されます。 DROP TABLE は、これらのテーブルにルールがある場合、データ ソースと指定されたデータベースまたはリレーションが削除されるテーブルに関連付けられた他のテーブルにも影響します。 ルールとの関係は無効になります、テーブルがデータベースから削除されるとします。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 アプリケーションで ODBC SQL ステートメントの DROP TABLE をデータ ソースに送信すると、Visual FoxPro ODBC ドライバーに、次の表に示す構文を使用して Visual FoxProDROP テーブル コマンドをコマンドに変換します。  
  
|ODBC 構文|データ ソース|Visual FoxPro 構文|  
|-----------------|-----------------|--------------------------|  
|DROP TABLE*ベース テーブル名*|データベース (.dbc ファイル)|テーブルの削除*TableName*削除|  
||無料のテーブル (.dbf ファイル) のディレクトリ|消去*dbfName*<br /><br /> 消去*cdxName*<br /><br /> 消去*fptName*|
