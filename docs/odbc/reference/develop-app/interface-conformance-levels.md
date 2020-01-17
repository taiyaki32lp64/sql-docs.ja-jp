---
title: インターフェイスの適合性レベル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 185e68ed8d083e3ccfbab99369f6a778766a4c09
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138909"
---
# <a name="interface-conformance-levels"></a>インターフェイスの適合性レベル
平準化の目的は、どのような機能を利用して、ドライバーからアプリケーションに通知するためにです。 関数に基づく平準化パターンがこの目標を十分に達成することはできません。 ODBC 3。*x*ドライバーを所有している特徴に基づいて分類されます。 はこの関数をサポートしている含めることができます、機能をサポートによって返される情報の種類の記述子フィールド、ステートメント属性を"Y"値のサポートを含めることができますも**SQLGetInfo**など。  
  
 インターフェイスの適合性の仕様を簡略化するのには、ODBC は、次の 3 つの適合性レベルを定義します。 特定の準拠レベルを満たすためには、ドライバーはすべての適合性レベルの要件を満たす必要があります。 特定のレベルへの準拠は、すべての下位レベルの完全な準拠を意味します。  
  
 適合性レベルは、常に除算を行わないでください一直線に並べる、ODBC 関数の特定のリストのサポートが、次のセクションに記載されている、サポートされている機能を指定します。 機能のサポートを提供するドライバーが特定の ODBC 関数の呼び出しの一部またはすべてのフォームをサポートする必要があります (詳細については、次を参照してください[関数の適合性](../../../odbc/reference/develop-app/function-conformance.md))、特定の属性を設定 (を参照してください[属性の適合性。](../../../odbc/reference/develop-app/attribute-conformance.md))、および特定の記述子フィールド (を参照してください[記述子フィールドの適合性](../../../odbc/reference/develop-app/descriptor-field-conformance.md))。  
  
 アプリケーションでは、ドライバーのインターフェイスへの準拠レベルを検出データ ソースに接続し、呼び出すことによって**SQLGetInfo** SQL_ODBC_INTERFACE_CONFORMANCE オプションを使用します。  
  
 ドライバーでは、完全な準拠本人レベル以上の機能を実装するために無料です。 アプリケーションが呼び出すことによって、このような追加機能を検出**SQLGetFunctions** (どの ODBC 関数が存在するかを決定) して**SQLGetInfo** (さまざまな他の ODBC の機能のクエリを実行) します。  
  
 ODBC インターフェイスへの準拠レベルは 3 つです。Core、レベル 1 および Level 2。  
  
> [!NOTE]
>  これらの適合性レベル ODBC 2 で同じ名前の ODBC API への準拠レベルよりも異なる要件があります *.x*します。 具体的には、ODBC 2 によって暗黙的にすべての機能 *.x* API への準拠レベル 1 は、コア インターフェイスへの準拠レベルの一部であるようになりました。 その結果、多くの ODBC ドライバーは、コア レベル インターフェイスの適合性を報告する可能性があります。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [コア インターフェイスの適合性](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [レベル 1 インターフェイスの適合性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [レベル 2 インターフェイスの適合性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [関数の適合性](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [属性の適合性](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [記述子フィールドの適合性](../../../odbc/reference/develop-app/descriptor-field-conformance.md)
