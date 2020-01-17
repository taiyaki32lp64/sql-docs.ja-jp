---
title: レベル 2 API 関数 (ODBC Driver for Oracle) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- ODBC API functions [ODBC]
- API functions [ODBC]
- level 2 API functions [ODBC]
ms.assetid: d9f49520-72d7-4234-8635-260d0ce4199c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7600734fef44071b1f5e35c136a6b9facdb8b390
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949035"
---
# <a name="level-2-api-functions-odbc-driver-for-oracle"></a>レベル 2 API 関数 (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 このレベルでの関数は、レベル 1 インターフェイスの適合性とブックマーク、動的パラメーター、および ODBC 関数の非同期実行のサポートなどの追加機能を提供します。  
  
|API 関数|注|  
|------------------|-----------|  
|**SQLBindParameter**|SQL ステートメントでパラメーター マーカーをバッファーに関連付けます。|  
|**SQLBrowseConnect**|連続するレベルの属性と属性値を返します。|  
|**SQLDataSources**|データ ソース名を一覧表示します。 ドライバー マネージャーによって実装されています。|  
|**SQLDescribeParam**|準備された SQL ステートメントに関連付けられているパラメーター マーカーの説明を返します。<br /><br /> どのようなパラメーターが、ステートメントの解析に基づくの最善の推測を返します。 パラメーターの型を特定できない場合は、長 2000 SQL_VARCHAR が返されます。|  
|**SQLDrivers**|ドライバー マネージャーによって実装されています。|  
|**SQLExtendedFetch**|ような**SQLFetch**が各列の配列を使用して複数の行を返します。 結果セットは前方スクロールし、旧バージョンとのスクロール可能な静的、順方向専用カーソルが定義されている場合に行んだことができます。 既定の列のバインドで順方向専用カーソルでは、データ バッファーに直接 BUFFERSIZE 接続属性よりも大きいデータ セットから列データがフェッチされます。 可変長のブックマークをサポートしていませんし、ブックマークからのオフセット位置 (0) 以外で行セットのフェッチをサポートしません。|  
|**SQLForeignKeys**|1 つのテーブル、または 1 つのテーブルを参照するその他のテーブルの外部キーの一覧で、外部キーの一覧を返します。|  
|**SQLMoreResults**|さらに結果が保留中かどうかを判断します hstmt、ステートメント ハンドルで SELECT、UPDATE、INSERT、または DELETE ステートメントを格納していると、そうである場合は、それらの結果の処理を初期化します。<br /><br /> Oracle は、{resultset...} エスケープ シーケンスを使用する場合にのみ、ストアド プロシージャから複数の結果セットをサポートします。|  
|**SQLNativeSql**|使用状況の詳細については、次を参照してください。[ストアド プロシージャから配列パラメーターを返す](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)します。|  
|**SQLNumParams**|SQL ステートメントのパラメーターの数を返します。 パラメーターの数が疑問符 (?) に渡された SQL ステートメント内の数と等しくなります**SQLPrepare**します。|  
|**SQLPrimaryKeys**|テーブルの主キーを構成する列の名前を返します。|  
|**SQLProcedureColumns**|入力と出力パラメーター、戻り値、1 つのプロシージャの結果セット内の列およびオーバー ロードと ORDINAL_POSITION、2 つの列の一覧を返します。 オーバー ロードは、Oracle のデータ辞書ビューの ALL_ARGUMENTS テーブルからオーバー ロードの列です。 ORDINAL_POSITION は、Oracle のデータ辞書ビューの ALL_ARGUMENTS テーブルからシーケンス列です。 パッケージ化されたプロシージャは、プロシージャ名の列は*packagename.procedurename*形式。 作成されたシノニムを参照するプロシージャまたは関数のプロシージャの列は返されません。|  
|**SQLProcedures**|データ ソース内には、プロシージャの一覧を返します。 パッケージ化されたプロシージャは、プロシージャ名の列は*packagename.procedurename*形式。<br /><br /> Oracle がパッケージ化された関数からのパッケージ化されたプロシージャを識別する手段を提供しないため、ドライバーは列 PROCEDURE_TYPE SQL_PT_UNKNOWN を返します。|  
|**SQLSetPos**|行セットのカーソル位置を設定します。 使用することができます**SQLSetPos**で**SQLGetData**行セット内の特定の行にカーソルを配置した後、バインドされていない列から行を取得します。 結果を使用してセットに追加された行*fOption* SQL_ADD が結果セットの最後の行の後に追加されます。|  
|**SQLSetScrollOptions**|Hstmt、ステートメント ハンドルに関連付けられているカーソルの動作を制御するオプションを設定します。 詳細については、次を参照してください。[カーソルの種類および同時実行の組み合わせ](../../odbc/microsoft/cursor-type-and-concurrency-combinations.md)します。|
