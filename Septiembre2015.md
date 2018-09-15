**_METODOLOGÍA DE LA PROGRAMACIÓN_**
====================================
Examen _Septiembre_ 2015
========================

En este documento estarán los tres ejercicios preparados para ser copiados y pegados en el editor de texto que usted desee.

  - [Ejercicio 1](#ejercicio-1)
  - [Ejercicio 2](#ejercicio-2)
  - [Ejercicio 3](#ejercicio-3)


## Ejercicio 1 ##

Implementa un programa que, **utilizando funciones** realice las siguientes operaciones secuencialmente:
  1. Crear una lista de N valores enteros.
  2. Imprimir la lista por pantalla.
  3. Determinar en una **única** función, el mayor y el menor valor de la lista, utilizando paso de parámetros por referencia.

  Ten en cuenta lo siguiente:
  1. La función para mostrar la lista será una función recursiva.
  2. El mayor y el menor valor de la lista se imprimirá desde el programa principal.
  
  
**_¡IMPORTANTE!_**
  - Se crearán los ficheros dentro de la carpeta _ejercicio1_ de tu cuenta de examen: _main.c_, _funciones.c_, _funciones.h_.
  - _¿Cómo compilar y crear ejecutable?_ Primero escribiremos en la linea de comandos (SIEMPRE DENTRO DE LA CARPETA DONDE SE ENCUENTRAN LOS ARCHIVOS DE ESTE EJERCICIO, en este caso, abriremos el terminal dentro de la carpeta _ejercicio1_) la sintaxis **gcc main.c funciones.c** y se nos creará un ejecutable por defecto **a.out**. A continuacón ejecutaremos _a.out_ como **./a.out** y veremos nuestro programa ejecutado en el terminal.




### main.c

	#include "funciones.h"


	int main() {
		int tam, mayor, menor;
		struct nodo* cabeza = NULL;

		//1.
		printf("Introduzca N: ");
		scanf("%d", &tam);
		creaLista(&cabeza, tam);

		//2.
		mostrarListaRecursiva(cabeza);

		//3.
		mayorMenor(cabeza, &mayor, &menor, tam);
		printf("mayor = %d\n", mayor);
		printf("menor = %d\n", menor);

		return 0;
	}




### funciones.c

	#include "funciones.h"


	void creaLista(struct nodo** cabeza, int tam) {
		int i, n;

		for (i = 0; i < tam; i++) {
			printf("Introduzca entero: ");
			scanf("%d", &n);
			insertarDetras(&(*cabeza), n);
		}
	}


	void insertarDetras(struct nodo** cabeza, int x) {
		struct nodo* nuevo = NULL;
		struct nodo* aux;

		nuevo = nuevoElemento();
		nuevo->dato = x;
		nuevo->sig = NULL;
		if (*cabeza == NULL) {
			(*cabeza) = nuevo;
		}
		else {
			aux = (*cabeza);
			while (aux->sig != NULL) {
				aux = aux->sig;
			}
			aux->sig = nuevo;
		}
	}


	struct nodo* nuevoElemento() {
		return (struct nodo*)malloc(sizeof(struct nodo));
	}


	void mostrarListaRecursiva(struct nodo* aux) {
		if (aux != NULL) {
			printf("%d -> ", aux->dato);
			aux = aux->sig;
			mostrarListaRecursiva(aux);
		}
		printf("\n");
	}


	void mayorMenor(struct nodo* cabeza, int* mayor, int* menor, int tam) {
		struct nodo* aux = cabeza;
		int v[tam], i = 0;

		while (aux != NULL) {
			v[i] = aux->dato;
			i++;
			aux = aux->sig;
		}

		*mayor = v[0];
		for (i = 0; i < tam; i++) {
			if (*mayor < v[i]) {
				*mayor = v[i];
			}
		}

		*menor = v[0];
		for (i = 0; i < tam; i++) {
			if (*menor > v[i]) {
				*menor = v[i];
			}
		}
	}




### funciones.h

	#include <stdio.h>
	#include <stdlib.h>
	#ifndef FUNCIONES_H
	#define FUNCIONES_H

	struct nodo {
		int dato;
		struct nodo* sig;
	};

	void creaLista(struct nodo** cabeza, int tam);
	void insertarDetras(struct nodo** cabeza, int x);
	struct nodo* nuevoElemento();
	void mostrarListaRecursiva(struct nodo* aux);
	void mayorMenor(struct nodo* cabeza, int* mayor, int* menor, int tam);

	#endif



## Ejercicio 2 ##

En el directorio _ejercicio2_ de tu cuenta de examen tienes un fichero binario (_productos.bin_) con información sobre productos que hay en una tienda. La información está almacenada mediante la siguiente estructura:

	struct producto {
		char nombre[50];
		int cod;
		float precio;
		int unidades;
	};

Diseña y codifica una función que distribuya los productos del fichero binario en dos ficheros de texto. En un fichero se almacenarán los productos con más de X unidades y en el otro, los productos con menos o igual número de unidades.

Ten en cuenta lo siguiente:
  - El programa recibirá como argumentos en la línea de órdenes los nombres de los ficheros binario y texto.
  - El programa deberá comprobar la existencia del fichero binario.
  - El programa principal deberá preguntar el valor de X.
  - Divide tu programa en 5 ficheros: _main.c texto.c binario.o texto.h_ y _binario.h_.
  - Utiliza inclusión condicional de código.
  En el directorio _ejercicio2_ tienes un programa denominado _visualiza.exe_ que te permite visualizar el fichero _productos.bin_.


**_¡IMPORTANTE!_**  
El archivo _visualiza.exe_ **sólo** sirve para mostrar el fichero binario _productos.bin_ que ya te viene hecho dentro de tu carpeta _ejercicio2_. Luego, si quieres ver el contenido del fichero binario (será necesario para tener la misma distribución en el fichero de texto que crearemos) sólo necesitas escribir en la línea de comandos **./visualiza.exe**. A continuación, procedemos a los apartados del ejercicio.
