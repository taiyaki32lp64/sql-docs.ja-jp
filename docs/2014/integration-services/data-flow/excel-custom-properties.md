---
title: Excel のカスタム プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bdcc72b8-8950-47bd-88bf-5db6d48cc6bf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ed4f6f89091b3e8d46a13f0a93e685b4520c697f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790514"
---
# <a name="excel-custom-properties"></a>Excel のカスタム プロパティ
  **変換元のカスタム プロパティ**  
  
 Excel ソースには、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、Excel ソースのカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|データベースへのアクセスに使用するモード。 指定できる値は**Openrowset**、 **Openrowset from Variable**、 `SQL Command`、および**SQL Command from Variable**します。 既定値は **OpenRowset**です。|  
|CommandTimeOut|Integer|コマンドのタイムアウトの秒数。値 0 は、タイムアウトしないことを表します。<br /><br /> **注** : このプロパティは、 **Excel ソース エディター**では使用できませんが、 **詳細エディター**を使用して設定できます。|  
|OpenRowset|String|行セットを開くために使用するデータベース オブジェクトの名前。|  
|OpenRowsetVariable|String|行セットを開くために使用するデータベース オブジェクトの名前を格納する変数。|  
|ParameterMapping|String|SQL コマンド内のパラメーターから変数へのマッピング。|  
|SqlCommand|String|実行する SQL コマンド。|  
|SqlCommandVariable|String|実行する SQL コマンドを格納する変数。|  
  
 Excel ソースの出力および出力列には、カスタム プロパティがありません。  
  
 詳細については、「 [Excel ソース](excel-source.md)」を参照してください。  
  
 **変換先のカスタム プロパティ**  
  
 Excel 変換先には、カスタム プロパティと、すべてのデータ フロー コンポーネントとの共通プロパティの両方があります。  
  
 次の表は、Excel 変換先のカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|説明|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer (列挙)|変換先が変換先となるデータベースにアクセスする方法を指定する値。<br /><br /> このプロパティの値は、次のいずれか 1 つです。<br /><br /> `OpenRowset` (0) のテーブルまたはビューの名前を指定します。<br /><br /> `OpenRowset from Variable` (1)-テーブルまたはビューの名前を格納する変数の名前を指定します。<br /><br /> `OpenRowset Using Fastload` (3)-テーブルまたはビューの名前を指定します。<br /><br /> `OpenRowset Using Fastload from Variable` (4)-テーブルまたはビューの名前を格納する変数の名前を指定します。<br /><br /> `SQL Command` (2)-SQL ステートメントを指定します。|  
|CommandTimeOut|Integer|SQL コマンドがタイムアウトになるまでの最大秒数。この値に **0** を指定すると、時間は無制限になります。 このプロパティの既定値は **0**です。<br /><br /> 注:このプロパティでは使用できません、 **Excel 変換先エディター**を使用して設定できますが、**高度なエディター**します。|  
|FastLoadKeepIdentity|ブール値|データが読み込まれるときに ID 値をコピーするかどうかを指定する値。 このプロパティは、高速読み取りオプションのいずれかを使用した場合のみ使用できます。 このプロパティの既定値は **False**です。|  
|FastLoadKeepNulls|ブール値|データが読み込まれるときに NULL 値をコピーするかどうかを指定する値。 このプロパティは、高速読み取りオプションのいずれかを使用した場合のみ使用できます。 このプロパティの既定値は **False**です。|  
|FastLoadMaxInsertCommitSize|Integer|高速読み込み操作の実行中に、Excel 変換先でコミットを試行するバッチ サイズを指定する値。 既定値は **2147483647**す。 値 **0** は、すべての行が処理された後で、コミット操作が 1 回行われることを示します。|  
|FastLoadOptions|String|高速読み込みオプションのコレクション。 高速読み込みオプションには、テーブルのロックおよび制約のチェックが含まれています。 どちらか 1 つまたは両方を指定することも、どちらも指定しないこともできます。<br /><br /> 注:このプロパティの一部のオプションでは使用できません、 **Excel 変換先エディター**を使用して設定できますが、**高度なエディター**します。|  
|OpenRowset|String|AccessMode がいつ`OpenRowset`、テーブルまたは Excel 変換先にアクセスするビューの名前。|  
|OpenRowsetVariable|String|AccessMode がいつ`OpenRowset from Variable`、テーブルまたは Excel 変換先にアクセスするビューの名前を格納する変数の名前。|  
|SqlCommand|String|AccessMode がいつ`SQL Command`、Excel 変換先を使用して、データの変換先列を指定する TRANSACT-SQL ステートメント。|  
  
 Excel 変換先の入力および入力列には、カスタム プロパティはありません。  
  
 詳細については、「 [Excel 変換先](excel-destination.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Common Properties](../common-properties.md)  
  
  
