# Comandos para la base de datos

## Crear usuario y contrasena en el CLI de postgreDB de tu PC
```bash
-- Crear el usuario con contraseña
CREATE USER "petcare-administrator" WITH PASSWORD 'root123';

-- Otorgar el rol de superusuario (todos los permisos)
ALTER USER "petcare-administrator" WITH SUPERUSER;
```
         
## Crear la base de datos con el código "Estructura.sql" en esta carpeta
```bash
psql -U petcare-administrator -h localhost -f PostgreDB/Estructura.sql
```

NAME: petcare_database,
USER': petcare-administrator,          
PASSWORD': root123,

```bash
-- Verificar usuarios y bases de datos
\du
\l

-- Salir
\q
```
