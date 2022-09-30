# Sistemas de Armários
O código deve gerir 8 armários de forma que o usuário pode escolher ocupar aleatoriamente um armário ou desocupar um armário especifico, além de imprimir quais armários estão ocupados e desocupados.

## Código
```c
#include <stdio.h>
#include <math.h>
#include <stdlib.h>
#include <time.h>
#define MX 8
#define CHEIO 0Xff

int main(void) {
  unsigned char ocupado = 0;
  int armario, escolha;

  srand(time(NULL));

  do {
    puts("############################");
    
    puts("Armários desocupados: ");
    for(int i = 0; i < MX; i++){
      if(!((ocupado >> i) & 1)){
        printf("%d ", i);
      }      
    }
    puts("\nArmários ocupados: ");
    for(int i = 0; i < MX; i++){
      if((ocupado >> i) & 1){
        printf("%d ", i);
      }      
    }

    printf("\nEscolha o que você quer fazer: \n(1) Reservar um armário \n(2) Esvaziar um armário \n(3) Sair\n");
    scanf("%d", &escolha);

    switch (escolha) {
      case 1:
        if(ocupado == CHEIO){
          puts("\nTodos os armários estão ocupados.");
          break;
        }

        do {
          armario = rand() % MX;
        } while ((ocupado >> armario) & 1);

        ocupado |= (int)pow(2, armario);
        printf("\nO armário %d foi ocupado.\n", armario);

        puts("############################\n");
      break;

      case 2:
        puts("\nDigite o armário que você quer desocupar: ");
        scanf("%d", &armario);

        if (armario < 0 || armario > MX) {
          puts("Armário inválido.");
          break;
        }

        if (!((ocupado >> armario) & 1)) {
          printf("\nO armário %d já está desocupado.\n", armario);
        } else {
          ocupado &= ~(int)pow(2, armario);
          printf("\nO armário %d foi desocupado.\n", armario);
        }
        puts("############################\n");        
      break;

      case 3:
        puts("Você saiu do programa.\n");
        puts("############################\n");
      break;

      default:
        puts("Escolha inválida.\n");
        puts("############################\n");
      break;
    }
  } while(escolha != 3);
}
```
