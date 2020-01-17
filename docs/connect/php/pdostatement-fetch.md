---
title: 'PDOStatement:: fetch |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4368e362-5bda-4da1-8462-33714683c39f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a69b1093240112a804504f8d0e636ffbdfe8439e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993060"
---
# <a name="pdostatementfetch"></a>PDOStatement::fetch
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

結果セットから行を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
mixed PDOStatement::fetch ([ $fetch_style[, $cursor_orientation[, $cursor_offset]]] );  
```  
  
#### <a name="parameters"></a>パラメーター  
$*fetch_style*: 行データの形式を指定する省略可能な (整数) 記号です。 $*fetch_style* で使用可能な値一覧については、「解説」セクションを参照してください。 既定値は PDO::FETCH_BOTH です。フェッチ メソッドの  $*fetch_style* によって PDO::query メソッドで指定した $*fetch_style* はオーバーライドされます。  
  
$*cursor_orientation*: 準備のステートメントが `PDO::ATTR_CURSOR => PDO::CURSOR_SCROLL` を指定している場合、取得する行を示す省略可能な (整数) 記号です。 $*cursor_orientation* で使用可能な値一覧については、「解説」セクションを参照してください。 スクロール可能なカーソルを使用する例については、「 [PDO::prepare](../../connect/php/pdo-prepare.md) 」を参照してください。  
  
$*cursor_offset*: $*cursor_orientation* が PDO::FETCH_ORI_ABS または PDO::FETCH_ORI_REL および PDO::ATTR_CURSOR が PDO::CURSOR_SCROLL である場合にフェッチする行を指定する省略可能な (整数) 記号です。  
  
## <a name="return-value"></a>戻り値  
行を返す複合値または false です。  
  
## <a name="remarks"></a>Remarks  
フェッチが呼び出されると、カーソルは自動的に前進します。 次の表は、可能な $*fetch_style* 値の一覧です。  
  
|$*fetch_style*|[説明]|  
|-------------------|---------------|  
|PDO::FETCH_ASSOC|列名でインデックス付けされた配列を指定します。|  
|PDO::FETCH_BOTH|列名でインデックス付けされた 0 から始まる配列を指定します。 これは既定値です。|  
|PDO::FETCH_BOUND|True を返し、 [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md)で指定された値を割り当てます。|  
|PDO::FETCH_CLASS|インスタンスを作成し、列を名前付きプロパティにマップします。<br /><br />フェッチを呼び出す前に、 [PDOStatement::setFetchMode](../../connect/php/pdostatement-setfetchmode.md) を呼び出します。|  
|PDO::FETCH_INTO|要求されたクラスのインスタンスを更新します。<br /><br />フェッチを呼び出す前に、 [PDOStatement::setFetchMode](../../connect/php/pdostatement-setfetchmode.md) を呼び出します。|  
|PDO::FETCH_LAZY|アクセス時に変数名を作成し、名前のないオブジェクトを作成します。|  
|PDO::FETCH_NUM|列の順が 0 から開始するインデックス付きの配列を指定します。|  
|PDO::FETCH_OBJ|列名にマップされるプロパティ名を持つ名前のないオブジェクトを指定します。|  
  
カーソルが結果セットの最後にあり (最後の行が取得され、カーソルが結果セットの境界範囲を超えたところにあります)、カーソルが前進のみの場合 (PDO::ATTR_CURSOR = PDO::CURSOR_FWDONLY)、それ以降のフェッチ呼び出しは失敗します。  
  
カーソルがスクロール可能な場合 (PDO::ATTR_CURSOR = PDO::CURSOR_SCROLL)、フェッチは結果セットの境界内にカーソルを移動します。 次の表は、可能な $*cursor_orientation* 値の一覧です。  
  
|$*cursor_orientation*|[説明]|  
|--------------------------|---------------|  
|PDO::FETCH_ORI_NEXT|次の行を取得します。 これは既定値です。|  
|PDO::FETCH_ORI_PRIOR|前の行を取得します。|  
|PDO::FETCH_ORI_FIRST|1 番目の行を取得します。|  
|PDO::FETCH_ORI_LAST|最後の行を取得します。|  
|PDO::FETCH_ORI_ABS, *num*|$*cursor_offset* で要求された行を行番号で取得します。|  
|PDO::FETCH_ORI_REL, *num*|$*cursor_offset* で要求された行を現在の位置からの相対位置で取得します。|  
  
$*cursor_offset* または $*cursor_orientation* に指定した値が、結果セットの境界外に位置する場合、フェッチは失敗します。  
  
PDO のサポートは [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]のバージョン 2.0 で追加されました。  
  
## <a name="example"></a>例  
  
```  
<?php  
   $server = "(local)";  
   $database = "AdventureWorks";  
   $conn = new PDO( "sqlsrv:server=$server ; Database = $database", "", "");  
  
   print( "\n---------- PDO::FETCH_CLASS -------------\n" );  
   $stmt = $conn->query( "select * from HumanResources.Department order by GroupName" );  
  
   class cc {  
      function __construct( $arg ) {  
         echo "$arg";  
      }  
  
      function __toString() {  
         return $this->DepartmentID . "; " . $this->Name . "; " . $this->GroupName;  
      }  
   }  
  
   $stmt->setFetchMode(PDO::FETCH_CLASS, 'cc', array( "arg1 " ));  
   while ( $row = $stmt->fetch(PDO::FETCH_CLASS)) {   
      print($row . "\n");   
   }  
  
   print( "\n---------- PDO::FETCH_INTO -------------\n" );  
   $stmt = $conn->query( "select * from HumanResources.Department order by GroupName" );  
   $c_obj = new cc( '' );  
  
   $stmt->setFetchMode(PDO::FETCH_INTO, $c_obj);  
   while ( $row = $stmt->fetch(PDO::FETCH_INTO)) {   
      echo "$c_obj\n";  
   }  
  
   print( "\n---------- PDO::FETCH_ASSOC -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_ASSOC );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_NUM -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_NUM );  
   print_r ($result );  
  
   print( "\n---------- PDO::FETCH_BOTH -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_BOTH );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_LAZY -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_LAZY );  
   print_r( $result );  
  
   print( "\n---------- PDO::FETCH_OBJ -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $result = $stmt->fetch( PDO::FETCH_OBJ );  
   print $result->Name;  
   print( "\n \n" );  
  
   print( "\n---------- PDO::FETCH_BOUND -------------\n" );  
   $stmt = $conn->query( "select * from Person.ContactType where ContactTypeID < 5 " );  
   $stmt->bindColumn('Name', $name);  
   $result = $stmt->fetch( PDO::FETCH_BOUND );  
   print $name;  
   print( "\n \n" );  
?>  
```  
  
## <a name="see-also"></a>参照  
[PDOStatement クラス](../../connect/php/pdostatement-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
