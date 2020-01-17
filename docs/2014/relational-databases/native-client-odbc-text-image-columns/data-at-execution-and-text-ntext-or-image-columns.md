---
title: 実行時のデータと Text、ntext、または Image 列 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7e7c57cf6444e5833b6deee0dcae36d71b7a6430
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63195129"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>実行時データと text 型、ntext 型、または image 型の列
  ODBC 実行時データは、バインドされた列やパラメーターに対して、アプリケーションが大量のデータを操作できるようにする機能です。 非常に大きなを取得するときに**テキスト**、 **ntext**、または**イメージ**列アプリケーションできないことがありますを単純に巨大なバッファーを割り当てる、バッファーに列をバインドおよびフェッチ行。 非常に大きな更新するときに**テキスト**、 **ntext**、または**イメージ**列アプリケーションできない単純に巨大なバッファーを割り当てる、SQL ではパラメーター マーカーにバインドするにはステートメントでは、し、ステートメントを実行します。 このような場合は、アプリケーションを使用する必要があります[SQLGetData](../native-client-odbc-api/sqlgetdata.md)または[SQLPutData](../native-client-odbc-api/sqlputdata.md)その実行時データ オプションを使用します。  
  
## <a name="see-also"></a>参照  
 [text 列と image 列の管理](managing-text-and-image-columns.md)  
  
  
