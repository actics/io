Дан исходник на C.

    //a little fun brought to you by bla

    #include <stdio.h>
    #include <stdlib.h>
    #include <signal.h>
    #include <unistd.h>

    void catcher(int a)
    {
        setresuid(geteuid(),geteuid(),geteuid());
        printf("WIN!\n");
        system("/bin/sh");
        exit(0);
    }

    int main(int argc, char **argv)
    {
        puts("source code is available in level02.c\n");

        if (argc != 3 || !atoi(argv[2]))
                return 1;
        signal(SIGFPE, catcher);
        return abs(atoi(argv[1])) / atoi(argv[2]);
    }

Устанавливается обработчик на SIGFPE (ошибочная арифметическая операция), в
котором дается шелл. В самой программе от нас требуют 2 аргумента командной
строки, которые потом перегоняются в int и первый делится на второй.
Самый простой способ вызвать SIGFPE - поделить на 0, однако в начале
программы второй аргумент проверяется на неравенство нулю. Значит, нужно найти
что-то по-сложнее. Идем гуглить. Вики заботливо говорит, что так же этот сигнал
можно получить при делении INT_MIN на -1 на x86 архитетуре, так как
-INT_MIN > INT_MAX. Передаем аргументами −2147483648 и -1 и получаем shell.

