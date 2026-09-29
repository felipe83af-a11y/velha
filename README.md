import java.util.Scanner;
import java.util.Random;

public class JogoDaVelha {

    public static void main(String[] args) {
        Scanner ler = new Scanner(System.in);
        Random random = new Random();
        int velha[][] = new int[3][3];

        int turno = 1;
        boolean jogando = true;

        while (jogando) {

            for (int i = 0; i < 3; i++) {
                for (int j = 0; j < 3; j++) {
                    if (velha[i][j] == 0) {
                        System.out.print("   ");
                    } else if (velha[i][j] == 1) {
                        System.out.print(" X ");
                    } else if (velha[i][j] == 2) {
                        System.out.print(" O ");
                    }

                    if (j < 2) System.out.print("|");
                }
                System.out.println();
                if (i < 2) System.out.println("-----------");
            }
            System.out.println();

            if (turno == 1) {
                int linha, coluna;
                boolean jogada = false;

                while (!jogada) {
                    System.out.println("Informe a linha (0 a 2):");
                    linha = ler.nextInt();
                
                    System.out.println("Informe a coluna (0 a 2):");
                    coluna = ler.nextInt();

                    if (linha >= 0 && linha <= 2 && coluna >= 0 && coluna <= 2) {
                        if (velha[linha][coluna] == 0) {
                            velha[linha][coluna] = 1;
                            jogada = true;
                        } else {
                            System.out.println("Essa casa esta ocupada");
                        }
                    } else {
                        System.out.println("Posiçao fora, escolha linha e coluna entre 0 e 2");
                    }
                }
            } else if (turno == 2) {
                int linha, coluna;

                do {
                    linha = random.nextInt(3);
                    coluna = random.nextInt(3);
                } while (velha[linha][coluna] != 0);

                velha[linha][coluna] = 2;
            }

            boolean venceu = false;

            for (int j = 0; j < 3; j++) {
                if (velha[0][j] != 0 && velha[0][j] == velha[1][j] && velha[1][j] == velha[2][j]) {
                    venceu = true;
                }
            }

            for (int i = 0; i < 3; i++) {
                if (velha[i][0] != 0 && velha[i][0] == velha[i][1] && velha[i][1] == velha[i][2]) {
                    venceu = true;
                }
            }

            if (velha[0][0] != 0 && velha[0][0] == velha[1][1] && velha[1][1] == velha[2][2]) {
                venceu = true;
            }

            if (velha[0][2] != 0 && velha[0][2] == velha[1][1] && velha[1][1] == velha[2][0]) {
                venceu = true;
            }

            if (venceu) {
                jogando = false;
            } else {
                boolean empate = true;

                for (int i = 0; i < 3; i++) {
                    for (int j = 0; j < 3; j++) {
                        if (velha[i][j] == 0) {
                            empate = false;
                        }
                    }
                }

                if (empate) {
                    System.out.println("Deu velha");
                    jogando = false;
                } else {
                    if (turno == 1) {
                        turno = 2;
                    } else {
                        turno = 1;
                    }
                }
            }
        }
    }
}
