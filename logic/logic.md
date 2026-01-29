# 📺 Lógica de Acceso a Vídeos — Academia Online

---

Este documento describe cómo funciona el control de acceso a los vídeos de la academia, garantizando que solo los usuarios autorizados puedan visualizar el contenido según su suscripción o curso comprado.

## 🎯 Objetivo

- **Proteger** los vídeos frente a acceso no autorizado

- **Permitir** acceso solo a usuarios autenticados

- **Controlar** el acceso por curso / módulo / lección

- **Evitar** enlaces directos reutilizables

- **Mantener** una experiencia fluida para el alumno

## 🧱 Arquitectura General

<pre style="background: rgba(200, 200, 200, 0.6); padding: 2rem; border-radius: 12px; width: fit-content">Usuario → Frontend → API → Autorización → Vídeo</pre>

## 🔐 Flujo de Acceso a un Vídeo

1. **El usuario inicia sesión**

2. **Selecciona una lección**

3. **El frontend solicita acceso al vídeo**

4. **La API valida permisos**

5. **Si está autorizado:**

    - **Se genera una URL firmada y temporal**

6. **El reproductor carga el vídeo**

7. **El acceso expira automáticamente**

## 🧑‍🎓 Reglas de Autorización

- Un usuario puede ver un vídeo si:

- Está autenticado

- Tiene acceso al curso

- El curso está:

    - comprado

    - o incluido en su suscripción

- El curso está activo

- El vídeo pertenece a ese curso

## 🗄️ Modelo de Datos Simplificado
**Usuarios**

- id

- email

- role

**Cursos**

- id

- título

- estado (activo / borrador)

**Lecciones**

- id

- curso_id

- orden

- video_key

**Accesos**

- user_id

- curso_id

- expires_at (opcional)