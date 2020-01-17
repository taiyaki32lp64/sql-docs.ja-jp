---
title: メタデータの使用方法 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], metadata
- metadata [ODBC]
ms.assetid: 70fb976c-9342-4edd-b066-1140696fd0fa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ab2efd47ca5b5492c67b88261795cf524c440bda
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139010"
---
# <a name="how-is-metadata-used"></a>メタデータの使用方法
アプリケーションは、ほとんどの結果セット操作にメタデータを必要とします。 たとえば、列のデータ型を使用して、列にバインドされている変数の種類を判断します。 その列のデータを表示するのに必要がある領域の量を決定するのに、文字型列のバイト長を使用します。 アプリケーションが列のメタデータを判断する方法は、アプリケーションの種類によって異なります。  
  
 垂直アプリケーションでは、定義済みのテーブルを操作して、それらのテーブルで定義済みの操作を実行します。 アプリケーションが作成され、アプリケーション開発者が制御する前に、このようなアプリケーションの結果セットのメタデータが定義されている、ため、アプリケーションにハードコーディングできます。 たとえば、データ ソース内で受注 ID 列が 4 バイト integer 型で定義されている場合、アプリケーションは常に 4 バイト integer をこの列にバインドできます。 メタデータがアプリケーション内でハードコーディングされている場合、アプリケーションが使用するテーブルへの変更は、通常、アプリケーション コードに対する変更になります。 これは、このような変更は通常、アプリケーションの新しいリリースの一部として行われるため、問題ではことはほとんどありません。  
  
 垂直方向のアプリケーションと同様にカスタム アプリケーションは一般に定義済みのテーブルを使用し、それらのテーブルで定義済みの操作を実行します。 たとえば、アプリケーションを; 次の 3 つの異なるデータ ソース間でデータを転送する記述可能性があります。通常は転送されるデータは、アプリケーションに書き込まれると呼ばれます。 そのため、カスタム アプリケーションでは、ハード コーディングされたメタデータが存在する傾向がもします。  
  
 汎用アプリケーション、特にアドホック クエリのサポート、ほとんどない結果セットの作成のメタデータを認識します。 関数を使用して、実行時にメタデータを検出する必要がありますので、 **SQLNumResultCols**、 **SQLDescribeCol**、および**SQLColAttribute**で説明される、次のセクションでは、 [SQLDescribeCol および SQLColAttribute](../../../odbc/reference/develop-app/sqldescribecol-and-sqlcolattribute.md)します。  
  
 自分の種類に関係なく、すべてのアプリケーションには、カタログ関数によって返される結果セットのメタデータをハード コーディングことができます。 これらの結果セットは、このマニュアルのリファレンス セクションで定義されます。
