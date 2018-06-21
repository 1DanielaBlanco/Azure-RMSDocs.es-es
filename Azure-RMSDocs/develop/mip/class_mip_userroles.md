# <a name="class-mipuserroles"></a>clase mip::UserRoles 
Representa un grupo de usuarios y los roles asociados con ellos.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
 public MIP_EXPORT UserRoles(const UserList& users, const RoleList& roles)  |  Constructor [UserRoles](class_mip_userroles.md).
 public const UserList& Users() const  |  Obtiene los usuarios asociados a un conjunto de roles.
 public const RoleList& Roles() const  |  Obtiene los roles asociados a un grupo de usuarios.
  
## <a name="members"></a>Miembros
  
### <a name="userroles"></a>UserRoles
Constructor [UserRoles](class_mip_userroles.md).

Parámetros:  
* **users**: grupo de usuarios que comparten los mismos roles 


* **roles**: [roles](class_mip_roles.md) compartidos por grupo de usuarios


  
### <a name="userlist"></a>UserList
Obtiene los usuarios asociados a un conjunto de roles.

  
**Devuelve**: usuarios asociados a un conjunto de roles
  
### <a name="rolelist"></a>RoleList
Obtiene los roles asociados a un grupo de usuarios.

  
**Devuelve**: [roles](class_mip_roles.md) asociados a un grupo de usuarios