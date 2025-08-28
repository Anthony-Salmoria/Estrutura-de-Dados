# Estrutura-de-Dados
Atividades

Jogo da Velha -> Alunos: Anthony Salmoria, Arthur Ricardo

using System;

class Program
{
    static char[,] tabuleiro = {
        { '1', '2', '3' },
        { '4', '5', '6' },
        { '7', '8', '9' }
    };

    static int jogadas = 0;
    static char jogadorA = 'X';

    static void Main(string[] args)
    {
        while (true)
        {
            Console.Clear();
            MostrarTabuleiro();

            Jogar();

            if (VerificarVencedor())
            {
                Console.Clear();
                MostrarTabuleiro();
                Console.WriteLine($"\n Jogador {jogadorA} venceu!");
                break;
            }

            if (jogadas == 9)
            {
                Console.Clear();
                MostrarTabuleiro();
                Console.WriteLine("\n Empate!");
                break;
            }

            jogadorA = (jogadorA == 'X') ? 'O' : 'X';
        }

        Console.WriteLine("\nPressione qualquer tecla para sair...");
        Console.ReadKey();
    }

    static void MostrarTabuleiro()
    {
        Console.WriteLine("Jogo da Velha\n");

        for (int i = 0; i < 3; i++)
        {
            Console.WriteLine($" {tabuleiro[i, 0]} | {tabuleiro[i, 1]} | {tabuleiro[i, 2]} ");
            if (i < 2)
                Console.WriteLine("---|---|---");
        }
    }

    static void Jogar()
    {
        int escolha;
        bool jogadaValida = false;

        do
        {
            Console.Write($"\nJogador {jogadorA}, escolha uma posição (1-9): ");
            string entrada = Console.ReadLine();

            if (int.TryParse(entrada, out escolha) && escolha >= 1 && escolha <= 9)
            {
                int linha = (escolha - 1) / 3;
                int coluna = (escolha - 1) % 3;

                if (tabuleiro[linha, coluna] != 'X' && tabuleiro[linha, coluna] != 'O')
                {
                    tabuleiro[linha, coluna] = jogadorA;
                    jogadas++;
                    jogadaValida = true;
                }
                else
                {
                    Console.WriteLine(" Essa posição já está ocupada, escolha outra");
                }
            }
            else
            {
                Console.WriteLine(" Entrada inválida, digite um número de 1 a 9.");
            }
        } while (!jogadaValida);
    }

    static bool VerificarVencedor()
    {
        
        for (int i = 0; i < 3; i++)
        {
            if ((tabuleiro[i, 0] == tabuleiro[i, 1] && tabuleiro[i, 1] == tabuleiro[i, 2]) ||
                (tabuleiro[0, i] == tabuleiro[1, i] && tabuleiro[1, i] == tabuleiro[2, i]))
            {
                return true;
            }
        }

    
        if ((tabuleiro[0, 0] == tabuleiro[1, 1] && tabuleiro[1, 1] == tabuleiro[2, 2]) ||
            (tabuleiro[0, 2] == tabuleiro[1, 1] && tabuleiro[1, 1] == tabuleiro[2, 0]))
        {
            return true;
        }

        return false;
    }
}
