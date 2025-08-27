# Estrutura-de-Dados
Atividades

Jogo da Velha -> Alunos: Anthony Salmoria, Arthur Ricardo

using System;

class Program
{
    static char[,] tabuleiro = {
        {'1', '2', '3'},
        {'4', '5', '6'},
        {'7', '8', '9'}

    };

    static int jogadas = 0;
    static char jodadorA = 'X';

    static void Main(string[] args)
    {
        while (true)
        {
            Console.Clear();
            mostrartabuleiro();
            jogar();

            if (verificarvencedor())
            {
                Console.Clear();
                mostrartabuleiro();
                Console.WriteLine($"\n Jogador {jodadorA} venceu");
                break;
            }

            if (jogadas == 9)
            {
                Console.Clear();
                mostrartabuleiro();
                Console.WriteLine("\n Empate");
                break;
            }

            jodadorA = (jodadorA == 'x') ? '0' : 'x';

        }
    }

    private static bool verificarvencedor()
    {
        throw new NotImplementedException();
    }

    static void mostrartabuleiro()
    {
        Console.WriteLine("Jogo da Velha\n");
        for (int i = 0; i < 3; i++)
        {
            Console.WriteLine($" {tabuleiro[i, 0]} | {tabuleiro[i, 1]} | {tabuleiro[i, 2]}");
            if (i < 2)
                Console.WriteLine("---|---|---");
        }
    }

    static void jogar()
    {
        int escolha;
        bool jogadavalida = false;

        do
        {
            Console.Write($"\nJogador {jodadorA}, escolha uma posição (1-9): ");
            string entrada = Console.ReadLine();

            if (int.TryParse(entrada, out escolha) && escolha >= 1 && escolha <= 9)
            {
                int linha = (escolha - 1) / 3;
                int coluna = (escolha - 1) % 3;

                if (tabuleiro[linha, coluna] != 'x' && tabuleiro[linha, coluna] != 'o')
                {
                    tabuleiro[linha, coluna] = jodadorA;
                    jogadas++;
                    jogadavalida = true;
                }
                else
                {
                    Console.WriteLine("Essa posição ja esta ocupada, escolha outra posição");
                }
            }
            else
            {
                Console.WriteLine("Entrada invalida, digite um número de 1 a 9");
            }

        } while (!jogadavalida);
    }

    static readonly bool verificar verificarvencedor()
    {
        for (int i = 0; i < 3; i++)
        {
            if ((tabuleiro[i, 0] != tabuleiro[i, 1] || tabuleiro[i, 1] != tabuleiro[i, 2]) && (tabuleiro[0, i] != tabuleiro[1, i] || tabuleiro[1, i] != tabuleiro[2, i]))
                continue;


        }
        if ((tabuleiro[0, 0] != tabuleiro[1, 1] || tabuleiro[1, 1] != tabuleiro[2, 2]) && (tabuleiro[0, 2] != tabuleiro[1, 1] || tabuleiro[1, 1] != tabuleiro[2, 0]))
            return;


    }

}
