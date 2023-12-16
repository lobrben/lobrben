
using System;

class VierGewinnt
{
    static char[,] spielfeld = new char[6, 7];
    static char aktuellerSpieler = 'X';

    static void Main()
    {
        InitialisiereSpielfeld();
        while (true)
        {
            ZeigeSpielfeld();
            int spalte = HoleSpielerEingabe();
            PlatziereStein(spalte);
            if (Gewonnen())
            {
                ZeigeSpielfeld();
                Console.WriteLine("Spieler " + aktuellerSpieler + " hat gewonnen!");
                break;
            }
            if (Unentschieden())
            {
                ZeigeSpielfeld();
                Console.WriteLine("Unentschieden!");
                break;
            }
            WechselSpieler();
        }
        Console.ReadLine();
    }

    static void InitialisiereSpielfeld()
    {
        for (int i = 0; i < 6; i++)
        {
            for (int j = 0; j < 7; j++)
            {
                spielfeld[i, j] = ' ';
            }
        }
    }

    static void ZeigeSpielfeld()
    {
        Console.Clear();
        for (int i = 0; i < 6; i++)
        {
            for (int j = 0; j < 7; j++)
            {
                Console.Write("|" + spielfeld[i, j]);
            }
            Console.WriteLine("|");
        }
        Console.WriteLine(" 1 2 3 4 5 6 7");
    }

    static int HoleSpielerEingabe()
    {
        int spalte;
        while (true)
        {
            Console.Write("Spieler " + aktuellerSpieler + ", wähle eine Spalte (1-7): ");
            if (int.TryParse(Console.ReadLine(), out spalte) && spalte >= 1 && spalte <= 7 && spielfeld[0, spalte - 1] == ' ')
            {
                return spalte - 1;
            }
            Console.WriteLine("Ungültige Eingabe. Bitte versuche es erneut.");
        }
    }

    static void PlatziereStein(int spalte)
    {
        for (int i = 5; i >= 0; i--)
        {
            if (spielfeld[i, spalte] == ' ')
            {
                spielfeld[i, spalte] = aktuellerSpieler;
                break;
            }
        }
    }

    static void WechselSpieler()
    {
        aktuellerSpieler = (aktuellerSpieler == 'X') ? 'O' : 'X';
    }

    static bool Gewonnen()
    {
        return HorizontaleGewonnen() || VertikaleGewonnen() || DiagonaleGewonnen();
    }

    static bool HorizontaleGewonnen()
    {
        for (int i = 0; i < 6; i++)
        {
            for (int j = 0; j < 4; j++)
            {
                if (spielfeld[i, j] != ' ' && spielfeld[i, j] == spielfeld[i, j + 1] && spielfeld[i, j] == spielfeld[i, j + 2] && spielfeld[i, j] == spielfeld[i, j + 3])
                {
                    return true;
                }
            }
        }
        return false;
    }

    static bool VertikaleGewonnen()
    {
        for (int i = 0; i < 3; i++)
        {
            for (int j = 0; j < 7; j++)
            {
                if (spielfeld[i, j] != ' ' && spielfeld[i, j] == spielfeld[i + 1, j] && spielfeld[i, j] == spielfeld[i + 2, j] && spielfeld[i, j] == spielfeld[i + 3, j])
                {
                    return true;
                }
            }
        }
        return false;
    }

    static bool DiagonaleGewonnen()
    {
        for (int i = 0; i < 3; i++)
        {
            for (int j = 0; j < 4; j++)
            {
                if (spielfeld[i, j] != ' ' && spielfeld[i, j] == spielfeld[i + 1, j + 1] && spielfeld[i, j] == spielfeld[i + 2, j + 2] && spielfeld[i, j] == spielfeld[i + 3, j + 3])
                {
                    return true;
                }
            }
        }
        for (int i = 0; i < 3; i++)
        {
            for (int j = 3; j < 7; j++)
            {
                if (spielfeld[i, j] != ' ' && spielfeld[i, j] == spielfeld[i + 1, j - 1] && spielfeld[i, j] == spielfeld[i + 2, j - 2] && spielfeld[i, j] == spielfeld[i + 3, j - 3])
                {
                    return true;
                }
            }
        }
        return false;
    }

    static bool Unentschieden()
    {
        for (int i = 0; i < 7; i++)
        {
            if (spielfeld[0, i] == ' ')
            {
                return false;
            }
        }
        return true;
    }
}
