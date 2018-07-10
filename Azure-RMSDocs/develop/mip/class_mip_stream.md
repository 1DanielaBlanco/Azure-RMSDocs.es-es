# <a name="class-mipstream"></a>clase mip::Stream 
Una clase que define la interfaz entre el SDK de MIP y el contenido basado en el flujo.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public int64_t Read(uint8_t* buffer, int64_t bufferLength)  |  Lee en un búfer desde el flujo.
 public int64_t Write(const uint8_t* buffer, int64_t bufferLength)  |  Escribe en el flujo desde un búfer.
 public bool Flush()  |  Vacía el flujo.
 public void Seek(uint64_t position)  |  Busca la posición específica en el flujo.
 public bool CanRead() const  |  Una comprobación de si el flujo es legible.
 public bool CanWrite() const  |  Un cheque si el flujo se puede escribir.
 public uint64_t Position()  |  Obtiene la posición actual en el flujo.
 public uint64_t Size()  |  Obtiene el tamaño del contenido dentro del flujo.
 public void Size(uint64_t value)  |  Establece el tamaño del flujo.
  
## <a name="members"></a>Miembros
  
### <a name="read"></a>Lectura
Lee en un búfer desde el flujo.

Parámetros:  
* **buffer**: puntero a un búfer 


* **bufferLength**: tamaño del búfer. 



  
**Devuelve**: número de bytes leídos realmente.
  
### <a name="write"></a>Escribir
Escribe en el flujo desde un búfer.

Parámetros:  
* **buffer**: puntero a un búfer 


* **bufferLength**: tamaño del búfer. 



  
**Devuelve**: número de bytes escritos realmente.
  
### <a name="flush"></a>Vaciar
Vacía el flujo.

  
**Devuelve**: true si es correcto; en caso contrario, false.
  
### <a name="seek"></a>Seek
Busca la posición específica en el flujo.

Parámetros:  
* **position**: para buscar en el flujo.


  
### <a name="canread"></a>CanRead
Una comprobación de si el flujo es legible.

  
**Devuelve**: true si se puede leer; en caso contrario, false.
  
### <a name="canwrite"></a>CanWrite
Un cheque si el flujo se puede escribir.

  
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

