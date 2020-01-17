---
title: '手順 1: pyodbc Python 開発環境を構成する |Microsoft Docs'
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a1a43540d866faaf79b1c020eb255689862e6d97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992522"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>手順 1: pyodbc Python 開発用に開発環境を構成する

## <a name="windows"></a>Windows  
Windows で pyodbc を使用して SQL Database に接続します。
  
1. **Python インストーラーをダウンロード**します。  
  コンピューターに Python がインストールされていない場合は、インストールします。 [Python のダウンロードページ](https://www.python.org/downloads/windows/)にアクセスし、適切なインストーラーをダウンロードします。 たとえば、64ビットのコンピューターを使用している場合は、Python 2.7 または 3.7 (x64) インストーラーをダウンロードします。  
  
2. **Python をインストール**します。  インストーラーをダウンロードしたら、次の手順を実行します。 a. ファイルをダブルクリックしてインストーラーを起動します。 B. 言語を選択し、使用条件に同意します。 c. 画面の指示に従って、コンピューターに Python をインストールする必要があります。 d. また`C:\Python27` `python -V` `py -V`はを実行し、または (2.x の場合) を実行して、Python がインストールされていることを確認できます。 `C:\Python37` 
      
3. [**Microsoft ODBC Driver for SQL Server on Windows をインストール**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)します。
  
4. **管理者として cmd.exe を開きます。**     

5. **Pip を使用して pyodbc をインストールする-Python パッケージマネージャー**(インストール`C:\Python27\Scripts`されている Python パスに置き換えてください)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Pyodbc を使用して SQL Database に接続します。
  
1. **ターミナルを開く**  

2. [**Microsoft ODBC Driver for SQL Server on Linux をインストール**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)します。

3.  **Pyodbc のインストール**  
```  
> sudo -H pip install pyodbc
```
