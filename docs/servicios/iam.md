# IAM

> Aquellos métodos que dentro del body contengan la palabra Optional, significa el el payload puede contener o no dicha llave

[Endpoint](https://48hfhzfcfe.execute-api.us-east-2.amazonaws.com/v1) :point_left:

## Usuarios

> Path: /users

Método GET

```Query strings
        {
            Optional("uuid"): Use(int),
            Optional("email"): And(str, Use(lambda e: e.lower())),
            Optional("uname"): And(str, Use(lambda e: e.lower())),
            Optional("doc_id"): str,
            Optional("page", default=1): And(
                Use(int),
                lambda n: n > 0,
                error="'page' debe ser un numero entero mayor a cero"
            ),
            Optional("sortBy", default="uuid"): And(
                str,
                lambda w: len(w) > 0,
                error="'sortBy' no debe ser vacio"
            ),
            Optional("limit", default=10): And(
                Use(int),
                lambda n: n >= 0,
                error="'limit' debe ser un numero entero mayor o igual a cero"
            ),
        }
```

Método POST

```json
        {
            Optional("id_name"): str,
            "email": And(str, Use(lambda e: e.lower())),
            "uname": str,
            "doc_id": str,
            "doc_type_id": Use(int),
            "phone": str,
            "direccion": str,
            Optional("active"): Use(bool),
        }
```

Método PUT

```Query strings
        {
            "uuid": Use(int),
            Optional("email"): And(str, Use(lambda e: e.lower())),
        }
```

```json
        {
            Optional("uname"): str,
            Optional("doc_id"): str,
            Optional("doc_type_id"): Use(int),
            Optional("phone"): str,
            Optional("direccion"): str,
            Optional("active"): Use(bool)
        }
```

### Creación masiva usuarios

Método POST

Solicita un archivo con estructura

```json
    file = request.files.get("file")
```

## Roles

> Path: /roles

Método GET

```Query strings

        {
            Optional("id_role"): Use(int),
            Optional("name_role"): And(str, Use(lambda e: e.lower())),
            Optional("page", default=1): And(
                Use(int),
                lambda n: n > 0,
                error="'page' debe ser un numero entero mayor a cero"
            ),
            Optional("sortBy", default="id_role"): And(
                str,
                lambda w: len(w) > 0,
                error="'sortBy' no debe ser vacio"
            ),
            Optional("limit", default=10): And(
                Use(int),
                lambda n: n >= 0,
                error="'limit' debe ser un numero entero mayor a cero"
            ),
        }
```

Método POST

```json
        {
            Optional("id_name"): str,
            "name_role": str,
        }
```

## Permisos

> Path: /permissions

Método GET

```Query strings
        {
            Optional("id_permission"): Use(int),
            Optional("name_permission"): And(str, Use(lambda e: e.lower())),
            Optional("page", default=1): And(
                Use(int),
                lambda n: n > 0,
                error="'page' debe ser un numero entero mayor a cero"
            ),
            Optional("sortBy", default="id_permission"): And(
                str,
                lambda w: len(w) > 0,
                error="'sortBy' no debe ser vacio"
            ),
            Optional("limit", default=10): And(
                Use(int),
                lambda n: n >= 0,
                error="'limit' debe ser un numero entero mayor a cero"
            ),
        }
```

Método POST

```json
        {
            Optional("id_name"): str,
            Optional("id_permission"): Use(int),
            "name_permission": Use(str),
            Optional("routes"): dict,
        }
```

Método PUT

```Query strings
        {
            "id_permission": Use(int),
        }
```

```json
        {
            Optional("name_permission"): Use(str),
        }
```

## Grupos

> Path: /groups

Método GET

```Query strings
        {
            Optional("id_group"): Use(int),
            Optional("name_group"): And(str, Use(lambda e: e.lower())),
            Optional("page", default=1): And(
                Use(int),
                lambda n: n > 0,
                error="'page' debe ser un numero entero mayor a cero"
            ),
            Optional("sortBy", default="id_group"): And(
                str,
                lambda w: len(w) > 0,
                error="'sortBy' no debe ser vacio"
            ),
            Optional("limit", default=10): And(
                Use(int),
                lambda n: n >= 0,
                error="'limit' debe ser un numero entero mayor a cero"
            ),
        }
```

Método POST

```json
        {
            Optional("id_name"): str,
            "name_group": str,
        }
```

Debido a que el sistema funciona de forma similar a como funciona IAM de AWS se proporcionan mas métodos que relacionan entre usuarios, permisos, grupos y roles

> Path: /users-groups

Método GET

```Query strings
        {
            Optional("Users_uuid"): Use(int),
            Optional("Groups_id_group"): Use(int),
        }
```

Método POST

```json
        {
            "Users_uuid": Use(int),
            "Groups_id_group": Use(int),
        }
```

Método DELETE

```Query strings
        {
            "Users_uuid": Use(int),
            "Groups_id_group": Use(int),
        }
```

> Path: /groups-roles

Método GET

```Query strings
        {
            Optional("Groups_id_group"): Use(int),
            Optional("Roles_id_role"): Use(int)
        }
```

Método POST

```json
        {
            "Groups_id_group": Use(int),
            "Roles_id_role": Use(int),
        }
```

Método DELETE

```Query strings
        {
            "Groups_id_group": Use(int),
            "Roles_id_role": Use(int),
        }
```

> Path: /roles-permissions

Método GET

```Query strings
        {
            Optional("Permissions_id_permission"): Use(int),
            Optional("Roles_id_role"): Use(int),
        }
```

Método POST

```json
        {
            "Permissions_id_permission": Use(int),
            "Roles_id_role": Use(int),
        }
```

Método DELETE

```Query strings
        {
            "Permissions_id_permission": Use(int),
            "Roles_id_role": Use(int),
        }
```

> Path: /permissions-opstrx

Método GET

```Query strings
        {
            Optional("Permissions_id_permission"): Use(int),
            Optional("Tipos_operaciones_id_tipo_op"): Use(int),
        }
```

Método POST

```json
        {
            "Permissions_id_permission": Use(int),
            "Tipos_operaciones_id_tipo_op": Use(int),
        }
```

Método DELETE

```json
        {
            "Permissions_id_permission": Use(int),
            "Tipos_operaciones_id_tipo_op": Use(int),
        }
```

> Path: /users-permissions

Método GET

> Path: /politicas

```Query strings
        {
            Optional("uuid"): Use(int),
            Optional("email"): And(str, Use(lambda e: e.lower())),
        }
```

Método GET

```Query strings
        {
            Optional("name_group"): And(str, Use(lambda e: e.lower())),
            Optional("name_role"): And(str, Use(lambda e: e.lower())),
        }
```
