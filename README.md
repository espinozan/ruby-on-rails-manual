# ruby-on-rails-manual
Este manual incluye todos los comandos específicos de Rails 8.1.1, organizados de manera profesional y con explicaciones claras.


# 🚀 MANUAL COMPLETO DE COMANDOS RAILS 8.1.1
*Guía Profesional Exhaustiva Ruby On Rails*

---

## 📋 **CONTENIDO ESTRUCTURADO**

### 🔰 **SECCIÓN 1: FUNDAMENTOS ESENCIALES**

#### `rails new [nombre-app]`
**¿Qué hace?**: Crea el esqueleto completo de una aplicación Rails.
**Objetivo**: Inicializar proyecto con estructura MVC y convenciones.
**Cuándo usarlo**: Inicio de cualquier proyecto nuevo.
**Configuración avanzada**:
```bash
rails new mi_app -d postgresql -c tailwind --skip-javascript --skip-test
# -d: postgresql, mysql, sqlite3
# -c: tailwind, bootstrap, sass
# --api: solo API
# --minimal: configuración mínima
```

#### `rails server` / `rails s`
**¿Qué hace?**: Inicia servidor de desarrollo Puma.
**Objetivo**: Probar aplicación localmente.
**Opciones**:
```bash
rails s -p 3001 -b 0.0.0.0 -e production
```

#### `rails console` / `rails c`
**¿Qué hace?**: Consola interactiva con aplicación cargada.
**Objetivo**: Debuggear y probar modelos.
**Variantes**:
```bash
rails c --sandbox  # Modo seguro (rollback automático)
rails c -e test    # Consola en entorno testing
```

#### `rails generate` / `rails g`
**¿Qué hace?**: Genera código automáticamente.
**Objetivo**: Seguir convenciones y ahorrar tiempo.
**Ejemplos**:
```bash
rails g model User name:string email:string
rails g controller Users index show
rails g migration AddAgeToUsers age:integer
```

#### `rails destroy` / `rails d`
**¿Qué hace?**: Revierte lo generado por `generate`.
**Objetivo**: Corregir errores o cambiar enfoque.
```bash
rails d scaffold Product
```

---

## 🗄️ **SECCIÓN 2: BASE DE DATOS Y MODELOS**

### **Comandos de Migración**

#### `rails db:create`
**¿Qué hace?**: Crea las bases de datos definidas en database.yml.
**Objetivo**: Preparar entorno para primera ejecución.
**Cuándo usarlo**: Nuevo entorno de desarrollo.

#### `rails db:drop`
**¿Qué hace?**: Elimina las bases de datos.
**Objetivo**: Limpiar entorno de desarrollo.
**⚠️ Precaución**: Nunca usar en producción.

#### `rails db:migrate`
**¿Qué hace?**: Ejecuta migraciones pendientes.
**Objetivo**: Sincronizar esquema de BD.
**Buenas prácticas**:
```bash
rails db:migrate:status  # Ver estado primero
rails db:migrate RAILS_ENV=production
```

#### `rails db:rollback`
**¿Qué hace?**: Revierte última migración.
**Objetivo**: Corregir migraciones problemáticas.
```bash
rails db:rollback STEP=3  # Revertir 3 migraciones
```

#### `rails db:migrate:status`
**¿Qué hace?**: Muestra estado de todas las migraciones.
**Objetivo**: Verificar sincronización en equipo.

### **Comandos de Esquema**

#### `rails db:schema:dump`
**¿Qué hace?**: Genera schema.rb desde la BD.
**Objetivo**: Mantener schema actualizado.

#### `rails db:schema:load`
**¿Qué hace?**: Carga schema.rb en la BD.
**Objetivo**: Inicializar BD rápidamente sin migraciones.

#### `rails db:structure:dump`
**¿Qué hace?**: Crea structure.sql (esquema DB-specific).
**Objetivo**: Para características avanzadas de BD.

#### `rails db:structure:load`
**¿Qué hace?**: Carga structure.sql en la BD.
**Cuándo usarlo**: Cuando se usa structure.sql en vez de schema.rb.

### **Comandos de Datos**

#### `rails db:seed`
**¿Qué hace?**: Ejecuta db/seeds.rb para poblar BD.
**Objetivo**: Datos iniciales o de prueba.
**Ejemplo seeds.rb**:
```ruby
User.create!(name: "Admin", email: "admin@example.com")
10.times { |i| Post.create!(title: "Post #{i}") }
```

#### `rails db:seed:replant`
**¿Qué hace?**: Trunca tablas y re-ejecuta seeds.
**Objetivo**: Refrescar datos sin borrar toda la BD.

#### `rails db:seed:reset`
**¿Qué hace?**: Ejecuta seeds y fixtures.
**Objetivo**: Reset completo de datos.

#### `rails db:fixtures:load`
**¿Qué hace?**: Carga datos de test/fixtures/.
**Objetivo**: Preparar datos para testing.
```bash
rails db:fixtures:load FIXTURES=users,products
```

### **Comandos de Configuración BD**

#### `rails db:version`
**¿Qué hace?**: Muestra versión actual de schema.
**Objetivo**: Verificar número de migración actual.

#### `rails db:charset`
**¿Qué hace?**: Muestra charset de la BD.
**Objetivo**: Debuggear problemas de encoding.

#### `rails db:collation`
**¿Qué hace?**: Muestra collation de la BD.
**Objetivo**: Verificar reglas de ordenamiento.

#### `rails db:abort_if_pending_migrations`
**¿Qué hace?**: Aborta si hay migraciones pendientes.
**Objetivo**: Usar en scripts CI/CD para prevenir deploy.

---

## 🎮 **SECCIÓN 3: CONTROLADORES Y VISTAS**

#### `rails generate controller Name [actions]`
**¿Qué hace?**: Genera controlador con acciones y vistas.
**Objetivo**: Crear endpoints web.
```bash
rails g controller Pages home about contact --skip-routes
```

#### `rails generate scaffold ModelName [field:type]`
**¿Qué hace?**: Genera CRUD completo.
**Objetivo**: Prototipado rápido.
```bash
rails g scaffold Product name:string price:decimal category:references
```

#### `rails routes`
**¿Qué hace?**: Muestra todas las rutas definidas.
**Objetivo**: Debuggear enrutamiento.
**Opciones**:
```bash
rails routes -g product      # Filtrar por patrón
rails routes -c users        # Solo controlador específico
rails routes -E              # Formato expandido
```

---

## 🧪 **SECCIÓN 4: TESTING COMPLETO**

#### `rails test` / `rails t`
**¿Qué hace?**: Ejecuta suite completa de tests.
**Opciones**:
```bash
rails test                       # Todos los tests
rails test test/models/user_test.rb  # Archivo específico
rails test test/models/           # Directorio específico
rails test -n "test_name"        # Por nombre de test
rails test -p                    # Paralelo (más rápido)
```

#### `rails test:models`
**¿Qué hace?**: Tests de modelos solamente.

#### `rails test:controllers`
**¿Qué hace?**: Tests de controladores.

#### `rails test:helpers`
**¿Qué hace?**: Tests de helpers.

#### `rails test:integration`
**¿Qué hace?**: Tests de integración.

#### `rails test:system`
**¿Qué hace?**: Tests de sistema (navegador).

---

## ⚙️ **SECCIÓN 5: CONFIGURACIÓN Y ENTORNO**

#### `rails about`
**¿Qué hace?**: Muestra información de Rails y entorno.
**Objetivo**: Diagnosticar problemas de instalación.

#### `rails -T`
**¿Qué hace?**: Lista todos los comandos disponibles.
**Objetivo**: Descubrir funcionalidades.

#### `rails environment`
**¿Qué hace?**: Carga entorno específico.
**Objetivo**: Scripting avanzado.

#### `rails initializers`
**¿Qué hace?**: Muestra inicializadores en orden de ejecución.
**Objetivo**: Debuggear problemas de arranque.

#### `rails middleware`
**¿Qué hace?**: Lista middleware stack en orden.
**Objetivo**: Entender procesamiento de requests.

#### `rails restart`
**¿Qué hace?**: Reinicia aplicación.
**Objetivo**: Aplicar cambios de configuración.

#### `rails secret`
**¿Qué hace?**: Genera clave secreta segura.
**Objetivo**: secret_key_base para producción.

#### `rails time:zones[us|all|local]`
**¿Qué hace?**: Lista zonas horarias disponibles.
**Objetivo**: Configuración de time zones.

---

## 📦 **SECCIÓN 6: ASSETS Y FRONTEND**

#### `rails assets:precompile`
**¿Qué hace?**: Compila y minifica assets para producción.
**Objetivo**: Optimizar rendimiento.
**Configuración**:
```ruby
# config/environments/production.rb
config.assets.compile = false
config.assets.digest = true
```

#### `rails assets:clean`
**¿Qué hace?**: Limpia assets compilados antiguos.
**Objetivo**: Liberar espacio.

#### `rails assets:clobber`
**¿Qué hace?**: Elimina todos los assets compilados.
**Objetivo**: Limpieza completa.

#### `rails assets:environment`
**¿Qué hace?**: Muestra entorno de compilación.
**Objetivo**: Debuggear assets.

---

## 🔍 **SECCIÓN 7: DEBUGGING Y LOGS**

#### `rails dev:cache`
**¿Qué hace?**: Activa/desactiva cache en desarrollo.
**Objetivo**: Probar comportamiento con cache.

#### `rails dev:cache:on` / `rails dev:cache:off`
**¿Qué hace?**: Control explícito de cache.
**Objetivo**: Testing de performance.

#### `rails dev:log`
**¿Qué hace?**: Muestra log de desarrollo en tiempo real.
**Objetivo**: Monitoreo de requests.

#### `rails log:clear`
**¿Qué hace?**: Limpia todos los archivos de log.
**Objetivo**: Liberar espacio en disco.

---

## 🗂️ **SECCIÓN 8: ARCHIVOS TEMPORALES**

#### `rails tmp:clear`
**¿Qué hace?**: Limpia archivos temporales.
**Objetivo**: Resolver problemas de cache.

#### `rails tmp:create`
**¿Qué hace?**: Crea directorio tmp/.
**Objetivo**: Si fue eliminado accidentalmente.

---

## 🔧 **SECCIÓN 9: MIGRACIONES AVANZADAS**

#### `rails generate migration Name`
**¿Qué hace?**: Crea migración personalizada.
**Patrones útiles**:
```bash
rails g migration AddEmailToUsers email:string
rails g migration RemoveAgeFromUsers age:integer
rails g migration RenameNameToFirstNameInUsers
rails g migration CreateJoinTableUserProduct user product
```

**Ejemplo migración compleja**:
```ruby
class AddComplexIndexToUsers < ActiveRecord::Migration[8.1]
  def change
    add_index :users, [:email, :company_id], unique: true, 
              name: 'index_users_on_email_and_company'
    add_column :users, :preferences, :jsonb, default: {}
  end
end
```

#### `rails db:prepare`
**¿Qué hace?**: Crea BD si no existe, luego carga schema y seeds.
**Objetivo**: Scripts de deploy automáticos.

#### `rails db:setup`
**¿Qué hace?**: Crea BD, carga schema, ejecuta seeds.
**Objetivo**: Setup completo de nuevo entorno.

#### `rails db:reset`
**¿Qué hace?**: Drops, crea, migra y seed.
**Objetivo**: Reset completo (solo desarrollo).

---

## 🌐 **SECCIÓN 10: INTERNACIONALIZACIÓN (I18N)**

#### `rails i18n:js:export`
**¿Qué hace?**: Exporta traducciones a JSON para JavaScript.
**Objetivo**: Usar I18n en frontend.
```bash
rails i18n:js:export
# Genera app/assets/javascripts/translations.js
```

#### `rails i18n:js:import`
**¿Qué hace?**: Importa traducciones desde JSON.
**Objetivo**: Sincronizar con sistemas externos.

---

## 🚀 **SECCIÓN 11: SPRING Y PERFORMANCE**

#### `rails spring`
**¿Qué hace?**: Muestra comandos de Spring.
**Objetivo**: Gestionar preloader.

#### `rails spring binstub`
**¿Qué hace?**: Crea binstubs que usan Spring.
**Objetivo**: Comandos más rápidos.

#### `rails spring status`
**¿Qué hace?**: Muestra estado de Spring.
**Objetivo**: Debuggear problemas.

---

## 📝 **SECCIÓN 12: ANOTACIONES Y DOCUMENTACIÓN**

#### `rails notes`
**¿Qué hace?**: Busca TODO, FIXME, OPTIMIZE en código.
**Objetivo**: Gestionar tareas pendientes.

#### `rails notes:custom ANOTACION`
**¿Qué hace?**: Busca anotaciones personalizadas.
```bash
rails notes:custom REVIEW
rails notes:custom HACK
```

#### `rails annotate`
**¿Qué hace?**: Añade esquema de BD como comentario en modelos.
**Objetivo**: Documentación automática.
```bash
rails annotate --models
rails annotate --routes
```

---

## 🔌 **SECCIÓN 13: ENGINES Y PLUGINS**

#### `rails plugin new [nombre]`
**¿Qué hace?**: Crea nuevo Rails Engine.
**Objetivo**: Desarrollar funcionalidades reusables.
```bash
rails plugin new my_engine --mountable --dummy-path=spec/dummy
```

#### `rails plugin install [ruta]`
**¿Qué hace?**: Instala plugin en aplicación.
**Objetivo**: Integrar engines.

#### `rails railties:install:migrations`
**¿Qué hace?**: Copia migraciones desde engine.
**Objetivo**: Sincronizar esquemas.
```bash
rails railties:install:migrations FROM=my_engine
```

---

## 🛠️ **SECCIÓN 14: GESTIÓN DE DEPENDENCIAS**

#### `rails yarn:install`
**¿Qué hace?**: Instala dependencias JavaScript.
**Objetivo**: Gestionar paquetes frontend.

#### `rails yarn:check`
**¿Qué hace?**: Verifica si Yarn está configurado.
**Objetivo**: Validar entorno.

#### `rails dependency:check`
**¿Qué hace?**: Verifica conflictos de dependencias.
**Objetivo**: Prevenir problemas de versiones.

---

## 🔐 **SECCIÓN 15: SEGURIDAD Y CREDENCIALES**

#### `rails credentials:edit`
**¿Qué hace?**: Edita credenciales encriptadas.
**Objetivo**: Gestionar secrets seguramente.
```bash
rails credentials:edit --environment production
```

**Uso en código**:
```ruby
Rails.application.credentials.dig(:aws, :access_key_id)
Rails.application.credentials.stripe_secret_key
```

#### `rails db:encryption:init`
**¿Qué hace?**: Genera claves para encriptación de ActiveRecord.
**Objetivo**: Encriptar datos sensibles en BD.
```ruby
class User < ApplicationRecord
  encrypts :email, :ssn
end
```

---

## 📊 **SECCIÓN 16: ESTADÍSTICAS Y ANÁLISIS**

#### `rails stats`
**¿Qué hace?**: Muestra métricas del código.
**Objetivo**: Análisis de calidad.
```
+----------------------+-------+-------+---------+---------+-----+-------+
| Name                 | Lines |   LOC | Classes | Methods | M/C | LOC/M |
+----------------------+-------+-------+---------+---------+-----+-------+
| Controllers          |   200 |   150 |       5 |      25 |   5 |     4 |
| Models               |   150 |   120 |       8 |      18 |   2 |     5 |
| ...                  |  ...  |  ...  |    ...  |    ...  | ... |   ... |
+----------------------+-------+-------+---------+---------+-----+-------+
```

#### `rails benchmark`
**¿Qué hace?**: Ejecuta benchmarks de performance.
**Objetivo**: Optimizar código lento.

---

## 🔄 **SECCIÓN 17: ACTUALIZACIÓN Y MIGRACIÓN**

#### `rails app:update`
**¿Qué hace?**: Actualiza archivos de configuración.
**Objetivo**: Migrar entre versiones de Rails.
```bash
# Proceso seguro
git commit -a -m "Before update"
rails app:update
# Revisar cambios cuidadosamente
git diff
```

#### `rails db:system:change`
**¿Qué hace?**: Cambia el sistema de BD.
**Objetivo**: Migrar entre SQLite, PostgreSQL, MySQL.
```bash
rails db:system:change TO=postgresql
```

---

## 🎯 **SECCIÓN 18: GEMAS ESPECÍFICAS**

#### `rails generate devise:install`
**¿Qué hace?**: Configura Devise (autenticación).
**Objetivo**: Sistema de usuarios rápido.

#### `rails generate devise User`
**¿Qué hace?**: Genera modelo de usuario con Devise.

#### `rails generate jsonapi:install`
**¿Qué hace?**: Instala JSONAPI::Resources.
**Objetivo**: API REST estándar JSON:API.

#### `rails generate jsonapi:scaffold Model`
**¿Qué hace?**: Scaffold para JSON API.

---

## 🆕 **SECCIÓN 19: COMANDOS NUEVOS EN RAILS 8.1.1**

#### `rails content_security_policy:update`
**¿Qué hace?**: Actualiza política de seguridad de contenido.
**Objetivo**: Seguridad moderna contra XSS.

#### `rails active_storage:update`
**¿Qué hace?**: Actualiza configuración de Active Storage.
**Objetivo**: Mantener compatibilidad.

#### `rails db:console` / `rails dbconsole`
**¿Qué hace?**: Abre consola de base de datos nativa.
**Objetivo**: Operaciones directas en BD.
```bash
rails dbconsole --mode=html  # Algunas BDs soportan modos
```

#### `rails dev:prime`
**¿Qué hace?**: Prepara app para profiling de performance.
**Objetivo**: Optimización avanzada.

---

## 📋 **SECCIÓN 20: FLUJOS DE TRABAJO COMPLETOS**

### **Desarrollo de Nueva Feature**:
```bash
# 1. Crear migración
rails g migration CreateProducts name:string price:decimal

# 2. Migrar
rails db:migrate

# 3. Generar modelo
rails g model Product name:string price:decimal

# 4. Generar controlador
rails g controller Products index show new create edit update destroy

# 5. Agregar rutas (config/routes.rb)
resources :products

# 6. Probar
rails test
rails server
```

### **Deploy a Producción**:
```bash
# 1. Precompilar assets
rails assets:precompile

# 2. Verificar migraciones
rails db:migrate:status

# 3. Ejecutar migraciones
rails db:migrate RAILS_ENV=production

# 4. Cargar seeds (opcional)
rails db:seed RAILS_ENV=production

# 5. Reiniciar
rails restart
```

### **Mantenimiento Diario**:
```bash
# Inicio del día
rails db:migrate:status
rails test

# Durante desarrollo
rails console --sandbox  # Probar ideas
rails routes -g resource  # Ver rutas

# Fin del día  
rails notes              # Revisar TODOs
rails log:clear          # Limpiar
```

---

## 🚨 **SECCIÓN 21: COMANDOS DE EMERGENCIA**

### **Cuando las cosas salen mal**:
```bash
# Migración problemática
rails db:rollback

# Assets corruptos
rails assets:clobber && rails assets:precompile

# Problemas de cache
rails tmp:clear && rails log:clear

# Spring desincronizado
spring stop

# Revertir generación
rails destroy scaffold Product
```

### **En Producción**:
```bash
# NUNCA hacer en producción:
rails db:drop
rails db:reset

# SEGURO en producción:
rails db:migrate
rails assets:precompile
rails db:seed (con cuidado)
```

---

## 💡 **SECCIÓN 22: MEJORES PRÁCTICAS POR CATEGORÍA**

### **Migraciones**:
- ✅ Usar `change` en vez de `up/down` cuando sea posible
- ✅ Añadir índices para campos de búsqueda frecuente
- ✅ Usar `null: false` y `default:` apropiadamente
- ✅ Revisar migración antes de ejecutar

### **Generadores**:
- ✅ Usar `--no-test-framework` si usas RSpec
- ✅ Considerar `--skip-routes` para control manual
- ✅ Usar nombres en plural para controladores, singular para modelos

### **Testing**:
- ✅ Ejecutar `rails test` antes de cada commit
- ✅ Usar `rails test -p` para desarrollo
- ✅ `rails test:system` para critical paths

### **Producción**:
- ✅ `RAILS_ENV=production` explícitamente
- ✅ Backup antes de migraciones críticas
- ✅ Monitorizar `rails db:migrate:status`

---

## 🎓 **EXPLICACIÓN: ¿POR QUÉ ESTA ESTRUCTURA?**

**Principio**: "Si no puedes explicarlo simple, no lo entiendes suficientemente bien"

### **Agrupación por Responsabilidad**:
- **Base de datos**: Todo lo relacionado con datos y esquema
- **Desarrollo**: Comandos de día a día  
- **Producción**: Comandos seguros para deploy
- **Emergencia**: Cuando algo sale mal

### **Patrón de Uso**:
Cada comando explica:
1. **QUÉ hace** (acción concreta)
2. **POR QUÉ** (objetivo real)
3. **CUÁNDO** (casos de uso específicos)
4. **CÓMO** (ejemplos prácticos)

### **Ejemplo**:
`rails db:migrate` no es solo "ejecuta migraciones", es:
- **Qué**: Aplica cambios al esquema de BD
- **Por qué**: Para que tu código y BD estén sincronizados  
- **Cuándo**: Después de cambiar modelos o en nuevo deploy
- **Cómo**: `rails db:migrate && rails test` (verificar que todo funciona)

---
