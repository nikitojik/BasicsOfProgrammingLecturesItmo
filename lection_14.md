# Шаблоны классов и функций
```cpp
int max(int a, int b){
    return a > b ? a : b;
}

const CRational& max(const CRational& a, const CRational& b){
    return a > b ? a : b;
}
```
Как избавиться от копипасты:
- препроцессор
- void* 
- макросы ()

или

## Шаблоны
- шаблоны определяют семейство ф-ий, классов, типов и переменных
- шаблон 


## Шаблоны функций
```cpp
template<class T>
const T& max(const T& a, const T& b){
    return a > b ? a : b;
}

template<class T>
void printMe(const T& value){
    std::cout << value;
}

int main(){
    std::cout << max<int>(1,2); // на основании шаблона компилятор сам сделает функцию int max на основании шаблона
    std::cout << max<double>(1.1,2.2); // на основании шаблона компилятор сам сделает функцию double max на основании шаблона
    return 0;
}
```
функция создается компилятором только один раз, при повторном вызове шаблонной функции с определенным типом он уже вызывает созданную ф-ию

шаблоны функциями **НЕ ЯВЛЯЮТСЯ**

## Template dediction
- компилятор может вывести типы из параметров, которые передали в функцию
```cpp
std::cout << max(1,2);
std::cout << max(1, 1.1); // неправильно
std::cout << max<double>(1, 1.1);
```

## Инстанциация
- без инстанциации не происходит генерации конкретного шаблона
- при использовании шаблонной функции или класса требуется полное определение, поэтому для использования в других единицах трансляции 

**!!!** в заголовочном файле шаблон должен быть полностью определен (то есть все необходимые типы данных для функции)

## Шаблон класса
```cpp
template <typename T1, typename T2>
class CPair{
public:
    CPair() = default;
    CPair(const T1& first, const T2& second)
        : first_(first)
        : second_(second)
    {}

    CPair& operator=(const CPair& other){
        if (this == &other)
            return *this
        first_ = other.first_;
        second_ = other.second_;

        return *this;
    }

private:
    T1 first_;
    T2 second_;
};

int main(){
    CPair<int,int> p1 {1,2};
    CPair<double,double> p2 {1.1,2.2};
}
```
## Non-type template parameter
