---
title: "Padrões de Projetos:"
seoTitle: "Padrões de Projetos: Uma Análise Behaviorista Radical | Java e Python"
seoDescription: "Design Patterns do GoF interpretados pela Análise do Comportamento. Factory, Strategy, Observer, State e como repertórios comportamentais. Java e Python"
datePublished: Wed Dec 17 2025 13:05:27 GMT+0000 (Coordinated Universal Time)
cuid: cmja0y3p1000102l4dxlzdpm7
slug: padroes-de-projetos-analise-comportamental-behaviorista
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1765667582956/263ac877-9004-4fc8-a454-7f79f17b0196.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1765667624583/63bba7f3-8d32-4fb5-94b8-d2d030d77e5e.png
tags: designpatterns-padroesdeprojetos-gof-programacao-java-python-analisedocomportamento-behaviorismoradical-engenhariadesoftware-arquitetura-skinner-poo

---

## Introdução

Os Padrões de Projetos (*Design Patterns*), catalogados por Gamma, Helm, Johnson e Vlissides, conhecidos como Gang of Four (GoF), representam soluções recorrentes para problemas comuns no desenvolvimento de software. Tradicionalmente apresentados como "receitas" ou "templates mentais", esses padrões podem ser interpretados sob a perspectiva do Behaviorismo Radical como **repertórios comportamentais padronizados** que emergem sob contingências específicas de desenvolvimento.

O presente artigo propõe uma análise comportamental de padrões selecionados das três categorias clássicas — criacionais, estruturais e comportamentais — demonstrando como cada padrão pode ser compreendido através de conceitos como modelagem, controle de estímulos, operações motivacionais, cadeias comportamentais e comportamento governado por regras. Os exemplos em Java e Python ilustram tanto a implementação técnica quanto a interpretação analítico-comportamental.

---

## Padrões Criacionais: Contingências de Estabelecimento de Repertórios

Os padrões criacionais abstraem o processo de instanciação de objetos. Na perspectiva comportamental, esses padrões especificam **contingências de estabelecimento** — as condições sob as quais novos repertórios (objetos) são produzidos e disponibilizados para o sistema.

---

### Factory Method: Modelagem Controlada por Contexto

#### O Padrão

O **Factory Method** define uma interface para criar objetos, mas permite que subclasses decidam qual classe instanciar. Delega a responsabilidade de criação para métodos especializados.

#### A Análise Comportamental

Este padrão pode ser interpretado como um processo de **modelagem** (*shaping*) **controlada por contexto**. Assim como no laboratório o experimentador seleciona qual aproximação reforçar com base nas contingências vigentes, o Factory Method seleciona qual classe concreta instanciar com base no contexto da requisição.

O conceito de **controle contextual** é central: o mesmo método (fábrica) produz resultados diferentes dependendo do contexto (subclasse, parâmetros), análogo ao comportamento que varia em função de estímulos contextuais que modulam a relação SD-R-SR.

Adicionalmente, o Factory Method estabelece uma **contingência de produção padronizada**: independentemente de qual produto concreto é criado, o processo segue um protocolo definido, garantindo consistência na "modelagem" de novos objetos.

#### Exemplo em Java

```java
// Produto abstrato: especificação do repertório a ser produzido
abstract class Contingencia {
    protected String antecedente;
    protected String resposta;
    protected String consequencia;

    public abstract void descrever();
    public abstract String getTipo();
}

// Produtos concretos: repertórios específicos
class ContingenciaDeReforcoPositivo extends Contingencia {
    public ContingenciaDeReforcoPositivo(String antecedente, String resposta) {
        this.antecedente = antecedente;
        this.resposta = resposta;
        this.consequencia = "Apresentação de estímulo reforçador";
    }

    @Override
    public void descrever() {
        System.out.println("=== Contingência de Reforço Positivo ===");
        System.out.println("SD: " + antecedente);
        System.out.println("R: " + resposta);
        System.out.println("SR+: " + consequencia);
        System.out.println("Efeito: Aumento da frequência da resposta");
    }

    @Override
    public String getTipo() {
        return "R+";
    }
}

class ContingenciaDeReforcoNegativo extends Contingencia {
    public ContingenciaDeReforcoNegativo(String antecedente, String resposta) {
        this.antecedente = antecedente;
        this.resposta = resposta;
        this.consequencia = "Remoção de estímulo aversivo";
    }

    @Override
    public void descrever() {
        System.out.println("=== Contingência de Reforço Negativo ===");
        System.out.println("SD: " + antecedente);
        System.out.println("R: " + resposta);
        System.out.println("SR-: " + consequencia);
        System.out.println("Efeito: Aumento da frequência da resposta");
    }

    @Override
    public String getTipo() {
        return "R-";
    }
}

class ContingenciaDePunicaoPositiva extends Contingencia {
    public ContingenciaDePunicaoPositiva(String antecedente, String resposta) {
        this.antecedente = antecedente;
        this.resposta = resposta;
        this.consequencia = "Apresentação de estímulo aversivo";
    }

    @Override
    public void descrever() {
        System.out.println("=== Contingência de Punição Positiva ===");
        System.out.println("SD: " + antecedente);
        System.out.println("R: " + resposta);
        System.out.println("SP+: " + consequencia);
        System.out.println("Efeito: Redução da frequência da resposta");
    }

    @Override
    public String getTipo() {
        return "P+";
    }
}

// Fábrica abstrata: especificação do processo de modelagem
abstract class FabricaDeContingencias {
    // Factory Method: delega criação para subclasses
    public abstract Contingencia criarContingencia(String antecedente, String resposta);

    // Template para uso da contingência criada
    public void programarContingencia(String antecedente, String resposta) {
        Contingencia contingencia = criarContingencia(antecedente, resposta);
        System.out.println("\nContingência programada: " + contingencia.getTipo());
        contingencia.descrever();
    }
}

// Fábricas concretas: contextos específicos de modelagem
class FabricaDeFortalecimentoPorAdicao extends FabricaDeContingencias {
    @Override
    public Contingencia criarContingencia(String antecedente, String resposta) {
        return new ContingenciaDeReforcoPositivo(antecedente, resposta);
    }
}

class FabricaDeFortalecimentoPorRemocao extends FabricaDeContingencias {
    @Override
    public Contingencia criarContingencia(String antecedente, String resposta) {
        return new ContingenciaDeReforcoNegativo(antecedente, resposta);
    }
}

class FabricaDeEnfraquecimento extends FabricaDeContingencias {
    @Override
    public Contingencia criarContingencia(String antecedente, String resposta) {
        return new ContingenciaDePunicaoPositiva(antecedente, resposta);
    }
}

// Demonstração
public class FactoryMethodDemo {
    public static void main(String[] args) {
        // Contexto determina qual fábrica usar
        FabricaDeContingencias fabrica;

        // Contexto 1: Ensino de habilidades (fortalecimento positivo)
        System.out.println(">>> CONTEXTO: Ensino de habilidades");
        fabrica = new FabricaDeFortalecimentoPorAdicao();
        fabrica.programarContingencia(
            "Terapeuta apresenta instrução",
            "Criança emite resposta correta"
        );

        // Contexto 2: Fuga/Esquiva (fortalecimento negativo)
        System.out.println("\n>>> CONTEXTO: Comportamento de esquiva");
        fabrica = new FabricaDeFortalecimentoPorRemocao();
        fabrica.programarContingencia(
            "Presença de estímulo aversivo",
            "Organismo emite resposta de fuga"
        );
    }
}
```

#### Exemplo em Python

```python
from abc import ABC, abstractmethod


# Produto abstrato: especificação do repertório
class Contingencia(ABC):
    def __init__(self, antecedente: str, resposta: str):
        self._antecedente = antecedente
        self._resposta = resposta
        self._consequencia = ""

    @abstractmethod
    def descrever(self) -> None:
        pass

    @abstractmethod
    def get_tipo(self) -> str:
        pass


# Produtos concretos
class ContingenciaDeReforcoPositivo(Contingencia):
    def __init__(self, antecedente: str, resposta: str):
        super().__init__(antecedente, resposta)
        self._consequencia = "Apresentação de estímulo reforçador"

    def descrever(self) -> None:
        print("=== Contingência de Reforço Positivo ===")
        print(f"SD: {self._antecedente}")
        print(f"R: {self._resposta}")
        print(f"SR+: {self._consequencia}")
        print("Efeito: Aumento da frequência da resposta")

    def get_tipo(self) -> str:
        return "R+"


class ContingenciaDeReforcoNegativo(Contingencia):
    def __init__(self, antecedente: str, resposta: str):
        super().__init__(antecedente, resposta)
        self._consequencia = "Remoção de estímulo aversivo"

    def descrever(self) -> None:
        print("=== Contingência de Reforço Negativo ===")
        print(f"SD: {self._antecedente}")
        print(f"R: {self._resposta}")
        print(f"SR-: {self._consequencia}")
        print("Efeito: Aumento da frequência da resposta")

    def get_tipo(self) -> str:
        return "R-"


class ContingenciaDePunicaoPositiva(Contingencia):
    def __init__(self, antecedente: str, resposta: str):
        super().__init__(antecedente, resposta)
        self._consequencia = "Apresentação de estímulo aversivo"

    def descrever(self) -> None:
        print("=== Contingência de Punição Positiva ===")
        print(f"SD: {self._antecedente}")
        print(f"R: {self._resposta}")
        print(f"SP+: {self._consequencia}")
        print("Efeito: Redução da frequência da resposta")

    def get_tipo(self) -> str:
        return "P+"


# Fábrica abstrata
class FabricaDeContingencias(ABC):
    @abstractmethod
    def criar_contingencia(self, antecedente: str, resposta: str) -> Contingencia:
        """Factory Method: subclasses definem qual contingência criar."""
        pass

    def programar_contingencia(self, antecedente: str, resposta: str) -> None:
        """Template que usa o Factory Method."""
        contingencia = self.criar_contingencia(antecedente, resposta)
        print(f"\nContingência programada: {contingencia.get_tipo()}")
        contingencia.descrever()


# Fábricas concretas: diferentes contextos de modelagem
class FabricaDeFortalecimentoPorAdicao(FabricaDeContingencias):
    def criar_contingencia(self, antecedente: str, resposta: str) -> Contingencia:
        return ContingenciaDeReforcoPositivo(antecedente, resposta)


class FabricaDeFortalecimentoPorRemocao(FabricaDeContingencias):
    def criar_contingencia(self, antecedente: str, resposta: str) -> Contingencia:
        return ContingenciaDeReforcoNegativo(antecedente, resposta)


class FabricaDeEnfraquecimento(FabricaDeContingencias):
    def criar_contingencia(self, antecedente: str, resposta: str) -> Contingencia:
        return ContingenciaDePunicaoPositiva(antecedente, resposta)


# Demonstração
if __name__ == "__main__":
    # Contexto determina qual fábrica usar

    print(">>> CONTEXTO: Ensino de habilidades")
    fabrica = FabricaDeFortalecimentoPorAdicao()
    fabrica.programar_contingencia(
        antecedente="Terapeuta apresenta instrução",
        resposta="Criança emite resposta correta"
    )

    print("\n>>> CONTEXTO: Comportamento de esquiva")
    fabrica = FabricaDeFortalecimentoPorRemocao()
    fabrica.programar_contingencia(
        antecedente="Presença de estímulo aversivo",
        resposta="Organismo emite resposta de fuga"
    )
```

---

### Singleton: Instância Única sob Controle Ambiental

#### O Padrão

O **Singleton** garante que uma classe tenha apenas uma instância e fornece um ponto global de acesso a ela.

#### A Análise Comportamental

O Singleton pode ser interpretado como a especificação de uma **resposta única sob controle de estímulos específicos**. Em termos comportamentais, representa um contexto em que apenas uma topografia de resposta (instância) está disponível, independentemente de quantas vezes o organismo (código cliente) tente emiti-la.

Este padrão também se relaciona com o conceito de **recurso ambiental limitado**: assim como em contingências naturais onde apenas um reforçador está disponível e deve ser compartilhado, o Singleton garante que todos os componentes do sistema acessem o mesmo recurso único.

A verificação de existência prévia da instância funciona como uma **contingência de economia**: se o comportamento (objeto) já foi estabelecido, não há necessidade de novo processo de modelagem — o repertório existente é reutilizado.

#### Exemplo em Java

```java
// Singleton: Gerenciador único de sessão experimental
public class SessaoExperimental {
    // Instância única (recurso ambiental limitado)
    private static SessaoExperimental instanciaUnica;

    // Estado da sessão
    private String sujeito;
    private int respostasRegistradas;
    private int reforcosLiberados;
    private boolean sessaoAtiva;

    // Construtor privado: impede instanciação externa
    private SessaoExperimental() {
        this.respostasRegistradas = 0;
        this.reforcosLiberados = 0;
        this.sessaoAtiva = false;
    }

    // Ponto global de acesso com criação lazy
    public static synchronized SessaoExperimental obterInstancia() {
        if (instanciaUnica == null) {
            System.out.println("[Singleton] Criando sessão experimental única");
            instanciaUnica = new SessaoExperimental();
        } else {
            System.out.println("[Singleton] Retornando sessão existente");
        }
        return instanciaUnica;
    }

    public void iniciarSessao(String sujeito) {
        if (!sessaoAtiva) {
            this.sujeito = sujeito;
            this.sessaoAtiva = true;
            this.respostasRegistradas = 0;
            this.reforcosLiberados = 0;
            System.out.println("Sessão iniciada para: " + sujeito);
        } else {
            System.out.println("Sessão já está ativa para: " + this.sujeito);
        }
    }

    public void registrarResposta() {
        if (sessaoAtiva) {
            respostasRegistradas++;
            System.out.println("Resposta #" + respostasRegistradas + " registrada");
        }
    }

    public void liberarReforco() {
        if (sessaoAtiva) {
            reforcosLiberados++;
            System.out.println(">>> Reforço #" + reforcosLiberados + " liberado");
        }
    }

    public void encerrarSessao() {
        if (sessaoAtiva) {
            System.out.println("\n=== Resumo da Sessão ===");
            System.out.println("Sujeito: " + sujeito);
            System.out.println("Total de respostas: " + respostasRegistradas);
            System.out.println("Total de reforços: " + reforcosLiberados);
            if (respostasRegistradas > 0) {
                double razao = (double) respostasRegistradas / reforcosLiberados;
                System.out.printf("Razão R/SR: %.2f\n", razao);
            }
            sessaoAtiva = false;
        }
    }
}

// Demonstração: múltiplos componentes acessam mesma instância
public class SingletonDemo {
    public static void main(String[] args) {
        // Diferentes "observadores" acessam a mesma sessão

        System.out.println("--- Observador 1 tenta acessar sessão ---");
        SessaoExperimental sessao1 = SessaoExperimental.obterInstancia();
        sessao1.iniciarSessao("Rato-S1");

        System.out.println("\n--- Observador 2 tenta acessar sessão ---");
        SessaoExperimental sessao2 = SessaoExperimental.obterInstancia();
        // sessao2 é a mesma instância que sessao1

        System.out.println("\n--- Registrando comportamentos ---");
        sessao1.registrarResposta();
        sessao1.registrarResposta();
        sessao2.liberarReforco();  // Mesmo objeto
        sessao1.registrarResposta();
        sessao2.registrarResposta();  // Mesmo objeto
        sessao1.liberarReforco();

        System.out.println("\n--- Verificação de identidade ---");
        System.out.println("sessao1 == sessao2? " + (sessao1 == sessao2));

        sessao1.encerrarSessao();
    }
}
```

#### Exemplo em Python

```python
from threading import Lock


class SessaoExperimental:
    """
    Singleton: garante instância única da sessão experimental.
    Análogo a recurso ambiental limitado que deve ser compartilhado.
    """

    _instancia_unica = None
    _lock = Lock()

    def __new__(cls):
        if cls._instancia_unica is None:
            with cls._lock:
                # Double-check locking
                if cls._instancia_unica is None:
                    print("[Singleton] Criando sessão experimental única")
                    cls._instancia_unica = super().__new__(cls)
                    cls._instancia_unica._inicializar()
        else:
            print("[Singleton] Retornando sessão existente")
        return cls._instancia_unica

    def _inicializar(self):
        """Inicialização dos atributos (executada apenas uma vez)."""
        self._sujeito = None
        self._respostas_registradas = 0
        self._reforcos_liberados = 0
        self._sessao_ativa = False

    def iniciar_sessao(self, sujeito: str) -> None:
        if not self._sessao_ativa:
            self._sujeito = sujeito
            self._sessao_ativa = True
            self._respostas_registradas = 0
            self._reforcos_liberados = 0
            print(f"Sessão iniciada para: {sujeito}")
        else:
            print(f"Sessão já está ativa para: {self._sujeito}")

    def registrar_resposta(self) -> None:
        if self._sessao_ativa:
            self._respostas_registradas += 1
            print(f"Resposta #{self._respostas_registradas} registrada")

    def liberar_reforco(self) -> None:
        if self._sessao_ativa:
            self._reforcos_liberados += 1
            print(f">>> Reforço #{self._reforcos_liberados} liberado")

    def encerrar_sessao(self) -> None:
        if self._sessao_ativa:
            print(f"\n{'='*40}")
            print("Resumo da Sessão")
            print('='*40)
            print(f"Sujeito: {self._sujeito}")
            print(f"Total de respostas: {self._respostas_registradas}")
            print(f"Total de reforços: {self._reforcos_liberados}")
            if self._reforcos_liberados > 0:
                razao = self._respostas_registradas / self._reforcos_liberados
                print(f"Razão R/SR: {razao:.2f}")
            self._sessao_ativa = False


# Demonstração
if __name__ == "__main__":
    print("--- Observador 1 tenta acessar sessão ---")
    sessao1 = SessaoExperimental()
    sessao1.iniciar_sessao("Rato-S1")

    print("\n--- Observador 2 tenta acessar sessão ---")
    sessao2 = SessaoExperimental()

    print("\n--- Registrando comportamentos ---")
    sessao1.registrar_resposta()
    sessao1.registrar_resposta()
    sessao2.liberar_reforco()  # Mesmo objeto
    sessao1.registrar_resposta()
    sessao2.registrar_resposta()  # Mesmo objeto
    sessao1.liberar_reforco()

    print("\n--- Verificação de identidade ---")
    print(f"sessao1 is sessao2? {sessao1 is sessao2}")

    sessao1.encerrar_sessao()
```

---

## Padrões Estruturais: Organização de Relações Funcionais

Os padrões estruturais lidam com a composição de classes e objetos. Na perspectiva comportamental, esses padrões especificam como **repertórios se organizam e interagem**, formando estruturas funcionais complexas.

---

### Adapter: Equivalência Funcional entre Repertórios Distintos

#### O Padrão

O **Adapter** permite que interfaces incompatíveis trabalhem juntas, convertendo a interface de uma classe na interface esperada pelo cliente.

#### A Análise Comportamental

O Adapter implementa um processo de **equivalência funcional** entre repertórios topograficamente distintos. Assim como na formação de classes de estímulos equivalentes, onde estímulos diferentes passam a controlar a mesma resposta, o Adapter permite que objetos com interfaces diferentes sejam tratados de forma funcionalmente equivalente.

Este padrão também pode ser interpretado como uma forma de **tradução de contingências**: o adaptador converte as "contingências" de um sistema (interface original) nas contingências esperadas por outro (interface alvo), mantendo a função comportamental enquanto modifica a topografia da interação.

O conceito de **generalização mediada** é aplicável: o cliente interage com a interface esperada, e essa interação é mediada pelo adaptador que a traduz para a interface real, permitindo generalização do comportamento do cliente para sistemas originalmente incompatíveis.

#### Exemplo em Java

```java
// Interface alvo: o que o cliente espera (contingência esperada)
interface RegistradorDeComportamento {
    void registrar(String comportamento, double tempo);
    List<String> obterRegistros();
    void limparRegistros();
}

// Sistema legado com interface diferente (contingência original)
class SistemaLegadoDeRegistro {
    private StringBuilder dados = new StringBuilder();

    public void inserirDado(String dado) {
        dados.append(dado).append(";");
    }

    public String exportarDados() {
        return dados.toString();
    }

    public void resetar() {
        dados = new StringBuilder();
    }
}

// Adapter: estabelece equivalência funcional entre interfaces
class AdaptadorSistemaLegado implements RegistradorDeComportamento {
    private SistemaLegadoDeRegistro sistemaLegado;

    public AdaptadorSistemaLegado(SistemaLegadoDeRegistro sistemaLegado) {
        this.sistemaLegado = sistemaLegado;
    }

    @Override
    public void registrar(String comportamento, double tempo) {
        // Traduz a contingência esperada para a contingência do sistema legado
        String dadoFormatado = String.format("%s@%.2fs", comportamento, tempo);
        sistemaLegado.inserirDado(dadoFormatado);
    }

    @Override
    public List<String> obterRegistros() {
        // Traduz o formato de saída
        String dados = sistemaLegado.exportarDados();
        if (dados.isEmpty()) {
            return new ArrayList<>();
        }
        return Arrays.asList(dados.split(";"));
    }

    @Override
    public void limparRegistros() {
        sistemaLegado.resetar();
    }
}

// Novo sistema com interface diferente (outro tipo de contingência original)
class SistemaModernoDeRegistro {
    private Map<Long, String> registros = new HashMap<>();
    private long contador = 0;

    public long adicionar(String evento, long timestamp) {
        registros.put(contador, evento + "|" + timestamp);
        return contador++;
    }

    public Map<Long, String> getTodosRegistros() {
        return new HashMap<>(registros);
    }

    public void esvaziar() {
        registros.clear();
        contador = 0;
    }
}

// Adapter para sistema moderno
class AdaptadorSistemaModerno implements RegistradorDeComportamento {
    private SistemaModernoDeRegistro sistemaModerno;

    public AdaptadorSistemaModerno(SistemaModernoDeRegistro sistemaModerno) {
        this.sistemaModerno = sistemaModerno;
    }

    @Override
    public void registrar(String comportamento, double tempo) {
        long timestamp = (long) (tempo * 1000);
        sistemaModerno.adicionar(comportamento, timestamp);
    }

    @Override
    public List<String> obterRegistros() {
        return new ArrayList<>(sistemaModerno.getTodosRegistros().values());
    }

    @Override
    public void limparRegistros() {
        sistemaModerno.esvaziar();
    }
}

// Cliente: trabalha com a interface esperada, independente do sistema real
class AnalisadorDeSessao {
    private RegistradorDeComportamento registrador;

    public AnalisadorDeSessao(RegistradorDeComportamento registrador) {
        this.registrador = registrador;
    }

    public void conduzirObservacao() {
        System.out.println("=== Conduzindo Observação Comportamental ===\n");

        // O cliente usa sempre a mesma interface (contingência padronizada)
        registrador.registrar("Pressão à barra", 2.5);
        registrador.registrar("Pressão à barra", 4.8);
        registrador.registrar("Resposta de orientação", 6.2);
        registrador.registrar("Pressão à barra", 8.1);

        System.out.println("Registros coletados:");
        for (String registro : registrador.obterRegistros()) {
            System.out.println("  - " + registro);
        }
    }
}

// Demonstração
public class AdapterDemo {
    public static void main(String[] args) {
        // Usando sistema legado através do adapter
        System.out.println(">>> Com Sistema Legado (via Adapter)");
        SistemaLegadoDeRegistro legado = new SistemaLegadoDeRegistro();
        RegistradorDeComportamento adaptadorLegado = new AdaptadorSistemaLegado(legado);
        AnalisadorDeSessao analisador1 = new AnalisadorDeSessao(adaptadorLegado);
        analisador1.conduzirObservacao();

        System.out.println("\n>>> Com Sistema Moderno (via Adapter)");
        SistemaModernoDeRegistro moderno = new SistemaModernoDeRegistro();
        RegistradorDeComportamento adaptadorModerno = new AdaptadorSistemaModerno(moderno);
        AnalisadorDeSessao analisador2 = new AnalisadorDeSessao(adaptadorModerno);
        analisador2.conduzirObservacao();
    }
}
```

#### Exemplo em Python

```python
from abc import ABC, abstractmethod
from typing import List, Dict


# Interface alvo: contingência esperada pelo cliente
class RegistradorDeComportamento(ABC):
    @abstractmethod
    def registrar(self, comportamento: str, tempo: float) -> None:
        pass

    @abstractmethod
    def obter_registros(self) -> List[str]:
        pass

    @abstractmethod
    def limpar_registros(self) -> None:
        pass


# Sistema legado: contingência original diferente
class SistemaLegadoDeRegistro:
    def __init__(self):
        self._dados = []

    def inserir_dado(self, dado: str) -> None:
        self._dados.append(dado)

    def exportar_dados(self) -> str:
        return ";".join(self._dados)

    def resetar(self) -> None:
        self._dados.clear()


# Adapter: tradução de contingências
class AdaptadorSistemaLegado(RegistradorDeComportamento):
    """
    Estabelece equivalência funcional entre a interface esperada
    e o sistema legado com interface incompatível.
    """

    def __init__(self, sistema_legado: SistemaLegadoDeRegistro):
        self._sistema_legado = sistema_legado

    def registrar(self, comportamento: str, tempo: float) -> None:
        dado_formatado = f"{comportamento}@{tempo:.2f}s"
        self._sistema_legado.inserir_dado(dado_formatado)

    def obter_registros(self) -> List[str]:
        dados = self._sistema_legado.exportar_dados()
        if not dados:
            return []
        return dados.split(";")

    def limpar_registros(self) -> None:
        self._sistema_legado.resetar()


# Sistema moderno: outra contingência original
class SistemaModernoDeRegistro:
    def __init__(self):
        self._registros: Dict[int, str] = {}
        self._contador = 0

    def adicionar(self, evento: str, timestamp: int) -> int:
        self._registros[self._contador] = f"{evento}|{timestamp}"
        self._contador += 1
        return self._contador - 1

    def get_todos_registros(self) -> Dict[int, str]:
        return self._registros.copy()

    def esvaziar(self) -> None:
        self._registros.clear()
        self._contador = 0


# Adapter para sistema moderno
class AdaptadorSistemaModerno(RegistradorDeComportamento):
    def __init__(self, sistema_moderno: SistemaModernoDeRegistro):
        self._sistema_moderno = sistema_moderno

    def registrar(self, comportamento: str, tempo: float) -> None:
        timestamp = int(tempo * 1000)
        self._sistema_moderno.adicionar(comportamento, timestamp)

    def obter_registros(self) -> List[str]:
        return list(self._sistema_moderno.get_todos_registros().values())

    def limpar_registros(self) -> None:
        self._sistema_moderno.esvaziar()


# Cliente: comportamento generalizado para qualquer sistema
class AnalisadorDeSessao:
    def __init__(self, registrador: RegistradorDeComportamento):
        self._registrador = registrador

    def conduzir_observacao(self) -> None:
        print("=== Conduzindo Observação Comportamental ===\n")

        # Mesmo comportamento, independente do sistema subjacente
        self._registrador.registrar("Pressão à barra", 2.5)
        self._registrador.registrar("Pressão à barra", 4.8)
        self._registrador.registrar("Resposta de orientação", 6.2)
        self._registrador.registrar("Pressão à barra", 8.1)

        print("Registros coletados:")
        for registro in self._registrador.obter_registros():
            print(f"  - {registro}")


# Demonstração
if __name__ == "__main__":
    print(">>> Com Sistema Legado (via Adapter)")
    legado = SistemaLegadoDeRegistro()
    adaptador_legado = AdaptadorSistemaLegado(legado)
    analisador1 = AnalisadorDeSessao(adaptador_legado)
    analisador1.conduzir_observacao()

    print("\n>>> Com Sistema Moderno (via Adapter)")
    moderno = SistemaModernoDeRegistro()
    adaptador_moderno = AdaptadorSistemaModerno(moderno)
    analisador2 = AnalisadorDeSessao(adaptador_moderno)
    analisador2.conduzir_observacao()
```

---

### Decorator: Encadeamento e Extensão de Repertórios

#### O Padrão

O **Decorator** anexa responsabilidades adicionais a um objeto dinamicamente, fornecendo alternativa flexível à subclasse para extensão de funcionalidade.

#### A Análise Comportamental

O Decorator pode ser interpretado como um mecanismo de **encadeamento de repertórios comportamentais**. Assim como em uma cadeia comportamental onde cada resposta adiciona algo ao resultado final, cada decorator adiciona funcionalidade ao objeto base sem modificá-lo.

Este padrão também se relaciona com o conceito de **comportamento adjuntivo**: comportamentos que se agregam ao comportamento principal, modulando-o ou complementando-o. O decorator não substitui a função original, mas a estende — similar a comportamentos que ocorrem em adjunção a um operante principal.

A **composição de contingências** é outro paralelo: múltiplas contingências podem operar simultaneamente sobre o mesmo comportamento, cada uma adicionando sua influência. O Decorator implementa essa composição de forma organizada e reversível.

#### Exemplo em Java

```java
// Interface base: comportamento fundamental
interface InterventorComportamental {
    void realizarIntervencao(String comportamentoAlvo);
    String getDescricao();
}

// Implementação base concreta
class IntervencaoBasica implements InterventorComportamental {
    @Override
    public void realizarIntervencao(String comportamentoAlvo) {
        System.out.println("Aplicando intervenção básica para: " + comportamentoAlvo);
    }

    @Override
    public String getDescricao() {
        return "Intervenção Básica";
    }
}

// Decorator abstrato
abstract class DecoradorDeIntervencao implements InterventorComportamental {
    protected InterventorComportamental interventor;

    public DecoradorDeIntervencao(InterventorComportamental interventor) {
        this.interventor = interventor;
    }

    @Override
    public void realizarIntervencao(String comportamentoAlvo) {
        interventor.realizarIntervencao(comportamentoAlvo);
    }

    @Override
    public String getDescricao() {
        return interventor.getDescricao();
    }
}

// Decorator concreto: adiciona análise funcional
class ComAnaliseFuncional extends DecoradorDeIntervencao {
    public ComAnaliseFuncional(InterventorComportamental interventor) {
        super(interventor);
    }

    @Override
    public void realizarIntervencao(String comportamentoAlvo) {
        realizarAnalise(comportamentoAlvo);
        super.realizarIntervencao(comportamentoAlvo);
    }

    private void realizarAnalise(String comportamento) {
        System.out.println("[Análise Funcional] Identificando variáveis de controle de: " + comportamento);
        System.out.println("  → Antecedentes identificados");
        System.out.println("  → Consequências mapeadas");
    }

    @Override
    public String getDescricao() {
        return super.getDescricao() + " + Análise Funcional";
    }
}

// Decorator concreto: adiciona registro de dados
class ComRegistroDeDados extends DecoradorDeIntervencao {
    private List<String> registros = new ArrayList<>();

    public ComRegistroDeDados(InterventorComportamental interventor) {
        super(interventor);
    }

    @Override
    public void realizarIntervencao(String comportamentoAlvo) {
        iniciarRegistro();
        super.realizarIntervencao(comportamentoAlvo);
        finalizarRegistro(comportamentoAlvo);
    }

    private void iniciarRegistro() {
        System.out.println("[Registro] Iniciando coleta de dados...");
    }

    private void finalizarRegistro(String comportamento) {
        String registro = "Intervenção em '" + comportamento + "' - " + 
                         java.time.LocalDateTime.now();
        registros.add(registro);
        System.out.println("[Registro] Dados salvos: " + registro);
    }

    @Override
    public String getDescricao() {
        return super.getDescricao() + " + Registro de Dados";
    }
}

// Decorator concreto: adiciona reforçamento diferencial
class ComReforcamentoDiferencial extends DecoradorDeIntervencao {
    private String comportamentoAlternativo;

    public ComReforcamentoDiferencial(InterventorComportamental interventor, 
                                       String comportamentoAlternativo) {
        super(interventor);
        this.comportamentoAlternativo = comportamentoAlternativo;
    }

    @Override
    public void realizarIntervencao(String comportamentoAlvo) {
        super.realizarIntervencao(comportamentoAlvo);
        aplicarDRA();
    }

    private void aplicarDRA() {
        System.out.println("[DRA] Reforçando comportamento alternativo: " + comportamentoAlternativo);
        System.out.println("  → Extinção do comportamento-problema");
        System.out.println("  → Reforçamento do comportamento adequado");
    }

    @Override
    public String getDescricao() {
        return super.getDescricao() + " + DRA";
    }
}

// Decorator concreto: adiciona treino de pais/cuidadores
class ComTreinoDePais extends DecoradorDeIntervencao {
    public ComTreinoDePais(InterventorComportamental interventor) {
        super(interventor);
    }

    @Override
    public void realizarIntervencao(String comportamentoAlvo) {
        super.realizarIntervencao(comportamentoAlvo);
        realizarTreino();
    }

    private void realizarTreino() {
        System.out.println("[Treino de Pais] Orientando cuidadores:");
        System.out.println("  → Instrução sobre contingências");
        System.out.println("  → Modelação de procedimentos");
        System.out.println("  → Feedback sobre implementação");
    }

    @Override
    public String getDescricao() {
        return super.getDescricao() + " + Treino de Pais";
    }
}

// Demonstração
public class DecoratorDemo {
    public static void main(String[] args) {
        String comportamentoAlvo = "Agressão física";

        // Intervenção básica
        System.out.println("=== Nível 1: Intervenção Básica ===");
        InterventorComportamental intervencao = new IntervencaoBasica();
        intervencao.realizarIntervencao(comportamentoAlvo);
        System.out.println("Descrição: " + intervencao.getDescricao());

        // Adicionando análise funcional
        System.out.println("\n=== Nível 2: Com Análise Funcional ===");
        intervencao = new ComAnaliseFuncional(new IntervencaoBasica());
        intervencao.realizarIntervencao(comportamentoAlvo);
        System.out.println("Descrição: " + intervencao.getDescricao());

        // Composição completa: múltiplos decorators
        System.out.println("\n=== Nível 3: Intervenção Completa ===");
        InterventorComportamental intervencaoCompleta = 
            new ComTreinoDePais(
                new ComReforcamentoDiferencial(
                    new ComRegistroDeDados(
                        new ComAnaliseFuncional(
                            new IntervencaoBasica()
                        )
                    ),
                    "Comunicação funcional"
                )
            );

        intervencaoCompleta.realizarIntervencao(comportamentoAlvo);
        System.out.println("\nDescrição completa: " + intervencaoCompleta.getDescricao());
    }
}
```

#### Exemplo em Python

```python
from abc import ABC, abstractmethod
from datetime import datetime
from typing import List


# Interface base: comportamento fundamental
class InterventorComportamental(ABC):
    @abstractmethod
    def realizar_intervencao(self, comportamento_alvo: str) -> None:
        pass

    @abstractmethod
    def get_descricao(self) -> str:
        pass


# Implementação base concreta
class IntervencaoBasica(InterventorComportamental):
    def realizar_intervencao(self, comportamento_alvo: str) -> None:
        print(f"Aplicando intervenção básica para: {comportamento_alvo}")

    def get_descricao(self) -> str:
        return "Intervenção Básica"


# Decorator abstrato
class DecoradorDeIntervencao(InterventorComportamental):
    def __init__(self, interventor: InterventorComportamental):
        self._interventor = interventor

    def realizar_intervencao(self, comportamento_alvo: str) -> None:
        self._interventor.realizar_intervencao(comportamento_alvo)

    def get_descricao(self) -> str:
        return self._interventor.get_descricao()


# Decorator: adiciona análise funcional
class ComAnaliseFuncional(DecoradorDeIntervencao):
    def realizar_intervencao(self, comportamento_alvo: str) -> None:
        self._realizar_analise(comportamento_alvo)
        super().realizar_intervencao(comportamento_alvo)

    def _realizar_analise(self, comportamento: str) -> None:
        print(f"[Análise Funcional] Identificando variáveis de controle de: {comportamento}")
        print("  → Antecedentes identificados")
        print("  → Consequências mapeadas")

    def get_descricao(self) -> str:
        return f"{super().get_descricao()} + Análise Funcional"


# Decorator: adiciona registro de dados
class ComRegistroDeDados(DecoradorDeIntervencao):
    def __init__(self, interventor: InterventorComportamental):
        super().__init__(interventor)
        self._registros: List[str] = []

    def realizar_intervencao(self, comportamento_alvo: str) -> None:
        self._iniciar_registro()
        super().realizar_intervencao(comportamento_alvo)
        self._finalizar_registro(comportamento_alvo)

    def _iniciar_registro(self) -> None:
        print("[Registro] Iniciando coleta de dados...")

    def _finalizar_registro(self, comportamento: str) -> None:
        registro = f"Intervenção em '{comportamento}' - {datetime.now()}"
        self._registros.append(registro)
        print(f"[Registro] Dados salvos: {registro}")

    def get_descricao(self) -> str:
        return f"{super().get_descricao()} + Registro de Dados"


# Decorator: adiciona DRA
class ComReforcamentoDiferencial(DecoradorDeIntervencao):
    def __init__(self, interventor: InterventorComportamental, 
                 comportamento_alternativo: str):
        super().__init__(interventor)
        self._comportamento_alternativo = comportamento_alternativo

    def realizar_intervencao(self, comportamento_alvo: str) -> None:
        super().realizar_intervencao(comportamento_alvo)
        self._aplicar_dra()

    def _aplicar_dra(self) -> None:
        print(f"[DRA] Reforçando comportamento alternativo: {self._comportamento_alternativo}")
        print("  → Extinção do comportamento-problema")
        print("  → Reforçamento do comportamento adequado")

    def get_descricao(self) -> str:
        return f"{super().get_descricao()} + DRA"


# Decorator: adiciona treino de pais
class ComTreinoDePais(DecoradorDeIntervencao):
    def realizar_intervencao(self, comportamento_alvo: str) -> None:
        super().realizar_intervencao(comportamento_alvo)
        self._realizar_treino()

    def _realizar_treino(self) -> None:
        print("[Treino de Pais] Orientando cuidadores:")
        print("  → Instrução sobre contingências")
        print("  → Modelação de procedimentos")
        print("  → Feedback sobre implementação")

    def get_descricao(self) -> str:
        return f"{super().get_descricao()} + Treino de Pais"


# Demonstração
if __name__ == "__main__":
    comportamento_alvo = "Agressão física"

    print("=== Nível 1: Intervenção Básica ===")
    intervencao = IntervencaoBasica()
    intervencao.realizar_intervencao(comportamento_alvo)
    print(f"Descrição: {intervencao.get_descricao()}")

    print("\n=== Nível 2: Com Análise Funcional ===")
    intervencao = ComAnaliseFuncional(IntervencaoBasica())
    intervencao.realizar_intervencao(comportamento_alvo)
    print(f"Descrição: {intervencao.get_descricao()}")

    print("\n=== Nível 3: Intervenção Completa ===")
    intervencao_completa = ComTreinoDePais(
        ComReforcamentoDiferencial(
            ComRegistroDeDados(
                ComAnaliseFuncional(
                    IntervencaoBasica()
                )
            ),
            comportamento_alternativo="Comunicação funcional"
        )
    )

    intervencao_completa.realizar_intervencao(comportamento_alvo)
    print(f"\nDescrição completa: {intervencao_completa.get_descricao()}")
```

---

## Padrões Comportamentais: Algoritmos de Interação e Resposta

Os padrões comportamentais lidam com algoritmos e atribuição de responsabilidades entre objetos. Na perspectiva da Análise do Comportamento, esses padrões especificam **como repertórios interagem e se influenciam mutuamente**.

---

### Strategy: Variabilidade Comportamental Programada

#### O Padrão

O **Strategy** define uma família de algoritmos, encapsula cada um deles e os torna intercambiáveis. Permite que o algoritmo varie independentemente dos clientes que o utilizam.

#### A Análise Comportamental

O Strategy implementa o conceito de **variabilidade comportamental** — a capacidade de emitir diferentes topografias de resposta que servem à mesma função. Este padrão reflete o princípio skinneriano de que o operante é definido por sua função, não por sua forma específica.

A **seleção de estratégias** pelo contexto pode ser interpretada como **controle de estímulos sobre classes de respostas alternativas**: dependendo do estímulo discriminativo presente (contexto), uma classe de resposta específica (estratégia) é selecionada dentre várias disponíveis no repertório.

Adicionalmente, o Strategy se relaciona com o conceito de **resolução de problemas**: diante de um problema (contexto), o organismo pode emitir diferentes sequências comportamentais (estratégias) que já produziram consequências reforçadoras em situações similares.

#### Exemplo em Java

```java
// Interface Strategy: especificação funcional do repertório de análise
interface EstrategiaDeAnalise {
    void analisar(List<Integer> dados);
    String getNome();
}

// Estratégia concreta: Análise de Taxa
class AnaliseDeTaxa implements EstrategiaDeAnalise {
    @Override
    public void analisar(List<Integer> dados) {
        System.out.println("=== Análise de Taxa de Resposta ===");
        int total = dados.stream().mapToInt(Integer::intValue).sum();
        double media = dados.stream().mapToInt(Integer::intValue).average().orElse(0);
        System.out.println("Total de respostas: " + total);
        System.out.printf("Taxa média: %.2f R/min\n", media);
    }

    @Override
    public String getNome() {
        return "Taxa de Resposta";
    }
}

// Estratégia concreta: Análise de Tendência
class AnaliseDeTendencia implements EstrategiaDeAnalise {
    @Override
    public void analisar(List<Integer> dados) {
        System.out.println("=== Análise de Tendência ===");
        if (dados.size() < 2) {
            System.out.println("Dados insuficientes para análise de tendência");
            return;
        }

        // Compara primeira e segunda metade
        int meio = dados.size() / 2;
        double mediaInicial = dados.subList(0, meio).stream()
                                   .mapToInt(Integer::intValue).average().orElse(0);
        double mediaFinal = dados.subList(meio, dados.size()).stream()
                                 .mapToInt(Integer::intValue).average().orElse(0);

        System.out.printf("Média inicial: %.2f\n", mediaInicial);
        System.out.printf("Média final: %.2f\n", mediaFinal);

        if (mediaFinal > mediaInicial * 1.1) {
            System.out.println("Tendência: CRESCENTE (aquisição)");
        } else if (mediaFinal < mediaInicial * 0.9) {
            System.out.println("Tendência: DECRESCENTE (extinção)");
        } else {
            System.out.println("Tendência: ESTÁVEL (manutenção)");
        }
    }

    @Override
    public String getNome() {
        return "Tendência";
    }
}

// Estratégia concreta: Análise de Variabilidade
class AnaliseDeVariabilidade implements EstrategiaDeAnalise {
    @Override
    public void analisar(List<Integer> dados) {
        System.out.println("=== Análise de Variabilidade ===");
        double media = dados.stream().mapToInt(Integer::intValue).average().orElse(0);

        double somaQuadrados = dados.stream()
            .mapToDouble(d -> Math.pow(d - media, 2))
            .sum();
        double desvioPadrao = Math.sqrt(somaQuadrados / dados.size());
        double coefVariacao = (desvioPadrao / media) * 100;

        System.out.printf("Média: %.2f\n", media);
        System.out.printf("Desvio padrão: %.2f\n", desvioPadrao);
        System.out.printf("Coeficiente de variação: %.2f%%\n", coefVariacao);

        if (coefVariacao < 15) {
            System.out.println("Interpretação: Comportamento ESTÁVEL");
        } else if (coefVariacao < 30) {
            System.out.println("Interpretação: Variabilidade MODERADA");
        } else {
            System.out.println("Interpretação: Alta variabilidade - verificar controle");
        }
    }

    @Override
    public String getNome() {
        return "Variabilidade";
    }
}

// Estratégia concreta: Análise de Padrão de Esquema
class AnaliseDePadraoDeEsquema implements EstrategiaDeAnalise {
    @Override
    public void analisar(List<Integer> dados) {
        System.out.println("=== Análise de Padrão de Esquema ===");

        // Verifica pausa pós-reforço (característico de FR)
        boolean temPausa = false;
        for (int i = 0; i < dados.size() - 1; i++) {
            if (dados.get(i) > 0 && dados.get(i + 1) == 0) {
                temPausa = true;
                break;
            }
        }

        // Calcula variabilidade do IRT
        List<Integer> diferencas = new ArrayList<>();
        for (int i = 1; i < dados.size(); i++) {
            diferencas.add(Math.abs(dados.get(i) - dados.get(i-1)));
        }
        double mediaIRT = diferencas.stream().mapToInt(Integer::intValue).average().orElse(0);

        System.out.println("Pausa pós-reforço detectada: " + (temPausa ? "SIM" : "NÃO"));
        System.out.printf("IRT médio: %.2f\n", mediaIRT);

        if (temPausa && mediaIRT > 5) {
            System.out.println("Padrão sugere: RAZÃO FIXA (FR)");
        } else if (!temPausa && mediaIRT < 3) {
            System.out.println("Padrão sugere: RAZÃO VARIÁVEL (VR)");
        } else {
            System.out.println("Padrão sugere: INTERVALO ou misto");
        }
    }

    @Override
    public String getNome() {
        return "Padrão de Esquema";
    }
}

// Contexto: usa a estratégia selecionada
class AnalisadorComportamental {
    private EstrategiaDeAnalise estrategia;
    private List<Integer> dadosSessao;

    public AnalisadorComportamental() {
        this.dadosSessao = new ArrayList<>();
    }

    public void setEstrategia(EstrategiaDeAnalise estrategia) {
        this.estrategia = estrategia;
        System.out.println("\n[Estratégia selecionada: " + estrategia.getNome() + "]\n");
    }

    public void adicionarDados(List<Integer> dados) {
        this.dadosSessao.addAll(dados);
    }

    public void executarAnalise() {
        if (estrategia == null) {
            System.out.println("Nenhuma estratégia definida!");
            return;
        }
        estrategia.analisar(dadosSessao);
    }
}

// Demonstração
public class StrategyDemo {
    public static void main(String[] args) {
        // Dados de sessão experimental
        List<Integer> dados = Arrays.asList(12, 15, 18, 14, 16, 20, 22, 19, 25, 23);

        AnalisadorComportamental analisador = new AnalisadorComportamental();
        analisador.adicionarDados(dados);

        System.out.println("Dados da sessão: " + dados);

        // Mesmos dados, diferentes estratégias de análise
        analisador.setEstrategia(new AnaliseDetaxa());
        analisador.executarAnalise();

        analisador.setEstrategia(new AnaliseDeTendencia());
        analisador.executarAnalise();

        analisador.setEstrategia(new AnaliseDeVariabilidade());
        analisador.executarAnalise();

        analisador.setEstrategia(new AnaliseDePadraoDeEsquema());
        analisador.executarAnalise();
    }
}
```

#### Exemplo em Python

```python
from abc import ABC, abstractmethod
from typing import List
import statistics


# Interface Strategy
class EstrategiaDeAnalise(ABC):
    @abstractmethod
    def analisar(self, dados: List[int]) -> None:
        pass

    @abstractmethod
    def get_nome(self) -> str:
        pass


# Estratégia: Análise de Taxa
class AnaliseDeTaxa(EstrategiaDeAnalise):
    def analisar(self, dados: List[int]) -> None:
        print("=== Análise de Taxa de Resposta ===")
        total = sum(dados)
        media = statistics.mean(dados) if dados else 0
        print(f"Total de respostas: {total}")
        print(f"Taxa média: {media:.2f} R/min")

    def get_nome(self) -> str:
        return "Taxa de Resposta"


# Estratégia: Análise de Tendência
class AnaliseDeTendencia(EstrategiaDeAnalise):
    def analisar(self, dados: List[int]) -> None:
        print("=== Análise de Tendência ===")
        if len(dados) < 2:
            print("Dados insuficientes para análise de tendência")
            return

        meio = len(dados) // 2
        media_inicial = statistics.mean(dados[:meio])
        media_final = statistics.mean(dados[meio:])

        print(f"Média inicial: {media_inicial:.2f}")
        print(f"Média final: {media_final:.2f}")

        if media_final > media_inicial * 1.1:
            print("Tendência: CRESCENTE (aquisição)")
        elif media_final < media_inicial * 0.9:
            print("Tendência: DECRESCENTE (extinção)")
        else:
            print("Tendência: ESTÁVEL (manutenção)")

    def get_nome(self) -> str:
        return "Tendência"


# Estratégia: Análise de Variabilidade
class AnaliseDeVariabilidade(EstrategiaDeAnalise):
    def analisar(self, dados: List[int]) -> None:
        print("=== Análise de Variabilidade ===")
        media = statistics.mean(dados)
        desvio = statistics.stdev(dados) if len(dados) > 1 else 0
        coef_variacao = (desvio / media * 100) if media > 0 else 0

        print(f"Média: {media:.2f}")
        print(f"Desvio padrão: {desvio:.2f}")
        print(f"Coeficiente de variação: {coef_variacao:.2f}%")

        if coef_variacao < 15:
            print("Interpretação: Comportamento ESTÁVEL")
        elif coef_variacao < 30:
            print("Interpretação: Variabilidade MODERADA")
        else:
            print("Interpretação: Alta variabilidade - verificar controle")

    def get_nome(self) -> str:
        return "Variabilidade"


# Estratégia: Análise de Padrão de Esquema
class AnaliseDePadraoDeEsquema(EstrategiaDeAnalise):
    def analisar(self, dados: List[int]) -> None:
        print("=== Análise de Padrão de Esquema ===")

        # Verifica pausa pós-reforço
        tem_pausa = any(dados[i] > 0 and dados[i+1] == 0 
                        for i in range(len(dados)-1))

        # Calcula IRT médio
        diferencas = [abs(dados[i] - dados[i-1]) for i in range(1, len(dados))]
        media_irt = statistics.mean(diferencas) if diferencas else 0

        print(f"Pausa pós-reforço detectada: {'SIM' if tem_pausa else 'NÃO'}")
        print(f"IRT médio: {media_irt:.2f}")

        if tem_pausa and media_irt > 5:
            print("Padrão sugere: RAZÃO FIXA (FR)")
        elif not tem_pausa and media_irt < 3:
            print("Padrão sugere: RAZÃO VARIÁVEL (VR)")
        else:
            print("Padrão sugere: INTERVALO ou misto")

    def get_nome(self) -> str:
        return "Padrão de Esquema"


# Contexto
class AnalisadorComportamental:
    def __init__(self):
        self._estrategia: EstrategiaDeAnalise = None
        self._dados_sessao: List[int] = []

    def set_estrategia(self, estrategia: EstrategiaDeAnalise) -> None:
        self._estrategia = estrategia
        print(f"\n[Estratégia selecionada: {estrategia.get_nome()}]\n")

    def adicionar_dados(self, dados: List[int]) -> None:
        self._dados_sessao.extend(dados)

    def executar_analise(self) -> None:
        if self._estrategia is None:
            print("Nenhuma estratégia definida!")
            return
        self._estrategia.analisar(self._dados_sessao)


# Demonstração
if __name__ == "__main__":
    dados = [12, 15, 18, 14, 16, 20, 22, 19, 25, 23]

    analisador = AnalisadorComportamental()
    analisador.adicionar_dados(dados)

    print(f"Dados da sessão: {dados}")

    # Mesmos dados, diferentes estratégias
    for estrategia in [AnaliseDeTaxa(), AnaliseDeTendencia(), 
                       AnaliseDeVariabilidade(), AnaliseDePadraoDeEsquema()]:
        analisador.set_estrategia(estrategia)
        analisador.executar_analise()
```

---

### Observer: Contingências Sociais e Comportamento de Observação

#### O Padrão

O **Observer** define uma dependência um-para-muitos entre objetos, de modo que quando um objeto muda de estado, todos os seus dependentes são notificados e atualizados automaticamente.

#### A Análise Comportamental

O Observer implementa um modelo de **contingências sociais** onde o comportamento de um agente (subject) afeta o comportamento de múltiplos outros agentes (observers). Este padrão reflete a natureza social do comportamento humano, onde mudanças no ambiente (incluindo comportamento de outros) funcionam como estímulos discriminativos ou operações motivacionais para observadores.

O conceito de **comportamento de observação** (Skinner, 1969) é diretamente aplicável: observadores mantêm "atenção" ao subject porque mudanças neste sinalizam consequências relevantes. A notificação funciona como um **estímulo discriminativo** que ocasiona comportamentos específicos nos observadores.

Adicionalmente, o Observer pode ser interpretado como um sistema de **feedback social**: o subject emite comportamento que produz consequências (notificações) que por sua vez ocasionam comportamentos em outros organismos, formando uma rede de contingências interdependentes.

#### Exemplo em Java

```java
// Interface Observer: especificação do repertório de observação
interface ObservadorDeSessao {
    void atualizar(String evento, Object dados);
}

// Subject: entidade observada
class SujetoExperimental {
    private List<ObservadorDeSessao> observadores = new ArrayList<>();
    private String estado;
    private int respostas;
    private int reforcos;

    public void adicionarObservador(ObservadorDeSessao observador) {
        observadores.add(observador);
        System.out.println("[Subject] Observador registrado: " + observador.getClass().getSimpleName());
    }

    public void removerObservador(ObservadorDeSessao observador) {
        observadores.remove(observador);
    }

    private void notificarObservadores(String evento, Object dados) {
        for (ObservadorDeSessao obs : observadores) {
            obs.atualizar(evento, dados);
        }
    }

    public void emitirResposta() {
        respostas++;
        System.out.println("\n>>> Sujeito emitiu resposta #" + respostas);
        notificarObservadores("RESPOSTA", respostas);
    }

    public void receberReforco() {
        reforcos++;
        System.out.println("\n>>> Reforço liberado #" + reforcos);
        notificarObservadores("REFORCO", reforcos);
    }

    public void mudarEstado(String novoEstado) {
        String estadoAnterior = this.estado;
        this.estado = novoEstado;
        System.out.println("\n>>> Estado mudou: " + estadoAnterior + " -> " + novoEstado);
        notificarObservadores("ESTADO", novoEstado);
    }
}

// Observers concretos

class RegistradorDeFrequencia implements ObservadorDeSessao {
    private int contadorRespostas = 0;
    private int contadorReforcos = 0;

    @Override
    public void atualizar(String evento, Object dados) {
        if ("RESPOSTA".equals(evento)) {
            contadorRespostas++;
            System.out.println("  [Registrador] Frequência atualizada: " + contadorRespostas + " respostas");
        } else if ("REFORCO".equals(evento)) {
            contadorReforcos++;
            System.out.println("  [Registrador] Reforços: " + contadorReforcos);
        }
    }

    public double calcularTaxa(double minutos) {
        return contadorRespostas / minutos;
    }
}

class AnalisadorDeContingencias implements ObservadorDeSessao {
    private List<String> sequencia = new ArrayList<>();

    @Override
    public void atualizar(String evento, Object dados) {
        sequencia.add(evento);

        // Detecta padrão R->SR (contingência de reforçamento)
        if (sequencia.size() >= 2) {
            int ultimo = sequencia.size() - 1;
            if ("REFORCO".equals(sequencia.get(ultimo)) && 
                "RESPOSTA".equals(sequencia.get(ultimo - 1))) {
                System.out.println("  [Analisador] Contingência R+ detectada: Resposta → Reforço");
            }
        }
    }
}

class MonitorDeEstado implements ObservadorDeSessao {
    @Override
    public void atualizar(String evento, Object dados) {
        if ("ESTADO".equals(evento)) {
            String estado = (String) dados;
            System.out.println("  [Monitor] Novo estado registrado: " + estado);

            if ("EXTINCAO".equals(estado)) {
                System.out.println("  [Monitor] ALERTA: Procedimento de extinção iniciado");
            } else if ("SACIACAO".equals(estado)) {
                System.out.println("  [Monitor] ALERTA: Possível saciação detectada");
            }
        }
    }
}

class GeradorDeGrafico implements ObservadorDeSessao {
    private List<Integer> pontosDeDados = new ArrayList<>();

    @Override
    public void atualizar(String evento, Object dados) {
        if ("RESPOSTA".equals(evento)) {
            pontosDeDados.add((Integer) dados);
            System.out.println("  [Gráfico] Ponto adicionado. Total: " + pontosDeDados.size());
        }
    }

    public void exibirGrafico() {
        System.out.println("\n[Gráfico] Registro cumulativo: ");
        for (int i = 0; i < pontosDeDados.size(); i++) {
            System.out.print("█");
        }
        System.out.println(" (" + pontosDeDados.size() + " respostas)");
    }
}

// Demonstração
public class ObserverDemo {
    public static void main(String[] args) {
        // Cria o sujeito (fonte das mudanças comportamentais)
        SujetoExperimental sujeito = new SujetoExperimental();

        // Cria e registra observadores
        RegistradorDeFrequencia registrador = new RegistradorDeFrequencia();
        AnalisadorDeContingencias analisador = new AnalisadorDeContingencias();
        MonitorDeEstado monitor = new MonitorDeEstado();
        GeradorDeGrafico grafico = new GeradorDeGrafico();

        System.out.println("=== Configurando Observadores ===\n");
        sujeito.adicionarObservador(registrador);
        sujeito.adicionarObservador(analisador);
        sujeito.adicionarObservador(monitor);
        sujeito.adicionarObservador(grafico);

        System.out.println("\n=== Iniciando Sessão ===");
        sujeito.mudarEstado("LINHA_DE_BASE");

        // Simulação de sessão
        sujeito.emitirResposta();
        sujeito.emitirResposta();
        sujeito.receberReforco();
        sujeito.emitirResposta();
        sujeito.emitirResposta();
        sujeito.emitirResposta();
        sujeito.receberReforco();

        sujeito.mudarEstado("EXTINCAO");
        sujeito.emitirResposta();
        sujeito.emitirResposta();

        grafico.exibirGrafico();
    }
}
```

#### Exemplo em Python

```python
from abc import ABC, abstractmethod
from typing import List, Any


# Interface Observer
class ObservadorDeSessao(ABC):
    @abstractmethod
    def atualizar(self, evento: str, dados: Any) -> None:
        pass


# Subject
class SujetoExperimental:
    def __init__(self):
        self._observadores: List[ObservadorDeSessao] = []
        self._estado: str = ""
        self._respostas: int = 0
        self._reforcos: int = 0

    def adicionar_observador(self, observador: ObservadorDeSessao) -> None:
        self._observadores.append(observador)
        print(f"[Subject] Observador registrado: {observador.__class__.__name__}")

    def remover_observador(self, observador: ObservadorDeSessao) -> None:
        self._observadores.remove(observador)

    def _notificar_observadores(self, evento: str, dados: Any) -> None:
        for obs in self._observadores:
            obs.atualizar(evento, dados)

    def emitir_resposta(self) -> None:
        self._respostas += 1
        print(f"\n>>> Sujeito emitiu resposta #{self._respostas}")
        self._notificar_observadores("RESPOSTA", self._respostas)

    def receber_reforco(self) -> None:
        self._reforcos += 1
        print(f"\n>>> Reforço liberado #{self._reforcos}")
        self._notificar_observadores("REFORCO", self._reforcos)

    def mudar_estado(self, novo_estado: str) -> None:
        estado_anterior = self._estado
        self._estado = novo_estado
        print(f"\n>>> Estado mudou: {estado_anterior} -> {novo_estado}")
        self._notificar_observadores("ESTADO", novo_estado)


# Observers concretos

class RegistradorDeFrequencia(ObservadorDeSessao):
    def __init__(self):
        self._contador_respostas = 0
        self._contador_reforcos = 0

    def atualizar(self, evento: str, dados: Any) -> None:
        if evento == "RESPOSTA":
            self._contador_respostas += 1
            print(f"  [Registrador] Frequência: {self._contador_respostas} respostas")
        elif evento == "REFORCO":
            self._contador_reforcos += 1
            print(f"  [Registrador] Reforços: {self._contador_reforcos}")

    def calcular_taxa(self, minutos: float) -> float:
        return self._contador_respostas / minutos if minutos > 0 else 0


class AnalisadorDeContingencias(ObservadorDeSessao):
    def __init__(self):
        self._sequencia: List[str] = []

    def atualizar(self, evento: str, dados: Any) -> None:
        self._sequencia.append(evento)

        # Detecta padrão R->SR
        if len(self._sequencia) >= 2:
            if (self._sequencia[-1] == "REFORCO" and 
                self._sequencia[-2] == "RESPOSTA"):
                print("  [Analisador] Contingência R+ detectada: Resposta → Reforço")


class MonitorDeEstado(ObservadorDeSessao):
    def atualizar(self, evento: str, dados: Any) -> None:
        if evento == "ESTADO":
            print(f"  [Monitor] Novo estado: {dados}")

            if dados == "EXTINCAO":
                print("  [Monitor] ALERTA: Procedimento de extinção iniciado")
            elif dados == "SACIACAO":
                print("  [Monitor] ALERTA: Possível saciação detectada")


class GeradorDeGrafico(ObservadorDeSessao):
    def __init__(self):
        self._pontos: List[int] = []

    def atualizar(self, evento: str, dados: Any) -> None:
        if evento == "RESPOSTA":
            self._pontos.append(dados)
            print(f"  [Gráfico] Ponto adicionado. Total: {len(self._pontos)}")

    def exibir_grafico(self) -> None:
        print(f"\n[Gráfico] Registro cumulativo:")
        print("█" * len(self._pontos) + f" ({len(self._pontos)} respostas)")


# Demonstração
if __name__ == "__main__":
    sujeito = SujetoExperimental()

    # Registra observadores
    registrador = RegistradorDeFrequencia()
    analisador = AnalisadorDeContingencias()
    monitor = MonitorDeEstado()
    grafico = GeradorDeGrafico()

    print("=== Configurando Observadores ===\n")
    for obs in [registrador, analisador, monitor, grafico]:
        sujeito.adicionar_observador(obs)

    print("\n=== Iniciando Sessão ===")
    sujeito.mudar_estado("LINHA_DE_BASE")

    # Simulação
    sujeito.emitir_resposta()
    sujeito.emitir_resposta()
    sujeito.receber_reforco()
    sujeito.emitir_resposta()
    sujeito.emitir_resposta()
    sujeito.emitir_resposta()
    sujeito.receber_reforco()

    sujeito.mudar_estado("EXTINCAO")
    sujeito.emitir_resposta()
    sujeito.emitir_resposta()

    grafico.exibir_grafico()
```

---

### State: Operações Motivacionais e Estados Comportamentais

#### O Padrão

O **State** permite que um objeto altere seu comportamento quando seu estado interno muda, parecendo mudar de classe.

#### A Análise Comportamental

O State implementa o conceito de **operações motivacionais** (OMs) — variáveis que alteram a eficácia reforçadora de estímulos e a frequência de comportamentos relacionados. Assim como uma OM altera todo o repertório disponível do organismo, uma mudança de estado no padrão State altera o conjunto de comportamentos que o objeto pode emitir.

**Estados de privação e saciação** exemplificam esse princípio: um organismo privado de alimento (estado de fome) emite comportamentos de busca alimentar com alta frequência; quando saciado, esses mesmos comportamentos tornam-se improváveis. O objeto não "é diferente" — seu **estado atual determina quais comportamentos estão disponíveis**.

O State também se relaciona com o conceito de **contexto comportamental**: diferentes contextos (estados) ocasionam diferentes relações entre estímulos e respostas, mesmo mantendo a estrutura básica do organismo (objeto).

#### Exemplo em Java

```java
// Interface State: especificação de estados comportamentais
interface EstadoMotivacional {
    void responderAEstimulo(Organismo organismo);
    void receberReforco(Organismo organismo);
    void passarTempo(Organismo organismo);
    String getNome();
}

// Estado concreto: Privação
class EstadoDePrivacao implements EstadoMotivacional {
    @Override
    public void responderAEstimulo(Organismo organismo) {
        System.out.println("[Privação] Alta probabilidade de resposta operante");
        System.out.println("  → Emitindo comportamento de busca");
        organismo.incrementarRespostas();

        // Possível transição após muito esforço
        if (organismo.getRespostas() > 10) {
            System.out.println("  → Fadiga detectada");
            organismo.setEstado(new EstadoDeFadiga());
        }
    }

    @Override
    public void receberReforco(Organismo organismo) {
        System.out.println("[Privação] Reforço tem alto valor!");
        System.out.println("  → Consumindo reforçador avidamente");
        organismo.incrementarReforcos();

        // Transição para saciação após reforços suficientes
        if (organismo.getReforcos() >= 5) {
            System.out.println("  → Transição: Privação → Saciação");
            organismo.setEstado(new EstadoDeSaciacao());
        }
    }

    @Override
    public void passarTempo(Organismo organismo) {
        System.out.println("[Privação] Tempo aumenta motivação");
    }

    @Override
    public String getNome() {
        return "PRIVAÇÃO";
    }
}

// Estado concreto: Saciação
class EstadoDeSaciacao implements EstadoMotivacional {
    private int tempoEmSaciacao = 0;

    @Override
    public void responderAEstimulo(Organismo organismo) {
        System.out.println("[Saciação] Baixa probabilidade de resposta");
        System.out.println("  → Comportamento de busca improvável");
        // Não incrementa respostas - comportamento suprimido
    }

    @Override
    public void receberReforco(Organismo organismo) {
        System.out.println("[Saciação] Reforço tem baixo valor");
        System.out.println("  → Ignorando ou rejeitando reforçador");
        // Não incrementa reforços consumidos
    }

    @Override
    public void passarTempo(Organismo organismo) {
        tempoEmSaciacao++;
        System.out.println("[Saciação] Tempo: " + tempoEmSaciacao + " unidades");

        // Transição de volta para privação
        if (tempoEmSaciacao >= 3) {
            System.out.println("  → Transição: Saciação → Privação");
            organismo.setEstado(new EstadoDePrivacao());
        }
    }

    @Override
    public String getNome() {
        return "SACIAÇÃO";
    }
}

// Estado concreto: Fadiga
class EstadoDeFadiga implements EstadoMotivacional {
    private int tempoDeDescanso = 0;

    @Override
    public void responderAEstimulo(Organismo organismo) {
        System.out.println("[Fadiga] Capacidade de resposta reduzida");
        System.out.println("  → Resposta lenta ou ausente");
    }

    @Override
    public void receberReforco(Organismo organismo) {
        System.out.println("[Fadiga] Reforço parcialmente efetivo");
        organismo.incrementarReforcos();
    }

    @Override
    public void passarTempo(Organismo organismo) {
        tempoDeDescanso++;
        System.out.println("[Fadiga] Descansando... " + tempoDeDescanso + " unidades");

        if (tempoDeDescanso >= 2) {
            System.out.println("  → Recuperado! Transição: Fadiga → Privação");
            organismo.setEstado(new EstadoDePrivacao());
        }
    }

    @Override
    public String getNome() {
        return "FADIGA";
    }
}

// Estado concreto: Extinção Comportamental
class EstadoDeExtincao implements EstadoMotivacional {
    private int respostasSemReforco = 0;

    @Override
    public void responderAEstimulo(Organismo organismo) {
        respostasSemReforco++;
        System.out.println("[Extinção] Resposta #" + respostasSemReforco + " sem reforço");

        if (respostasSemReforco <= 3) {
            System.out.println("  → Burst de extinção: taxa aumentada");
            organismo.incrementarRespostas();
            organismo.incrementarRespostas(); // Taxa dobrada
        } else {
            System.out.println("  → Taxa diminuindo...");
        }
    }

    @Override
    public void receberReforco(Organismo organismo) {
        System.out.println("[Extinção] Reforço inesperado!");
        System.out.println("  → Recondicionamento rápido");
        organismo.setEstado(new EstadoDePrivacao());
    }

    @Override
    public void passarTempo(Organismo organismo) {
        System.out.println("[Extinção] Comportamento em redução gradual");
    }

    @Override
    public String getNome() {
        return "EXTINÇÃO";
    }
}

// Contexto: Organismo cujo comportamento depende do estado
class Organismo {
    private EstadoMotivacional estado;
    private int respostas = 0;
    private int reforcos = 0;

    public Organismo() {
        // Estado inicial: privação
        this.estado = new EstadoDePrivacao();
    }

    public void setEstado(EstadoMotivacional estado) {
        this.estado = estado;
    }

    public EstadoMotivacional getEstado() {
        return estado;
    }

    public void incrementarRespostas() {
        respostas++;
    }

    public void incrementarReforcos() {
        reforcos++;
    }

    public int getRespostas() {
        return respostas;
    }

    public int getReforcos() {
        return reforcos;
    }

    // Delegação para o estado atual
    public void responderAEstimulo() {
        System.out.println("\n--- Estímulo Apresentado (Estado: " + estado.getNome() + ") ---");
        estado.responderAEstimulo(this);
    }

    public void receberReforco() {
        System.out.println("\n--- Reforço Disponível (Estado: " + estado.getNome() + ") ---");
        estado.receberReforco(this);
    }

    public void passarTempo() {
        System.out.println("\n--- Passagem de Tempo (Estado: " + estado.getNome() + ") ---");
        estado.passarTempo(this);
    }

    public void iniciarExtincao() {
        System.out.println("\n=== INICIANDO PROCEDIMENTO DE EXTINÇÃO ===");
        setEstado(new EstadoDeExtincao());
    }
}

// Demonstração
public class StateDemo {
    public static void main(String[] args) {
        Organismo rato = new Organismo();

        System.out.println("=== Simulação de Estados Motivacionais ===");
        System.out.println("Estado inicial: " + rato.getEstado().getNome());

        // Fase 1: Respostas em privação
        for (int i = 0; i < 3; i++) {
            rato.responderAEstimulo();
        }

        // Fase 2: Reforçamento até saciação
        for (int i = 0; i < 6; i++) {
            rato.receberReforco();
        }

        // Fase 3: Comportamento em saciação
        rato.responderAEstimulo();
        rato.receberReforco();

        // Fase 4: Passagem de tempo restaura privação
        for (int i = 0; i < 4; i++) {
            rato.passarTempo();
        }

        // Fase 5: Extinção
        rato.iniciarExtincao();
        for (int i = 0; i < 5; i++) {
            rato.responderAEstimulo();
        }

        System.out.println("\n=== Resumo Final ===");
        System.out.println("Total de respostas: " + rato.getRespostas());
        System.out.println("Total de reforços: " + rato.getReforcos());
        System.out.println("Estado final: " + rato.getEstado().getNome());
    }
}
```

#### Exemplo em Python

```python
from abc import ABC, abstractmethod


# Interface State
class EstadoMotivacional(ABC):
    @abstractmethod
    def responder_a_estimulo(self, organismo: 'Organismo') -> None:
        pass

    @abstractmethod
    def receber_reforco(self, organismo: 'Organismo') -> None:
        pass

    @abstractmethod
    def passar_tempo(self, organismo: 'Organismo') -> None:
        pass

    @abstractmethod
    def get_nome(self) -> str:
        pass


# Estado: Privação
class EstadoDePrivacao(EstadoMotivacional):
    def responder_a_estimulo(self, organismo: 'Organismo') -> None:
        print("[Privação] Alta probabilidade de resposta operante")
        print("  → Emitindo comportamento de busca")
        organismo.incrementar_respostas()

        if organismo.respostas > 10:
            print("  → Fadiga detectada")
            organismo.set_estado(EstadoDeFadiga())

    def receber_reforco(self, organismo: 'Organismo') -> None:
        print("[Privação] Reforço tem alto valor!")
        print("  → Consumindo reforçador avidamente")
        organismo.incrementar_reforcos()

        if organismo.reforcos >= 5:
            print("  → Transição: Privação → Saciação")
            organismo.set_estado(EstadoDeSaciacao())

    def passar_tempo(self, organismo: 'Organismo') -> None:
        print("[Privação] Tempo aumenta motivação")

    def get_nome(self) -> str:
        return "PRIVAÇÃO"


# Estado: Saciação
class EstadoDeSaciacao(EstadoMotivacional):
    def __init__(self):
        self._tempo_em_saciacao = 0

    def responder_a_estimulo(self, organismo: 'Organismo') -> None:
        print("[Saciação] Baixa probabilidade de resposta")
        print("  → Comportamento de busca improvável")

    def receber_reforco(self, organismo: 'Organismo') -> None:
        print("[Saciação] Reforço tem baixo valor")
        print("  → Ignorando reforçador")

    def passar_tempo(self, organismo: 'Organismo') -> None:
        self._tempo_em_saciacao += 1
        print(f"[Saciação] Tempo: {self._tempo_em_saciacao} unidades")

        if self._tempo_em_saciacao >= 3:
            print("  → Transição: Saciação → Privação")
            organismo.set_estado(EstadoDePrivacao())

    def get_nome(self) -> str:
        return "SACIAÇÃO"


# Estado: Fadiga
class EstadoDeFadiga(EstadoMotivacional):
    def __init__(self):
        self._tempo_descanso = 0

    def responder_a_estimulo(self, organismo: 'Organismo') -> None:
        print("[Fadiga] Capacidade de resposta reduzida")
        print("  → Resposta lenta ou ausente")

    def receber_reforco(self, organismo: 'Organismo') -> None:
        print("[Fadiga] Reforço parcialmente efetivo")
        organismo.incrementar_reforcos()

    def passar_tempo(self, organismo: 'Organismo') -> None:
        self._tempo_descanso += 1
        print(f"[Fadiga] Descansando... {self._tempo_descanso} unidades")

        if self._tempo_descanso >= 2:
            print("  → Recuperado! Transição: Fadiga → Privação")
            organismo.set_estado(EstadoDePrivacao())

    def get_nome(self) -> str:
        return "FADIGA"


# Estado: Extinção
class EstadoDeExtincao(EstadoMotivacional):
    def __init__(self):
        self._respostas_sem_reforco = 0

    def responder_a_estimulo(self, organismo: 'Organismo') -> None:
        self._respostas_sem_reforco += 1
        print(f"[Extinção] Resposta #{self._respostas_sem_reforco} sem reforço")

        if self._respostas_sem_reforco <= 3:
            print("  → Burst de extinção: taxa aumentada")
            organismo.incrementar_respostas()
            organismo.incrementar_respostas()
        else:
            print("  → Taxa diminuindo...")

    def receber_reforco(self, organismo: 'Organismo') -> None:
        print("[Extinção] Reforço inesperado!")
        print("  → Recondicionamento rápido")
        organismo.set_estado(EstadoDePrivacao())

    def passar_tempo(self, organismo: 'Organismo') -> None:
        print("[Extinção] Comportamento em redução gradual")

    def get_nome(self) -> str:
        return "EXTINÇÃO"


# Contexto: Organismo
class Organismo:
    def __init__(self):
        self._estado: EstadoMotivacional = EstadoDePrivacao()
        self._respostas = 0
        self._reforcos = 0

    def set_estado(self, estado: EstadoMotivacional) -> None:
        self._estado = estado

    @property
    def estado(self) -> EstadoMotivacional:
        return self._estado

    @property
    def respostas(self) -> int:
        return self._respostas

    @property
    def reforcos(self) -> int:
        return self._reforcos

    def incrementar_respostas(self) -> None:
        self._respostas += 1

    def incrementar_reforcos(self) -> None:
        self._reforcos += 1

    def responder_a_estimulo(self) -> None:
        print(f"\n--- Estímulo Apresentado (Estado: {self._estado.get_nome()}) ---")
        self._estado.responder_a_estimulo(self)

    def receber_reforco(self) -> None:
        print(f"\n--- Reforço Disponível (Estado: {self._estado.get_nome()}) ---")
        self._estado.receber_reforco(self)

    def passar_tempo(self) -> None:
        print(f"\n--- Passagem de Tempo (Estado: {self._estado.get_nome()}) ---")
        self._estado.passar_tempo(self)

    def iniciar_extincao(self) -> None:
        print("\n=== INICIANDO PROCEDIMENTO DE EXTINÇÃO ===")
        self.set_estado(EstadoDeExtincao())


# Demonstração
if __name__ == "__main__":
    rato = Organismo()

    print("=== Simulação de Estados Motivacionais ===")
    print(f"Estado inicial: {rato.estado.get_nome()}")

    # Fase 1: Respostas em privação
    for _ in range(3):
        rato.responder_a_estimulo()

    # Fase 2: Reforçamento até saciação
    for _ in range(6):
        rato.receber_reforco()

    # Fase 3: Comportamento em saciação
    rato.responder_a_estimulo()

    # Fase 4: Passagem de tempo
    for _ in range(4):
        rato.passar_tempo()

    # Fase 5: Extinção
    rato.iniciar_extincao()
    for _ in range(5):
        rato.responder_a_estimulo()

    print("\n=== Resumo Final ===")
    print(f"Total de respostas: {rato.respostas}")
    print(f"Total de reforços: {rato.reforcos}")
    print(f"Estado final: {rato.estado.get_nome()}")
```

---

## Síntese: Padrões de Projetos como Repertórios de Solução

A análise behaviorista radical dos Padrões de Projetos revela paralelos consistentes entre soluções de design e princípios comportamentais:

| Padrão | Conceito Comportamental |
| --- | --- |
| **Factory Method** | Modelagem controlada por contexto — produção seletiva de repertórios |
| **Singleton** | Instância única — recurso ambiental limitado sob controle |
| **Adapter** | Equivalência funcional — tradução de contingências entre sistemas |
| **Decorator** | Encadeamento de repertórios — composição de comportamentos adjuntivos |
| **Strategy** | Variabilidade comportamental — classes de respostas alternativas sob controle contextual |
| **Observer** | Contingências sociais — comportamento de observação e feedback |
| **State** | Operações motivacionais — estados que alteram o repertório disponível |

Os Padrões de Projetos podem ser compreendidos como **repertórios de solução padronizados** que foram selecionados por contingências de desenvolvimento de software. Assim como comportamentos bem-sucedidos são selecionados e mantidos por suas consequências, padrões eficazes foram selecionados pela comunidade de desenvolvedores por produzirem código mais manutenível, flexível e compreensível.

---

## Considerações Finais

Os Padrões de Projetos, interpretados sob a ótica do Behaviorismo Radical, revelam-se não como abstrações cognitivas, mas como **repertórios comportamentais cristalizados** que emergiram da prática coletiva de programação. Cada padrão representa uma solução que, tendo produzido consequências reforçadoras (código funcional, manutenível, extensível), foi transmitida verbalmente através da comunidade de desenvolvedores.

Esta análise demonstra que os conceitos da Análise do Comportamento — contingências, controle de estímulos, operações motivacionais, cadeias comportamentais — oferecem ferramentas interpretativas poderosas para compreender não apenas comportamento de organismos individuais, mas também as práticas e convenções que emergem em comunidades técnicas.

O programador que compreende Padrões de Projetos sob esta perspectiva ganha dupla competência: técnica (saber aplicar os padrões) e analítica (compreender por que funcionam e quando adaptá-los). Essa combinação produz repertório mais flexível e eficaz para enfrentar os desafios variados do desenvolvimento de software.

---

## Referências

Catania, A. C. (1999). *Aprendizagem: Comportamento, linguagem e cognição* (4ª ed.). Artmed.

Gamma, E., Helm, R., Johnson, R., & Vlissides, J. (1994). *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley.

Michael, J. (1982). Distinguishing between discriminative and motivational functions of stimuli. *Journal of the Experimental Analysis of Behavior*, 37(1), 149-155.

Skinner, B. F. (1957). *Verbal Behavior*. Appleton-Century-Crofts.

Skinner, B. F. (1969). *Contingencies of Reinforcement: A Theoretical Analysis*. Appleton-Century-Crofts.

Skinner, B. F. (1974). *Sobre o Behaviorismo*. Cultrix.

---

*Este artigo faz parte de uma série que explora conceitos de programação sob a perspectiva da Análise do Comportamento. Acompanhe para mais conteúdos que integram Psicologia Comportamental e Engenharia de Software.*

---

**Tags:** #designpatterns #padrõesdeprojetos #gof #programação #java #python #análisedocomportamento #behaviorismoradical #engenhariadesoftware #arquitetura #skinner #poo