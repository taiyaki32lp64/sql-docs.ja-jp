---
title: 列のデータ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f4bc57a5a0b500dc8828d5b0e35c2d6023165ac5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019251"
---
# <a name="column-data"></a>列のデータ
> [!IMPORTANT]  
>  この機能は、Windows の将来のバージョンで削除されます。 新しい開発作業でこの機能を使用しないようにして、現在この機能を使用しているアプリケーションの変更を検討してください。 ドライバーのカーソル機能を使用することをお勧めします。  
  
 カーソル ライブラリのキャッシュを使用して結果セットにバインドされている各データ バッファーでバッファーを作成する**SQLBindCol**します。 これらのバッファーで値を使用して構築を**場所**位置指定をエミュレートするものと句の update または delete ステートメント。 位置指定の update ステートメントを実行すると、データ ソースからデータをフェッチするときは、これらのバッファー行セットのバッファーからを更新します。  
  
 指定された C データ型に従ったデータを転送するとき、カーソル ライブラリでは、行セットのバッファーからそのキャッシュを更新、 **SQLBindCol**します。 たとえば、SQL_C_SLONG を行セットのバッファーの C データ型には、カーソル ライブラリは データの 4 バイトを転送します。SQL_C_CHAR である場合と*BufferLength*が 10、カーソル ライブラリは、10 バイトのデータを転送します。 カーソル ライブラリを転送するデータの型チェックや変換を実行しません。  
  
> [!NOTE]  
>  カーソル ライブラリが列のキャッシュを更新していない場合は **StrLen_or_IndPtr* SQL_DATA_AT_EXEC または SQL_LEN_DATA_AT_EXEC マクロの結果、対応する行セットのバッファーでは。  
  
 ときに、列、データ ソースの空白を埋め込みます固定長文字データおよび必要に応じて、ゼロを埋め込みます固定長のバイナリ データを更新します。 など、データ ソースは、"Smith"として char (10) の列に"Smith"を格納します。 カーソル ライブラリは、位置指定の update ステートメントの実行後のキャッシュにこのデータをコピーするときに、行セットのバッファー内の空白パッドまたはゼロで埋め込んでしないデータをしません。 そのため、アプリケーションでは、カーソル ライブラリのキャッシュに値は、空白が埋め込まれてまたはゼロが埋め込まれている必要がある場合する必要があります空白パッドまたはゼロで埋め込んで行セットのバッファー内の値、位置指定の update ステートメントを実行する前にします。
