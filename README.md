## Код для исследования
```java

public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}
```

Изначально проиходит подгрузка класса JvmComprehension:  
Application Classloader получает запрос на загрузку класса -> запрос делегируется Platform Classloader  
Platform Classloader получает запрос на загрузку класса -> запрос делегируется Bootstrep Classloader  
Bootstrep Classloader ищет класс, класс не найден -> запрос делегируется Platform Classloader  
Platform Classloader ищет класс, класс не найден -> запрос делегируется Application Classloader  
Application Classloader находит класс JvmComprehension. После едёт процесс связывания: проверка кода на валидность, создание примитивов в статических полях, связывание ссылок на другие классы. В конце идёт процесс инициализации static методов   
1 - создание фрейма метода main(), создаётся переменная примитивного типа i = 1, она хранится в стеке  
2 - инициализациия объекта класса Object в куче, создание переменной "о", которая хранит ссылку на Object   
3 - инициализация объекта класса Integer со значением 2 в куче, создание переменной ii, которая хранит ссылку на неё  
4 - создание нового фрейма метода printAll(), а также создание в нём переменной примитивного типа i = 1 (хранится в стеке), создрание ссылки ii на Integer в куче со значение 2, создание ссылки о на Object в куче  
5 - инициализация объекта класса Integer со значением 700 в куче, создание переменной uselessVar, которая хранит ссылку на неё    
6 - создание нового фрейма System.out.println(), а также создание в нём переменной примитивного типа i = 1 (хранится в стеке), создрание ссылки ii на Integer в куче со значение 2, создание ссылки о на Object в куче. Создание объекта String со значением "o.toString() + i + ii"  
Между 6 и 7 - очистка стека от фреймов printAll() и System.out.println(). _Сборщик мусора_ удаляет из кучи Integer со значением 700, так как он нигде не используется  
7 - создание нового фрейма System.out.println(), а также создание объекта String со значением "finished" в куче
В конце _Сборщик мусора_ очищает кучу, программа закончила своё выполнение.  
[Поправка: не совсем уверен про String, так как они хранятся в String pool и насколько я читал, даже после окончания работы программы остатки сохраняются в памяти, и именно поэтому String не используют для хранения паролей]
![image](https://github.com/Beruf20yo/JVMUnderstanding/assets/134109602/4866af57-0bdc-4109-b89b-f285544c8a75)





