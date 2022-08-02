# Cupo-comisiones

> Aquellos metodos que dentro del body contengan la palabra Optional, significa el el payload puede contener o no dicha llave

[Endpoint](https://48hfhzfcfe.execute-api.us-east-2.amazonaws.com/v1) :point_left:

Metodo POST

> Path: /cupo

aumenta o disminuye el cupo según como se envie el valor, si son valores negativos se resta cupo y si son positivos se suma

```json
        {
            Optional("id_trx"): Use(int),
            "id_comercio": Use(int),
            "id_usuario": Use(int),
            "id_terminal": Use(int),
            "valor": Use(float),
        }
```

## Aplicación comisiones

Metodo POST

> Path: /aplicacion_comision/consultar

Consulta la respectiva aplicación de las comisiones

```json
        {
            "id_comercio": Use(int),
            "id_usuario": Use(int),
            "id_terminal": Use(int),
            "valor": Use(float),
            Optional("id_trx",default=""):Use(int),
            Optional("id_tipo_op",default=""):Use(int),
            Optional("id_convenio",default=""):Use(int),
            Optional("type",default=1):Use(int),
        }
```

Metodo POST

> Path: /aplicacion_comision/retornar

Retorna la aplicación de comisiones en caso de error

```json
        {
            "id_trx":Use(int),
            "id_usuario":Use(int),
            "id_terminal":Use(int),
            "monto_trx":Use(float)
        }
```

Metodo POST

> Path: /aplicacion_comision/consultar_comision_comercio

Consulta aplicación de comisiones a comercios

```json
        {
            "id_comercio":Use(int),
        }
```

Metodo POST

> Path: /aplicacion_comision/cuadre_mensual_comisiones

Cuadre mensual de comisiones generado a oficinas o comercios _`Verificar`_

```json
        {
            "key":Use(str),
        }
```

## Autorizadores

Metodo POST

> Path: /autorizador/crear

Crear los respectivos autorizadores relacionados en la plataforma

```json
        {
            "id_tipo_contrato": Use(int),
            "nombre_autorizador": Use(str),
            "nit": Use(str),
            Optional("descripcion"): Use(str)
        }
```

Metodo POST

> Path: /autorizador/consultar_autorizadores

Consultar autorizadores relacionados en la plataforma

```json
        {
            Optional("id_tipo_contrato"): Use(int),
            Optional("id_autorizador"): Use(int),
            Optional("nombre_autorizador"): And(str, Use(lambda e: e.lower())),
            Optional("page", default=1): And(
                Use(int),
                lambda n: n > 0,
                error="'page' debe ser un numero entero mayor a cero"
            ),
            Optional("sortBy", default="id_autorizador"): And(
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

Metodo PUT

> Path: /autorizador/modificar

Modificar autorizadores de la plataforma

```Query strings
        {
            "id_autorizador": Use(int)
        }

```

```json
        {
            Optional("nombre_autorizador"): Use(str),
            Optional("id_tipo_contrato"): Use(int),
            Optional("nit"):  Use(str),
            Optional("descripcion"): Use(str)
        }
```

## Código de barras comercios

Metodo POST

> Path: /codigo_barras_comercio/generar

Generar respectivo código de barras para comercios

```json
        {
            "id_comercio": Use(str),
            "nombre_comercio": Use(str),
        }
```

## Comisiones

Metodo POST

> Path: /comision/crear

Crear parametrización de comisiones

```json
        {
            Optional("id_convenio"): Use(int),
            Optional("id_comercios"): Use(list),
            Optional("id_tipo_op"): Use(int),
            "id_autorizador": Use(int),
            Optional("nombre_comision"): Use(str),
            Optional("fecha_inicio"): Use(str),
            Optional("fecha_fin"): Use(str),
            "comisiones":dict
        }
```

Metodo POST

> Path: /comision/consultar_comisiones

Consultar comisión

```json
        {
            Optional("nombre_operacion"):And(str, Use(lambda e: e.lower())),
            Optional("nombre_convenio"):And(str, Use(lambda e: e.lower())),
            Optional("nombre_autorizador"):And(str, Use(lambda e: e.lower())),
            Optional("nombre_comision"):And(str, Use(lambda e: e.lower())),
            Optional("id_comision_pagada"): Use(int),
            Optional("id_convenio"): Use(int),
            Optional("id_comercio"): Use(int),
            Optional("id_autorizador"): Use(int),
            Optional("id_tipo_op"): Use(int),
            Optional("page", default=1): And(
                Use(int),
                lambda n: n > 0,
                error="'page' debe ser un numero entero mayor a cero"
            ),
            Optional("sortBy", default="id_comision_pagada"): And(
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

Metodo PUT

> Path: /comision/modificar

Modificar comisión

```Query strings
        {
            "id_comision_pagada": Use(int)
        }
```

```json
        {
            Optional("comisiones"): dict,
            Optional("fecha_inicio"): Use(str),
            Optional("fecha_fin"): Use(str),
            Optional("nombre_comision"): Use(str),
            Optional("estado"): Use(bool),
        }
```

## Comisiones cobradas

Metodo POST

> Path: /comisiones_cobradas/crear

Crear comision a cobrar

```json
        {
            "id_autorizador": Use(int),
            Optional("id_convenio"):Use(int),
            Optional("id_tipo_op"):Use(int),
            Optional("nombre_comision"):Use(str),
            "comisiones":dict,
        }
```

Metodo POST

> Path: /comisiones_cobradas/consultar_comision_cobrada

Consultar comisiones a cobrar

```json
        {
            Optional("nombre_autorizador"):And(str, Use(lambda e: e.lower())),
            Optional("nombre_convenio"):And(str, Use(lambda e: e.lower())),
            Optional("nombre_operacion"):And(str, Use(lambda e: e.lower())),
            Optional("nombre_comision"):And(str, Use(lambda e: e.lower())),
            Optional("id_comision_cobrada"): Use(int),
            Optional("id_autorizador"): Use(int),
            Optional("id_convenio"): Use(int),
            Optional("id_tipo_op"): Use(int),
            Optional("page", default=1): And(
                Use(int),
                lambda n: n > 0,
                error="'page' debe ser un numero entero mayor a cero"
            ),
            Optional("sortBy", default="id_comision_cobrada"): And(
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

Metodo PUT

> Path: /comisiones_cobradas/modificar

```Query strings
        {
            "id_comision_cobrada": Use(int)
        }
```

```json
        {
            Optional("comisiones"): dict,
            Optional("nombre_comision"):Use(str),
            Optional("estado"):  Use(bool),
        }
```

## Configuración comercios

Metodo POST

> Path: /configuracion_comercios/crear

```json
        {
            "id_comercio": Use(int),
            "id_tipo_contrato": Use(int),
            "tipo_pago_comision": Use(str),
        }
```

Metodo POST

> Path: /configuracion_comercios/consultar_configuracion_comercios

```json
        {
            Optional("id_configuracion_comercio"): Use(int),
            Optional("id_comercio"): Use(int),
            Optional("id_tipo_contrato"): Use(int),
            Optional("tipo_pago_comision"): And(str, Use(lambda e: e.lower())),
            Optional("page", default=1): And(
                Use(int),
                lambda n: n > 0,
                error="'page' debe ser un numero entero mayor a cero"
            ),
            Optional("sortBy", default="id_configuracion_comercio"): And(
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

Metodo PUT

> Path: /configuracion_comercios/modificar

```Query strings
        {
            "id_configuracion_comercio": Use(int)
        }
```

```json
        {
            Optional("id_tipo_contrato"):  Use(int),
            Optional("tipo_pago_comision"): Use(str)
        }
```

## Reporte comisiones

Metodo POST

> Path: /reportes_comisiones/comisiones_general

Reporte de comisiones general

```json
        {
            Optional("type"): Use(str),
        }
```

Metodo POST

> Path: /reportes_comisiones/aplicacion_comisiones

```json
        {
            Optional("id_convenio"): Use(int),
            Optional("id_comercio"): Use(int),
            Optional("id_autorizador"): Use(int),
            "date_ini": Use(str),
            "date_end": Use(str),
        }
```

## Tabla parametros autorizadores

Metodo POST

> Path: /tabla_parametros_autorizadores/crear

Crear parametrización para autorizadores

```json
        {
            "id_autorizador": Use(int),
            "nombre_parametro": Use(str),
            "valor_parametro": Use(str),
        }
```

Metodo POST

> Path: /tabla_parametros_autorizadores/consultar_parametros_autorizadores

Consulta de parametros autorizadores

```json
        {
            Optional("id_tabla_general_parametros_autorizadores"): Use(int),
            Optional("id_autorizador"): Use(int),
            Optional("nombre_parametro"): And(str, Use(lambda e: e.lower())),
            Optional("page", default=1): And(
                Use(int),
                lambda n: n > 0,
                error="'page' debe ser un numero entero mayor a cero"
            ),
            Optional("sortBy", default="id_tabla_general_parametros_autorizadores"): And(
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

Metodo PUT

> Path: /tabla_parametros_autorizadores/modificar

```Query strings
        {
            "id_tabla_general_parametros_autorizadores": Use(int)
        }
```

```json
        {
            Optional("nombre_parametro"): Use(str),
            Optional("valor_parametro"): Use(str)
        }
```

## Tipo contrato comisiones

Metodo POST

> Path: /contrato_comision/consultar

Consultar tipo de contrato comisión

```json
        {
            Optional("id_tipo_contrato"): Use(int),
            Optional("nombre_contrato"): And(str, Use(lambda e: e.lower())),
            Optional("page", default=1): And(
                Use(int),
                lambda n: n > 0,
                error="'page' debe ser un numero entero mayor a cero"
            ),
            Optional("sortBy", default="id_tipo_contrato"): And(
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

Metodo POST

> Path: /contrato_comision/crear

Crear tipo de contrato comisión

```json
        {
            "nombre_contrato":str,
            "iva":Use(float),
            "rete_fuente":Use(float),
            "rete_ica":Use(float)
        }
```

Metodo PUT

> Path: /contrato_comision/modificar

Modificar tipo de contrato comisión

```Query strings
        {
            "id_tipo_contrato": Use(int)
        }
```

```json
        {
            Optional("nombre_contrato"): str,
            Optional("iva"): Use(float),
            Optional("rete_fuente"): Use(float),
            Optional("rete_ica"): Use(float),
            Optional("created_at"): Use(str),
            Optional("estado"): Use(bool)
        }
```

## Transacciones cupo

Metodo POST

> Path: /transacciones_cupo/retornar

Retorno de cupo de transacciones

```json
        {
            "idTrx":Use(int),
        }
```
