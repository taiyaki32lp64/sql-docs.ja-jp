---
title: デスクトップ データベース ドライバー パフォーマンスの問題 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 660b7c123d0ddd0a3f1b972fa3b1dc153b15ed50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071932"
---
# <a name="desktop-database-driver-performance-issues"></a>デスクトップ データベース ドライバー パフォーマンスの問題
ANSI の既存のアプリケーションとの互換性のために、SQL_WCHAR、SQL_WVARCHAR、SQL_WLONGVARCHAR データ型は、Microsoft アクセス 4.0 または高のデータ ソースの SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR として公開されます。 データ ソースはデータ型のワイド文字を返しませんが、データもする必要があります送信 jet ワイド文字形式で。 変換が行われる SQL_C_CHAR パラメーターまたは結果列が、ANSI アプリケーションで SQL_CHAR データ型にバインドされている場合を理解しておく必要があります。  
  
 この変換型 LONGVARCHAR のパラメーターを SQL_C_CHAR 型がバインドされている場合に特に、メモリの観点から効率的なことができます。 Jet 4.0 データベース エンジンが LONGTEXT パラメーター データのストリームにできないため、UNICODE 変換のバッファーを割り当てる必要がある SQL_C_CHAR ANSI バッファーのサイズの 2 倍であります。 最も効率的なメカニズムでは、アプリケーションが UNICODE 変換を実行し、型 SQL_C_WCHAR としてパラメーターをバインドします。 パラメーターが実行時のデータとしてマークされているし、SQLPutData に複数の呼び出しで指定されているデータ、longtext データ バッファーは拡張します。 SQL_DATA_AT_EXEC_LEN(x) を使用して、省略可能な長さを指定する、この成長の費用を回避する方法の 1 つの「データの配置」バッファーが、 *x*予想されるバイトの長さです。 これに内部 PutData バッファーのサイズが初期化されます*x*バイト。  
  
> [!NOTE]  
>  使用して挿入または長い形式のデータを更新する効率的な方法を実現できます**SQLBulkOperations()** または**SQLSetPos()** SQL_DATA_AT_EXEC に長いデータを設定するとします。 (この場合 EXEC_LEN を無視) します。呼び出してデータをチャンク単位でストリーミングできます**SQLPutData**複数回、これは効果的にデータ テーブルに追加します。  
  
 バージョン 4.0 を Microsoft ODBC のデスクトップ データベース ドライバーを使用して Jet 3.5 データベースを使用してアプリケーションをアップグレードすると、パフォーマンスが低下し、作業セット サイズの増加が発生する可能性があります。 これはバージョン 3。*x*データベースを新しいバージョン 4.0 のドライバーを使用して開くことは、Jet 4.0 を読み込みます。 Jet 4.0 データベースを開くし、されることを確認するときに、データベースは、3 です。*x*バージョンについては、Jet の 3.5 エンジンもの読み込みに相当するインストール可能な ISAM ドライバーを読み込みます。 パフォーマンスとサイズの低下、Jet 3 を削除します。*x* Jet 4.0 形式のデータベースにデータベースを圧縮する必要があります。 2 つの Jet エンジンの読み込みを排除され、データへのコード パスを最小化されます。  
  
 また、Jet 4.0 データベース エンジンは、Unicode エンジンです。 すべての文字列が格納され、Unicode で操作します。 ときに、ANSI アプリケーションでは、Jet 3 にアクセスします。*x* Jet 4.0 データベース エンジン、データを使用してデータベースは、Unicode、ANSI に ANSI から変換されます。 バージョン 4.0 の形式に、データベースを更新すると場合、文字列が Unicode 文字列の変換の 1 つのレベルを削除すると 1 つだけの Jet エンジンを通過して、データへのコード パスを最小限に抑えるに変換されます。
