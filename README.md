# Readme
Game em C

wanted to get the conditions of the plays in the array in random with the function, but I'm not figuring out a way to do that.

#include <stdio.h>
#include <stdlib.h>


#define L 5
#define C 10


int main()
{
	char mat[L][C],op;

    do
    {
        IniciaMatriz(mat);
        Instrucoes(mat);
        Jogada(mat);
        printf("\n ---> Deseja Jogar Novamente? sim(s) ou nao(n): ");
        getchar();
        scanf("%c", &op);
        getchar();
        clear();
    }
    while(op == 's' || op == 'S');


	return 0;
}

void clear()
{
	system("clear || cls");   /*Funcao para limpeza de tela tanto no windows ou no linux*/
}

void IniciaMatriz(char mat[L][C])
{
	int i, j;

	printf("\t       *** JOGO ***\n\n");
	printf("\t\t");

	for(i = 0; i < L; i++)
	{
		for(j = 0; j < C; j++)
		{                             /*Funcao para impressao da matriz de caractere */
			mat[i][j] = '#';
			printf("%c", mat[i][j]);
		}
		printf("\n\t\t");
	}
}

void Instrucoes(char mat[L][C])
{
	printf("\n\t     *** Instrucoes ***\n");
	printf("\n\t-> Escolha a Linha e a Coluna.\n\t-> Acertar Bomba (*) - [10] Pts.\n");
	printf("\t-> Acertar o Alvo ($) + [10] Pts.\n\t-> Acertar Vazio ( ) mantem os Pts.\n"); /*Funcao com  as instrucoes do jogo  */
	printf("\t-> Voce tem 20 Jogadas.");
	printf("\n\n\t Aperte [ENTER] para iniciar");
	getchar();
	clear();
	IniciaMatriz(mat);
}

void Jogada(char mat[L][C])
{
	int i, j, jogadas = 1, pontos = 0;



	while(jogadas <= 20) /*laco para jogadas */
	{
		do
		{
			printf("\n\t -> Escolha a linha e coluna <-\n");
			do
			{
				printf("\tLinha entre [0] e [4]: ");
				scanf("%d", &i);
			}
			while(i < 0 || i > 4);   /*restricao de jogadas fora dos limites */

			do
			{
				printf("\tColuna entre [0] e [9]: ");
				scanf("%d", &j);
			}
			while(j < 0 || j > 9 ); /*restricao de jogadas fora dos limites */

			if(mat[i][j] != '#')
				printf("\n\t     Jogada Repetida!!\n");
		}
		while((mat[i][j] != '#')); /*restricao para jogadas repetidas*/

       clear();

		/*condicao para cada jogada Acerto,Bomba e Vazio*/
		if((i == 0 && j == 7) || ( i == 0 && j == 3) || ( i == 1 && j == 4) || (i == 1 && j == 8) || ( i == 2 && j == 4) || (i == 2 && j == 1) || ( i == 3 && j == 4) || (i == 3 && j == 6) || ( i == 4 && j == 7) || (i == 4 && j == 2) )
		{
			mat[i][j] = '$';
			printf("\t      $$$ Acertou $$$\n");
			pontos++;
		}

		else if((i == 0 && j == 5) || (i == 0 && j == 9) || (i == 1  && j == 1) | ( i == 1 && j == 5) || (i == 2  && j == 2) || ( i == 2 && j == 7) || (i == 3  && j == 2) | ( i == 3 && j == 9) || (i == 4  && j == 1) || ( i == 4 && j == 6))
		{
			mat[i][j] = '*';
			printf("\t       *** Bomba ***\n");
			pontos--;
		}

		else
		{
			mat[i][j] = ' ';
			printf("\t\t   Vazio \n");
		}

            		 if(jogadas == 20)
          		  {
               	       	     printf("\t\t -->FIM<-- \n");
           		  }

		printf(" JOGADAS:[%d]\t\t      PONTOS:[%d]\n", 20 - jogadas , pontos * 10);
		printf("\t\t");
		for(i = 0; i < L; i++)
		{
			for(j = 0; j < C; j++)              /*impressao da matriz de caractere com sua respectiva condicao de jogada*/
			{
				printf("%c", mat[i][j]);
			}
			printf("\n\t\t");

		}
		jogadas++;/*contador de jogadas */
	}
	clear();
    printf("\n\n");
	printf("\t--------------------------------------------------\n");
    printf("\t|****** FIM DE JOGO!! TOTAL DE PONTOS  [%d] ******|\n ", pontos * 10);
    printf("\t--------------------------------------------------\n");
        if(pontos < 10)
        {                                                                                /*Pontuacao e condicoes para cada tipo de resultado. */
            printf("\n\n");
            printf("\t\t\t-----------------------\n");
            printf("\t\t\t|MELHORE ESSA PONTUACAO|\n");
            printf("\t\t\t-----------------------");
        }
        printf("\n\n\n\n");
}
