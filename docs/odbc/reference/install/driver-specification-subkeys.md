---
title: ドライバーの仕様のサブキー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f5523c54286ed2e7cc554745dc269599115793e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094173"
---
# <a name="driver-specification-subkeys"></a>ドライバーの仕様のサブキー
ODBC ドライバーのサブキーの一覧の各ドライバーでは、独自のサブキーがあります。 このサブキーは、ODBC ドライバーのサブキーの下の対応する値として同じ名前を持ちます。 このサブキーの下の値は、ドライバーとドライバーのセットアップ Dll、によって返されるドライバー キーワードの値の完全なパスを一覧表示**SQLDrivers**、および使用状況カウントします。 値の形式は、次の表に示すようにします。  
  
|名前|データ型|data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**N**} {**Y**&#124;**N**} {**Y**&#124;**N**}|  
|CreateDSN|REG_SZ|*ドライバーの説明*|  
|Driver|REG_SZ|*ドライバー DLL のパス*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *ファイル extension1*[ **、\*します。** *ファイル extension2*].|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|セットアップ|REG_SZ|*セットアップ DLL へのパス*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*count*|  
  
 各キーワードの使用は、次の表に示します。  
  
|Keyword|使用方法|  
|-------------|-----------|  
|**APILevel**|ODBC を示す数値インターフェイスのドライバーでサポートされている一致レベル。<br /><br /> 0 = なし<br /><br /> 1 = レベル 1 のサポート<br /><br /> 2 = レベル 2 のサポート<br /><br /> これは SQL_ODBC_INTERFACE_CONFORMANCE オプションに返される値と同じである必要があります**SQLGetInfo**します。|  
|**CreateDSN**|ドライバーのインストール時に作成される 1 つまたは複数のデータ ソースの名前。 システム情報と共に表示されるデータ ソースごとに 1 つのデータ ソースの仕様セクションを含める必要があります、 **CreateDSN**キーワード。 これらのセクションを含めないでください、**ドライバー**キーワード、これは、ドライバーの仕様のセクションで指定が十分な情報を含める必要があります、 **ConfigDSN**ドライバーで関数すべてのダイアログ ボックスを表示せず、データ ソースの仕様を作成する DLL をセットアップします。 データ ソースの仕様のセクションの形式の場合、次を参照してください。[データ ソースの仕様のサブキー](../../../odbc/reference/install/data-source-specification-subkeys.md)します。|  
|**ConnectFunctions**|ドライバーがサポートしているかどうかを示す 3 文字の文字列**SQLConnect**、 **SQLDriverConnect**、および**SQLBrowseConnect**します。 ドライバーがサポートしている場合**SQLConnect**、最初の文字は"Y"; 以外の場合は"N"です。 ドライバーがサポートしている場合**SQLDriverConnect**、2 番目の文字は"Y"; 以外の場合は"N"です。 ドライバーがサポートしている場合**SQLBrowseConnect**、3 番目の文字は"Y"; 以外の場合は"N"です。 たとえば、ドライバーをサポートしている場合**SQLConnect**と**SQLDriverConnect**なく**SQLBrowseConnect**、3 文字の文字列は"YYN"。|  
|**DriverODBCVer**|ドライバーがサポートする ODBC のバージョンと文字の文字列。 形式は、バージョン*nn.nn*最初の 2 つの数字、メジャー バージョンとは、次の 2 つの数字はマイナー バージョン。 このマニュアルで説明されている ODBC のバージョン、ドライバーは「03.00」返す必要があります。<br /><br /> これは SQL_DRIVER_ODBC_VER オプションに返される値と同じである必要があります**SQLGetInfo**します。|  
|**FileExtns**|ファイル ベースのドライバーでは、ファイルの拡張子のコンマ区切りの一覧を使用できます。 たとえば、dBASE ドライバー指定\*.dbf と書式設定されたテキスト ファイル ドライバーを指定\*.txt、\*.csv です。 アプリケーションがこの情報を使用する方法の例は、次を参照してください。、 **FileUsage**キーワード。|  
|**FileUsage**|ファイル ベースのドライバーが直接データ ソース内のファイルを処理する方法を示す数です。<br /><br /> 0 = ドライバーは、ファイル ベースのドライバーではありません。 たとえば、ORACLE ドライバーは、DBMS ベースのドライバーです。<br /><br /> 1 = テーブルとしてデータ ソースで、ファイル ベースのドライバー扱いますファイル。 たとえば、Xbase ドライバーはテーブルとして各 Xbase ファイルを扱います。<br /><br /> 2 = カタログとしてデータ ソース内のファイル ベースのドライバー扱いますファイル。 たとえば、Microsoft® Access ドライバーは完全なデータベースとして各 Microsoft Access ファイルを扱います。<br /><br /> アプリケーションは、これを使用のユーザーがデータを選択する方法を決定するのに可能性があります。 たとえば、Xbase および Paradox ユーザーでは、データ テーブルに格納されている、この ORACLE および Microsoft Access のユーザーは、通常のデータと考えるときに、ファイルに格納されているのと考えがちです。<br /><br /> ユーザーが選択すると**データ ファイルを開く**から、**ファイル**] メニューの [アプリケーションを表示でした、 **Windows ファイルを開く**コモン ダイアログ ボックス。 ファイルの種類の一覧がで指定されたファイル拡張子を使用して、 **FileExtns**キーワードを指定するドライバーに対して、 **FileUsage**の値が 1 と"Y"の値の 2 番目の文字として、 **ConnectFunctions**キーワード。 アプリケーションを呼び出すと、ユーザーがファイルを選択後 **SQLDriverConnect** で、 **ドライバー** キーワードし、実行、 **選択** \*FROM *テーブル名* ステートメント。<br /><br /> ユーザーが選択すると**データのインポート**から、**ファイル**] メニューの [アプリケーション表示、説明を指定するドライバーの一覧を**FileUsage** 0 または 2、および"Y"の値値の 2 番目の文字として、 **ConnectFunctions**キーワード。 アプリケーションを呼び出すと、ユーザーがドライバーを選択後**SQLDriverConnect**で、**ドライバー**キーワードと、表示、カスタム**テーブルの選択** ダイアログ ボックス。|  
|**SQLLevel**|ドライバーによってサポートされている SQL 92 文法を示す数値。<br /><br /> 0 = SQL 92 エントリ<br /><br /> 1 = FIPS127 2 の移行<br /><br /> 2 = SQL 92 中間<br /><br /> 3 = sql-92 Full<br /><br /> これは SQL_SQL_CONFORMANCE オプションに返される値と同じである必要があります**SQLGetInfo**します。|  
  
 使用状況カウントの詳細については、次を参照してください。[使用状況のカウント](../../../odbc/reference/install/usage-counting.md)このセクションで前述しました。  
  
 アプリケーションでは、使用率カウントは設定しないでください。 ODBC では、この数を維持します。  
  
 たとえば、書式設定されたテキスト ファイル用のドライバーをドライバー Text.dll という名前の DLL があるとします個別のドライバー セットアップ DLL Txtsetup.dll、という 3 回がインストールされています。 ドライバーは、レベル 1 API への準拠レベルをサポート、Minimum SQL 文法の準拠レベルをサポートしています、によるファイルの処理として、テーブル、および .txt および .csv の拡張子を持つファイルを使用することができますを場合、としては、次のようにテキスト サブキーの値になります。  
  
```  
APILevel : REG_SZ : 1  
ConnectFunctions : REG_SZ : YYN  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\TEXT.DLL  
DriverODBCVer : REG_SZ : 03.00.00  
FileExtns : REG_SZ : *.txt,*.csv  
FileUsage : REG_SZ : 1  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\TXTSETUP.DLL  
SQLLevel : REG_SZ : 0  
UsageCount : REG_DWORD : 0x3  
```
