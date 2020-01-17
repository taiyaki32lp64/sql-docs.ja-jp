---
title: bcp を使用したデータ ファイルのプレフィックス長の指定 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server], prefix length
- prefix length [SQL Server]
- lengths [SQL Server], prefix characters
- data formats [SQL Server], prefix length
ms.assetid: ce32dd1a-26f1-4f61-b9fa-3f1feea9992e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5d91c82d892888d2e6edde5615ba05a2a9ebf3c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011756"
---
# <a name="specify-prefix-length-in-data-files-by-using-bcp-sql-server"></a>bcp を使用したデータ ファイルのプレフィックス長の指定 (SQL Server)
  **bcp** コマンドでは、ネイティブ形式のデータをデータ ファイルに一括エクスポートするためのファイル ストレージが最も少なくなるように、各フィールドの前にそのフィールドの長さを 1 文字以上の文字列で指定します。 このような文字列を、 *プレフィックス長文字列*と呼びます。  
  
## <a name="the-bcp-prompt-for-prefix-length"></a>プレフィックス長の bcp プロンプト  
 対話型の **bcp** コマンドで、フォーマット ファイル スイッチ ( **-f** ) またはデータ形式スイッチ ( **-n** 、 **-c**、 **-w**、または **-N**) のどちらも付けずに **in**または **out**オプションを指定すると、次のように各データ フィールドのプレフィックス長を要求するプロンプトが表示されます。  
  
 `Enter prefix length of field <field_name> [<default>]:`  
  
 0 を指定すると、フィールドの長さ (文字データ型の場合) またはフィールド ターミネータ (文字以外のネイティブ型の場合) のいずれかが、 **bcp** によって要求されます。  
  
> [!NOTE]  
>  **bcp** コマンドですべてのフィールドを対話形式で指定すると、各フィールドへの応答を XML 形式以外のファイルに保存するように要求するプロンプトが表示されます。 XML 以外のフォーマット ファイルの詳細については、「[XML 以外のフォーマット ファイル &#40;SQL Server&#41;](xml-format-files-sql-server.md)」を参照してください。  
  
## <a name="overview-of-prefix-length"></a>プレフィックス長の概要  
 フィールドのプレフィックス長を格納するには、フィールドの最大長を表すのに十分なバイト数が必要です。 必要なバイト数は、ファイル ストレージの型、列の NULL 値許容属性、およびデータがネイティブ形式または文字形式でデータ ファイルに格納されるかどうかによって異なります。 たとえば、`text` データ型または `image` データ型では、フィールド長を格納するために 4 文字のプレフィックス文字列が必要ですが、`varchar` データ型で必要なのは 2 文字です。 データ ファイルでは、このようなプレフィックス長文字列は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の内部バイナリ データ形式で格納されます。  
  
> [!IMPORTANT]  
>  ネイティブ形式を使用するときは、フィールド ターミネータではなくプレフィックス長を使用します。 ネイティブ形式のデータ ファイルは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の内部バイナリ データ形式で格納されるので、ネイティブ形式のデータがターミネータと競合することがあります。  
  
##  <a name="PrefixLengthsExport"></a> 一括エクスポートのプレフィックス長  
  
> [!NOTE]  
>  フィールドをエクスポートするときにプレフィックス長のプロンプトに表示される既定値は、フィールドの最も効率的なプレフィックス長を示します。  
  
 NULL 値は空のフィールドとして表現されます。 フィールドが空 (NULL) であることを示すには、フィールド プレフィックスに値 -1 を含めます。つまり、少なくとも 1 バイトが必要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブル列で NULL 値を許可する場合は、ファイル ストレージの型に応じて、1 以上のプレフィックス長が必要になります。  
  
 データを一括エクスポートし、ネイティブ データ型または文字形式のいずれかで格納する場合は、次の表に示すプレフィックス長を使用します。  
  
|SQL Server<br /><br /> データ型 (data type)|ネイティブ形式<br /><br /> NOT NULL|ネイティブ形式<br /><br /> NULL|文字形式<br /><br /> NOT NULL|文字形式<br /><br /> NULL|  
|------------------------------|--------------------------------|----------------------------|-----------------------------------|-------------------------------|  
|`char`|2|2|2|2|  
|`varchar`|2|2|2|2|  
|`nchar`|2|2|2|2|  
|`nvarchar`|2|2|2|2|  
|`text` <sup>1</sup>|4|4|4|4|  
|`ntext` <sup>1</sup>|4|4|4|4|  
|`binary`|2|2|2|2|  
|`varbinary`|2|2|2|2|  
|`image` <sup>1</sup>|4|4|4|4|  
|`datetime`|0|1|0|1|  
|`smalldatetime`|0|1|0|1|  
|`decimal`|1|1|1|1|  
|`numeric`|1|1|1|1|  
|`float`|0|1|0|1|  
|`real`|0|1|0|1|  
|`int`|0|1|0|1|  
|`bigint`|0|1|0|1|  
|`smallint`|0|1|0|1|  
|`tinyint`|0|1|0|1|  
|`money`|0|1|0|1|  
|`smallmoney`|0|1|0|1|  
|`bit`|0|1|0|1|  
|`uniqueidentifier`|1|1|0|1|  
|`timestamp`|1|1|1|1|  
|`varchar(max)`|8|8|8|8|  
|`varbinary(max)`|8|8|8|8|  
|UDT (ユーザー定義データ型)|8|8|8|8|  
|XML|8|8|8|8|  
  
 <sup>1</sup> 、 `ntext`、 `text`、および`image`データ型はの将来のバージョンで削除される[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 新しい開発作業では、これらのデータ型の使用は避け、現在これらのデータ型を使用しているアプリケーションは修正するようにしてください。 代わりに `nvarchar(max)`、`varchar(max)`、および `varbinary(max)` 型を使用してください。  
  
##  <a name="PrefixLengthsImport"></a> 一括インポートのプレフィックス長  
 データが一括インポートされるときは、プレフィックス長はデータ ファイルが作成されたときに指定された値になります。 **bcp** コマンドでデータ ファイルが作成されなかった場合、プレフィックス長文字列が存在しない場合があります。 この場合は、プレフィックス長に 0 を指定します。  
  
> [!NOTE]  
>  **bcp**を使用して、作成されなかったデータ ファイルのプレフィックス長を指定するには、このトピックの「 [一括エクスポートのプレフィックス長](#PrefixLengthsExport)」に記載した長さを使用してください。  
  
## <a name="see-also"></a>参照  
 [bcp ユーティリティ](../../tools/bcp-utility.md)   
 [データ型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [bcp を使用したフィールド長の指定 &#40;SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md)   
 [フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [bcp を使用したファイル ストレージ型の指定 &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
  
