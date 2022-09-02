package magicopar2;
import java.util.Scanner;
public class Principal 
{
     public static void main(String[] args) 
     {
        Scanner sd = new Scanner(System.in);
        int n;
        boolean a;
        System.out.println("Introduzca el valor de n: ");
        n = sd.nextInt();
        while (n > 2) 
        {
            MagicoPar2 magico = new MagicoPar2(n);
            magico.Magico();
            if (magico.CuadroMagico()) 
            {
                System.out.println("La suma de cada columna,fila y diagonal es de: " + magico.suma());
                System.out.println();
                System.out.println(magico.imprimirCuadro()); 
                System.out.println("Si desea salir escriba 'true' o por el contrario desea seguir en el programa escriba 'false': ");
                a=sd.nextBoolean();
                if (a== true)
                {
                   System.out.println("Usted ha salido del programa");
                   break;
                }
                
            }
            System.out.println("Introduzca el valor de n: ");
            n = sd.nextInt();
        }
    }
}
