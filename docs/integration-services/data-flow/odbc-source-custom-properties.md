---
title: ODBC 入力元のカスタム プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 362bbcd8-b7b0-4bab-8afe-1212b2ad1af9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c8a84015c19df80f252e9e0364fc1f68917d1dcd
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298174"
---
# <a name="odbc-source-custom-properties"></a>ODBC 入力元のカスタム プロパティ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  次の表は、ODBC 入力元のカスタム プロパティを示しています。 すべてのプロパティは、SSIS プロパティ式から設定できます。  
  
|プロパティ名|データ型|[説明]|  
|-------------------|---------------|-----------------|  
|接続|ODBC Connection|入力元データベースにアクセスするための ODBC 接続。|  
|AccessMode|Integer (列挙)|データベースへのアクセスに使用するモード。 有効な値は、テーブル名 (0) およびSQLコマンド (1) です。<br /><br /> 既定値はテーブル名 (0) です。|  
|BatchSize|Integer|一括抽出のバッチのサイズ。 これは、配列として抽出されるレコード数です。 選択した ODBC プロバイダーが配列をサポートしていない場合のバッチ サイズは 1 です。|  
|BindCharColumnAs|Integer (列挙)|このプロパティは、ODBC 入力元で SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR などの複数バイト文字列型の列をバインドする方法を決定します。<br /><br /> 有効な値は、SQL_C_WCHAR として列をバインドする Unicode (0) と、SQL_C_CHAR として列をバインドする ANSI (1) です。 既定値は Unicode (0) です。<br /><br /> **注**:このプロパティは、**ODBC 入力元エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|BindNumericAs|Integer (列挙)|このプロパティは、ODBC 入力元で SQL_TYPE_NUMERIC データ型および SQL_TYPE_DECIMAL データ型の数値データの列をバインドする方法を決定します。<br /><br /> 有効なオプションは、SQL_C_CHAR として列をバインドする Char (0) と、SQL_C_NUMERIC として列をバインドする Numeric (1) です。 既定値は Char (0) です。<br /><br /> **注**:このプロパティは、**ODBC 入力元エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|DefaultCodePage|Integer|文字列の出力列に対して使用するコード ページ。<br /><br /> **注**:このプロパティは、**ODBC 入力元エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|ExposeCharColumnsAsUnicode|Boolean|このプロパティは、コンポーネントが CHAR 型の列を公開する方法を決定します。 既定値は False で、CHAR 型の列がマルチバイト文字列 (DT_STR) として公開されることを示します。 True の場合、CHAR 型の列はワイド文字列 (DT_WSTR) として公開されます。<br /><br /> **注**:このプロパティは、**ODBC 入力元エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|FetchMethod|Integer (列挙)|データの取得に使用されるメソッド。 有効なオプションは、行ごと (0) およびバッチ (1) です。 既定値はバッチ (1) です。<br /><br /> これらのオプションの詳細については、「 [ODBC ソース](../../integration-services/data-flow/odbc-source.md)」を参照してください。<br /><br /> **注**:このプロパティは、**ODBC 入力元エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|SqlCommand|String|AccessMode が SQL コマンドに設定されている場合に実行される SQL コマンド。|  
|StatementTimeout|Integer|エラーを返してアプリケーションに戻らず、SQL ステートメントが実行されるまで待機する秒数。 既定値は 0 です。 値 0 は、システムがタイムアウトしないことを示します。|  
|TableName|String|AccessMode がテーブル名に設定されている場合に使用される、データが保存されているテーブルの名前。|  
|LobChunckSize|Integer|LOB 列のチャンク サイズ割り当て。|  
||||  
  
## <a name="see-also"></a>参照  
 [ODBC ソース](../../integration-services/data-flow/odbc-source.md)   
 [ODBC ソース エディター ([接続マネージャー] ページ)](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md)  
  
  
