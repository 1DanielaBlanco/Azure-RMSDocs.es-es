---
title: clase mip Stream
description: Referencia de la clase mip Stream
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: e6296c5e15590741e008979dcf12373ff5fcdf00
ms.sourcegitcommit: 1cf14852cd14ea91ac964fb03a901238455ffdff
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2018
ms.locfileid: "47445230"
---
# <a name="class-mipstream"></a>clase mip::Stream 
Una clase que define la interfaz entre el SDK de MIP y el contenido basado en el flujo.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public int64_t Read(uint8_t* buffer, int64_t bufferLength)  |  Lee en un búfer desde el flujo.
 public int64_t Write(const uint8_t* buffer, int64_t bufferLength)  |  Escribe en el flujo desde un búfer.
 public bool Flush()  |  Vacía el flujo.
 public void Seek(int64_t position)  |  Busca la posición específica en el flujo.
 public bool CanRead() const  |  Una comprobación de si se puede leer la secuencia.
 public bool CanWrite() const  |  Una comprobación de si se puede escribir en la secuencia.
 public int64_t Position()  |  Obtiene la posición actual en el flujo.
 public int64_t Size()  |  Obtiene el tamaño del contenido dentro del flujo.
 public void Size(int64_t value)  |  Establece el tamaño del flujo.
  
## <a name="members"></a>Miembros
  
### <a name="read"></a>Lectura
Lee en un búfer desde el flujo.

Parámetros:  
* **buffer**: puntero a un búfer 


* **bufferLength**: tamaño del búfer. 



  
**Devuelve**: el número de bytes leídos.
  
### <a name="write"></a>Escribir
Escribe en el flujo desde un búfer.

Parámetros:  
* **buffer**: puntero a un búfer 


* **bufferLength**: tamaño del búfer. 



  
**Devuelve**: el número de bytes escritos.
  
### <a name="flush"></a>Vaciar
Vacía el flujo.

  
**Devuelve**: true si es correcto; en caso contrario, false.
  
### <a name="seek"></a>Seek
Busca la posición específica en el flujo.

Parámetros:  
* **position**: para buscar en el flujo.


  
### <a name="canread"></a>CanRead
Una comprobación de si se puede leer la secuencia.

  
**Devuelve**: true si se puede leer; en caso contrario, false.
  
### <a name="canwrite"></a>CanWrite
Una comprobación de si se puede escribir en la secuencia.

  
**Devuelve**: true si se puede escribir; en caso contrario, false.
  
### <a name="position"></a>Posición
Obtiene la posición actual en el flujo.

  
**Devuelve**: posición en el flujo.
  
### <a name="size"></a>Tamaño
Obtiene el tamaño del contenido dentro del flujo.

  
**Devuelve**: el tamaño del flujo.
  
### <a name="size"></a>Tamaño
Establece el tamaño del flujo.

Parámetros:  
* **stream**: tamaño.

