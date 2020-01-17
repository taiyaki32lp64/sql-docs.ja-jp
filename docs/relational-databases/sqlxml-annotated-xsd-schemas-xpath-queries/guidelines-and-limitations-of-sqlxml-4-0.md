---
title: SQLXML 4.0 のガイドラインと制限
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
ms.assetid: fe433d30-90a1-421e-85c6-af13294dc18d
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3ba2e7438a9084d7ad2d4f8edee9564236ecbadd
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257239"
---
# <a name="guidelines-and-limitations-of-sqlxml-40"></a>SQLXML 4.0 のガイドラインと制限
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SQLXML 4.0 を使用する場合は次の点に注意してください。  
  
-   クエリ結果として返される XML は、XML を生成したマッピング スキーマに対して検証されません。  
  
-   SQLXML 4.0 には、バージョン固有ではない PROGID とバージョン固有の PROGID が含まれています。 すべての実稼働アプリケーションでは、バージョン固有の PROGID を使用することをお勧めします。 SQLXML 4.0 には旧バージョンとの互換性は完全ではないため、これは特に重要です。 バージョン固有の PROGID を使用すると、新しいリリースをインストールして動作に問題が起こった場合にプログラムを保護できます。 リリースが変わるたび、バグ修正や設計変更などさまざまな理由によって、プログラムの動作は変更される可能性があります。 バージョン固有の PROGID を使用すると、新しいリリースをインストールして予期しないエラーが発生した場合にプログラムを保護できます。 バージョン固有の PROGID を使用すれば、新しいバージョンのリリースをインストールしても、アプリケーションは問題なく正常に動作します。 それまで使っていたバージョン固有の PROGID を変更し、新しいリリースで最新のものを使用する場合は、実稼働する前にアプリケーションをテストする必要があります。 たとえば、バージョン固有の PROGID を使用するアプリケーションでは、特定の状況下でエラーが発生する可能性があります。  
  
     つまり、SQLXML 4.0 とバージョン固有の PROGID を使用するアプリケーションを実行している状態で、他のソフトウェア プログラムをインストールすると、 このプログラムによって以前のバージョンの SQLXML がインストールされる可能性があり、 この場合、アプリケーションのバージョン固有の PROGID では以前のバージョンの SQLXML が参照されるため、アプリケーションで使用する SQLXML 機能が含まれていないと、エラーが発生します。  
  
-   何らかの理由で SQLXMLOLEDB プロバイダーを使用せず、代わりに SQLOLEDB プロバイダーを SQLXML 機能に使用する場合は、 **Sqlxml Version**プロパティを "sqlxml. 4.0" に設定します。  
  
  
