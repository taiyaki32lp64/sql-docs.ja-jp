---
title: カタログ データの使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc8999c0a7189772145f553646b45eb1f1fbd695
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091609"
---
# <a name="uses-of-catalog-data"></a>カタログ データの使用
アプリケーションでは、さまざまな方法で、カタログ データを使用します。 一般的な使用方法を次に示します。  
  
-   **SQL ステートメントの実行時に作成します。** 、受注アプリケーションなどの垂直方向のアプリケーションには、ハード コーディングされた SQL ステートメントが含まれます。 テーブルと、アプリケーションで使用される列は、これらのテーブルにアクセスするステートメントが事前に、修正されます。 受注アプリケーションが、通常、1 つを含む、パラメーター化された**挿入**ステートメント、システムに新しい注文を追加します。  
  
     ODBC を使用して、データを取得するスプレッドシート プログラムなどの汎用アプリケーションは、多くの場合、ユーザーからの入力に基づいて実行時に SQL ステートメントを作成します。 このようなアプリケーションでは、テーブルおよび使用する列の名前を入力するユーザーを必要があります。 ただし、できれば、ユーザーを簡単にアプリケーションには、テーブルとユーザーが選択を行うことが列のリストが表示されます。 これらのリストをビルドするアプリケーションを呼び出すと、 **SQLTables**と**SQLColumns**カタログ関数。  
  
-   **開発時に SQL ステートメントを構築します。** アプリケーションの開発環境は、通常、プログラマは、プログラムの開発中に、データベース クエリの作成を許可します。 クエリは、作成するアプリケーションにハードコーディングしは。  
  
     また、このような環境を使用**SQLTables**と**SQLColumns**プログラマが選択を行うでしたリストを作成します。 これらの環境を使うことも**SQLPrimaryKeys**と**SQLForeignKeys**自動的に決定して、選択したテーブル間のリレーションシップを表示、使用**SQLStatistics**を特定し、プログラマは、効率的なクエリを作成できるように、インデックス付きフィールドを強調表示します。  
  
-   **カーソルを作成します。** アプリケーション、ドライバー、またはスクロール可能なカーソル エンジンを提供するミドルウェアを使用して、でした**SQLSpecialColumns**行を一意に識別する列または列を確認します。 プログラムを作成できます、*キーセット*がフェッチされた行ごとにこれらの列の値を格納します。 アプリケーションは、行にスクロールするときを使用してこれらの値の行の最新のデータをフェッチします。 スクロール可能なカーソルとキーセットの詳細については、次を参照してください。[スクロール可能なカーソル](../../../odbc/reference/develop-app/scrollable-cursors.md)します。
