# Git Survival Guide 

> Guía personal para **no romper `main`**, **no entrar en pánico** y **rescatar trabajo** aunque todo parezca perdido.
>
> Escrita después de hacer un desastre xd

---

##  Objetivo

* Tener una **referencia clara y rápida** para trabajar con Git sin miedo
* Saber **qué hacer cuando algo sale mal**
* Entender **qué está pasando realmente** (no solo copiar comandos)
* Usar esta guía como **checklist mental** antes de hacer commits o merges

---

##  Conceptos clave 

###  Repositorio

* Es el proyecto completo
* Puede ser:

  * **Local** → el que está en mi compu
  * **Remoto** → GitHub / GitLab / Bitbucket

###  Rama (branch)

* Es una **línea de tiempo** del proyecto
* No es una copia del proyecto, es un **apuntador** a commits

Tipos importantes:

* `main` → código estable (NO experimentar / mergear o hacer cosas a la ligera aquí)
* `fix/*` o `feature/*` → donde sí se trabaja

###  Commit

* Es una **foto del estado del proyecto**
* Un commit debe:

  * tener sentido
  * explicar *qué* y *por qué*

###  Merge

* Unir una rama con otra
* Normalmente:

  * `feature → main`

###  Origin

* Es el **repositorio remoto**
* `origin/main` ≠ `main`

---

##  Regla de oro (NO negociable)

>  **NUNCA trabajes directamente en `main`**

Siempre:

```bash

##  Flujo correcto de trabajo (modo seguro)

```text
main (actualizado)
  ↓
crear rama nueva
  ↓
trabajar
  ↓
commits claros
  ↓
push
  ↓
Merge Request
```

### Paso a paso

1.- Asegúrate de estar en `main` y tener los ultimos `cambios`

```bash
git checkout main
git pull origin main
```

2.- Crear rama

```bash
git checkout -b 'name-example'
```

3.- Trabaja normal

```bash
git add src
git commit -m "feat: ajustes en dashboard"
```

4.- Sube tu rama

```bash
git push -u origin fix/frontend-v3
```

5.- Merge Request (desde GitLab/GitHub)

---

##  Escenarios reales y qué hacer

### Caso 1: Trabajé un monton pero ya se mergeó `main` xdd

**Síntomas:**

* Tu rama ya no existe
* `main` avanzó
* Tú seguiste trabajando local

**Solución segura (probada):**

1.- Haz commit de TODO en tu rama actual

```bash
git add .
git commit -m "rescue: trabajo local antes de merge"
```

2.- Vete a `main` y actualiza

```bash
git checkout main
git pull origin main
```

3.- Crea una nueva rama limpia

```bash
git checkout -b fix/frontend-v3
```

4.- Traer el trabajo anterior

```bash
git merge fix/frontend-v2
```

Resultado: trabajo salvado + main actualizado

---

###  Caso 2: Me equivoqué de rama y ya hice commits

**Todo tiene solución we**

```bash
git checkout rama-correcta
git cherry-pick <hash-del-commit>
```

---

### Caso 3: Hice `git pull` y salió un merge raro

* Lee el mensaje
* Si abre editor → **solo guarda y cierra**
* Git NO hace nada sin confirmación

---

## ¿Cómo revisar que todo salió bien?

### Revisión rápida

```bash
git status
git branch
git log --oneline --graph --decorate --all
```

### Corre el proyecto

* Si el server ya estaba corriendo y **sigue jalando** → buen indicio
* Recarga
* Revisa consola

---

##  Conceptos IMPORTANTES

* `main` es **sagrado**
* Las ramas son **baratas**, úsala sin miedo
* Un commit es un **checkpoint**, no una carga
* Merge Request > merge directo
* Si dudas → **crea una rama nueva**

---

## Buenas prácticas 

* Commits pequeños y claros
* Prefijos:

  * `feat:` nueva funcionalidad
  * `fix:` bug
  * `docs:` documentación
  * `rescue:` salvar trabajo

Ejemplo:

```bash
git commit -m "docs: git survival guide"
```

---

## Kit anti-pánico

Antes de hacer algo drástico:

```bash
git status
git branch
git log --oneline --decorate -5
```

Respira.
Git casi siempre **tiene tu trabajo**.

---

## Frases para nunca olvidar

> "Si no has hecho commit, Git no puede ayudarte"

> "main no es para experimentar"

> "Las ramas se crean, el estrés no"

---

## Nota final

Esta guía existe porque:

* ya me paso esto
* ya me espanté
* y ya aprendí

Si algo raro pasa:
 **crear rama nueva y salvar trabajo primero**

Fin 🫡
git checkout -b feature/nueva-cosa
```

