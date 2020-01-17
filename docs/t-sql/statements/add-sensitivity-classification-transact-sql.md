---
title: ADD SENSITIVITY CLASSIFICATION (Transact-SQL) | Microsoft Docs
ms.date: 03/25/2019
ms.reviewer: ''
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
ms.custom: ''
ms.manager: craigg
ms.author: giladm
author: giladmit
f1_keywords:
- ADD SENSITIVITY CLASSIFICATION
- ADD_SENSITIVITY_CLASSIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- ADD SENSITIVITY CLASSIFICATION statement
- add labels
- adding labels
- adding labels
- classification [SQL]
- labels [SQL]
- information types
- data classification
- rank
monikerRange: " >= sql-server-linux-ver15 || >= sql-server-ver15 || = azuresqldb-current || = sqlallproducts-allversions"
ms.openlocfilehash: 93c0511a6d2756c41d80745f0c0d2409f8d494ce
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882405"
---
# <a name="add-sensitivity-classification-transact-sql"></a>ADD SENSITIVITY CLASSIFICATION (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

1 つ以上のデータベース列に秘密度の分類に関するメタデータを追加します。 分類には、機密ラベルと情報の種類を含めることができます。

SQL Server では、これは SQL Server 2019 で導入されました。

データベース環境で機密データを分類すると、可視性の拡張と保護の強化が実現します。 詳しくは、[SQL Information Protection の概要](https://aka.ms/sqlip)に関する記事をご覧ください。

## <a name="syntax"></a>構文  

```
ADD SENSITIVITY CLASSIFICATION TO
    <object_name> [, ...n ]
    WITH ( <sensitivity_option> [, ...n ] )     

<object_name> ::=
{
    [schema_name.]table_name.column_name
}

<sensitivity_option> ::=  
{   
    LABEL = string |
    LABEL_ID = guidOrString |
    INFORMATION_TYPE = string |
    INFORMATION_TYPE_ID = guidOrString | 
    RANK = NONE | LOW | MEDIUM | HIGH | CRITICAL
}
```  

## <a name="arguments"></a>引数  

*object_name* ([schema_name.]table_name.column_name)

分類するデータベース列の名前です。 現在サポートされているのは列の分類のみです。
    - *schema_name* (省略可能) - 分類される列が属するスキーマの名前です。
    - *table_name* - 分類される列が属するテーブルの名前です。
    - *column_name* - 分類される列の名前です。

*LABEL*

人間が判読できる機密ラベルの名前です。 機密ラベルは、データベース列に格納されているデータの秘密度を表します。

*LABEL_ID*

機密ラベルに関連付けられている識別子です。 多くの場合、システムにおいてラベルを一意に識別するために、一元的な情報保護プラットフォームで使用されます。

*INFORMATION_TYPE*

人間が判読できる情報の種類の名前です。 情報の種類は、データベース列に格納されているデータの種類を記述するために使用されます。

*INFORMATION_TYPE_ID*

情報の種類に関連付けられている識別子です。 多くの場合、システムにおいて情報の種類を一意に識別するために、一元的な情報保護プラットフォームで使用されます。

*RANK*

感度の順位を定義する事前定義された値セットに基づく識別子です。 Advanced Threat Protection などの他のサービスによって使用され、順位に基づいて異常を検出します。


## <a name="remarks"></a>Remarks  

- 1 つのオブジェクトには分類を 1 つだけ追加できます。 分類済みのオブジェクトに分類を追加すると、既存の分類が上書きされます。
- 1 つの `ADD SENSITIVITY CLASSIFICATION` ステートメントを使用して複数のオブジェクトを分類できます。
- システム ビュー [sys.sensitivity_classifications](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md) を使用すると、データベースの秘密度の分類に関する情報を取得できます。


## <a name="permissions"></a>アクセス許可

ALTER ANY SENSITIVITY CLASSIFICATION 権限が必要です。 ALTER ANY SENSITIVITY CLASSIFICATION は、データベース権限 ALTER またはサーバー権限 CONTROL SERVER によって示されます。


## <a name="examples"></a>使用例  

### <a name="a-classifying-two-columns"></a>A. 2 つの列の分類

次の例では、機密ラベル **Highly Confidential** および情報の種類 **Financial** を使用して、**dbo.sales.price** 列と **dbo.sales.discount** 列を分類します。

```sql
ADD SENSITIVITY CLASSIFICATION TO
    dbo.sales.price, dbo.sales.discount
    WITH ( LABEL='Highly Confidential', INFORMATION_TYPE='Financial' )
```  

### <a name="b-classifying-only-a-label"></a>B. ラベルのみの分類
次の例では、ラベル **Confidential** およびラベル ID **643f7acd-776a-438d-890c-79c3f2a520d6** を使用して、**dbo.customer.comments** 列を分類します。 この列では情報の種類は分類されません。

```sql
ADD SENSITIVITY CLASSIFICATION TO
    dbo.customer.comments
    WITH ( LABEL='Confidential', LABEL_ID='643f7acd-776a-438d-890c-79c3f2a520d6' )
```  

## <a name="see-also"></a>参照  

[DROP SENSITIVITY CLASSIFICATION (Transact-SQL)](../../t-sql/statements/drop-sensitivity-classification-transact-sql.md)

[sys.sensitivity_classifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql.md)

[権限 (データベース エンジン)](https://docs.microsoft.com/sql/relational-databases/security/permissions-database-engine)

[SQL Information Protection の概要](https://aka.ms/sqlip)
