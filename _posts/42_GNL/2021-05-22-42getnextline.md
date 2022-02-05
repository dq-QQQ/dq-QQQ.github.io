---
title: Get_Next_Line
categories: 
   - 42_GNL
excerpt: "파일 입출력을 이용해서 파일을 개행단위로 나눠보자:)"
date:   2021-05-22 21:13:51 +0900
tags:
- 42seoul
- Get_Next_Line
- FILE
---

# 개요
Get_Next_Line 과제의 내용과 과제를 해결하기 위해 필요한 지식에 대해 살펴보겠습니다.

---



# GNL 프로젝트 요구사항 분석

#### 프로젝트의 개요
파일 디스크립터에서 읽은 파일의 내용을 개행 '\n'을 기준으로 나누어 반환하는 함수를 작성하는 것이다.

#### 프로젝트의 목표

C 프로그래밍에서 아주 흥미로운 새로운 개념인 '정적 변수'를 배울 수 있도록 할 것입니다.

또한 파일 입출력에 대한 이해를 하도록 할 것입니다.

#### 프로젝트의 특이사항

필요한 경우 heap에 할당된 모든 메모리 공간은 적절하게 해제되어야 합니다. 메모리 누수는 용납되지 않을 것입니다.

get_next_line 함수를 반복문 안에서 호출하면 파일 디스크립터에서 사용할 수 있는 텍스트를 EOF가 올때까지 한 번에 한 줄씩 읽을 수 있을 것입니다.

get_next_line.c가 동작하는 데 필요한 함수들이 들어있는 get_next_line_utils.c 파일을 추가해야 합니다.

하나의 정적변수로 get_next_line 성공하는 것을 목표로합니다.

각 디스크립터의 리딩 쓰레드를 잃지 않고 get_next_line을 사용하여 다중 파일 디스크립터를 관리 할 수 있어야합니다.


---

# get_next_line.h

---

<br />

#### DESCRIPTION

get_next_line 과제를 해결하기 위해 필요한 함수, 매크로, 라이브러리를 선언한 헤더파일이다.

#### get_next_line.h CODE

``` c
#ifndef GET_NEXT_LINE_H
# define GET_NEXT_LINE_H

# include <stdlib.h>
# include <unistd.h>
# include <fcntl.h>

# ifndef BUFFER_SIZE
#  define BUFFER_SIZE 2
# endif

# ifndef OPEN_MAX
#  define OPEN_MAX 256
# endif

int		get_next_line(int fd, char **line);
char	*my_strndup(const char *s1, size_t idx);
size_t	my_strnewline(char *s);
char	*my_strjoin(char const *s1, char const *s2);
size_t	my_strlen(const char *s);
void	*my_memcpy(void *dst, const void *src, size_t n);

#endif
```

설명 

<br />
<br />


---

# get_next_line.c

---

#### SYNOPSIS

* `함수 원형` : int get_next_line(int fd, char **line);
* `int fd` : 
* `char **line` : 
* `리턴값` : 1: 한 라인이 읽혔을 때. // 0: EOF에 도달했을 때 // -1: 에러가 발생했을 때

<br />

#### DESCRIPTION

파일 디스크럽터로부터 읽어 온 하나의 라인(newline 없이)을 반환하는 함수 작성

#### get_next_line.c CODE

``` c
#include "get_next_line.h"

char	*get_restdata(char *str)
{
	char	*ret;
	size_t	total_len;
	size_t	real_len;
	size_t	i;

	if (!str)
		return (0);
	real_len = 0;
	while (*(str + real_len) && *(str + real_len) != '\n')
		real_len++;
	if (!*(str + real_len))
	{
		free(str);
		return (0);
	}
	total_len = my_strlen(str);
	if ((ret = (char *)malloc(total_len - real_len + 1)) == 0)
		return (0);
	i = 0;
	real_len++;
	while (real_len < total_len)
		*(ret + i++) = *(str + real_len++);
	*(ret + i) = 0;
	free(str);
	return (ret);
}

char	*get_line_until_newline(char *str)
{
	char	*ret;
	size_t	len;

	len = 0;
	while (*(str + len) && *(str + len) != '\n')
		len++;
	ret = my_strndup(str, len);
	return (ret);
}

int		get_next_line(int fd, char **line)
{
	static char	*data[OPEN_MAX];
	char		*buff;
	int			read_byte;
	read_byte = 1;
	if (fd >= OPEN_MAX || fd < 0 || !line || BUFFER_SIZE <= 0)
		return (-1);
	if ((buff = (char *)malloc(BUFFER_SIZE + 1)) == 0)
		return (-1);
	while (!my_strnewline(*(data + fd)) && read_byte)
	{
		if ((read_byte = read(fd, buff, BUFFER_SIZE)) == -1)
		{
			free(buff);
			return (-1);
		}
		*(buff + read_byte) = '\0';
		*(data + fd) = my_strjoin(*(data + fd), buff);
	}
	free(buff);
	*line = get_line_until_newline(*(data + fd));
	*(data + fd) = get_restdata(*(data + fd));
	if (read_byte == 0)
		return (0);
	return (1);
}
```

설명

<br />
<br />

---


---

# get_next_line_utils.c

---

#### SYNOPSIS

* `사용한 함수` : my_strlen, my_memcpy, my_strjoin, my_strndup, my_strnewline
* `my_strlen` : 
* `my_memcpy` : 
* `my_strjoin` : 
* `my_strndup` : 
* `my_strnewline` : 
<br />

#### DESCRIPTION

get_next_line 과제를 해결하기 위해 필요한 함수들을 구현해 놓은 소스파일

#### get_next_line_utils.c CODE

``` c
size_t	my_strlen(const char *s)
{
	int	i;

	i = 0;
	if (!s)
		return (0);
	while (*(s + i))
		i++;
	return (i);
}

void	*my_memcpy(void *dst, const void *src, size_t n)
{
	if (!dst && !src)
		return ((void *)0);
	while (n-- > 0)
		*((char *)dst + n) = *((char *)src + n);
	return (dst);
}

char	*my_strjoin(char const *s1, char const *s2)
{
	size_t	len_1;
	size_t	len_2;
	char	*ret;

	if (!s1 && !s2)
		return (0);
	len_1 = my_strlen(s1);
	len_2 = my_strlen(s2);
	if ((ret = (char *)malloc(len_1 + len_2 + 1)) == 0)
		return (0);
	*(ret + len_1 + len_2) = 0;
	my_memcpy(ret, s1, len_1);
	my_memcpy(ret + len_1, s2, len_2);
	free((char *)s1);
	return (ret);
}

char	*my_strndup(const char *s1, size_t len)
{
	char	*ret;
	size_t	i;

	i = 0;
	if ((ret = (char *)malloc(len + 1)) == 0)
		return (0);
	*(ret + len) = 0;
	my_memcpy(ret, s1, len);
	return (ret);
}

size_t	my_strnewline(char *str)
{
	size_t i;

	i = 0;
	if (!str)
		return (0);
	while (*(str + i))
		if (*(str + i++) == '\n')
			return (1);
	return (0);
}
```

설명

<br />
<br />

