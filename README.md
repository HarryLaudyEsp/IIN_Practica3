# Descripción del Proyecto

The objectiv of this repository is to train us to use git and the github environment.

# Pruebas de Código

Here is an exemple of a code that i wrote with the language C in 1st year in my country :

```c
/*
** EPITECH PROJECT, 2020
** main
** File description:
** main
*/

#include "../include/my.h"

char **init_tab(char *line)
{
    char **tab;
    if (is_dq(line))
        tab = my_str2_word_array_dq(line);
    else if (is_pip(line))
        tab = my_str2_word_array_pip(line);
    else
        tab = my_str2_word_array(line);
    return (tab);
}

char *read_command(void)
{
    char * line = NULL;
    char *str;
    size_t len = 0;
    ssize_t read;
    int z = 0;

    if (read = getline(&line, &len, stdin) != -1) {
        for (; line[z] != '\n'; z++);
        str = malloc(sizeof(char) * z);
        for (int i = 0; i < z; i++)
            str[i] = line[i];
        str[z++] = '\0';
        return (str);
    } else {
        return (NULL);
    }
}

int display_prompt(int ac, char ** av, char **env)
{
    char *str = NULL, *line = NULL;
    char **tab, **tmp_tab;
    while (1) {
        write(1, "$> ", 3);
        line = read_command();
        int nb_arg = count_args(line);
        char **path_tab = find_path(env);
        tab = init_tab(line);
        for (int i = 0; i < nb_arg; i++) {
            if (nb_arg > 1)
                tmp_tab = my_str2_word_array(tab[i]);
            else
                tmp_tab = tab;
            int pid = fork();
            if (pid > 0)
                wait(NULL);
            else if (pid == 0) {
                if (my_strcmp("setenv", tab[0]) == 0 || my_strcmp("unsetenv", tab[0]) == 0)
                    env = setenv_unsetenv(tmp_tab, env);
                else
                    execute_line(path_tab, env, tmp_tab, line);
            }
        }
        if (my_strcmp(line, "exit") == 0)
            break;
    }
    return (0);
}

```

---

![alt text](image.jpg)

# Autor
Harry LAUDY