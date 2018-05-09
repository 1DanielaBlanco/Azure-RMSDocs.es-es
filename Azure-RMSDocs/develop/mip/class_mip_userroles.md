# <a name="class-mipuserroles"></a>clase mip::UserRoles 
Representa un grupo de usuarios y los roles asociados con ellos.
  
## <a name="summary"></a>Resumen
 Miembros                        | Descripciones                                
--------------------------------|---------------------------------------------
public MIP_EXPORT UserRoles(const UserList& users, const RoleList& roles)  |  Constructor [UserRoles](#classmip_1_1_user_roles).
public inline const UserList& Users() const  |  Obtiene los usuarios asociados a un conjunto de roles.
public inline const RoleList& Roles() const  |  Obtiene los roles asociados a un grupo de usuarios.
  
## <a name="members"></a>Miembros
  
### <a name="userroles"></a>UserRoles
Constructor [UserRoles](#classmip_1_1_user_roles).
  
#### <a name="parameters"></a>Parámetros
* users Grupo de usuarios que comparten los mismos roles 
* roles [Roles](#classmip_1_1_roles) compartidos por grupo de usuarios
  
### <a name="userlist"></a>UserList
Obtiene los usuarios asociados a un conjunto de roles.
  
#### <a name="returns"></a>Devuelve
Usuarios asociados a un conjunto de roles
  
### <a name="rolelist"></a>RoleList
Obtiene los roles asociados a un grupo de usuarios.
  
#### <a name="returns"></a>Devuelve
[Roles](#classmip_1_1_roles) asociados a un grupo de usuarios