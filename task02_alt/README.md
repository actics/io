Дан исходник на C:

    /* submitted by noname */

    #include <stdio.h>
    #include <stdlib.h>
    #include <unistd.h>


    #define answer 3.141593

    void main(int argc, char **argv) {

        float a = (argc - 2)?: strtod(argv[1], 0);

        printf("You provided the number %f which is too ", a);


        if(a < answer)
            puts("low");
        else if(a > answer)
            puts("high");
        else
            execl("/bin/sh", "sh", "-p", NULL);
    }

Видим, что требуют аргумент, который перегоняют во float и сравнивают с числом PI.
Известно, что строгое сравнение с float не работает, поскольку введенное число
будет либо чуть больше, либо чуть меньше данного. Поэтому нужно найти другое,
которое будет не меньше, не больше и не равно данному. В спецификации чисел с
плавающей запятой такое есть - nan, и strtod его поддерживает. Передаем аргументом
стороку nan и получает shell.

