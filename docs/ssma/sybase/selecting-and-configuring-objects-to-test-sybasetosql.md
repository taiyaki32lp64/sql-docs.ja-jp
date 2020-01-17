---
title: 選択し、テスト (SybaseToSQL) にオブジェクトの構成 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Parameter Comparision Setting
- Tester Component,Selecting Objects
ms.assetid: 89c23aad-bfee-4917-bc16-175288390ac0
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 2951d4c3bf1eae73ffd066d796b0e3dda4d28cf6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020961"
---
# <a name="selecting-and-configuring-objects-to-test-sybasetosql"></a>テストするオブジェクトの選択と構成 (SybaseToSQL)
この手順では、テスト、およびプロシージャの関数の出力パラメーターと関数の戻り値を比較するための設定を構成するオブジェクトを選択します。  
  
## <a name="selection-of-objects-to-test"></a>テストするオブジェクトの選択  
ウィンドウの左側にある Sybase オブジェクト ツリーで、テスト プロセス中に起動するオブジェクトを確認します。 テスト可能なオブジェクトの完全な一覧を参照してください、[移行対象のデータベース オブジェクトのテスト&#40;SybaseToSQL&#41; ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)トピック。  
  
SSMA のテスト担当者が、いずれかのテスト用に選択されたオブジェクトもサポートしていない場合は、というラベルの付いたリンクが表示されます**いくつかの選択したオブジェクトがエラーを含む**オブジェクト ツリーの下。 なぜこれらのオブジェクトをテストできない理由を表示して、不適切なオブジェクトの選択を解除する、このリンクをクリックします。  
  
右側にある、いくつかのページを表示することができます、 **SQL**ページには、現在のオブジェクトの定義が表示されます。 **前 SQL**と**Post SQL**ページは、テスト オブジェクトを開始の呼び出しの前後に実行されるスクリプトを指定できます。 オブジェクトは、このような一時テーブルまたはカーソルに他のオブジェクトを必要とする場合、これが便利な可能性があります。 **パラメーター**ページは、オブジェクトがストアド プロシージャまたは関数の場合、パラメーターを一覧表示されます。 **プロパティ**ページには、オブジェクトの他の特性が表示されます。 説明を参照して**パラメーター Comparsions**と**呼び出す値**以下のページ。  
  
## <a name="parameter-comparison-settings"></a>パラメーターの比較の設定  
出力パラメーターに対して比較の規則の確立し、内の値を返す、**パラメーターを比較する**ページ。 次の設定を行うことができます。  
  
### <a name="use-during-comparisons"></a>比較の際に使用  
テスト結果の比較で選択されたパラメーターを使用して有効にします。  
  
-   選択した場合**True**SSMA に対応する値を持つ Sybase でプロシージャの実行後にこのパラメーターの出力値を比較 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   選択した場合**False**パラメーター、結果の検証から除外されます。  
  
### <a name="use-custom-scale"></a>カスタムのスケールを使用します。  
概数と固定長の数値データ型のパラメーターは、比較のためのカスタム スケールを設定できます。  
  
-   選択した場合**True**、に従って数値は丸められます、**を比較するスケール**値の前に、比較されます。  
  
-   選択した場合**False**、数値比較を正確になります。  
  
### <a name="comparing-scale"></a>スケールを比較します。  
使用可能な場合にのみ、**使用のカスタム スケール**にオプションが設定されている**True**します。 これは、数値比較の有効桁数です。  
  
### <a name="date-time-comparing"></a>日付時刻を比較します。  
定義する方法、日付/時刻値が比較されます。  
  
-   選択した場合**全体の日付の比較**、両方のプラットフォームからの値の完全な比較を実行します。  
  
-   選択した場合**日付のみを比較**、時刻部分は無視されます。  
  
-   選択した場合**時刻のみを比較**日付の部分は無視されます。  
  
-   選択した場合**無視ミリ秒**結果は秒単位までと比較されます。  
  
-   選択した場合**を無視する日付とミリ秒**秒の時間部分でのみ比較し、無視の小数部になります。  
  
### <a name="ignore-strings-case"></a>文字列の大文字小文字を区別します。  
比較の大文字小文字の区別を制御します。  
  
-   選択した場合**True**、大文字と小文字を区別しない比較になります。  
  
-   選択した場合**False**比較は大文字小文字が区別されます。  
  
### <a name="ignore-trailing-spaces"></a>[末尾のスペースを無視する]  
どの末尾のスペースを制御します。 比較時に扱われます。  
  
-   選択した場合**True**、比較対象の文字列になります右トリム比較する前にします。  
  
-   選択した場合**False**、比較対象の文字列の末尾の空白は保持します。  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>プロシージャおよび関数 (呼び出しの値) の入力値を指定します。  
入力パラメーターの値を指定できます、**呼び出す値**ページ。 **の呼び出しの追加**ボタンが空のパラメーター値を持つ新しい呼び出しを追加します。 **呼び出す削除**ボタンは、現在の呼び出しを削除します。  
  
## <a name="next-step"></a>次の手順  
[影響を受けるオブジェクトの選択と構成&#40;SybaseToSQL&#41;](../../ssma/sybase/selecting-and-configuring-affected-objects-sybasetosql.md)  
  
## <a name="see-also"></a>関連項目  
[移行されたデータベース オブジェクトのテスト&#40;SybaseToSQL&#41;](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
