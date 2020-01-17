---
title: ConnectionValidSharedMemory dbmslpcn
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9c64fe0020ca6c406cadd5b5b71ade1641919a81
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244199"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>dbmslpcn.dll 共有メモリの ConnectionValidSharedMemory 関数
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  関数は SQL Server 共有メモリがインストールされアクティブになっているかどうかを判断します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>パラメーター  
 *szServerName*  
  
-   型: **char\* **  
  
-   SQL server の名前。  
  
## <a name="return-value"></a>戻り値  
 型: **BOOL**  
  
 無効な場合は0を返します。それ以外の場合は0以外を返します。  
  
  
