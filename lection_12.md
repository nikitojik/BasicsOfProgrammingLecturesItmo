# Наследование и полиморфизм
```cpp
class CRerson{
    public:
        CPerson(const std::string& name, unsigned yearOfBirth)
            : yearOfBirth_(yearOFBirth)
            , name_(name)   {}
        unsigned age() const{
            const std::chrono::time_point now{std::chrono::system_clock::now()};
            const std::chrono::year_month_day ymd{std::chrono::floor<std::chrono::days>(now)};
            return static_cast<int>(ymd.year()) - yearOfBirth_;
        }

        const std::string& name() const{
            return name_;
        }
    private:
        std::string name_;
        unsigned yearOfBirth_;

       
};


class CStudent : public CPerson{
    public:
        CStudent(const std::string& name, unsigned age, const std::string& university)
            :CPerson(name, age)
            ,university(university)
        {}
    private:
        std::string university_;
};

class CBudgetStudent : public CStudent{
    public:
        CBudgetStudent(const std::string& name, unsigned yearOfBirth, const std::string& university, unsigned salary)
            :CStudent(name, yearOfBirth, university)
            ,salary(salary)
        {}
    private:
        unsigned salary_;
};

void Hello(const Cperson& p){
    std::cout << "Hello. I'm " << p.name() << std::endl;
}

int main(){
    CPerson p{"Ivan Ivanov", 2007};
    CStudent st{"Petr Petrov", 1998, "ITMO"};

    st.name();
    st.age();

    Hello(st);

    return 0;
}
```

## Наследование:
- позволяет написать новый класс на основе уже существующего с частично или полностью заимствующей функциональностью. Класс, от которого производится наследование, называется базовым, родительским или суперклассом. Новый класс - потомком, наследником, дочерним или производным классом.

- полиморфизм подтипов, **is-a relationship**

- обеспечивает повторное использование кода (следствие но не причина)

- наследование может быть множественным

### Порядок вызова конструкторов:
- базовый класс
- дочерний класс
### Порядок вызова деструкторов:
- дочерний класс
- базовый класс

### Наследник
- хранит в себе родителя
- сохраняет методы родителя*
- приведение к базовому классу **(slicing)**
- модификаторы доступа

### модификатор доступа к полям базового класса
```cpp
class CStudent : public CPerson{}
```

- регулирует доступ к деталям реализации базового класса

ключевое слово **protected** - позволяет получить доступ к скрытым полям базового класса, но скрывает извне. 
то есть извне не можем обращаться, но из классов-наследников можно

### Множественное наследование
- класс наследует поля и методы n-количества классов

### Diamond Problem
если в двух базовых классах, есть одинаковые поля (допустим два имени),то будет ошибка компиляции
(компилятор не понимает, что надо подставить)
Решение: явно указать, метод какого класса надо использовать

### Проблема множественного наследования
- надо либо явно указать метод того класса, который нужен или поставить по умолчанию (using)

### final
- можно явно запретить наследование, класс не может быть теперь базовым
```cpp
class CPerson final{}
```

## Полиморфизм
- это свойство 

```cpp
class ConsoleLogger{
    public:
        void Log(const char& message){
            std::cout << message << std::endl;
        }
};
```
### virtual
Таблица виртуальных ф-ций - указатель, который указывает, какая функция должна использоваться для экземпляра класса
храним лишние 8 байт информации + вызов виртуальных методов "дороже".


