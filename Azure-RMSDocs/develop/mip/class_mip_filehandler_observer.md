# <a name="class-mipfilehandlerobserver"></a>clase mip::FileHandler::Observer 
Interfaz de [Observer](class_mip_filehandler_observer.md) para que los clientes obtengan notificaciones de eventos relacionados con el controlador de archivos.
Si *se produce el evento de error, el objeto de error se almacena en la clase [mip::Error](class_mip_error.md). El cliente no debe volver a llamar al motor en el subproceso que llama al observador.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public virtual ~Observer()  | _No se ha documentado todavía._
public virtual void OnCreateFileHandlerSuccess(const std::shared_ptr<FileHandler>& fileHandler, const std::shared_ptr<void>& context)  |  Se llama cuando el controlador se ha creado correctamente.
public virtual void OnCreateFileHandlerFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando no se pudo crear el controlador debido a un error.
public virtual void OnGetLabelSuccess(const std::shared_ptr<ContentLabel>& label, const std::shared_ptr<void>& context)  |  Se llama cuando la etiqueta se recupera correctamente (desde el archivo).
public virtual void OnGetLabelFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando la recuperación de la etiqueta (del archivo) no se realizó correctamente debido a un error.
public virtual void OnGetProtectionSuccess(const std::shared_ptr<ProtectionHandler>& protectionHandler, const std::shared_ptr<void>& context)  |  Se llama cuando la directiva de protección se recupera correctamente (desde el archivo).
public virtual void OnGetProtectionFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando la recuperación de la directiva de protección (del archivo) no se realizó correctamente debido a un error.
public virtual void OnCommitSuccess(bool committed, const std::shared_ptr<void>& context)  |  Se llama cuando se realizó correctamente la confirmación de los cambios en el archivo.
public virtual void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando se produce un error al confirmar los cambios en el archivo debido a un error.
 protected Observer()  | _No se ha documentado todavía._
  
## <a name="members"></a>Miembros
  
### <a name="observer"></a>~Observer
_No se ha documentado todavía._

  
### <a name="oncreatefilehandlersuccess"></a>OnCreateFileHandlerSuccess
Se llama cuando el controlador se ha creado correctamente.
  
### <a name="oncreatefilehandlerfailure"></a>OnCreateFileHandlerFailure
Se llama cuando no se pudo crear el controlador debido a un error.
  
### <a name="ongetlabelsuccess"></a>OnGetLabelSuccess
Se llama cuando la etiqueta se recupera correctamente (desde el archivo).
  
### <a name="ongetlabelfailure"></a>OnGetLabelFailure
Se llama cuando la recuperación de la etiqueta (del archivo) no se realizó correctamente debido a un error.
  
### <a name="ongetprotectionsuccess"></a>OnGetProtectionSuccess
Se llama cuando la directiva de protección se recupera correctamente (desde el archivo).
  
### <a name="ongetprotectionfailure"></a>OnGetProtectionFailure
Se llama cuando la recuperación de la directiva de protección (del archivo) no se realizó correctamente debido a un error.
  
### <a name="oncommitsuccess"></a>OnCommitSuccess
Se llama cuando se realizó correctamente la confirmación de los cambios en el archivo.
  
### <a name="oncommitfailure"></a>OnCommitFailure
Se llama cuando se produce un error al confirmar los cambios en el archivo debido a un error.
  
### <a name="observer"></a>Observador
_No se ha documentado todavía._
