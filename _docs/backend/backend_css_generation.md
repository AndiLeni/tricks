---
title: Module im Backend mit CSS aus dem Frontend stylen
---

# **Inhalt:**  
Dieser Trick beschreibt am Beispiel des Frameworks UiKit wie man sich eine backend.css Datei erstellen kann, sodass die Modulvorschau im Backend identisch aussieht wie im Frontend.


> **Benötigte Software:**
> - ein sass/less/scss compiler


## Vorgehen:

Für diesen Trick wird folgende Ordnerstruktur angenommen, um das Vorgehen beispielhaft zu demonstrieren:
```
css/
├─ node_modules/
├─ styles.scss
├─ backend.scss
```

Inhalt in der Datei `styles.scss`:  
Hier werden die regulären Styles abgelegt, so wie sie im Frontend erscheinen sollen.

```scss
...

@import "node_modules/uikit/src/scss/...";

@mixin hook-card() { color: #000; }

.my_element {
    color: blue;
}

...
```

Nun zum eigentlichen, interessanten Teil. Damit diese Styles im Backend verwendet werden können (ohne dass sie das Redaxo-Backend-CSS verändern) werden diese mit einem Präfix versehen.  
Die Datei `backend.scss` sieht dann folgendermaßen aus:
```scss
.rex-slice-output .panel-body {
  @import "styles.scss";
}

.my_other_backend_style {
    color: blue;
}
```

Dadurch werden die Frontend-Stile mit dem Präfix `.rex-slice-output .panel-body` versehen, sodass diese im Backend nicht mehr mit dem Redaxo-CSS interferieren können.

Abschließend können die Dateien `styles.scss` für das Frontend und `backend.scss` unabhängig voneinander kompiliert werden.















