//Magico Par
package magicopar2;
public class MagicoPar2 
{
    int n;
    int magico[][];

    public MagicoPar2(int n) 
    {
        this.n = n;
        magico = new int[n][n];
        
    }

    public boolean CuadroMagico() 
    {
        return sumaFilas() && sumaColumnas() && sumaDiagonales();
    }

    public int suma() 
    {
        int suma = n * (n * n + 1) / 2;
        return suma;
    }

    public boolean sumaFilas() 
    {
        boolean siSuma = true;
        int sumaFila = 0;
        int constante = suma();
        int f = 0;
        while (f < n && siSuma) 
        {
            for (int c = 0; c < n; c++) 
            {
                sumaFila += magico[f][c];
            }
            if (sumaFila != constante) 
            {
                siSuma = false;
            }
            f++;
            sumaFila = 0;
        }
        return siSuma;
    }

    public boolean sumaColumnas() 
    {
        boolean siSuma = true;
        int sumaColumna = 0;
        int constante = suma();
        int j = 0;
        while (j < n && siSuma) 
        {
            for (int i = 0; i < n; i++) 
            {
                sumaColumna += magico[i][j];
            }

            if (sumaColumna != constante) 
            {
                siSuma = false;
            }
            j++;
            sumaColumna = 0;
        }
        return siSuma;
    }

    public boolean sumaDiagonales() 
    {
        boolean siSuma = true;
        int constante = suma();
        int sumaDiagonal1 = 0;
        int f = 0, c = 0;
        while (f < n && c < n) 
        {
            sumaDiagonal1 += magico[f][c];
            f++;
            c++;
        }
        if (sumaDiagonal1 != constante) 
        {
            siSuma = false;
        } 
        else 
        {
            int sumaDiagonal2 = 0;
            f = 0;
            c = n - 1;
            while (f < n && c >= 0) 
            {
                sumaDiagonal2 += magico[f][c];
                f++;
                c--;
            }
            if (sumaDiagonal2 != constante) 
            {
                siSuma = false;
            }
        }
        return siSuma;
    }

    public void Magico() 
    {
        if (n % 2 == 1) 
        {
            setCuadro(cuadroMagicoImpar(n));
        } 
        else 
        {   
            if (n % 4 == 0) 
            {
            cuadroMagicoPar4();
            } 
            else 
            {
            cuadroMagicoPar2();
            }
        }
    }

    public int[][] cuadroMagicoImpar(int n) 
    {
        int colUltima = 0, filUltima = 0;

        int[][] cuadro = new int[n][n];

        /* Ubica el número 1 en la casilla central en la fila superior*/
        int colSiguiente = (n - 1) / 2;
        int filSiguiente = 0;
        int unidad = 1;

        for (int i = 0; i < n; i++) 
        {
            for (int j = 0; j < n; j++) 
            {
                //guardamos el numero en el cuadro
                cuadro[filSiguiente][colSiguiente] = unidad;

                //guardamos la ultima posicion donde guardamos algo
                filUltima = filSiguiente;
                colUltima = colSiguiente;

                /* Primer paso Mover una casilla hacia arriba y luego una casilla hacia la derecha*/
                filSiguiente = filUltima - 1;
                colSiguiente = colUltima + 1;

                /* Si un movimiento te lleva a una "casilla" por encima de la fila
                superior del cuadrado mágico, permanece en esa columna, pero ubica
                el número en la fila inferior de dicha columna*/
                if (filSiguiente < 0) 
                {
                    filSiguiente = n - 1;
                }

                /*Si el movimiento te lleva a una "casilla" fuera del límite derecho 
                del cuadrado mágico, permanece en la fila de dicha casilla, pero ubica 
                el número en la columna más alejada hacia la izquierda de esa fila.*/
                if (colSiguiente >= n) 
                {
                    filSiguiente = filUltima - 1;
                    colSiguiente = 0;
                }

                /*Si el movimiento te lleva a una casilla que ya está ocupada, regresa 
                a la última casilla que llenaste y ubica el número debajo.*/
                if (filSiguiente == -1 || cuadro[filSiguiente][colSiguiente] != 0) 
                {
                    filSiguiente = filUltima + 1;
                    colSiguiente = colUltima;
                }
                unidad++;
            }
        }
        return cuadro;
    }

    public void cuadroMagicoPar4() 
    {
        int a = n / 4;
        int unidad = 1;
        int fin = n - 1 - a;

        for (int i = 0; i < n; i++) 
        {
            for (int j = 0; j < n; j++) 
            {
                if ((j < a && i < a) || (j < a && i > fin) || (j > fin && i < a) || (j > fin && i > fin)) 
                {
                    magico[i][j] = unidad;
                } 
                else 
                {    
                    if ((j >= a && i >= a) && (j >= a && i <= fin) && (j <= fin && i >= a) && (j <= fin && i <= fin)) 
                    {
                    magico[i][j] = unidad;
                    }
                
                }
                unidad++;
            }
        }
        unidad = 1;
        for (int f = n - 1; f >= 0; f--) 
        {
            for (int c = n - 1; c >= 0; c--) 
            {
                if (magico[f][c] == 0) 
                {
                    magico[f][c] = unidad;
                }
                unidad++;
            }
        }
    }

    public void cuadroMagicoPar2() 
    {
        int a = n / 2;

        // Divide el cuadrado mágico en cuatro cuadrantes del mismo tamaño. 
        int[][] A = cuadroMagicoImpar(a); //cuadrante superior izq
        int[][] B = new int[a][a]; //cuadrante inferior derecho
        int[][] C = new int[a][a]; //cuadrante superior derecho
        int[][] D = new int[a][a]; //cuadrante inferior izquiero

        int unidad = a * a;
        for (int i = 0; i < a; i++) 
        {
            for (int j = 0; j < a; j++) 
            {
                B[i][j] = A[i][j] + unidad;
                C[i][j] = A[i][j] + unidad * 2;
                D[i][j] = A[i][j] + unidad * 3;
            }
        }

        //Resalta las áreas A y D e Intercambia las áreas resaltadas A y D
        int media = a / 2;
        for (int i = 0; i < a; i++) 
        {
            for (int j = 0; j <= media; j++) 
            {
                if ((i < media && j < media) || (i > media && j < media) || (i == media && j > 0)) 
                {
                    int auxiliar = A[i][j];
                    A[i][j] = D[i][j];
                    D[i][j] = auxiliar;
                }
            }
        }

        //mover ultimas columnas URL: http://www.1728.org/magicsq3.htm
        for (int j = (a - 1); j > (media + 1); j--) 
        {
            for (int i = 0; i < a; i++) 
            {
                int auxiliar = C[i][j];
                C[i][j] = B[i][j];
                B[i][j] = auxiliar;
            }
        }

        //armar el cuadro
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++) 
            {
                if (i < a && j < a) 
                {
                    magico[i][j] = A[i][j];
                } 
                else
                {
                    if (i >= a && j >= a) 
                    {
                        magico[i][j] = B[i - a][j - a];
                    } 
                    else
                    {
                        if (i < a && j >= a) 
                        {
                            magico[i][j] = C[i][j - a];
                        } 
                        else
                        {
                            if (i >= a && j < a) 
                            {
                                magico[i][j] = D[i - a][j];
                            }
                        }
                    }
                }
            }
        }
    }

    public String imprimirCuadro() 
    {
        String impr = "";
        for (int i = 0; i < n; i++) 
        {
            for (int j = 0; j < n; j++) 
            {
                impr += magico[i][j] + "\t";
            }
            impr += "\n";
        }
        return impr;
    }

    public int[][] getCuadro() 
    {
        return magico;
    }

    public void setCuadro(int[][] cuadro) 
    {
        this.magico = cuadro;
    }
}
