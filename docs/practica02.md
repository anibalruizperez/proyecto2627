# PRÁCTICA 02: Creación de formularios y recogida de valores por POST

---

## 1. Front-end (UT02P02.html)

En la parte de cliente se muestra un formulario donde el usuario debe introducir su sueldo, que debe ser mayor a 1000, y su puesto, el cual puede ser base, directivo o alto cargo.

### Código formularios

```html

<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <style>
        @import "https://cdn.jsdelivr.net/npm/bulma@1.0.4/css/bulma.min.css";
    </style>

    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">

    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>

    <title>UT02P02</title>
</head>

<body>
    <h1 class="title">Calculadora de aumentos</h1>

    <form name="formulario_sueldos" method="post" action="UT02P02.php">
        <input
            class="input is-link" ;
            type="text"
            placeholder="Escribe tu sueldo"
            name="sueldo"
            required />

    <br> <br>

    <label for="puesto">Elige tu puesto:</label>
    <select id="puesto" name="puesto" required>
        <option value="" disabled selected>Selecciona un valor</option>
        <option value="base">Base</option>
        <option value="directivo">Directivo</option>
        <option value="altocargo">Alto cargo</option>
    </select>

    <br> <br>

    <input type="submit" class="button is-link" value="Enviar" />

    </form>

</body>

</html>

```

## 2. Back-end (UT02P02.php)

En la parte del servidor se recoge por post tanto el valor de sueldo como el del puesto y los almacena en variables. Después en base al puesto se calcula su complemento, que será de un 10% el del puesto base, un 15% el del puesto directivo y de un 20% el del puesto alto cargo.

Por último devuelve por pantalla el valor del sueldo final.

### Código php

```php

<!DOCTYPE html>
<html lang="es">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <style>
        @import "https://cdn.jsdelivr.net/npm/bulma@1.0.4/css/bulma.min.css";
    </style>

    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">

    <script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>

    <title>UT02P02</title>
</head>

<body>
    <?php
    $sueldo = $_POST['sueldo'] ?? 1200;
    $puesto = $_POST['puesto'] ?? "base";
    $complemento = 0;

    echo "Tu sueldo es: $sueldo €<br>";
    echo "Tu puesto es: $puesto <br>";

    if ($puesto == "base") {
        $complemento = (int)$sueldo * 0.10;
    } elseif ($puesto == "directivo") {
        $complemento = (int)$sueldo * 0.15;
    } elseif ($puesto == "altocargo") {
        $complemento = (int)$sueldo * 0.20;
    }

    $sueldo = (int)$sueldo + $complemento;

    echo "Tu sueldo final más los complementos es: $sueldo €"
    ?>

    <br>

</body>

</html>

```