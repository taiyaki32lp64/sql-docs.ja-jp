---
title: ODBC とは | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bda4abf9802bd58e81f35bd4223b28f687e89b4f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67951794"
---
# <a name="what-is-odbc"></a>ODBC とは
ODBC に関する多くの誤解は、コンピューティングの世界に存在します。 エンドユーザーでは、Microsoft® Windows® コントロール パネルのアイコンがあります。 アプリケーションのプログラマには、データ アクセス ルーチンを含むライブラリを勧めします。 他の多くを想像ではこれまですべてのデータベース アクセスの問題に対する回答になります。  
  
 何よりもまず、ODBC、データベース API の仕様です。 この API は、任意の 1 つの DBMS またはオペレーティング システムに依存しません。このマニュアルは、C を使用して、ODBC API は言語に依存しません。 ODBC API は、Open Group および ISO/IEC から CLI 仕様に基づいています。 ODBC 3。*x*完全 - 以前のバージョンの ODBC は、これらの仕様の予備バージョンに基づいていますが完全に実装していない - これらの仕様の両方を実装し、よくスクリーン ベースの開発者に必要な機能を追加します。スクロール可能なカーソルなどのデータベース アプリケーション。  
  
 ODBC API の関数は、DBMS 固有のドライバーの開発者によって実装されます。 アプリケーションでは、DBMS に依存しない方法でデータにアクセスするには、これらドライバーの関数を呼び出します。 ドライバー マネージャーは、アプリケーションとドライバーの間の通信を管理します。  
  
 Microsoft では、Microsoft Windows® 95 を実行しているコンピューターのドライバー マネージャーを提供し、後が記述されたいくつかの ODBC ドライバー、および ODBC 関数の呼び出しから一部のアプリケーションでそのは、ODBC アプリケーションやドライバーだれでも記述できます。 実際には、今日、大半の ODBC アプリケーションおよび利用可能なドライバは Microsoft 以外の会社で記述されます。 さらに、ODBC ドライバーとアプリケーション、Macintosh® とさまざまな UNIX プラットフォーム上に存在します。  
  
 ODBC ソフトウェア開発キット (SDK) Windows 95 が実行しているコンピューターを提供している Microsoft アプリケーションとドライバー開発者のため、され、後でドライバー マネージャー、インストーラー DLL、テスト ツール、およびサンプル アプリケーションを提供します。 Microsoft はこれらの Sdk には、Macintosh、UNIX プラットフォームのさまざまなポートへのソフトウェアの Visigenic と提携しています。  
  
 データベース機能を公開するにはないを追加し、ODBC が設計されているかを理解しておく必要があります。 したがって、アプリケーションの作成者では、こと ODBC を使用しては突然単純なデータベースを変換、全機能を備えたリレーショナル データベース エンジンは限りません。 またドライバー開発者は、基になるデータベースではない機能を実装するが必要です。 この例外は、Xbase ファイル内のデータ) などのファイル データに直接アクセスするドライバーを作成する開発者が SQL の最低限の機能をサポートするデータベース エンジンを記述するために必要なことです。 別の例外は、以前に、Microsoft Data Access Components (MDAC) SDK に含まれる、Windows SDK の ODBC コンポーネントは、特定のレベルの機能を実装するドライバーのスクロール可能なカーソルをシミュレートする、カーソル ライブラリが提供です。  
  
 ODBC を使用するアプリケーションでは、任意のデータベースにまたがる機能を担当します。 たとえば、ODBC、異種結合エンジンではありませんも分散トランザクション プロセッサ。 ただし、DBMS に依存しないであるために、このようなデータベースにまたがるツールを構築する使用できます。
