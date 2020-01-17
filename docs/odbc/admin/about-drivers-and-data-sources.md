---
title: ドライバーとデータ ソースについて |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC data source administrator [ODBC], concepts
ms.assetid: 2bb83ef1-4bbe-4be3-8c32-c4d1140aae1d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4e9b7229882b3b7f94e6b059e04c6496bde09641
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938042"
---
# <a name="about-drivers-and-data-sources"></a>ドライバーとデータ ソースについて
*ドライバー*は ODBC の要求を処理し、アプリケーションにデータを返すコンポーネントです。 必要に応じて、ドライバーは、データ ソースで認識できる形式にアプリケーションの要求を変更します。 ドライバーのセットアップ プログラムを使用して、追加またはドライバーをコンピューターから削除する必要があります。  
  
 *データ ソース*データベースと、ドライバーによってアクセスされたファイル、およびデータ ソース名 (DSN) によって識別されます。 ODBC データ ソース アドミニストレーターを使用して、追加、構成、およびシステムからデータ ソースを削除します。 次の表は、使用できるデータ ソースの種類を説明します。  
  
|データ ソース|説明|  
|-----------------|-----------------|  
|ユーザー|ユーザー Dsn はコンピューターにローカルであり、現在のユーザーによってのみ使用できます。 これらは、HKEY_CURRENT_USER レジストリ サブツリーに登録されます。|  
|System|システム Dsn は、専用のユーザーではなく、コンピューターに対してローカルです。 システムまたは特権を持つ任意のユーザーは、データ ソースがシステム DSN を使用して設定を使用できます。 システム Dsn は、レジストリの HKEY_LOCAL_MACHINE サブツリーに登録されます。|  
|File|ファイル Dsn は、同じドライバーがインストールされているすべてのユーザー間で共有することができますし、そのため、データベースへのアクセスを持つファイル ベースのソースです。 これらのデータ ソースは、ユーザーには専用ない必要がありますも、コンピューターにローカルでいます。 ファイル データ ソース名は専用のレジストリ エントリを識別しません。代わりに、拡張子が .dsn ファイル名によって識別されます。|  
  
 ユーザーおよびシステムのデータ ソースと総称されます*マシン*データ ソースのコンピューターに対してローカルにいるためです。  
  
 タブが、これらのデータ ソースの各、 **ODBC データ ソース アドミニストレーター**  ダイアログ ボックス。 使用できるデータ ソースの詳細については、「 [データ ソース](../../odbc/reference/data-sources.md)」を参照してください。
