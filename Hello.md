
<!-- HEADING -->
# MI TITLE H1
## MI TITLE H2
### MY TITLE H3
#### MY TITLE H4
##### MY TITLLE H5

<!-- italic -->
This is an *italic* text
<!-- Strong -->
This is an **Strong** text

<!-- crossed out/strikethrough -->
This is an ~~Crossed out~~ text 

<!-- UL Order list -->

* apple
   * apple 2
* orange
  * orange 2
* grape

1. Samsung
   1. Samsung 1
   2. Samsung 2

2. Banana 
   1. Banana 1
   2. Banana 2
- Pacupata
- Carpapata
- San Vicente de Yanayacu
1. Samsung 
   - Modelo A
   - Modelo B
   - Modelo C

2. Xiomi 
   1. Xiomi mini
      - Mini 1
      - Mini 2
   2. Xiomi pro 
   3. Xiomi ultra

[Texto de enlac](https://www.google.com)

[Texto alternativo](https://upload.wikimedia.org/wikipedia/commons/a/a7/React-icon.svg)
   
<!-- this is a quote -->
> this is a quote


```java
// RegexCounter.java
// Compilar: javac RegexCounter.java
// Ejecutar: java RegexCounter /ruta/al/archivo "ERROR|WARN"

import java.nio.file.*;
import java.util.regex.*;
import java.io.IOException;

public class RegexCounter {
    public static void main(String[] args) throws IOException {
        if (args.length < 2) {
            System.out.println("Uso: java RegexCounter <archivo> <regex>");
            System.exit(1);
        }

        Path path = Paths.get(args[0]);
        Pattern pattern = Pattern.compile(args[1]);

        long total = 0, matches = 0;
        try (var lines = Files.lines(path)) {
            for (String line : (Iterable<String>) lines::iterator) {
                total++;
                if (pattern.matcher(line).find()) matches++;
            }
        }

        System.out.printf("Líneas: %d | Coincidencias: %d%n", total, matches);
    }
}
```
---
---

<!-- this is a quote -->

```cpp

#include <iostream>
#include <vector>

int main() {
    std::vector<int> v{1,2,3};
    for (auto x : v) std::cout << x << " ";
    std::cout << "\n";
    return 0;
}
```

```python
 print("Hello python")
```

---
---



