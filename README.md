# modelo-teste
package com.Matheus.estruturadados.fila.labs;

public class Documento {

	private String nome;
	private int numFolhas;

	public Documento(String nome, int numFolhas) {
		super();
		this.nome = nome;
		this.numFolhas = numFolhas;
	}

	public String getNome() {
		return nome;
	}
	public void setNome(String nome) {
		this.nome = nome;
	}
	public int getNumFolhas() {
		return numFolhas;
	}
	public void setNumFolhas(int numFolhas) {
		this.numFolhas = numFolhas;
	}



}
public class documentos 1{

	public static void main(String[] args) {

		Fila<Documento> filaImpressora = new Fila<>();

		filaImpressora.enfileira(new Documento("A", 1));
		filaImpressora.enfileira(new Documento("B", 2));
		filaImpressora.enfileira(new Documento("C", 3));
		filaImpressora.enfileira(new Documento("D", 7));
		filaImpressora.enfileira(new Documento("E", 9));

		while (!filaImpressora.estaVazia()) {
			Documento doc = filaImpressora.desenfileira();
			System.out.println("Imprimindo documento " + doc.getNome());
			try {
				Thread.sleep(200 * doc.getNumFolhas());
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}

		System.out.println("Todos os documentos foram impressos.");
	}

}
public static void main(String[] args) {

	Fila<String> regular = new Fila<>();
	Fila<String> prioridade = new Fila<>();

	final int MAX_PRIORIDADE = 3;

	regular.enfileira("Pessoa 1");
	regular.enfileira("Pessoa 2");
	regular.enfileira("Pessoa 3");
	prioridade.enfileira("Pessoa 1P");
	prioridade.enfileira("Pessoa 2P");
	prioridade.enfileira("Pessoa 3P");
	prioridade.enfileira("Pessoa 4P");
	prioridade.enfileira("Pessoa 5P");
	regular.enfileira("Pessoa 4");
	regular.enfileira("Pessoa 5");
	regular.enfileira("Pessoa 6");
	regular.enfileira("Pessoa 7");
	regular.enfileira("Pessoa 8");

	while (!regular.estaVazia() || !prioridade.estaVazia()) {

		int cont = 0;

		while(!prioridade.estaVazia() && cont < MAX_PRIORIDADE) {
			atendePessoa(prioridade);
			cont++;
		}

		if (!regular.estaVazia()) {
			atendePessoa(regular);
		}

		if (prioridade.estaVazia()) {
			while (!regular.estaVazia()) {
				atendePessoa(regular);
			}
		}
	}
}

public static void atendePessoa(Fila<String> fila) {
	String pessoaAtendida = fila.desenfileira();
	System.out.println(pessoaAtendida + " foi atendida.");
}

}
PSAtendimento atendimento = new PSAtendimento(fila);
PSNovosPacientes pacientes = new PSNovosPacientes(fila);

Thread t1 = new Thread(atendimento);
Thread t2 = new Thread(pacientes);

t1.start();
t2.start();
}

}
