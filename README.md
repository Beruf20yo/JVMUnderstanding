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
2 - поиск в Application ClassLoader(не найден)-> поиск в Platform ClassLoader(не найден) -> поиск в Bootstrap ClassLoader(найден)  
3 - поиск в Application ClassLoader(не найден)-> поиск в Platform ClassLoader(не найден) -> поиск в Bootstrap ClassLoader(найден)  
5 - поиск в Application ClassLoader(не найден)-> поиск в Platform ClassLoader(не найден) -> поиск в Bootstrap ClassLoader(найден)  
![image](https://github.com/Beruf20yo/JVMUnderstanding/assets/134109602/4c4cee90-578d-40a3-abef-496127fd1639)



