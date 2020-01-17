---
title: float 型と real 型 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- float
- real_TSQL
- real
- float_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- numeric data type, floating point
- float data type
- floating point data [SQL Server]
- real data type
ms.assetid: 08ea66b7-624e-4d8b-86bc-750ff76cdfc5
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7f31e3894448e5d6a044af75c7e86b704b993aa6
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "71682016"
---
# <a name="float-and-real-transact-sql"></a>float 型と real 型 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

浮動小数点数値データで使用する概数型です。 浮動小数点データは概数であるため、データ型の範囲に含まれるすべての値を正確に表せるわけではありません。 **real** の ISO シノニムは、 **float (24)** です。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
**float** [ **(** _n_ **)** ]。*n* は、科学的表記法で **float** 数の仮数部を格納するために使用されるビット数であるため、精度と格納サイズを指示します。 *n* を指定する場合、**1** から **53** までの値にする必要があります。 *n* の既定値は **53** です。
  
|*n* 値|有効桁数|ストレージ サイズ|  
|---|---|---|
|**1 ～ 24**|7 桁|4 バイト|  
|**25-53**|15 桁|8 バイト|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、*n* は次の 2 つの値のいずれかの値として扱われます。 **1**<=n<=**24** の場合、*n* は **24** として処理されます。 **25**<=n<=**53** の場合、*n* は **53** として処理されます。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float** **[(n)]** データ型は、*n* (**1** ～ **53**) のすべての値で ISO 標準に準拠しています。 **double precision** のシノニムは **float (53)** です。
  
## <a name="remarks"></a>Remarks  
  
|データ型|範囲|ストレージ|  
|---|---|---|
|**float**|- 1.79E+308 から -2.23E-308、0、および 2.23E-308 から 1.79E+308|*n* の値により異なります|  
|**real**|- 3.40E + 38 から -1.18E - 38、0、および 1.18E - 38 から 3.40E + 38|4 バイト|  
  
##  <a name="converting-float-and-real-data"></a>float 型データと real 型データの変換  
**float** の値は、任意の整数型への変換時に切り捨てられます。
  
**float** または **real** を文字データに変換するときには、STR 文字列関数を使用する方が CAST () よりも便利です。 これは、STR 関数の方がより柔軟に形式を制御できるためです。 詳細については、「[STR &#40;Transact-SQL&#41;](../../t-sql/functions/str-transact-sql.md)」と「[関数 &#40;Transact-SQL&#41;](../../t-sql/functions/functions.md)」を参照してください。
  
[!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] より前では、**float** 値から **decimal** または **numeric** への変換は、有効桁数 17 桁までの値に制限されます。 5E-18 未満の **float** 値はすべて (5E-18 の科学的記数法または 0.0000000000000000050000000000000005 の小数点表記のいずれかを使用して設定されている場合) 0 に丸められます。 これは [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)] の時点で制限がなくなりました。
  
## <a name="see-also"></a>参照
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[データ型の変換&#40;Transact-SQL&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  
