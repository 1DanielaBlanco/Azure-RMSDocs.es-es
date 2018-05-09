# <a name="class-mipfilehandlerobserver"></a>clase mip::FileHandler::Observer 
Interfaz de [Observer](#classmip_1_1_file_handler_1_1_observer) para que los clientes obtengan notificaciones de eventos relacionados con el controlador de archivos.
Si *se produce el evento de error, el objeto de error se almacena en la clase [mip::Error](#classmip_1_1_error). El cliente no debe volver a llamar al motor en el subproceso que llama al observador.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public inline virtual ~Observer()  |  
public void OnGetLabelSuccess(const std::shared_ptr<ContentLabel>& label, const std::shared_ptr<void>& context)  |  Se llama cuando la etiqueta se recupera correctamente (desde el archivo).
public void OnGetLabelFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando la recuperación de la etiqueta (del archivo) no se realizó correctamente debido a un error.
public void OnGetProtectionSuccess(const std::shared_ptr<UserPolicy>& userPolicy, const std::shared_ptr<void>& context)  |  Se llama cuando la directiva de protección se recupera correctamente (desde el archivo).
public void OnGetProtectionFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando la recuperación de la directiva de protección (del archivo) no se realizó correctamente debido a un error.
public void OnCommitSuccess(bool commited, const std::shared_ptr<void>& context)  |  Se llama cuando se realizó correctamente la confirmación de los cambios en el archivo.
public void OnCommitFailure(const std::exception_ptr& error, const std::shared_ptr<void>& context)  |  Se llama cuando se produce un error al confirmar los cambios en el archivo debido a un error.
protected inline Observer()  |  
  
## <a name="members"></a>Miembros
  
### <a name="observer"></a>~Observer
  
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