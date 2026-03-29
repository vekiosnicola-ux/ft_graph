---
tags: ['CheatSheet', 'Tutorials']
date: 2026-03-29
status: complete
---


# Tutorials

<a href="https://www.youtube.com/watch?v=Jen46qkZVNI&t=30s" target="_blank"><img src="http://img.youtube.com/vi/Jen46qkZVNI/0.jpg"
alt="Boxer's Perfect Rush SCV" width="240" height="180" border="10" /></a>

---
## 0x00 ~ Optimization - Aiming for the lowest latency

When you want to aim for lowest latency - *i.e maximum speed* - there are many things that will improve your program to create a better binary: Optimization flag, parallelization, vectorization and carefully crafting your algorithm.


### Optimization flags

Especially for Computer Graphics projects, you will want to turn on these optimization flags, [listed on gcc website](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html).

> Without any optimization option, the compiler’s goal is to reduce the cost of compilation and to make debugging produce the expected results. Statements are independent: if you stop the program with a breakpoint between statements, you can then assign a new value to any variable or change the program counter to any other statement in the function and get exactly the results you expect from the source code.
Turning on optimization flags makes the compiler attempt to improve the performance and/or code size at the expense of compilation time and possibly the ability to debug the program.

**To use it simply compile the program with:**
```
gcc -O2 a.c
```
NB: It is the letter 'o' and not a zero. You may also use O3.


### Multithreading and Parallelization

The historical (and current) approach is to add more power via [multithreading](https://en.wikipedia.org/wiki/Multithreading_(computer_architecture)), [multiprocessing](https://en.wikipedia.org/wiki/Multiprocessing), [Grid Computing](https://en.wikipedia.org/wiki/Grid_computing) or even [Cloud Computing](https://en.wikipedia.org/wiki/Cloud_computing). Two libraries exist for this use: [OpenMP](https://www.openmp.org/wp-content/uploads/openmp-examples-4.5.0.pdf) and [pthread](http://man7.org/linux/man-pages/man7/pthreads.7.html), you will have to compile respectively with:
```
gcc -fopenmp -O3 a.c
```
and:
```
gcc -pthread -O3 a.c
```


### [Vectorization](https://en.wikipedia.org/wiki/Streaming_SIMD_Extensions)

> Modern graphics processing units (GPUs) are often wide SIMD implementations, capable of branches, loads, and stores on 128 or 256 bits at a time.
Intel's latest AVX-512 SIMD instructions now process 512 bits of data at once.

As a double is 64 bits - *i.e 8 bytes or octets* - **instead of iterating overs value 1 by 1, you will be able to compute up to 8 double at the time** - *i.e 512 / 64* - if your computer support it (but most likely, as of 2020, your computer will only handle 256 bits register).

**Vectorization the most efficient way to quickly gain performance gains without the overhead of threads' initialization**.

**Demonstration: Getting Min and Max value from a float array**
```c
/* Vectorization example by agavrel */
 <stdio.h>  // printf
 <stdlib.h> // rand()
 <time.h>   // time
 <xmmintrin.h>  // 128 bits register _m128

float m128_max_float(__m128 src) {
    __m128 n[4];

	// a) n[0] = src >> 64                                  So lets say src is composed of floats a b c d, it becomes 0 0 a b
    n[0] = _mm_shuffle_ps(src, src, _MM_SHUFFLE(0,0,3,2));
	// b) n[1] = {max(a,0), max(b,0) max(a,c) max(b,d)}     NB: actually we don't care about the two highest float at this point, I will call them 'x': {x, x max(a,c) max(b,d)}
    n[1] = _mm_max_ps(src, n[0]);                             
	// c) n[2] = n[1] >> 32                                 So n2 become {0 x x max(a,c)}
    n[2] = _mm_shuffle_ps(n[1], n[1], _MM_SHUFFLE(0,0,0,1));
	// d) n[3] = {x x x max(max(a,c), max(b,d))}
    n[3] = _mm_max_ps(n[1], n[2]);                            

    return _mm_cvtss_f32(n[3]);   // d) Hence max(a,b,c,d), stored in the lowest 32 bits of n[3], is loaded into a float that we return. We don't care about the other bits
}

float m128_min_float(__m128 src) {
    __m128 n[4];

    n[0] = _mm_shuffle_ps(src, src, _MM_SHUFFLE(0,0,3,2));
    n[1] = _mm_min_ps(src, n[0]);
    n[2] = _mm_shuffle_ps(n[1], n[1], _MM_SHUFFLE(0,0,0,1));
    n[3] = _mm_min_ps(n[1], n[2]);

    return _mm_cvtss_f32(n[3]);
}

 SIZE  1000000000L // 1 billion. Yes.

void  get_min_max(long i, float array[i]) {
  __m128 max;
  __m128 min;
  
  max = _mm_loadu_ps(array); // will load first 4 float into max
  min = _mm_loadu_ps(array); // will load first 4 float into min
  while ((i -= 4L))
  {
    __m128 tmp = _mm_loadu_ps(array + i);
    max = _mm_max_ps(max, tmp);
    min = _mm_min_ps(min, tmp);
  }

  printf("Max value: %f\t Min value: %f\n", m128_max_float(max), m128_min_float(min));
}

void  get_min_max_like_bocalian(long size, float array[size]) {
  float max;
  float min;
  int i;

  max = array[0];
  min = array[0];
  i = 1L;
  while (i < size)
  {
    float tmp = array[i++];
    max = tmp < max ? max : tmp;
    min = tmp > min ? min : tmp;
  }

  printf("Max value: %f\t Min value: %f\n", max, min);
}

int main()
{
  long i;
  float *data;
  clock_t time;

  srand(time(NULL));  // seed
  data = (float *)malloc(SIZE * sizeof(float));
  i = -1L;
  while (++i < SIZE) {
    data[i] = (float)rand() / (float)(RAND_MAX) * 1000.0f;
   /* printf("%.02f\t\t", data[i]);     // I commented these lines because it slows considerably the program.
    if (!(i & 15))
      printf("\n");*/
  }

  time = clock();
  get_min_max(SIZE, data);
  time = clock() - time;
  double elapsed_time = ((double)time) / CLOCKS_PER_SEC;
  printf("Executed in %f seconds\n", elapsed_time);

  time = clock();
  get_min_max_like_bocalian(SIZE, data);
  time = clock() - time;
  elapsed_time = ((double)time) / CLOCKS_PER_SEC;
  printf("Executed in %f seconds\n", elapsed_time); 

  return 0;
}
```

And compile with:
```
gcc vectorization.c -O3  && ./a.out 
```

You will notice that the vectorized approach will be about 3 times faster (NB: For this specific example). If I was using mm256 or mm512 registers, the vectorized program would be even faster by a factor of 2 and 4 respectively.

*Now that you realize the performance boost, how about using what you just learn for your RayTracing project?*


### Combining Optimization Flags, Parallelization and Vectorization

*a) **You can take a look at [this very interesting project](https://github.com/expr-fi/fastlwc/blob/master/fastlwc-mt.c)** which aim to show how fast wc can get using the various tools C has to offer to optimize speed. After downloading the file, you will also need to download the header: [simd.h](https://github.com/expr-fi/fastlwc/blob/master/simd.h), which make use of [Intel intrinsic](https://software.intel.com/sites/landingpage/IntrinsicsGuide/).*  

*b) Compile it with the flags:*
```
gcc fastlwc-mt.c -fopenmp -O3
```

*c) Create a random file:*
```
dd if=/dev/urandom of=sample.txt bs=64M count=16 iflag=fullblock
```

*d) Compare wc with the new binary with:*
```
time ./a.out sample.txt \
&& time wc sample.txt
```

### The Right Algorithm

**The right algorithm is usually the corner stone of an efficient program.**

*How about solving this [algorithm problem](https://github.com/agavrel/Nailing-the-Coding-Interview/tree/master/math/the_dancer):*

```c
int32_t dancer_position(uint32_t time_elapsed) { ;}
```


### Exploring Compiler's Assembly Output

Let's take and example with the brilliant [UTF-8](https://en.wikipedia.org/wiki/UTF-8) implementation, especially at how continuation bytes are designed: 

> continuation bytes start with 10 while single bytes start with 0 and longer lead bytes start with 11

Let's say that you have to write a function that determines if the byte is a continuation one, you can think of many ways that would end with the same result. But they will have a different output in their assembly.


You can retain the two first bits wwith ```& 0b11000000``` and then make sure that the first one is set and the second one is not with ```== 0b10000000``` :
```c
 <stdbool.h>

bool is_utf8_continuation_byte(char c) {
	return ((c & 0b11000000) == 0b10000000);  
}
```

Which corresponds to the following compiler output with ```gcc x86-64 9.3 with -O3 optimization flag``` :
```asm
and     edi, 192
cmp     edi, 128
sete    al
```


Another way would be to shift the bits to the right:
```c
bool is_utf8_continuation_byte(char c) {
	return (!((((unsigned char)c >> 6) ^ 0b10)));
}
```
Here I cast c into unsigned in order to be able to shift the MSB to the right with ```(unsigned char)c```  
Then I shift it 6 times to the right with ``` >> 6``` because we do not care about the content of the 6 lowest bits.  
Finally I xor the result by 0b10 with ```^ 0b10```, which corresponds to specification of a continuation byte as quoted before.
As a number xored by itself gives 0, I use the exclamation mark ! to reverse the result from 0 to 1. (Else we would have to rename the function ```is_not_utf8_continuation_byte```)


It is not producing the following output that you could imagine:
```asm
sar     edi, 6
xor     edi, 2
not		edi,
```

But the optimized version:
```asm
movzx   edi, dil
sar     edi, 6
cmp     edi, 2
sete    al
```
It's even less efficient.


Finally since the valid range 0b10111111 to 0b10000000 (corresponding to -128 to -65, both included), you can add 0b01000000 and check if the byte is negative:
```c
bool is_utf8_continuation_byte(char c) {
	return (c + 0b01000000 < 0);
}
```

In other word you compare to -64 and check if it is lower:
```asm
cmp     dil, -64
setl    al
```

**To see the assembly output you can use the following command which will generate an assembly file with intel syntax (more readable than AT&T):**
```
gcc -O3 -S -masm=intel a.c && cat a.s
```

*or use the excellent [compiler explorer from godbolt](https://godbolt.org/)*

**I hope that you liked this demonstration that shows that functions with same behaviors can produce different assembly output, hence being more or less efficient. If you want to build your program to be the most efficient you should explore the assembly code of functions in critical loops**


---
## 0x01 ~ Computer Graphics - Using [SDL2](https://www.libsdl.org/index.php) to create Fractal

### Using SDL2 to create Computer Graphics
You can follow tutorials to create a simple program with SDL on [Lazyfoo's website](https://lazyfoo.net/tutorials/SDL/01_hello_SDL/linux/index.php) or on SDL2 official website.

You will also have to install SDL2:
```
brew install sdl2
```

With SDL2 you have to first ```init_sdl``` - *see function below*. Then you will keep the user entertained with a loop ```while (42)``` that can only be escaped by clicking on the the close button or pressing escape. While the loop is active, user's actions will be recorded thanks to ```SDL_PollEvent```. You then draw pixel by using ```SDL_RenderDrawPoint``` and you refresh image with ```SDL_RenderPresent```.

### Example with a Barnsley Fern Fractal

[Michael Barnsley](https://en.wikipedia.org/wiki/Michael_Barnsley) was a British mathematician who coined a fractal algorithm to represent a fern.  

![Barnsley Fern](https://raw.githubusercontent.com/agavrel/42_CheatSheet/master/img/BarnsleyFern.png)

The algorithm is explained in detail on [wikipedia](https://en.wikipedia.org/wiki/Barnsley_fern)  

Find below the code for the whole program, compile it with :
```
gcc barnsley.c -lSDL2 -O3
```

You will need about 10 000 iterations of n to draw the shape. On each keypress you will increase the number of iterations by 400.
```c
 message "\033[1;31mRequire SDL2\033[0m, \033[1;92mbrew install sdl2\033[0m and compile with \033[1;5;36mgcc barnsley.c -lSDL2\033[0m  && ./a.out  " __FILE__ "..."
// gcc main.c -lSDL2 -O3 -Wall -Werror -Wextra --pedantic&& ./a.out
 <stdio.h>
 <SDL2/SDL.h>
 <stdbool.h>

 WINDOW_WIDTH	600
	WINDOW_HEIGHT	800

typedef struct		s_cnb
{
	double			real;
	double			imag;
}					t_cnb;

typedef struct		s_pixel
{
	int				x;
	int				y;
}					t_pixel;

void	barnsley(SDL_Renderer *renderer, t_cnb *c) {
	float	rng;
	t_pixel	i;
	static const float probability[3] = {0.01f, 0.08f, 0.15f};
	long n = 400;

	while (n--) {
		rng = ((float)rand() / (float)RAND_MAX);
		if (rng <= probability[0]) {
			c->real = 0;
			c->imag *= 0.16f;
		}
		else if (rng <= probability[1]){
			c->real = -0.15f * c->real + 0.28f * c->imag;
			c->imag = 0.26f * c->real + 0.24f * c->imag + 0.44f;
		}
		else if (rng <= probability[2]) {
			c->real = 0.2f * c->real + -0.26f * c->imag;
			c->imag = 0.23f * c->real + 0.22f * c->imag + 1.6f;
		}
		else {
			c->real = 0.85f * c->real + 0.04f * c->imag;
			c->imag = -0.04f * c->real + 0.85f * c->imag + 1.6f;
		}
		i.x = (c->real + 3) * 70;
		i.y = WINDOW_HEIGHT - c->imag * 70;
    	SDL_RenderDrawPoint(renderer, i.x, i.y);
	}
}

bool	error_sdl(char *error_msg) {
	printf( "%s! SDL_Error: %s\n", error_msg, SDL_GetError() );
	return false;
}

bool	init_sdl(SDL_Window **window, SDL_Renderer **renderer) {
	if (SDL_Init(SDL_INIT_VIDEO) < 0)
		return (error_sdl("SDL could not initialize!"));
	SDL_CreateWindowAndRenderer(WINDOW_WIDTH, WINDOW_HEIGHT, 0, window, renderer);
	if (*window == NULL)
		return (error_sdl("Window could not be created!"));
	SDL_SetRenderDrawColor(*renderer, 0, 0, 0, 0);
	SDL_RenderClear(*renderer);
    SDL_SetRenderDrawColor(*renderer, 0xbf, 0xff, 0, 0);

	return true;
}

int		main(void) {
    SDL_Event event;
    SDL_Window *window;
	SDL_Renderer *renderer;
	t_cnb c;
	
	if (!(init_sdl(&window, &renderer)))
		return 1;

	c = (t_cnb) {.real = 0, .imag = 0}; // PS: legal for Norminette
    while (42) {
		if (SDL_PollEvent(&event)) {
			if (event.type == SDL_QUIT)
				break ;
			else if (event.type == SDL_KEYDOWN) {
				if (event.key.keysym.sym == SDLK_ESCAPE)
					break ;
				barnsley(renderer, &c);
				SDL_RenderPresent(renderer);
			}
		}
    }
    SDL_DestroyRenderer(renderer);
    SDL_DestroyWindow(window);
    SDL_Quit();
    return EXIT_SUCCESS;
}
```

---
## 0x02 ~ Hacking - Buffer Overflow

### Introduction

Let's take a look at the function strcpy, shall we? Type ```man strcpy``` in your terminal:

> *The  strcpy() function copies the string pointed to by src, including the terminating null byte ('\0'), to the buffer pointed to by dest.  The strings may not overlap, and the destination string dest must be large enough to receive the copy.  Beware of buffer overruns!  **(See BUGS.)***

**NB: Usage of brackets for what is considered as one of the most critical security flaw in the world**

> ***BUGS:**  
If  the  destination  string of a strcpy() is not large enough, then anything might happen ― **NB: Undefined Behavior**.  Overflowing fixed-length string buffers is a favorite cracker technique for taking complete control of the machine.  Any time a program reads or copies data into a buffer, the program first needs to  check  that  there's  enough  space. This may be unnecessary if you can show that overflow is impossible, but be careful: programs can get changed over time, in ways that may make the impossible possible.*

```c
 <string.h>
 <stdio.h>

int main(void) {
	char s[11];

	strcpy(s, "hello world");
	puts(s);	

	return 0;
}
```

While this look okay if you count each letter, if you happen to read again the definition of strcpy (just above) you will notice: 
> ***including the terminating null byte ('\0')***

So you are trying to copy 12 characters in fact, into a 11 characters buffer. You will get the nice message:

```bash
In function ‘main’:
warning: ‘__builtin_memcpy’ writing 12 bytes into a region of size 11 overflows the destination [-Wstringop-overflow=]
strcpy(s, "hello world");
```

In fact all functions that you will find in [```#include <banned.h>```](https://github.com/git/git/blob/master/banned.h) represent potential security risks and should be avoided as much as possible.

### Buffer overflow to hijack a password

```c
 <stdio.h>
 <string.h> // for strcmp, compare two strings and return 0 if they are equal

char    *strcpy_until(char *dst, char *src, char until)
{
	int i = -1;

	while (src[++i] != until)
		dst[i] = src[i];
    
	return (dst);
}

int     main(int ac, char **av) {
    int n = 5;
    char password[] = "sarang hae"; // we don't know
    char buffer[4] = "kkk";

    if (ac != 2)
        return 1;
    printf("n equals %d\n", n);
    printf("you would have never guessed, password was '%s'\n\n", password);
    char *s = &buffer[3];
    char shellcode[] = "\x42\x61\x67\x61\x76\x72\x65\x6c\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00\x2a\x00\x00\x01";
    strcpy_until(s, shellcode, '\x01');
    printf("n equals '%d'\n", n);
    printf("password now equals: '%s'\n", password);

    if (!strcmp(password, av[1])) {
        printf("\nSuccessfully hacked user with password \e[1;5;92m%s\e[0m\n", password);        
    }
    return 0;
}
```
*Would you have guessed the password?*  

Some explanations:
* ```strcpy_until``` will copy until a specific character, hence allowing to bypass the NULL that terminates the string
* ```char shellcode[]``` can be used to, instead of just replacing value at memory addresses, execute the value that have been replaced. See next below...


### Shellcode Execution to get root access

> **When something is important enough, you do it even if the odds are not in your favor** ― *Elon Musk*

You will now have to compile with:
```
gcc -fno-stack-protector -z execstack a.c
```

* ```-fno-stack-protector a.c``` is to disable the [Stack-Guard mechanism](https://en.wikipedia.org/wiki/Buffer_overflow_protection)
* Compiler make prevent stack from being executable and ```-z execstack``` reverse that protection.


Last you will also **temporarily** disable randomize va space with:
```
sudo sysctl -w kernel.randomize_va_space=0
```
NB: You can use safer method ```setarch `uname -m` -R /bin/bash``` which is [more safe](https://askubuntu.com/questions/318315/how-can-i-temporarily-disable-aslr-address-space-layout-randomization)

Once done with experiments do not forget to set back randomize back to normal:
```
sysctl -a --pattern "randomize" && \
sudo sysctl -w kernel.randomize_va_space=2
```

{WIP}


---
## 0x03 ~ Chess Bitboard

Often you will have programs where you want to represent data the following way:

```c
int	map[8][8];
```

While it looks like it is convenient, you can make it convenient using the right functions. But if you are using an integer to tell if the board is filled with pieces, you are wasting a lot of memory.

```c++
 <iostream>
 <map>

using namespace std;

void    print_binary(uint64_t n)
{
    uint64_t mask = 0;
    for (mask = ~mask ^ (~mask >> 1); mask != 0; mask >>= 1)
        putchar('0' + !!(n & mask));
    putchar('\n');
}

void    fill_board(uint64_t board[12], uint64_t *used_cells)
{
    const uint64_t initial_pos[6] = {   0b0000000011111111000000000000000000000000000000001111111100000000, // most right is a1, most left is h8
                                        0b1000000100000000000000000000000000000000000000000000000010000001,
                                        0b0100001000000000000000000000000000000000000000000000000001000010,
                                        0b0010010000000000000000000000000000000000000000000000000000100100,
                                        0b0001000000000000000000000000000000000000000000000000000000001000,
                                        0b0000100000000000000000000000000000000000000000000000000000010000
    };
    const uint64_t  color_mask[2] = {   0b0000000000000000000000000000000011111111111111111111111111111111,
                                        0b1111111111111111111111111111111100000000000000000000000000000000
    };

	*used_cells = 0;
    for (int i = 0; i < 12; i++) {
        board[i] = (initial_pos[i >> 1]) & (color_mask[i & 1]);
		*used_cells |= board[i];
	}
}

void    display_board(uint64_t board[12])
{
    for (int i = 0; i < 12; i++)
        print_binary(board[i]);
}

std::map<string, uint64_t>  fill_move() {
    std::map<string, uint64_t>  move;

    for (char r = '1'; r <= '8'; r++) {
        for (char c = 'a'; c <= 'h'; c++) {
            char cell[3] = {c, r, '\0'};
            move[cell] = (1UL << (8 * (c - 'a'))) << (r - '1');
        }
    }
    return move;
}

enum PIECE {
    __PAWN_W = 0,
    __PAWN_B,
    __ROOK_W,
    __ROOK_B,
    KNIGHT_W,
    KNIGHT_B,
    BISHOP_W,
    BISHOP_B,
    _QUEEN_W,
    _QUEEN_B,
    __KING_W,
    __KING_B = 11
};


int main()
{    
    uint64_t    board[12];
	uint64_t	used_cells;
    std::map<string, uint64_t> move = fill_move();

    fill_board(board, &used_cells);
    display_board(board);
    
    putchar('\n');
    print_binary(board[__PAWN_W]);

    if (board[__PAWN_W] & move["b4"]) // check if exist
        board[__PAWN_W] ^=  ((move["b4"] | move["e4"]));
    
    print_binary(board[__PAWN_W]);
    putchar('\n');

    return 0;
}
```


--- 
# Epilogue

--- 
## 0x00 ~ Wanted Pull Requests

> **If you know how to make software, then you can create big things** ― *Xavier Niel*

*One function related to each 42 project to help students get started*  
*In-depth examples with pointers*  
*Books on system design*  
*Exemple of a Makefile "qui fait le cafe"*


---
## 0x01 ~ Question ? Broken Link ? Wanna contribute ?

> **I think it's very important to have a feedback loop, where you're constantly thinking about what you've done and how you could be doing it better** ― *Elon Musk*

*Raise an issue or even better: submit a pull request*

First fork the repository and clone it locally (you will be forgiven for this kind of git clone)

Make the desired changed to the README.md file

Then open the terminal containing your fork and enter:
```
git checkout -b agavrel
git commit -am "[ADD] Interesting link about C Hash"
git push --set-upstream origin agavrel
```

Go back to internet and you will see that you can submit a pull request.

*I will personally review contributions*


---
## 0x02 ~ Liked it ?
*Show your appreciation by starring the repo, sharing on slack, RT and 'lache un com magueule' skyblog™*

![Kimg Jeong Un applauding](https://raw.githubusercontent.com/agavrel/42_CheatSheet/master/img/kimjeongun_meme.gif)

> 잘했어 동무 계속 [배우자](https://www.youtube.com/watch?v=ukBcC-sK3wQ) ― *Good Job Comrade, let's keep studying*


---
## :musical_score: 0x2A ~ About the Author

**Antonin GAVREL**

*Feel free to reach me on [LinkedIn](https://www.linkedin.com/in/antonin-gavrel-086b2618/)*
