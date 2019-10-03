# MatrizAdj
Primeiro Exercício de Grafos

import java.io.IOException;

public class Main {
    public static void main(String [] args) {
        try {
            MatrizAdjacente matriz = new MatrizAdjacente(args[0]);
        } catch (IOException e) {
            System.out.println(e.getMessage());
        }
    }
}

import java.io.*;
import java.util.Scanner;

public class MatrizAdjacente {
    private String nomeArq;
    private int matriz[][];

    public MatrizAdjacente(String nomeArq) throws IOException{
        this.nomeArq = nomeArq;
        confirmaArquivo();
        formarMatriz();
        exibirMatriz();
    }

    private void confirmaArquivo() throws IOException{
        File arq = new File(nomeArq);
        if(!arq.exists()) {
            throw  new IOException("Arquivo não existente.");
        }
    }

    private void formarMatriz() {
        Scanner s;
        int valor, linhaAtual = 0;
        String linha;

        try(BufferedReader bf = new BufferedReader(new InputStreamReader(new FileInputStream(nomeArq)))) {
            s = new Scanner(bf.readLine());
            inicializaMatriz(s.nextInt());
            while((linha = bf.readLine()) != null) {
                s = new Scanner(linha);
                while(s.hasNext()) {
                    valor = s.nextInt();
                    if(valor != -1) {
                        matriz[linhaAtual][valor] = 1;
                    } else {
                        linhaAtual++;
                    }
                }
            }

        } catch (IOException e) {

        }
    }

    private void inicializaMatriz(int vertices) {
        matriz = new int[vertices][vertices];
        for(int i = 0; i < vertices ; i++) {
            for (int j = 0 ; j < vertices; j++) {
                matriz[i][j] = 0;
            }
        }
    }

    private void exibirMatriz() {
        for(int i = 0; i < matriz.length ; i++) {
            for(int j = 0 ; j < matriz.length ; j++) {
                System.out.print(matriz[i][j] +" ");
            }
            System.out.println();
        }
    }
}

