---
tags: [Level_3, exam]
---



# Exam 03 - Level 3 Quick Reference

## ft_range (MEMORIZE)
```c
int *ft_range(int min, int max)
{
    int *arr;
    int i;
    
    if (min >= max)
        return (NULL);
    arr = malloc((max - min) * sizeof(int));
    if (!arr)
        return (NULL);
    i = 0;
    while (min < max)
    {
        arr[i] = min;
        min++;
        i++;
    }
    return (arr);
}
```

## ft_list_size (MEMORIZE)
```c
int ft_list_size(t_list *begin_list)
{
    int count = 0;
    
    while (begin_list)
    {
        count++;
        begin_list = begin_list->next;
    }
    return (count);
}
```

## hidenp
```c
int hidenp(char *s1, char *s2)
{
    int i = 0;
    int j = 0;
    
    while (s1[i] && s2[j])
    {
        if (s1[i] == s2[j])
            j++;
        i++;
    }
    return (s2[j] == '\0');
}
```

## lcm
```c
unsigned int lcm(unsigned int a, unsigned int b)
{
    unsigned int n;
    
    if (a == 0 || b == 0)
        return (0);
    n = (a > b) ? a : b;
    while (1)
    {
        if (n % a == 0 && n % b == 0)
            return (n);
        n++;
    }
}
```

## ft_atoi (Level 2 - REVIEW!)
```c
int ft_atoi(char *str)
{
    int i = 0;
    int sign = 1;
    int result = 0;
    
    while (str[i] == ' ' || (str[i] >= 9 && str[i] <= 13))
        i++;
    if (str[i] == '-' || str[i] == '+')
    {
        if (str[i] == '-')
            sign = -1;
        i++;
    }
    while (str[i] >= '0' && str[i] <= '9')
    {
        result = result * 10 + (str[i] - '0');
        i++;
    }
    return (result * sign);
}
```

## ft_strcmp (Level 2 - REVIEW!)
```c
int ft_strcmp(char *s1, char *s2)
{
    int i = 0;
    
    while (s1[i] && s2[i] && s1[i] == s2[i])
        i++;
    return (s1[i] - s2[i]);
}
```

## print_bits (Level 2 - REVIEW!)
```c
void print_bits(unsigned char octet)
{
    int i = 7;
    
    while (i >= 0)
    {
        if ((octet >> i) & 1)
            write(1, "1", 1);
        else
            write(1, "0", 1);
        i--;
    }
}
```

## SKELETON: while loop
```c
int i = 0;
while (str[i])
{
    // do something
    i++;
}
```

## SKELETON: Two pointers reverse
```c
int start = 0;
int end = len - 1;
while (start < end)
{
    temp = str[start];
    str[start] = str[end];
    str[end] = temp;
    start++;
    end--;
}
```

## Common mistakes
- ❌ Forgetting NULL check after malloc
- ❌ Forgetting to free memory
- ❌ Off-by-one: using `<=` instead of `<`
- ❌ Forgetting `return` statements
- ❌ Using `printf` instead of `write`
