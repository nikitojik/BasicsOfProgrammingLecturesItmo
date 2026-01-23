# Template specialization
```cpp
template<class T>
struct Boo {
    void foo(){
        std::cout << "foo" << std::endl;
    }
    void func() {};
};

template<> // специализация этого шаблона конкретно для int
struct Boo<int>{
    void foo(){
        std::cout << "foo(int)" << std::endl;
    }
};
```

## Full Template Specialization
- Предоставляем конкретную реализацию для всех параметров шаблона.

- Специализация шаблона класса стоит делать если
изменить какое-то внутреннее поведение относительно определенного типа. Пример std::vector(она меняет способ хранения элементов(1 байт под 8 буллов))
    
## Partial specialization
специализация для определенного шаблонна (нельзя для функций на уровнеи стандарта C++, так как есть перегрузка функций, Part. spec создает неоднозначаность и усложняет разрещение перегрузок)
```cpp
template<class T, class U>
struct Boo {
    void foo(){
        std::cout << "foo" << std::endl;
    }
    void func() {};
};

template<class U>
struct Boo<int,U> {
    void foo(){
        std::cout << "foo(int)" << std::endl;
    }
};
```

## RAII - resource acquisition is initialization (захват ресурса - есть инициализация)
- обеспечивает инкапсуляцию ресурса и инвариант состаяния
- безопасна к исключениям для объектов лежащих на стеке
- применяется для указателей, мьютексов, файлов...
