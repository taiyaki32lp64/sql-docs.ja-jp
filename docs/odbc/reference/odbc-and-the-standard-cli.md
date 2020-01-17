---
title: ODBC と標準の CLI |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5222282bce2acf49cc6a144667ddd691528b3693
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944844"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC と標準の CLI
ODBC は、次の仕様およびコールレベル インターフェイス (CLI) を処理する標準に揃えて配置します。 (ODBC の機能は、これらの標準のそれぞれのスーパー セットです)。  
  
-   Open Group CAE 仕様"のデータ管理。SQL 呼び出しレベルのインターフェイス (CLI)"  
  
-   ISO/IEC 9075-3:1995 (E) コールレベル インターフェイス (SQL/CLI)  
  
 この配置では、結果として、以下が該当します。  
  
-   Open Group および ISO CLI 仕様に記述されたアプリケーションは、ODBC *3.x*ドライバーまたは ODBC でコンパイルされるときに、標準に準拠したドライバー *3.x*ヘッダー ファイルし、リンクされています。ODBC *3.x*ライブラリ、ドライバーは ODBC へのアクセスを得る場合と*3.x*ドライバー マネージャー。  
  
-   Open Group および ISO CLI 仕様に記述されたドライバーは ODBC *3.x*アプリケーションまたは ODBC でコンパイルされるときに、標準に準拠したアプリケーションを*3.x*ヘッダー ファイルし、リンクODBC を使って*3.x*ライブラリ、ODBC を使用してドライバー、アプリケーションがアクセスおよび*3.x*ドライバー マネージャー。 (詳細については、次を参照してください。[標準に準拠したアプリケーションやドライバー](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)します。  
  
 コア インターフェイスの適合性レベルには、ISO CLI でのすべての機能と、開いているグループ CLI で nonoptional すべての機能が含まれます。 開くグループ CLI の省略可能な機能より高いインターフェイスの適合性レベルに表示されます。 ため、すべての ODBC *3.x*ドライバーは、コア インターフェイスへの準拠レベルの機能をサポートするために必要で、次が該当します。  
  
-   ODBC *3.x*ドライバーは、標準に準拠したアプリケーションで使用されるすべての機能をサポートします。  
  
-   ODBC *3.x* ISO CLI での機能のみと、開いているグループの CLI の nonoptional 機能を使用してアプリケーションが標準に準拠したドライバーを使用します。  
  
 ISO/IEC およびオープン グループ CLI 標準に含まれている呼び出しレベルのインターフェイスの仕様、だけでなくは、ODBC は、次の機能を実装します。 (これらの機能の一部には、ODBC が ODBC より前のバージョンに存在していた*3.x*)。  
  
-   1 つの関数の呼び出しによって複数行のフェッチ  
  
-   パラメーターの配列へのバインド  
  
-   ブックマーク、可変長のブックマークを一括してフェッチなどのブックマーク サポートの更新し、連続しない行のブックマークの操作によって削除  
  
-   行方向のバインド  
  
-   オフセットのバインド  
  
-   ストアド プロシージャまたはを通じて実行された SQL ステートメントのシーケンスとしての SQL ステートメントのバッチ サポート**SQLExecute**または**SQLExecDirect**  
  
-   真数または概数値カーソル行をカウントします。  
  
-   関数呼び出しでの更新と削除の操作およびバッチ更新および削除の配置 (**SQLSetPos**)  
  
-   カタログ情報スキーマ ビューをサポートするため必要としない情報スキーマから情報を抽出する関数  
  
-   外部結合、スカラー関数、日付時刻リテラル、interval のリテラル、およびストアド プロシージャのエスケープ シーケンス  
  
-   コード ページ変換ライブラリ  
  
-   ドライバーの ansi 規格適合性レベルと SQL のサポートのレポート  
  
-   実装パラメーター記述子のオンデマンドでの自動作成  
  
-   診断の機能強化と行とパラメーターの状態配列  
  
-   Datetime、間隔、数値/10 進数、および 64 ビット整数アプリケーション バッファーの種類  
  
-   非同期実行  
  
-   ストアド プロシージャのサポート、エスケープ シーケンスなどのパラメーター バインディング機構では、出力し、カタログ関数  
  
-   接続属性および属性の参照のサポートを含む接続の機能強化
