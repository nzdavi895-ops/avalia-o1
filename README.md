# avalia-o1import java.util.InputMismatchException;
import java.util.Scanner;

public class SistemaEscolar {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        double[] notas = new double[8];
        double[] bimestres = new double[4];
        double[] semestres = new double[2];

        // Entrada das notas com validação (0.0 - 10.0)
        for (int i = 0; i < notas.length; i++) {
            while (true) {
                System.out.print("Digite a nota " + (i + 1) + " (0.0 - 10.0): ");
                try {
                    double valor = scanner.nextDouble();
                    if (valor >= 0.0 && valor <= 10.0) {
                        notas[i] = valor;
                        break;
                    } else {
                        System.out.println("Valor inválido. A nota deve estar entre 0.0 e 10.0.");
                    }
                } catch (InputMismatchException e) {
                    System.out.println("Entrada inválida. Por favor digite um número (ex: 7.5).");
                    scanner.next(); // descarta token inválido
                }
            }
        }

        // Cálculo das médias bimestrais
        for (int i = 0; i < bimestres.length; i++) {
            bimestres[i] = (notas[2 * i] + notas[2 * i + 1]) / 2.0;
        }

        // Cálculo das médias semestrais
        for (int i = 0; i < semestres.length; i++) {
            semestres[i] = (bimestres[2 * i] + bimestres[2 * i + 1]) / 2.0;
        }

        // Cálculo da média final
        double mediaFinal = (semestres[0] + semestres[1]) / 2.0;

        // Exibição dos resultados (formatados com duas casas decimais)
        System.out.println("\nResultados:");
        for (int i = 0; i < bimestres.length; i++) {
            System.out.printf("%dº Bimestre: %.2f%n", (i + 1), bimestres[i]);
        }
        for (int i = 0; i < semestres.length; i++) {
            System.out.printf("%dº Semestre: %.2f%n", (i + 1), semestres[i]);
        }
        System.out.printf("Média Final: %.2f%n", mediaFinal);

        scanner.close();
    }
}
