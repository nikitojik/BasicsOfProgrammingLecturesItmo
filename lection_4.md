## структура - это одна или несколько переменных (возможно, различных типов), 
которые для удобства работы с ними сгруппированы под одним именем


struct Point{
    int x;
    int y;

} pt1, pt2, pt3; - объявление переменные этого типа

Point p4; - объявление переменной

Point max_point = {200,300};
(max_point.x == 200;) - обращение к полям структуры

вложенные структуры:

rect.max_poit.x; пример

Инициализация:
Point p1 = {1,2};
Point p2 = {.x = 1, .y = 2};
Point p3 {.x = 1, .y = 2};

Rect r1 = { {1,2}, p2};
Rect r2 = { .pt1 = {1,2}, .pt2 = p2}

Анонимные структуры
struct Button {
    struct{
        int x;
        int y;
    };

    struct {
        size_t width;
        size_t height;
    }
};


Операции со структурами
- копирование
- присваивание
- взятие адреса
- доступ к элементам
- передавать в функцию и получать ее оттуда

Массивы структур 
struct Record {
    char name[10];
    char surname[10];
    long phone;
};

Record phonebook[200];

указатели на структуры
Record* FindRecord(long phone, Record* records, int count){
    for (int i = 0; i < count; ++i){
        if(records[i].phone = phone){
            return &records[i];
        }
    }

    return nullptr
}

-> - обращение к элементу через указатель структуры

выравнивание структур округляется вверх до кратного выравниванию самого крупного поля
#pragma pack(1) - экономит память, но уменьшает произв

struct alignas(64) Foo{}- для спец оптимизаций можно увеличить выравнивание

## Объединения - это переменная, которая может содержать (в разные моменты времени) объекты различных типов и размеров.
union Name{
    struct{
        char name[13];
        char code[3];
    };

    struct{
        int32_t i1;
        int32_t i2;
        int32_t i3;
        int32_t i4;
    };
};

## указатель на функцию
int main(){
    int (*funcPtr)(int) = &foo;
    int arr[] = {1,2,3,4,5};
}


void* FindMax(void* array, size_t size, bool(*compare)(void*)(void*)){
    assert(array);
    assert(size > 0);


    void* result = array;

    for (int i =0; i < size; ++i){
        if(!compare(result,array[i]))
            result = array[i];
    }

    return result;
}

bool less(void* a, void* b){
    return a < b;
}

bool greater(void* a, void* b){
    return a > b;
}