---
title: 付録 - 1 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 00665e16-2990-4bfc-8e17-d97ca9fb4999
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: ca084ec1849ab22940bb1617476637c105e90609
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68115030"
---
# <a name="appendix---1-accesstosql"></a>付録 - 1 (AccessToSQL)
SSMA コンソールのコマンド ライン オプションを簡単に確認します。  
  
|Sl. No.|スイッチ|必須/省略可能|スイッチ引数|使用できる値|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|はい|scriptfile|有効な XML ファイルの名前。<br /><br />スクリプトの定義ファイルのコンソールです。|  
|2|-v/変数|いいえ|variablevaluefile|有効な XML ファイルの名前。 変数は、スクリプト ファイルで使用される、このファイルを指定する必要があります。|  
|3|-c/serverconnection|いいえ|serverconnectionfile|有効な XML ファイルの名前。 このファイルには、サーバーの接続情報が含まれています。|  
|4|-x/xmloutput|いいえ|xmloutputfile|このオプションでは、XML 形式でコンソール出力を示します。 このオプションが指定されていない場合、既定の出力は、テキスト形式では。<br /><br />Xmloutputfile が指定されていない場合、XML 出力は STDOUT に送られます。<br /><br />Xmloutputfile では、XML 形式でコンソール出力の書き込み先ファイルの名前です。|  
|5|-l/log|いいえ|logfile|有効なファイル名。|  
|6|-e/projectenvironment|いいえ|projectenvironmentfolder|SSMA プロジェクト環境ファイルを含む有効なフォルダー名。|  
|7|-p/securepassword|いいえ|-、/add {< server_id > [,...n]&#124;すべて}-c&#124;serverconnection < サーバー接続ファイル > [-v&#124;変数 < 変数値ファイル >] [-o/上書き]<br /><br />または<br /><br />-、/add {< server_id > [,...n]&#124;すべて}-s&#124;スクリプト < スクリプト ファイル > [-v&#124;変数 < 変数値ファイル >] [-o/上書き]<br /><br />-r/remove {<server_id> [, ...n] &#124; all}<br /><br />-l/一覧表示<br /><br />-e/エクスポート {< サーバー id > [,...n]&#124;すべて} < 暗号化-パスワード ファイル ><br /><br />-i/インポート {< サーバー id > [,...n]&#124;すべて} < 暗号化パスワード-ファイル >|指定した場合、このオプションをその他のオプションと組み合わされていない必要があります。<br /><br />サーバー id:サーバー {文字列} に指定された一意の ID<br /><br />サーバー接続ファイル: サーバーの定義ファイル (serverconnectionfile または scriptfile)。<br /><br />変数の値のファイル:変数の定義ファイルし、サーバー接続ファイルで使用します。<br /><br />暗号化されたパスワード ファイルに:サーバー パスワード ファイルがユーザーが指定したパス フレーズを使用して暗号化することをお勧めします。|  
|8|-?|いいえ|適用できません|適用できません|  
  
## <a name="see-also"></a>関連項目  
[SSMA コンソール (アクセス) の実行](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
