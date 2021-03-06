---
title: "Lenguaje de expresiones regulares: referencia rápida"
description: "Lenguaje de expresiones regulares: referencia rápida"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/28/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 8c5dee8c-7bc7-4e6e-aff1-986965c4d98e
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: a6644fc2431beafa2128287eeac73bd598ee304a
ms.lasthandoff: 03/02/2017

---

# <a name="regular-expression-language---quick-reference"></a>Lenguaje de expresiones regulares: referencia rápida

Una expresión regular es un modelo con el que el motor de expresiones regulares intenta buscar una coincidencia en el texto de entrada. Un modelo consta de uno o más literales de carácter, operadores o estructuras. Para obtener una breve introducción, consulte [Expresiones regulares en .NET](regular-expressions.md). 

Cada sección de esta referencia rápida enumera una categoría determinada de caracteres, operadores y construcciones que puede usar para definir expresiones regulares: 

* [Escapes de carácter](#character-escapes)

* [Clases de carácter](#character-classes)
      
* [Delimitadores](#anchors)
    
* [Construcciones de agrupamiento](#grouping-constructs)
      
* [Cuantificadores](#quantifiers)
    
* [Construcciones de referencia inversa](#backreference-constructs)
      
* [Construcciones de alternancia](#alternation-constructs)
     
* [Sustituciones](#substitutions)
      
* [Opciones de expresiones regulares](#regular-expression-options)
      
* [Construcciones misceláneas](#miscellaneous-constructs)

Esta información también se proporciona en dos formatos que se puede descargar e imprimir para facilitar su consulta: 

* [Descarga en formato Word (.docx)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)
    
* [Descarga en formato PDF (.pdf)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)
    
## <a name="character-escapes"></a>Escapes de carácter

El carácter de barra diagonal inversa (\) en una expresión regular indica que el carácter que le sigue es un carácter especial (como se muestra en la tabla siguiente) o que se debe interpretar literalmente. Para obtener más información, consulte [Escapes de carácter en expresiones regulares](escapes.md). 

Carácter de escape | Descripción | Modelo | Coincidencias
----------------- | ----------- | ------- | -------
**\a** | Coincide con un carácter de campana, \u0007. | `\a` | "\u0007" en "¡Error!" + '\u0007'
**\b** | En una clase de caracteres, coincide con un retroceso, \u0008. | `[\b]{3,}` | "\b\b\b\b" en "\b\b\b\b"
**\t** | Coincide con una tabulación, \u0009. | `(\w+)\t` | "artículo1\t", "artículo2\t" en "artículo1\tartículo2\t"
**\r** | Coincide con un retorno de carro, \u000D. (**\r** no es equivalente al carácter de nueva línea, **\n**). | `\r\n(\w+)` | "\r\nEstas" en "\r\nEstas son\ndos líneas."
**\v** | Coincide con una tabulación vertical, \u000B. | `[\v]{2,}` | "\v\v\v" en "\v\v\v"
**\f** | Coincide con un avance de página, \u000C. | `[\f]{2,}` | "\f\f\f" en "\f\f\f" 
**\n** | Coincide con una nueva línea, \u000A. | `\r\n(\w+)` | "\r\nEstas" en "\r\nEstas son\ndos líneas."
**\e** | Coincide con un escape, \u001B. | `\e` | "\x001B" en "\x001B"
**\**_nnn_ | Usa la representación octal para especificar un carácter (*nnn* consta de dos o tres dígitos). | `\w\040\w` | "a b", "c d" en "a bc d"
**\x**_nn_ | Usa la representación hexadecimal para especificar un carácter (*nn* consta de exactamente dos dígitos). | `\w\x20\w` | "a b", "c d" en "a bc d"
**\c**_X_ o **\c**_x_ | Coincide con el carácter de control ASCII especificado por *X* o *x*, donde *X* o *x* es la letra del carácter de control. | `\cC` | "\x0003" en "\x0003" (Ctrl-C) 
**\u**_nnnn_ | Coincide con un carácter Unicode mediante el uso de la representación hexadecimal (exactamente cuatro dígitos, según representa *nnnn*). | `\w\u0020\w` | "a b", "c d" en "a bc d"
**\\** | Cuando va seguido de un carácter que no se reconoce como un carácter de escape en esta y otras tablas de este tema, coincide con ese carácter. Por ejemplo, __\*__ es igual que **\x2A**, y **\.** es igual que **\x2E**. Esto permite que el motor de expresiones regulares elimine la ambigüedad de los elementos del lenguaje (como `*` o `?`) y los literales de carácter (representados por `\*` o `\?)`). | `\d+[\+-x\*]\d+` | "2+2" y "3*9" en "(2+2) * 3*9"
 
## <a name="character-classes"></a>Clases de carácter

Una clase de caracteres coincide con cualquiera de un juego de caracteres. Las clases de caracteres incluyen los elementos del lenguaje enumerados en la tabla siguiente. Para obtener más información, consulte [Clases de carácter en expresiones regulares](classes.md).

Clase de carácter | Descripción | Modelo | Coincidencias
--------------- | ----------- | ------- | ------- 
__[__*grupo_caracteres*__]__ | Coincide con cualquier carácter individual de grupo_caracteres. De forma predeterminada, la coincidencia distingue entre mayúsculas y minúsculas. | `[ae]` | "a" en "gray", "a", "e" en "lane"
__[^__*grupo_caracteres*__]__ | Negación: coincide con cualquier carácter individual que no esté en *grupo_caracteres*. De forma predeterminada, los caracteres de *grupo_caracteres* distinguen mayúsculas de minúsculas. | `[^aei]` |  "r", "n", "o" en "reino"
__[__*primero-último*__]__ | Intervalo de caracteres: coincide con cualquier carácter individual en el intervalo de *primero* a *último*. | `[A-Z]` | "A", "B" en "AB123"
**.** | Carácter comodín: coincide con cualquier carácter excepto con \n. Para coincidir con un carácter de punto literal (. o \u002E), debe anteponerle el carácter de escape (\.). | `a.e` |  "ave" en "nave", "ate" en "water"
__\p{__*nombre*__}__ | Coincide con cualquier carácter individual que pertenezca a la categoría general Unicode o al bloque con nombre especificado por *nombre*. | `\p{Lu}`, `\p{IsCyrillic}` | "C", "L" en "City Lights", "?", "?" en "??em"
__\P{__*nombre*__}__ | Coincide con cualquier carácter individual que no pertenezca a la categoría general Unicode o al bloque con nombre especificado por *nombre*. | `\P{Lu}`, `\P{IsCyrillic}` |"i", "t", "y" en "City", "e", "m" en "??em"
**\w** | Coincide con cualquier carácter de una palabra. | `\w` | "I", "D", "A", "1", "3" en "ID A1.3" 
**\W** | Coincide con cualquier carácter que no pertenezca a una palabra. | `\W` | " ", "." en "ID A1.3"
**\s** | Coincide con cualquier carácter que sea un espacio en blanco. | `\w\s` | "D " en "ID A1.3"
**\S** | Coincide con cualquier carácter que no sea un espacio en blanco. | `\s\S` | " _" en "int __ctr" 
**\d** | Coincide con cualquier dígito decimal. | `\d` | "4" en "4 = IV" 
**\D** | Coincide con cualquier carácter que no sea un dígito decimal. | `\D` | " ", "=", " ", "I", "V" en "4 = IV" 

## <a name="anchors"></a>Delimitadores

Los delimitadores, o aserciones atómicas de ancho cero, hacen que una coincidencia tenga éxito o no dependiendo de la posición actual en la cadena, pero no hacen que el motor avance por la cadena ni consuma caracteres. Los metacaracteres enumerados en la tabla siguiente son delimitadores. Para obtener más información, consulte [Delimitadores en expresiones regulares](anchors.md).

Aserción | Descripción | Modelo | Coincidencias
--------- | ----------- | ------- | ------- 
**^** | La coincidencia debe comenzar al principio de la cadena o de la línea. | `^\d{3}` | "901" en "901-333-"
**$** | La coincidencia se debe producir al final de la cadena o antes de **\n** al final de la línea o de la cadena. | `-\d{3}$` | "-333" en "-901-333"
**\A** | La coincidencia se debe producir al principio de la cadena. | `\A\d{3}` | "901" en "901-333-"
**\Z** | La coincidencia se debe producir al final de la cadena o antes de **\n** al final de la cadena. | `-\d{3}\Z` | "-333" en "-901-333"
**\z** | La coincidencia se debe producir al final de la cadena. | `-\d{3}\z` | "-333" en "-901-333"
**\G** | La coincidencia se debe producir en el punto en el que finalizó la coincidencia anterior. | `\G\(\d\)` | "(1)", "(3)", "(5)" en "(1)(3)(5)[7]&#40;9)"
**\b** | La coincidencia se debe producir en un límite entre un carácter **\w** (alfanumérico) y un carácter **\W** (no alfanumérico). | `\b\w+\s\w+\b` | "ellos ello", "ellos ellos" en "ellos ello ellos ellos" 
**\B** | La coincidencia no se debe producir en un límite **\b**. | `\Bend\w*\b` | "fin", "final" en "finalizar finalista finalizador finalizó"

## <a name="grouping-constructs"></a>Construcciones de agrupamiento

Las construcciones de agrupamiento definen subexpresiones de una expresión regular y, normalmente, capturan subcadenas de una cadena de entrada. Las construcciones de agrupamiento incluyen los elementos del lenguaje enumerados en la tabla siguiente. Para obtener más información, consulte [Construcciones de agrupamiento en expresiones regulares](grouping.md).

Construcción de agrupamiento | Descripción | Modelo | Coincidencias
------------------ | ----------- | ------- | ------- 
**(**_subexpresión_**)** | Captura la subexpresión coincidente y le asigna un número ordinal basado en uno. | `(\w)\1` | "aa" en "aarón"
**(?**<name> _subexpresión_**)** | Captura la subexpresión coincidente en un grupo con nombre. | `(?<double>\w)\k<double>` | "aa" en "aarón"
**(?**<nombre1-nombre2> _subexpresión_**)** | Define una definición de grupo de equilibrio. Para obtener más información, consulte la sección [Definiciones de grupos de equilibrio](grouping.md#balancing-group-definitions) en [Construcciones de agrupamiento en expresiones regulares](grouping.md). | `(((?'Open'\()[^\(\)]*)+((?'Close-Open'\))[^\(\)]*)+)*(?(Open)(?!))$` | "((1-3)*(3-1))" en "3+2^((1-3)*(3-1))"
**(?**: subexpresión**)** | Define un grupo sin captura. | `Write(?:Line)?` | "WriteLine" en "Console.WriteLine()", "Write" en "Console.Write(value)"
**(?imnsx-imnsx**: _subexpresión_**)** | Aplica o deshabilita las opciones especificadas dentro de _subexpresión_. Para obtener más información, consulte [Opciones de expresiones regulares](options.md). | `A\d{2}(?i:\w+)\b` | "A12xl", "A12XL" en "A12xl A12XL a12xl"
**(?**= _subexpresión_**)** | Aserción de búsqueda anticipada positiva de ancho cero. | `\w+(?=\.)` | "es", "corría" y "hermoso" en "Él es. El perro corría. El sol está hermoso."
**(?!** _subexpresión_**)** | Aserción de búsqueda anticipada negativa de ancho cero. | `\b(?!un)\w+\b` | "seguro", "usado" en "aseguro seguro unidad usado"
**(?**<= _subexpresión_**)** | Aserción de búsqueda tardía positiva de ancho cero. | `(?<=19)\d{2}\b` | "99", "50", "05" en "1851 1999 1950 1905 2003"
**(?**<! _subexpresión_**)** | Aserción de búsqueda tardía negativa de ancho cero. | `(?<!19)\d{2}\b` | "51", "03" en "1851 1999 1950 1905 2003"
**(?**> _subexpresión_**)** | Subexpresión sin retroceso (o "expansiva"). | `[13579](?>A+B+)` | "1ABB", "3ABB" y "5AB" en "1ABB 3ABBC 5AB 5AC"

## <a name="quantifiers"></a>Cuantificadores

Un cuantificador especifica cuántas instancias del elemento anterior (que puede ser un carácter, un grupo o una clase de caracteres) debe haber en la cadena de entrada para que se encuentre una coincidencia. Los cuantificadores incluyen los elementos del lenguaje enumerados en la tabla siguiente. Para obtener más información, consulte [Cuantificadores en expresiones regulares](quantifiers.md).

Cuantificador | Descripción | Modelo | Coincidencias
---------- | ----------- | ------- | -------
__*__ | Coincide con el elemento anterior cero o más veces. | `\d*\.\d` | ".0", "19.9", "219.9"
**+** | Coincide con el elemento anterior una o más veces. | `"be+"` | "caí" en "caída", "be" en "bebé"
**?** | Coincide con el elemento anterior cero veces o una vez. | `"rai?n"` | "rata", "raicilla"
**{**_n_**}** | Coincide con el elemento anterior exactamente *n* veces. | `",\d{3}"` | ",043" en "1,043.6", ",876", ",543", y ",210" en "9,876,543,210"
**{**_n_,**}** | Coincide con el elemento anterior al menos *n* veces. | `"\d{2,}"` | "166", "29", "1930"
**{**_n_,_m_**}** | Coincide con el elemento anterior al menos *n* veces, pero no más de *m* veces. | `"\d{3,5}"` | "166", "17668"; "19302" en "193024"
__*?__ | Coincide con el elemento anterior cero o más veces, pero el menor número de veces que sea posible. | `\d*?\.\d` | ".0", "19.9", "219.9"
**+?** | Coincide con el elemento anterior una o más veces, pero el menor número de veces que sea posible. | `"be+?"` | "be" en "bebida", "be" en "bebé"
**??** | Coincide con el elemento anterior cero o una vez, pero el menor número de veces que sea posible. | `"rai??n"` | "rata", "raicilla"
**{**_n_**}?** | Coincide con el elemento precedente exactamente *n* veces. | `",\d{3}?"` | ",043" en "1,043.6", ",876", ",543", y ",210" en "9,876,543,210"
**{**_n_,**}?** | Coincide con el elemento anterior al menos *n* veces, pero el menor número de veces posible. | `"\d{2,}?"` | "166", "29", "1930"
**{**_n_,_m_**}?** | Coincide con el elemento anterior entre *n* y *m* veces, pero el menor número de veces posible. | `"\d{3,5}?"` | "166", "17668"; "193", "024" en "193024"

## <a name="backreference-constructs"></a>Construcciones de referencia inversa

Una referencia inversa permite identificar una subexpresión coincidente previamente más adelante en la misma expresión regular. En la tabla siguiente se enumeran las construcciones de referencia inversa admitidas en las expresiones regulares de .NET Framework. Para obtener más información, consulte [Construcciones de referencia inversa en expresiones regulares](backreference.md).

Construcción de referencias inversas | Descripción | Modelo | Coincidencias
----------------------- | ----------- | ------- | -------
**\**_número_ | Referencia inversa. Coincide con el valor de una subexpresión numerada. | `(\w)\1    ` | "aa" en "aarón"
**\k<**_nombre_**>** | Referencia inversa con nombre Coincide con el valor de una expresión con nombre. | `(?<char>\w)\k<char>` | "aa" en "aarón"

## <a name="alternation-constructs"></a>Construcciones de alternancia

Las estructuras de alternancia modifican una expresión regular para habilitar o no la coincidencia. Estas construcciones incluyen los elementos del lenguaje enumerados en la tabla siguiente. Para obtener más información, consulte [Construcciones de alternancia en expresiones regulares](alternation.md).

Construcciones de alternancia | Descripción | Modelo | Coincidencias
--------------------- | ----------- | ------- | ------- 
**&#124;** | Coincide con cualquier elemento separado por el carácter de barra vertical (*&#124;). | `th(e*&#124;is*&#124;at)` | "el", "este" en "este es el día. "
__(?(__*expresión*__)__*sí*__&#124;__*no*__)__ | Coincide con *sí* si el patrón de expresión regular designado por *expresión* coincide. En caso contrario, coincide con la parte opcional *no*. *expresión* se interpreta como una aserción de ancho cero. | `(?(A)A\d{2}\b*&#124;\b\d{3}\b)` | "A10", "910" en "A10 C103 910"
**(?(**_nombre_**)**_sí_&#124;_no_**)** | Coincide con *sí* si *nombre*, un grupo de capturas con nombre o numerado, tiene una coincidencia. En caso contrario, coincide con la parte opcional *no*. | `(?<quoted>")?(?,(quoted).+?"*&#124;\S+\s)` | Dogs.jpg, "Yiska playing.jpg" en "Dogs.jpg "Yiska playing.jpg""

## <a name="substitutions"></a>Sustituciones

Las sustituciones son elementos del lenguaje de expresiones regulares que se admiten en modelos de reemplazo. Para obtener más información, consulte [Sustituciones en expresiones regulares](substitutions.md). Los metacaracteres enumerados en la tabla siguiente son aserciones atómicas de ancho cero.

Carácter | Descripción | Modelo | Modelo de reemplazo | Cadena de entrada | Cadena de resultado
--------- | ----------- | ------- | ------------------- | ------------ | ------------- 
**$**_número_ | Sustituye la subcadena que coincide con el grupo *número*. | `\b(\w+)(\s)(\w+)\b` | `$3$2$1` | "one two" | "two one"
**${**_nombre_**}** | Sustituye la subcadena que coincide con el grupo con nombre *nombre*. | `\b(?<word1>\w+)(\s)(?<word2>\w+)\b` | `${word2} ${word1}` | "one two" | "two one"
**$$** | Sustituye un "$" literal. | `\b(\d+)\s?USD` | `$$$1` | "103 USD" | "$103"
**$&** | Sustituye una copia de toda la coincidencia. | `\$?\d*\.?\d+` | `**$&**` | "$1.30" | "**$1.30**"
**$`** | Sustituye todo el texto de la cadena de entrada delante de la coincidencia. | `B+` | `$`` | "AABBCC" | "AAAACC"
**$'** | Sustituye todo el texto de la cadena de entrada detrás de la coincidencia. | `B+` | `$'` | "AABBCC" | "AACCCC"
**$+** | Sustituye el último grupo capturado. | `B+(C+)` | `$+` | "AABBCCDD" | "AACCDD"
**$_** | Sustituye toda la cadena de entrada. | `B+` | `$_` | "AABBCC" | "AAAABBCCCC"

## <a name="regular-expression-options"></a>Opciones de expresiones regulares

Puede especificar opciones que controlen cómo debe interpretar el motor de expresiones regulares un patrón de expresión regular. Muchas de estas opciones pueden especificarse alineadas (en el patrón de expresión regular) o como una o más constantes de `RegexOptions`. Esta referencia rápida solo muestra las opciones alineadas. Para obtener más información sobre las opciones alineadas y `RegexOptions`, consulte el artículo [Opciones de expresiones regulares](options.md). 

Puede especificar una opción alineada de dos formas:

* Con la construcción miscelánea **(?imnsx-imnsx)**, donde el signo menos (-) delante de una opción o un conjunto de opciones desactiva dichas opciones. Por ejemplo, **(?i-mn)** activa una coincidencia que no distingue mayúsculas de minúsculas (i), desactiva el modo multilínea (**m**) y desactiva las capturas de grupo sin nombre (**n**). La opción se aplica al patrón de expresión regular a partir del punto en el que esta se define y es efectiva hasta el final del patrón o hasta el punto en el que otro constructor invierte la opción.

* Con la construcción de agrupamiento **(?imnsx-imnsx:**_subexpresión_**)**, que define opciones solo para el grupo especificado.

El motor de expresiones regulares de .NET admite las siguientes opciones insertadas.

Opción | Descripción | Modelo | Coincidencias
------ | ----------- | ------- | ------- 
**i** | Usa la coincidencia sin distinción entre mayúsculas y minúsculas. | **\b(?i)a(?-i)a\w+\b** | "aardvark", "aaaAuto" en "aardvark AAAuto aaaAuto Adam breakfast" 
**m** | Usa el modo multilínea. **^** y **$** coinciden con el principio y el final de una línea, en lugar del principio y el final de una cadena. | Para obtener un ejemplo, consulte la sección "Modo multilínea" en [Opciones de expresiones regulares](options.md). | 
**n*** | No se capturan grupos sin nombre. | Para obtener un ejemplo, consulte la sección "Solo capturas explícitas" en [Opciones de expresiones regulares](options.md). | 
**s** | Usa el modo de una sola línea. | Para obtener un ejemplo, consulte la sección "Modo de una sola línea" en [Opciones de expresiones regulares](options.md). | 
**x** | Se omite el espacio en blanco sin escape en el patrón de expresión regular. | **\b(?x) \d+ \s \w+** | "1 aardvark", "2 cats" en "1 aardvark 2 cats IV centurions" 

##<a name="miscellaneous-constructs"></a>Construcciones misceláneas

Las estructuras misceláneas modifican un modelo de expresión regular o proporcionan información sobre él. En la tabla siguiente se enumeran las construcciones misceláneas admitidas por .NET. Para obtener más información, consulte [Construcciones misceláneas en expresiones regulares](miscellaneous.md).

Construcción | Definición | Ejemplo
--------- | ---------- | ------- 
**(?imnsx-imnsx)** | Establece o deshabilita opciones como la no distinción entre mayúsculas y minúsculas en medio de un modelo. Para obtener más información, consulte [Opciones de expresiones regulares](options.md). | `\bA(?i)b\w+\b` coincide con "ABA", "Able" en "ABA Able Act"
**(?#** _comentario_**)** | Comentario alineado. El comentario termina en el primer paréntesis de cierre. | `\bA(?#` coincide con palabras que empiezan por `A)\w+\b`
**#** [hasta el final de la línea] | Comentario en modo X. El comentario comienza en un carácter # sin escape y continúa hasta el final de la línea. | `(?x)\bA\w+\b#` coincide con palabras que empiezan por `A`

## <a name="see-also"></a>Vea también




[System.Text.RegularExpressions](xref:System.Text.RegularExpressions)

[Regex](xref:System.Text.RegularExpressions.Regex)

[Expresiones regulares en .NET](regular-expressions.md)

[El modelo de objetos de expresión regular](object-model.md)

[Ejemplos de expresiones regulares](regex-examples.md)

[Descarga en formato Word (.docx)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.docx)
    
[Descarga en formato PDF (.pdf)](http://download.microsoft.com/download/D/2/4/D240EBF6-A9BA-4E4F-A63F-AEB6DA0B921C/Regular%20expressions%20quick%20reference.pdf)

