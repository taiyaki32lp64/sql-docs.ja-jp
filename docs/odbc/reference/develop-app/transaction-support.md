---
title: トランザクションのサポート |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0b5e33f94c5452a2062f7c18339f27c8da73fa9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086064"
---
# <a name="transaction-support"></a>トランザクションのサポート
トランザクションのサポートの程度は、ドライバーの定義です。 ODBC は、そのデータを複数の更新プログラムを管理する必要がない、またはデスクトップでのシングル ユーザー データベースの実装に設計されています。 さらに、トランザクションをサポートする一部のデータベースのみに行うため SQL; のデータ操作言語 (DML) ステートメントトランザクションがアクティブな場合に、制限、またはデータ定義言語 (DDL) の使用に関する特別なトランザクション セマンティクスはあります。 つまり、テーブルに複数の同時更新プログラムの数と、トランザクション中にテーブルの定義の変更ではなく、トランザクションのサポートがあります。  
  
 アプリケーションが DDL トランザクション、およびトランザクションでは、DDL を呼び出すことによってなどの特別な効果に含まれるかどうか、トランザクションはサポートされているかどうかを決定**SQLGetInfo** SQL_TXN_CAPABLE オプションを使用します。 詳細については、次を参照してください。、 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)関数の説明。  
  
 ドライバーがトランザクションをサポートしていませんが、ロック、およびデータのロックを解除する (ODBC 以外の API を使用) 機能を備えて場合、アプリケーションは、ロックおよびロック解除のレコードと、必要に応じてテーブルでトランザクションのサポートを実現できます。 アカウント転送の例を実装するには、アプリケーションは両方のアカウントのレコードをロック、現在の値をコピー、借方最初のアカウント、2 つ目のアカウントのクレジットおよびレコードのロックを解除します。 すべての手順が失敗した場合、アプリケーションは、コピーを使用するアカウントにリセットされます。  
  
 トランザクションをサポートするものデータ ソースはできない、特定の環境内で一度に 1 つ以上のトランザクションをサポートすることがあります。 アプリケーション呼び出し**SQLGetInfo**データ ソースが同じ環境では、複数の接続で同時にアクティブなトランザクションをサポートできるかどうかを判断する SQL_MULTIPLE_ACTIVE_TXN オプションを使用します。 接続ごとに 1 つのトランザクションがあるため、これは、同じデータ ソースに複数の接続を持つアプリケーションに興味深いのみです。
