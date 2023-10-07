#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <unistd.h>

#define NUM_THREADS_CLIENTE 4

pthread_t clientes[NUM_THREADS_CLIENTE];
pthread_t servidor;


int request = 0;
int respond = 0;

int soma = 0;

void *client(void *arg){

    int i = *(int*) arg;

    printf("thread %d\n", i);

    while(1){

        while(respond != i) request = i; 
        // seção crítica
        int local = soma;
        sleep(rand()%2);
        soma = local + 1;
        printf("Thread %d está com a soma igual: %d \n", i, soma);
        respond = 0;
        
    }

}

void *server(void *arg){

    while(1){
        while(request == 0);
        respond = request;
        while(respond != 0);
        request = 0;
    }

}

int main(){

    int i;
    int ids[NUM_THREADS_CLIENTE];



    for (i = 0; i < NUM_THREADS_CLIENTE; i++) {
        ids[i] = i + 1;
        pthread_create(&clientes[i], NULL, client, &ids[i]);
    }
    
    pthread_create(&servidor, NULL, server, NULL);


    for (i = 0; i < NUM_THREADS_CLIENTE; i++) {
        pthread_join(clientes[i], NULL);  
    }

    pthread_join(servidor, NULL);

    return 0;   
}
