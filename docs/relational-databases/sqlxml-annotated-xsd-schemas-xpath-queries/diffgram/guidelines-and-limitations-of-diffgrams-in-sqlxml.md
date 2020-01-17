---
title: SQLXML における DiffGram のガイドラインと制限
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], about DiffGrams
ms.assetid: cf8689c4-2a63-4d05-b202-21b5ff187d7f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eae0b81b3c55a4afe611cd8ed6fdbb495b498c61
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246596"
---
# <a name="guidelines-and-limitations-of-diffgrams-in-sqlxml"></a>SQLXML における DiffGram のガイドラインと制限
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  SQLXML 4.0 で DiffGram を使用するときには、次の点に注意してください。  
  
-   **Text/ntext**および image のようなバイナリラージオブジェクト (BLOB) 型は、 ** \<** diffgram を操作するときに、>ブロックの前に使用しないでください。これには、同時実行制御に使用するものが含まれます。 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で、BLOB 型の比較の制限によって問題が発生する可能性があります。 たとえば、 **text**データ型の列を比較するには、WHERE 句で LIKE キーワードを使用します。ただし、データのサイズが8K を超える BLOB 型の場合、比較は失敗します。  
  
-   **Ntext**データ内の特殊文字は、BLOB 型の比較の制限により、SQLXML 4.0 で問題が発生する可能性があります。 たとえば、次のように、 **ntext**型の列の同時実行制御チェックで使用するときに、diffgram の** \<>** ブロックで "[Serializable]" を使用すると、次の SQLOLEDB エラーの説明で失敗します。  
  
    ```  
    Empty update, no updatable rows found   Transaction aborted  
    ```  
  
  
