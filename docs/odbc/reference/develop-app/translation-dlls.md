---
title: 翻訳の Dll |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 168b7b5ef6f8b88a39dbbb0942cf1520adf261e6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086033"
---
# <a name="translation-dlls"></a>トランザクション DLL
アプリケーションとデータ ソース多くの場合、異なる文字セットでデータを格納します。 ODBC では、1 つの文字セットを他のデータを変換するドライバーをできるようにする汎用メカニズムを提供します。 変換関数を実装する DLL から成る**SQLDriverToDataSource**と**SQLDataSourceToDriver**、すべてのデータ フロー、データ ソース間の変換に、ドライバーによって呼び出されドライバー。 この DLL は、アプリケーション開発者は、ドライバーの開発者を書き込んだまたはサード パーティの。  
  
 特定のデータ ソースの翻訳の DLL は、そのデータ ソースのシステム情報で指定できます。詳細については、次を参照してください。[データ ソースの仕様のサブキー](../../../odbc/reference/install/data-source-specification-subkeys.md)します。 SQL_ATTR_TRANSLATE_DLL と SQL_ATTR_TRANSLATE_OPTION 接続属性を持つ実行時に設定することもできます。  
  
 翻訳オプションは、特定の翻訳の DLL によってのみ解釈可能な値です。 たとえば、異なるコード ページ間 DLL の変換を平行移動、オプションは、アプリケーションとデータ ソースで使用されるコード ページの数を与える可能性があります。 翻訳オプションを使用する翻訳の DLL の要件はありません。  
  
 DLL が指定されている、変換した後、ドライバーは読み込み、、アプリケーションとデータ ソース間を流れるすべてのデータを変換する関数を呼び出します。 これには、すべての SQL ステートメントと、データ ソースに送信される文字パラメーターが含まれ、データ ソースからすべての文字の結果、列名、およびエラー メッセージなどの文字のメタデータを取得します。 アプリケーションがデータ ソースに接続した後に、翻訳の DLL は、まで読み込まれていないため、接続データは翻訳されません。
