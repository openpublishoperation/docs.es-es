---
title: /win32icon | Documentos de Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- win32icon compiler option [Visual Basic]
- -win32icon compiler option [Visual Basic]
- /win32icon compiler option [Visual Basic]
ms.assetid: aecaab01-9353-46c5-941c-6edabd4eff92
caps.latest.revision: 13
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 110a3861d6628dc2c3fb251aaa31762fb94f04c9
ms.lasthandoff: 03/13/2017

---
# <a name="win32icon"></a>/win32icon
Inserta un archivo .ico en el archivo de salida. Este archivo .ico representa el archivo de salida en **Explorador de archivos**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
/win32icon:filename  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Término|Definición|  
|---|---|  
|`filename`|El archivo .ico para agregar al archivo de salida. Encierre el nombre de archivo entre comillas ("") si contiene espacios.|  
  
## <a name="remarks"></a>Comentarios  
 Puede crear un archivo .ico con el compilador de recursos de Microsoft Windows (RC). El compilador de recursos se invoca cuando se compila un programa de Visual C++; se crea un archivo .ico en el archivo .rc. El `/win32icon` y `/win32resource` opciones son mutuamente excluyentes.  
  
 Consulte [/linkresource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/linkresource.md) para hacer referencia a un [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] archivo de recursos, o [/resource (Visual Basic)](../../../visual-basic/reference/command-line-compiler/resource.md) para adjuntar un [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] archivo de recursos. Consulte [/win32resource](../../../visual-basic/reference/command-line-compiler/win32resource.md) para importar un archivo. res.  
  
|Para establecer /win32icon en el IDE de Visual Studio|  
|---|  
|1.  Seleccione un proyecto en el **Explorador de soluciones**. En el **proyecto** menú, haga clic en **propiedades**. Para obtener más información, consulte [Introducción al Diseñador de proyectos](http://msdn.microsoft.com/en-us/898dd854-c98d-430c-ba1b-a913ce3c73d7).<br />2.  Haga clic en la pestaña **Aplicación** .<br />3.  Modifique el valor en el **icono** cuadro.|  
  
## <a name="example"></a>Ejemplo  
 El siguiente código compila `In.vb` y adjunta un archivo .ico, `Rf.ico`.  
  
```  
vbc /win32icon:rf.ico in.vb  
```  
  
## <a name="see-also"></a>Vea también  
 [Compilador de línea de comandos de Visual Basic](../../../visual-basic/reference/command-line-compiler/index.md)   
 [Líneas de comandos de compilación de ejemplo](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
