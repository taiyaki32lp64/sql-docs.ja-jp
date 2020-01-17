---
title: ODBC 入力先のカスタム プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 07508c40-6c08-4359-96cd-8ff17671244d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: efeed5fe9390a9e498e225138522bdc1769a22d6
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292229"
---
# <a name="odbc-destination-custom-properties"></a>ODBC 入力先のカスタム プロパティ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  次の表は、ODBC 入力先のカスタム プロパティを示しています。 すべてのプロパティは、SSIS プロパティ式から設定できます。  
  
|プロパティ名|データ型|[説明]|  
|-------------------|---------------|-----------------|  
|接続|ODBC Connection|入力先データベースにアクセスするための ODBC 接続。|  
|BatchSize|Integer|一括読み込みのバッチのサイズ。 これは、バッチとして読み込まれる行数です。 これは、行方向のパラメーターのバインドがサポートされている場合にのみ有効です。 行方向のパラメーターのバインドがサポートされていない場合のバッチ サイズは 1 です。|  
|BindCharColumnAs|Integer (列挙)|このプロパティは、ODBC 入力先で SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR などの複数バイト文字列型の列をバインドする方法を決定します。<br /><br /> 有効な値は、SQL_C_WCHAR として列をバインドする Unicode (0) と、SQL_C_CHAR として列をバインドする ANSI (1) です。 既定値は Unicode (0) です。<br /><br /> Unicode は、CHAR パラメーターのワイド文字列としてのバインドをサポートする、ほとんどの ODBC 3.x プロバイダーおよび ODBC 2.x プロバイダーに最適です。 Unicode を選択し、ExposeCharColumnsAsUnicode を True にする場合、入力元データベースで使用されるコード ページをユーザーが指定する必要はありません。<br /><br /> **注:** このプロパティは、**ODBC 入力先エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|BindNumericAs|Integer (列挙)|このプロパティは、ODBC 入力先で SQL_TYPE_NUMERIC データ型および SQL_TYPE_DECIMAL データ型の数値データの列をバインドする方法を決定します。<br /><br /> 有効な値は、SQL_C_CHAR として列をバインドする Char (0) と、SQL_C_NUMERIC として列をバインドする Numeric (1) です。 既定値は Char (0) です。<br /><br /> **注**:このプロパティは、**ODBC 入力先エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|DefaultCodePage|Integer|文字列の列に対して使用するコード ページ。<br /><br /> **注**:このプロパティは、**ODBC 入力先エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|InsertMethod|Integer (列挙)|データの挿入に使用されるメソッド。 有効な値は、行ごと (0) およびバッチ (1) です。 既定値はバッチ (1) です。<br /><br /> これらのオプションの詳細については、「[ODBC 入力元](../../integration-services/data-flow/odbc-destination.md)」の "読み込みオプション" を参照してください。|  
|StatementTimeout|Integer|エラーを返してアプリケーションに戻らず、SQL ステートメントが実行されるまで待機する秒数。 既定値は 120 です。|  
|TableName|String|データを挿入する、入力先テーブルの名前。|  
|TransactionSize|Integer|1 つのトランザクションの挿入数。 既定値は 0 で、ODBC 入力先が自動コミット モードで動作します。<br /><br /> ODBC 接続マネージャーでは分散トランザクションがサポートされないので、このプロパティに 0 以外の値を設定することができます。 ただし、接続マネージャーの **RetainSameConnection** プロパティが **true** に設定されている場合、このプロパティを 0 に設定する必要があります。<br /><br /> **注**:このプロパティは、**ODBC 入力先エディター**では使用できませんが、**詳細エディター**を使用して設定できます。|  
|LobChunkSize|Integer|LOB 列のチャンク サイズ割り当て。|  
  
  
