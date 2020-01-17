---
title: GetPathLocator (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- GetPathLocator
- GetPathLocator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetPathLocator function
ms.assetid: 78b7e220-445b-4fdf-811b-7253f4f2b058
author: rothja
ms.author: jroth
ms.openlocfilehash: 4cec490522f8bacc774213ec1af5cce1af0eefef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910252"
---
# <a name="getpathlocator-transact-sql"></a>GetPathLocator (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  FileTable 内のパス ロケーターの指定したファイルまたはディレクトリの ID 値を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
GetPathLocator(filenamespace_path)  
```  
  
## <a name="arguments"></a>引数  
 *filenamespace_path*  
 FileTable 内の名前空間パス。 型の名前空間のパスは、 **nvarchar (max)** します。  
  
 データベースが Always On 可用性グループに属している場合、 **GetPathLocator**関数は、仮想ネットワーク名 (VNN) またはコンピューター名を受け取ります。  
  
## <a name="return-type"></a>戻り値の型  
 **hierarchyid**  
  
## <a name="general-remarks"></a>全般的な解説  
 詳しくは、「 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)」をご覧ください。  
  
## <a name="examples"></a>使用例  
 使用することができます、 **GetPathLocator**ファイル サーバーからファイルを FileTable に移行するときに機能します。 このシナリオで、FileTable にファイルを移動し、各ファイルの元の UNC パスを FileTable の UNC パスに置き換えますしたいです。 完全な例を参照してください。 [Filetable にファイルを読み込む](../../relational-databases/blob/load-files-into-filetables.md)します。  
  
## <a name="see-also"></a>関連項目  
 [FileTable 内のディレクトリとパスの操作](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
