# Mis Apuntes
## 1. Introduccion 

## Habilitar Forwadrinf en Linux
Esos comandos sirven para habilitar el reenvio de paquetes en Linux
```bash
# editar
sudo vim /etc/sysctl.conf y agregar:
# Para pv4
net.ipv4.ip_forward=1
```
## Comandos 
```bash
```
<!--  italicc -->
this is an *italic* text
<!--  italicc -->
this is an *strong* text

<!--  italicc -->
this is ~~strikethrough~~ text

<!--  UL -->
* apple
  * apple 
* orange
* etc


1.apple
  1. apple x
  2. apple l
 
2. organge
3. etc
* Como agregar enlaces
[YouTube](https://www.youtube.com/ "Yotube")

>This is a example of java
``` java
public class CuentaBancaria {
    private String titular;
    private double saldo;

    public CuentaBancaria(String titular, double saldoInicial) {
        this.titular = titular;
        if (saldoInicial >= 0) {
            this.saldo = saldoInicial;
        }
    }

    public String getTitular() {
        return titular;
    }

    public double getSaldo() {
        return saldo;
    }

    public void depositar(double monto) {
        if (monto > 0) {
            saldo += monto;
        }
    }
}
```
> This is a example of c++
```C++
/// Esto es primero 
#include <coroutine>
#include <iostream>
/// Esto es segundo
struct Generator {
    struct promise_type {
        int current_value;
        Generator get_return_object() { return Generator{Handle::from_promise(*this)}; }
        std::suspend_always initial_suspend() { return {}; }
        std::suspend_always final_suspend() noexcept { return {}; }
        std::suspend_always yield_value(int value) { current_value = value; return {}; }
        void return_void() {}
        void unhandled_exception() { std::terminate(); }
    };

    using Handle = std::coroutine_handle<promise_type>;
    Handle handle;

    explicit Generator(Handle h) : handle(h) {}
    ~Generator() { if (handle) handle.destroy(); }

    bool next() {
        handle.resume();
        return !handle.done();
    }
    int value() { return handle.promise().current_value; }
};

Generator contador(int max) {
    for (int i = 1; i <= max; ++i) {
        co_yield i; // Suspende la ejecución y devuelve el valor
    }
}

int main() {
    auto gen = contador(3);
    while (gen.next()) {
        std::cout << gen.value() << " ";
    }
    return 0;
}

```
`\|'
```html
<h1>hello World</h1>
```
| Tablas   |Are  |Cool   |
|----------|-----|----   |
| cool 3 us|right|amnbdasj|
# Imagenes
![VSCode](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRoffYpdb9Xg0YztJA3tLe8-YliSZXxZX47lW_xOIZsnQ&s=10)

<!-- GITHU MARKDOWN -->
* [x] Task 1
* [x] Task 2
* [x] Task 3
* [ ] Task 4
* [ ] Task 5
* [ ] Task 6

@dcanavi.abx :relaxed: :v: :rofl:





