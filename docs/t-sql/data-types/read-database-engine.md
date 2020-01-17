---
title: Read (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9fb69a5c4e9d303ab0e3a7a3e2edeeeeed228391
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000607"
---
# <a name="read-database-engine"></a>Read (データベース エンジン)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

読み取り のバイナリ表現を読み込む **SqlHierarchyId** から渡されるで **BinaryReader** し、設定、 **SqlHierarchyId** オブジェクトをその値にします。 読み取り [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して呼び出すことができない です。 代わりに、CAST または CONVERT を使用してください。
  
## <a name="syntax"></a>構文  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>引数  
*r*  
 **hierarchyid** ノードのバイナリ表現に対応するバイナリ ストリームを生成する **BinaryReader** オブジェクト。  
  
## <a name="return-types"></a>戻り値の型
 **CLR の戻り値の型: void**  
  
## <a name="remarks"></a>Remarks  
 読み取り は、入力は検証されません。 無効なバイナリの入力を指定した場合 読み取り で例外が発生します。 または、成功し、生成、無効な場合があります、 **SqlHierarchyId** オブジェクト メソッドを持つ予期しない結果が得られますか、例外が発生します。  
  
 読み取りは、新しく作成された **SqlHierarchyId** オブジェクトでのみ呼び出すことができます。  
  
 読み取り [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内部で使用される 必要な場合、ようにデータを書き込む場合 **hierarchyid** 列です。 読み取り 間で変換が行われるときに内部的に呼び出されますも **varbinary** と **hierarchyid**です。  
  
## <a name="examples"></a>使用例  
  
```sql
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>参照  
[Write &#40;データベース エンジン&#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString &#40;データベース エンジン&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[hierarchyid データ型メソッド リファレンス](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
