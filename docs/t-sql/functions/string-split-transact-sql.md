---
title: STRING_SPLIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRING_SPLIT
- STRING_SPLIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_SPLIT function
ms.assetid: 3273dbf3-0b4f-41e1-b97e-b4f67ad370b9
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = azuresqldb-current||=azure-sqldw-latest||>= sql-server-2016 || >= sql-server-linux-2017 || = sqlallproducts-allversions
ms.openlocfilehash: b93f85235b2676773ea3686c17d7d17e3a424d7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67906832"
---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md.md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

指定した区切り文字に基づいて、文字列を部分文字列の行に分割するテーブル値関数です。

#### <a name="compatibility-level-130"></a>互換性レベル 130

STRING_SPLIT は、互換性レベル 130 以上にする必要があります。 レベルが 130 未満の場合、SQL Server から STRING_SPLIT 関数を検出できません。

データベースの互換性レベルを変更するには、「[データベースの互換性レベルの表示または変更](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)」を参照してください。

![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  

```sql
STRING_SPLIT ( string , separator )  
```

## <a name="arguments"></a>引数

 *string*  
 任意の文字型 (**nvarchar**、**varchar**、**nchar**、**char** など) の[式](../../t-sql/language-elements/expressions-transact-sql.md)です。  
  
 *separator*  
 任意の文字型の 1 文字の[式](../../t-sql/language-elements/expressions-transact-sql.md)です (**nvarchar(1)** 、**varchar(1)** 、**nchar(1)** 、**char(1)** など)。連結する部分文字列の区切り文字として使用されます。  
  
## <a name="return-types"></a>戻り値の型  

行が部分文字列の、単一列のテーブルを返します。 列の名前は **value** です。 入力引数のいずれかが **nvarchar** または **nchar** の場合は、**nvarchar** を返します。 それ以外の場合は **varchar** を返します。 戻り値の型の長さは、文字列引数の長さと同じです。  
  
## <a name="remarks"></a>Remarks  

**STRING_SPLIT** には、部分文字列を区切った文字列と、区切り記号や区切りとして使用される 1 文字を入力します。 STRING_SPLIT では、行に部分文字列が含まれる、単一列テーブルが出力されます。 出力列の名前は **value** です。

出力行には任意の順序を指定できます。 この順序が入力文字列の部分文字列の順序と一致するかどうかは保証_されません_。 SELECT ステートメントで ORDER BY 句 (`ORDER BY value`) を使用して、最終的な並べ替え順序をオーバーライドできます。

入力文字列に区切り文字が 2 つ以上連続して含まれている場合、長さ 0 の空の部分文字列が存在します。 空の部分文字列は、プレーンな部分文字列と同じように扱われます。 WHERE 句 (`WHERE value <> ''`) を使用して、空の部分文字列が含まれているすべての行をフィルター処理できます。 入力文字列が NULL の場合、STRING_SPLIT テーブル値関数は空のテーブルを返します。  

たとえば、次の SELECT ステートメントでは、空白文字が区切り記号として使用されます。

```sql
SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');
```

実際に実行すると、前の SELECT からは、次の結果テーブルが返されます。  
  
|value|  
| :-- |  
|Lorem|  
|ipsum|  
|dolor|  
|sit|  
|amet.|  
| &nbsp; |

## <a name="examples"></a>使用例  
  
### <a name="a-split-comma-separated-value-string"></a>A. コンマ区切り値文字列を分割する

コンマ区切り値リストを解析し、空ではないすべてのトークンを返します。  

```sql
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';
```

区切り記号の間に何もない場合、STRING_SPLIT は空の文字列を返します。 条件 RTRIM(value) <> '' を指定すると、空のトークンが削除されます。  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>B. 列内のコンマ区切り値文字列を分割する

次の例のように、Product テーブルには、コンマで区切られたタグのリストを含む列があります。  
  
|ProductId|[オブジェクト名]|Tags|  
|---------------|----------|----------|  
|1|Full-Finger Gloves|clothing,road,touring,bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike,mountain|  
  
次のクエリは、タグの各リストを変換し、元の行と結合します。  

```sql  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```

 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|ProductId|[オブジェクト名]|value|  
|---------------|----------|-----------|  
|1|Full-Finger Gloves|clothing|  
|1|Full-Finger Gloves|road|  
|1|Full-Finger Gloves|touring|  
|1|Full-Finger Gloves|bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike|  
|3|HL Mountain Frame|mountain|  

  >[!NOTE]
  > この順序が入力文字列の部分文字列の順序と一致するかどうかは保証 "_されない_" ため、出力の順序は異なる場合があります。
  
### <a name="c-aggregation-by-values"></a>C. 値による集計

ユーザーは、製品数で並べ替え、タグごとに製品数を表示するレポートを作成し、2 製品を超えるタグのみに絞り込む必要があります。  

```sql  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```

### <a name="d-search-by-tag-value"></a>D. タグ値で検索する

開発者はキーワードで記事を検索するクエリを作成する必要があります。 この場合、次のクエリを使用できます。  
  
1 つのタグ (clothing) を持つ製品を検索するには:  

```sql
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```

指定された 2 つのタグ (clothing と road) を持つ製品を検索するには:  

```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road'));  
```

### <a name="e-find-rows-by-list-of-values"></a>E. 値のリストで行を検索する

開発者は、ID のリストで記事を検索するクエリを作成する必要があります。 この場合、次のクエリを使用できます。  

```sql  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')
    ON value = ProductId;  
```  

前の STRING_SPLIT の使用方法は、一般的なアンチ パターンの置き換えです。 このようなアンチ パターンには、アプリケーション レイヤーまたは Transact-SQL での動的 SQL 文字列の作成が含まれる場合があります。 または、アンチ パターンは、LIKE 演算子を使用して実現できます。 次の例の SELECT ステートメントを参照してください。

```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```

## <a name="see-also"></a>参照

[LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)<br />
[LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)<br />
[RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)<br />
[RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)<br />
[SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)<br />
[TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)<br />
[文字列関数 &#40;Transact-SQL&#41;](../../t-sql/functions/string-functions-transact-sql.md)
