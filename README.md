### Ver informacion del procesador

~~~
$ cat /proc/cpuinfo | less
~~~

### Ver solo el modelo

~~~
$ cat /proc/cpuinfo | grep 'model name' | head -n 1
~~~

### Ver numeros de cores

~~~
$ cat /proc/cpuinfo | grep 'cpu cores' | head -n 1
~~~

### Ver hilos por core

~~~
$ cat /proc/cpuinfo | grep 'core id' | sort | uniq -c | head -n 1 | awk '{print $1}'
~~~

### Ver numero de hilos totales
~~~
$ cat /proc/cpuinfo | grep 'core id' | wc -l
~~~

### cpu soporte

- REF: https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git/tree/arch/x86/include/asm/cpufeatures.h

~~~
$ cat /proc/cpuinfo | grep 'flags' | head -n 1
~~~

### Principales a considerar a la fecha 2020

- mmx

- sse
- sse2
- ssse3
- sse4_1
- sse4_2

- avx
- avx2
- avx512

- fma

### Calcular rendimiento pico teorico

~~~
  rendimiento pico en GFlops = velocidad de CPU en GHz * numero de cores * numero de hilos por core * SIMD registro * instrucciones por ciclo
~~~

- buscar en google: Intel export spec
- REF: https://www.intel.com/content/www/us/en/support/articles/000005755/processors.html

###  Calcularlo para mi laptop [ Intel(R) Core(TM) i7-7500U CPU @ 2.70GHz ]

- Segun la referencia anterior si buscamos mi procesador sale como resultado: 86.4 GFLOPS vamos a comprobar este dato

- Velocidad de reloj: 2.70GHz
- Cores: 2
- Hilos por core: 2
- Soporta AVX2 por lo tanto 256/8 -> 32 bytes y si buscamos presicion doble 32 bytes / 8 bytes = 4 bytes
- Soporta FMA que significa que podemos sumar y multiplicar en el mismo ciclo de reloj entonces hacemos 2 instrucciones por ciclo

~~~
  resultado = 2.7 GHz * 2 * 2 * 4 * 2 = 86.4 GFLOPS 
~~~
