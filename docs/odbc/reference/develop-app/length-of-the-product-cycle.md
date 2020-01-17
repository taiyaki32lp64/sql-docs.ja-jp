---
title: 製品サイクルの長さ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 203ad92dd6abfc71b0fdeddc466752612e666cee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100454"
---
# <a name="length-of-the-product-cycle"></a>製品サイクルの長さ
相互運用性に関する最後の質問には時間です。 通常、相互運用可能なアプリケーションの開発 noninteroperable の 1 つの開発よりも時間がかかります。 理由は、アプリケーションする必要があります DBMS 機能を確認、さまざまな Dbms の異なる方法で同じタスクを実行、一部の Dbms でサポートされる機能を回避するようのです。  
  
 だけでなく、開発時間製品の有効期間と見なす必要があります。 アプリケーションの目的は、別の 1 つの DBMS から移行する場合は、データを転送するアプリケーションなど、1 回使用する場合の相互運用可能なポイントはありません。 アプリケーションは 1 回使用され、破棄されます。  
  
 長期間存在する場合、アプリケーション、容易に相互運用可能なアプリケーションとして管理する場合があります。 これは、ターゲットとして 1 つの DBMS を持つカスタム アプリケーションにも当てはまります。 理由は、相互運用可能なコードがデータベース機能の限定されたサブセットを使用することです。 基になる DBMS の変更が発生しても、使用できる機能を保持するには、ドライバーが必要です。 そのため、相互運用可能なコードはアプリケーション開発者は、ドライバー開発者から、dbms の変更に対処する負担を切り替えることができます。
