---
title: MinDbCompatibilityLevel (geography データ型) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MinDbCompatibilityLevel
- MinDbCompatibilityLevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MinDbCompatibilityLevel method (geography)
ms.assetid: a9e44748-4a9e-4179-abc4-7631597be5a7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a8aaa21498c95c215de5e5a49f9ced8089b4c71e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223661"
---
# <a name="mindbcompatibilitylevel-geography-data-type"></a>MinDbCompatibilityLevel (geography データ型)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  **geography** データ型を認識する最小データベース互換性を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
. MinDbCompatibilityLevel ( )  
```  
  
## <a name="return-types"></a>戻り値の型  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の戻り値の型: **int**  
  
 CLR の戻り値の型: **int**  
  
## <a name="remarks"></a>Remarks  
 `MinDbCompatibilityLevel()` を使用すると、データベースで互換性レベルを変更する前に、空間オブジェクトの互換性をテストできます。 無効な **geography** 型を入力すると 110 が返されます。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-testing-circularstring-type-for-compatibility-with-compatibility-level-110"></a>A. 互換性レベル 110 で CircularString 型の互換性をテストする  
 次の例では、`CircularString` インスタンスの、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との互換性がテストされます。  
  
```  
DECLARE @g geometry = 'CIRCULARSTRING(-120.533 46.566, -118.283 46.1, -122.3 47.45)';  
IF @g.MinDbCompatibilityLevel() <= 110  
BEGIN  
    SELECT @g.ToString();  
END  
  
```  
  
### <a name="b-testing-linestring-type-for-compatibility-with-compatibility-level-100"></a>B. 互換性レベル 100 で LineString 型の互換性をテストする  
 次の例では、`LineString` インスタンスの [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] との互換性をテストします。  
  
```  
DECLARE @g geometry = 'LINESTRING(-120.533 46.566, -118.283 46.1, -122.3 47.45)';  
IF @g.MinDbCompatibilityLevel() <= 100  
BEGIN  
    SELECT @g.ToString();  
END  
  
```  
  
### <a name="c-testing-the-value-of-a-geography-instance-for-compatibility"></a>C. Geography インスタンスの値の互換性をテストする  
 次の例では、2 つの `geography` インスタンスの互換性レベルを表示します。 一方は半球よりも小さく、もう一方は半球よりも大きくなっています。  
  
```  
DECLARE @g geography = geography::Parse('POLYGON((0 -10, 120 -10, 240 -10, 0 -10))');  
DECLARE @h geography = geography::Parse('POLYGON((0 10, 120 10, 240 10, 0 10))');  
IF (@g.EnvelopeAngle() >= 90)  
BEGIN  
SELECT @g.MinDbCompatibilityLevel();  
END     
IF (@h.EnvelopeAngle() < 90)  
BEGIN  
SELECT @h.MinDbCompatibilityLevel();  
END  
  
```  
  
 最初の SELECT ステートメントは 110 を返し、2 番目の SELECT ステートメントは 100 を返します。  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)   
 [SQL Server データベース エンジンの旧バージョンとの互換性](../../database-engine/sql-server-database-engine-backward-compatibility.md)  
  
  
