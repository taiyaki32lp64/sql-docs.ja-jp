---
title: Index 要素 (DTA) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Index element (DTA)
ms.assetid: 447d3964-b387-40f6-9189-71386774c29e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3e7b86c8ac990c7add4856e2c00e43550903f55a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034836"
---
# <a name="index-element-dta"></a>Index 要素 (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  ユーザー指定の構成のために作成したり削除したりするインデックスの情報が含まれます。  
  
## <a name="syntax"></a>構文  
  
```  
  
<Recommendation>  
  <Create>  
    <Index [Clustered | Unique | Online | IndexSizeInMB | NumberOfRows             | QUOTED_IDENTIFIER | ARITHABORT | CONCAT_NULL_YIELDS_NULL             | ANSI_NULLS | ANSI_PADDING | ANSI_WARNINGS  
            | NUMERIC_ROUNDABORT]  
     ...code removed here...  
    </Index>  
```  
  
## <a name="element-attributes"></a>要素の属性  
  
|Index の属性|データ型|[説明]|  
|---------------------|---------------|-----------------|  
|**クラスター化インデックス**|**boolean**|省略可。 クラスター化インデックスを指定します。 「true」か「false」のいずれかに設定します。以下はその例です。<br /><br /> `<Index Clustered="true">`<br /><br /> 既定では、この属性は「false」に設定されます。|  
|**[一意]**|**boolean**|省略可。 一意のインデックスを指定します。 「true」か「false」のいずれかに設定します。以下はその例です。<br /><br /> `<Index Unique="true">`<br /><br /> 既定では、この属性は「false」に設定されます。|  
|**オンライン**|**boolean**|省略可。 サーバーがオンラインのときに操作を実行できるインデックスを指定します (そのためには、一時ディスク領域が必要になります)。 「true」か「false」のいずれかに設定します。以下はその例です。<br /><br /> `<Index Online="true">`<br /><br /> 既定では、この属性は「false」に設定されます。<br /><br /> 詳しくは、「 [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)」をご覧ください。|  
|**IndexSizeInMB**|**double**|省略可。 インデックスの最大サイズを MB 単位で指定します。以下はその例です。<br /><br /> `<Index IndexSizeInMB="873.75">`<br /><br /> 既定の設定はありません。|  
|**NumberOfRows**|**整数 (integer)**|省略可。 インデックス サイズを変更した場合のシミュレーションを行います。これにより、異なるテーブル サイズの有効なシミュレーションを行えます。以下はその例です。<br /><br /> `<Index NumberOfRows="3000">`<br /><br /> 既定の設定はありません。|  
|**QUOTED_IDENTIFIER**|**boolean**|省略可。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に対して、識別子とリテラル文字列を区切る引用符に関して、ISO 規格に従うことを指定します。 計算列またはビューを対象とするインデックスの場合は、この属性をオンにする必要があります。 たとえば、以下の構文では、この属性をオンに設定しています。<br /><br /> `<Index QUOTED_IDENTIFIER [...]>`<br /><br /> 既定では、この属性はオフに設定されます。<br /><br /> 詳細については、「[SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)」をご覧ください。|  
|**ARITHABORT**|**boolean**|省略可。 クエリ実行中にオーバーフローまたは 0 除算エラーが発生した場合に、クエリを終了します。 計算列またはビューを対象とするインデックスの場合は、この属性をオンにする必要があります。 たとえば、以下の構文では、この属性をオンに設定しています。<br /><br /> `<Index ARITHABORT [...]>`<br /><br /> 既定では、この属性はオフに設定されます。<br /><br /> 詳細については、「[SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)」をご覧ください。|  
|**CONCAT_NULL_YIELDS_**<br /><br /> **NULL**|**boolean**|省略可。 連結の結果を NULL として取り扱うのか、空文字列として取り扱うのかを制御します。 計算列またはビューを対象とするインデックスの場合は、この属性をオンにする必要があります。 たとえば、以下の構文では、この属性をオンに設定しています。<br /><br /> `<Index CONCAT_NULL_YIELDS_NULL [...]>`<br /><br /> 既定では、この属性はオフに設定されます。<br /><br /> 詳細については、「[SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)」をご覧ください。|  
|**ANSI_NULLS**|**boolean**|省略可。 等号 (=) 比較演算子と不等号 (<>) 比較演算子を NULL 値に対して使用した場合に ISO に準拠した動作をすることを指定します。 計算列またはビューを対象とするインデックスの場合は、この属性をオンにする必要があります。 たとえば、以下の構文では、この属性をオンに設定しています。<br /><br /> `<Index ANSI_NULLS [...]>`<br /><br /> 既定では、この属性はオフに設定されます。<br /><br /> 詳細については、「[SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)」をご覧ください。|  
|**ANSI_PADDING**|**boolean**|省略可。 列に定義されているサイズよりも短い値を格納する方法を制御します。 計算列またはビューを対象とするインデックスの場合は、この属性をオンにする必要があります。 たとえば、以下の構文では、この属性をオンに設定しています。<br /><br /> `<Index ANSI_PADDING [...]>`<br /><br /> 既定では、この属性はオフに設定されます。<br /><br /> 詳細については、「[SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)」を参照してください。|  
|**ANSI_WARNINGS**|**boolean**|省略可。 複数のエラー条件に対して ISO 標準の動作をすることを指定します。 計算列またはビューを対象とするインデックスの場合は、この属性をオンにする必要があります。 たとえば、以下の構文では、この属性をオンに設定しています。<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> 既定では、この属性はオフに設定されます。<br /><br /> 詳細については、「[SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)」をご覧ください。|  
|**NUMERIC_ROUNDABORT**|**boolean**|省略可。 式の丸め処理で精度が低下するときに作成されるエラー レポートのレベルを指定します。 計算列またはビューを対象とするインデックスの場合は、この属性をオフにする必要があります。<br /><br /> 以下の構文では、この属性をオンに設定しています。<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> 既定では、この属性はオフに設定されます。<br /><br /> 詳細については、「[SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)」を参照してください。|  
  
## <a name="element-characteristics"></a>要素の特性  
  
|特性|[説明]|  
|--------------------|-----------------|  
|**データ型と長さ**|[なし] :|  
|**既定値**|[なし] :|  
|**個数**|**Statistics** 要素または **Heap** 要素で他の物理設計構造が指定されてない場合、 **Create** 要素または **Drop** 要素につき 1 回の出現が必要です。|  
  
## <a name="element-relationships"></a>要素の関係  
  
|リレーションシップ|要素|  
|------------------|--------------|  
|**親要素**|[Create 要素 &#40;DTA&#41;](../../tools/dta/create-element-dta.md)<br /><br /> **Drop** 要素。 詳細については、データベース エンジン チューニング アドバイザーの XML スキーマを参照してください。|  
|**子要素**|[Index の Name 要素 &#40;DTA&#41;](../../tools/dta/name-element-for-index-dta.md)<br /><br /> [Index の Column 要素 &#40;DTA&#41;](../../tools/dta/column-element-for-index-dta.md)<br /><br /> **PartitionScheme** 要素。 詳細については、データベース エンジン チューニング アドバイザーの XML スキーマを参照してください。<br /><br /> **PartitionColumn** 要素。 詳細については、データベース エンジン チューニング アドバイザーの XML スキーマを参照してください。<br /><br /> [Index の Filegroup 要素 &#40;DTA&#41;](../../tools/dta/filegroup-element-for-index-dta.md)<br /><br /> **NumberOfReferences** 要素。 詳細については、データベース エンジン チューニング アドバイザーの XML スキーマを参照してください。<br /><br /> **PercentUsage** 要素。 詳細については、データベース エンジン チューニング アドバイザーの XML スキーマを参照してください。|  
  
## <a name="example"></a>例  
 この要素の使用例については、「[ユーザー指定の構成を指定した XML 入力ファイルのサンプル &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [XML 入力ファイル リファレンス &#40;データベース エンジン チューニング アドバイザー&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
