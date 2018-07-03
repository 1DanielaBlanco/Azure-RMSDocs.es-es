# <a name="class-mipcontentlabel"></a>clase mip::ContentLabel 
Abstracción para una etiqueta de Microsoft Information Protection que se aplica a un fragmento de contenido, normalmente un documento.
Además de la información de la etiqueta, contiene propiedades para una etiqueta aplicada específica.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public const std::string& GetCreationTime() const  |  Obtiene la hora de creación de la solicitud.
 public AssignmentMethod GetAssignmentMethod() const  |  Obtiene el método de asignación de la etiqueta.
public std::shared_ptr<Label> GetLabel() const  |  Obtiene el objeto de la etiqueta real que se aplica en el contenido.
  
## <a name="members"></a>Miembros
  
### <a name="getcreationtime"></a>GetCreationTime
Obtiene la hora de creación de la solicitud.

  
**Devuelve**: hora de creación como una cadena gmt.
  
### <a name="getassignmentmethod"></a>GetAssignmentMethod
Obtiene el método de asignación de la etiqueta.

  
**Devuelve**: AssignmentMethod STANDARD | PRIVILEGED | AUTO. 
  
**Consulte también**: mip::AssignmentMethod
  
### <a name="label"></a>Etiqueta
Obtiene el objeto de la etiqueta real que se aplica en el contenido.

  
**Devuelve**: el objeto de la etiqueta que se aplica en el contenido. 
  
**Consulte también**: [mip::Label](class_mip_label.md)