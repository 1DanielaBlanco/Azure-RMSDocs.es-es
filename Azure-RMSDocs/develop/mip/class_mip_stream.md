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
public std::shared_ptr<Stream> Clone()  |  Clona el flujo.
  
## <a name="members"></a>Miembros
  
### <a name="read"></a>Lectura
Lee en un búfer desde el flujo.
  
#### <a name="parameters"></a>Parámetros
* puntero de búfer a un búfer 
* bufferLength Tamaño del búfer. 
  
#### <a name="returns"></a>Devuelve
Número de bytes leídos realmente.
  
### <a name="write"></a>Escribir
Escribe en el flujo desde un búfer.
  
#### <a name="parameters"></a>Parámetros
* puntero de búfer a un búfer 
* bufferLength Tamaño del búfer. 
  
#### <a name="returns"></a>Devuelve
Número de bytes leídos realmente.
  
### <a name="flush"></a>Vaciar
Vacía el flujo.
  
#### <a name="returns"></a>Devuelve
true si es correcto; en caso contrario, false.
  
### <a name="seek"></a>Seek
Busca la posición específica en el flujo.
  
#### <a name="parameters"></a>Parámetros
* Posición para buscar en el flujo.
  
### <a name="canread"></a>CanRead
Una comprobación de si el flujo es legible.
  
#### <a name="returns"></a>Devuelve
true si se puede leer; en caso contrario, false.
  
### <a name="canwrite"></a>CanWrite
Un cheque si el flujo se puede escribir.
  
#### <a name="returns"></a>Devuelve
true si se puede escribir; en caso contrario, false.
  
### <a name="position"></a>Posición
Obtiene la posición actual en el flujo.
  
#### <a name="returns"></a>Devuelve
Posición en el flujo.
  
### <a name="size"></a>Tamaño
Obtiene el tamaño del contenido dentro del flujo.
  
#### <a name="returns"></a>Devuelve
El tamaño del flujo.
  
### <a name="size"></a>Tamaño
Establece el tamaño del flujo.
  
#### <a name="parameters"></a>Parámetros
* El tamaño del flujo.
  
### <a name="stream"></a>Transmitir
Clona el flujo.
  
#### <a name="returns"></a>Devuelve
Nuevo flujo.