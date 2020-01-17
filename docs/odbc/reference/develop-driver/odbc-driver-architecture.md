---
title: ODBC ドライバーのアーキテクチャ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], architecture
ms.assetid: 21a62c7c-192e-4718-a16e-aa12b0de4419
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5d123bdf1ea3357a4846a223c41950c952c1af2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915535"
---
# <a name="odbc-driver-architecture"></a>ODBC ドライバーのアーキテクチャ
ドライバー開発者は、ドライバーのアーキテクチャは、アプリケーションは DBMS 固有の SQL を使用できるかどうかに影響は対応である必要があります。  
  
 ![ODBC ドライバーのアーキテクチャ](../../../odbc/reference/develop-driver/media/odbcdriverovruarch.gif "ODBCDriverOvruArch")  
  
 [ファイル ベースのドライバー](../../../odbc/reference/file-based-drivers.md)  
  
 ドライバーは、物理的なデータを直接アクセスする場合、ドライバーがドライバーとデータの両方のソースとして機能します。 ドライバーは ODBC 呼び出しと SQL ステートメントの両方を処理する必要があります。 ファイル ベースのドライバーの開発者は、独自のデータベース エンジンを記述する必要があります。  
  
 [DBMS ベースのドライバー](../../../odbc/reference/dbms-based-drivers.md)  
  
 別のデータベース エンジンを使用すると、物理データにアクセスすると、ドライバーは ODBC の呼び出しのみを処理します。 SQL ステートメントに渡すには、データベース エンジンを処理します。  
  
 [ネットワーク アーキテクチャ](../../../odbc/reference/network-example.md)  
  
 ファイルと DBMS の ODBC の構成は、1 つのネットワークに存在できます。  
  
 [その他のドライバーのアーキテクチャ](../../../odbc/reference/other-driver-architectures.md)  
  
 さまざまなデータ ソースを使用するドライバーが必要な場合は、ミドルウェアとして使用できます。 異種結合エンジンのアーキテクチャでは、ドライバーをドライバー マネージャーとして表示を作成できます。 ドライバーは、一連のクライアントで共有できる、サーバーにもインストールできます。  
  
 ドライバーのアーキテクチャの詳細については、次を参照してください。[ドライバー マネージャー](../../../odbc/reference/the-driver-manager.md)と[ドライバーのアーキテクチャ](../../../odbc/reference/driver-architecture.md)に関するセクションで[ODBC アーキテクチャ](../../../odbc/reference/odbc-architecture.md)します。  
  
 ドライバーの問題の詳細については、次の表で説明されている場所で見つかります。  
  
|問題点|トピック|場所|  
|-----------|-----------|--------------|  
|アプリケーションおよびドライバーと互換性の問題|[アプリケーション/ドライバーの互換性](../../../odbc/reference/develop-app/application-and-driver-compatibility.md)|[プログラミングに関する考慮事項](../../../odbc/reference/develop-app/programming-considerations.md)、ODBC プログラマ リファレンス|  
|ODBC ドライバーの記述|[ODBC 3.x ドライバーの作成](../../../odbc/reference/develop-app/writing-odbc-3-x-drivers.md)|[プログラミングに関する考慮事項](../../../odbc/reference/develop-app/programming-considerations.md)、ODBC プログラマ リファレンス|  
|旧バージョンとの互換性のためのドライバーのガイドライン|[旧バージョンとの互換性のためのドライバーのガイドライン](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)|[付録 g:旧バージョンとの互換性のためのドライバーのガイドライン](../../../odbc/reference/appendixes/appendix-g-driver-guidelines-for-backward-compatibility.md)、ODBC プログラマ リファレンス|  
|ドライバーへの接続|[データ ソースまたはドライバーの選択](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)|[データ ソースまたはドライバー](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)、ODBC プログラマ リファレンス|  
|ドライバーを識別します。|[ドライバーの表示](../../../odbc/admin/viewing-drivers.md)|[ドライバーの表示](../../../odbc/admin/viewing-drivers.md)、Microsoft ODBC データ ソース アドミニストレーターのオンライン ヘルプ|  
|接続プールを有効にします。|[ODBC 接続プール](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)|[データ ソースまたはドライバー](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)、ODBC プログラマ リファレンス|  
|UNICODE/ANSI のドライバーと接続の問題|[Unicode ドライバー](../../../odbc/reference/develop-app/unicode-drivers.md)|[プログラミングに関する考慮事項](../../../odbc/reference/develop-app/programming-considerations.md)、ODBC プログラマ リファレンス|  
  
## <a name="see-also"></a>参照  
 [ODBC ドライバーの開発](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)
