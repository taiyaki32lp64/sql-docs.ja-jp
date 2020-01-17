---
title: 追加および変更データ ソースのセットアップを使用して |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], adding
- editing data sources [ODBC], ODBC driver for Oracle
- adding data sources [ODBC], ODBC driver for Oracle
- data sources [ODBC], changing
- data sources [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], adding data sources
ms.assetid: 54b2d61d-6ce5-45af-a776-e03180470ecf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 621d10c3c602b2f406461a24e53b2302e45835eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901401"
---
# <a name="adding-and-modifying-data-sources-using-setup"></a>セットアップを使用してデータ ソースを追加および変更する
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用します。  
  
 データ ソースは、ネットワーク ライブラリをサーバー、データベース、およびその他の属性を含めることがデータへのパスを識別します。-この場合、データ ソースは、Oracle データベースへのパス。 データ ソースに接続するには、ドライバー マネージャーは、Windows レジストリで特定の接続情報を確認します。  
  
 ODBC データ ソース アドミニストレーターによって作成されたレジストリ エントリは、ODBC ドライバー マネージャーと ODBC ドライバーによって使用されます。 このエントリには、各データ ソースとその関連するドライバーに関する情報が含まれています。 データ ソースに接続することができます、前に、その接続情報はレジストリに追加する必要があります。  
  
 追加し、データ ソースの構成を使用して、 [ODBC データ ソース アドミニストレーター](../../odbc/admin/odbc-data-source-administrator.md)します。 Odbc データ ソース アドミニストレーターは、データ ソースの接続情報を更新します。 データ ソースを追加すると、odbc データ ソース アドミニストレーターは、レジストリ情報を更新します。  
  
### <a name="to-add-a-data-source-for-windows"></a>Windows のデータ ソースを追加するには  
  
1.  ODBC データ ソース アドミニストレーターを開きます。  
  
2.  ODBC データ ソース アドミニストレーター ダイアログ ボックスで、追加 をクリックします。 新しいデータ ソースの作成ダイアログ ボックスが表示されます。  
  
3.  Oracle 用 Microsoft ODBC を選択し、[完了] をクリックします。 Microsoft ODBC の Oracle のセットアップ ダイアログ ボックスが表示されます。  
  
4.  データ ソース名 ボックスにアクセスするデータ ソースの名前を入力します。 選択した任意の名前になります。  
  
5.  [説明] ボックスには、ドライバーの説明を入力します。 この省略可能なフィールドには、データ ソースに接続するデータベース ドライバーがについて説明します。 選択した任意の名前になります。  
  
6.  ユーザー名 ボックスで、データベース ユーザー名 (データベース ユーザー ID) を入力します。  
  
7.  サーバー ボックスに、データベースの別名を入力するか、接続文字列にアクセスする、Oracle Server エンジン。  
  
8.  このデータ ソースを追加するには、[ok] をクリックします。  
  
> [!NOTE]  
>  [データ ソース] ダイアログ ボックスが表示されたら、odbc データ ソース アドミニストレーターは、レジストリ情報を更新します。 ユーザー名し、接続文字列を入力したに接続するときにこのデータ ソースの既定の接続値となります。  
  
1.  ODBC Driver for Oracle のセットアップに関する多くの仕様作成のオプションをクリックします。  
  
    -   **翻訳**-[読み込まれたデータの翻訳者を選択する] をクリックします。 既定値は\<いいえ Translator >。  
  
    -   **パフォーマンス**のカタログ関数のチェック ボックスが含まれての解説では、ドライバーでの「解説」列を返すかどうかを指定します、 [SQLColumns](../../odbc/microsoft/level-1-api-functions-odbc-driver-for-oracle.md)結果セット。 ODBC Driver for Oracle は、この値が設定されていないときに、高速アクセスを提供します。  
  
         SQL の列のチェック ボックスで、シノニムは、ドライバーが列の情報を返すかどうかを指定します。 **バッファー サイズ**(バイト)、フェッチされたデータを受信する割り当てサイズを指定します。 ドライバーは、Oracle サーバーから 1 つのフェッチが指定されたサイズのバッファーに格納のための十分な行を返されるようにフェッチを最適化します。 大きな値は、大量のデータをフェッチするときにパフォーマンスを向上する傾向があります。  
  
    -   **カスタマイズ**-適用 ODBC DayOfWeek 標準のチェック ボックスは、結果セットは (日曜日が 1 になります ODBC 指定曜日単位形式に準拠しているかどうかを指定します。土曜日に = 7)。 このチェック ボックスがオフの場合は、Oracle のロケール固有の値が返されます。  
  
         SQLDescribeCol**常に有効桁数の値を返します** チェック ボックスは、ドライバーがの 0 以外の値を返すかどうかを指定します、 *cbColDef*の引数**SQLDescribeCol**. この接続文字列の属性は、場所がない Oracle 定義のスケールでは、計算など、数値列に対してのみ適用列と列のない、有効桁数または小数点数として定義します。 A **SQLDescribeCol** Oracle にその情報が提供されない場合に、有効桁数の返します 130 を呼び出します。 このチェック ボックスをオフにした場合、ドライバーはこれらの型の列 0 を代わりに返します。  
  
2.  別のデータ ソースを追加する追加 をクリックしてまたは終了して閉じる をクリックします。  
  
### <a name="to-modify-a-data-source-for-windows"></a>Windows のデータ ソースを変更するには  
  
1.  ODBC データ ソース アドミニストレーターを開きます。 適切な DSN タブをクリックします。  
  
2.  変更し、構成 をクリックする、Oracle データ ソースを選択します。 Microsoft ODBC の Oracle のセットアップ ダイアログ ボックスが表示されます。  
  
3.  該当するデータ ソース フィールドを変更し、[ok] をクリックします。  
  
 このダイアログ ボックスで情報の変更が完了したら、odbc データ ソース アドミニストレーターは、レジストリ情報を更新します。
