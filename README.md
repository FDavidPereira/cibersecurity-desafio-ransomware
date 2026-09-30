# Laboratório Educacional de Ransomware com Python

Projeto desenvolvido durante um desafio de cibersegurança da **Digital Innovation One (DIO)**, com o objetivo de compreender, em ambiente controlado, o funcionamento básico da criptografia e descriptografia de arquivos associadas a ataques do tipo ransomware.

> ⚠️ **Aviso:** este projeto possui finalidade exclusivamente educacional. Os testes foram realizados em máquina virtual isolada, utilizando somente arquivo fictício e ambiente autorizado.

## Objetivos

- Compreender o funcionamento básico de um ransomware.
- Praticar manipulação de arquivos com Python.
- Aplicar criptografia AES em um arquivo fictício.
- Entender o processo de descriptografia.
- Identificar riscos e limitações de uma implementação simplificada.
- Reforçar a importância de backups e controles de segurança.

## Tecnologias utilizadas

- Kali Linux
- Python 3
- Biblioteca `pyaes`
- AES no modo CTR
- Git e GitHub
- Oracle VirtualBox

## Estrutura do projeto

```text
.
├── encrypter.py
├── decrypter.py
├── teste.txt
├── .gitignore
└── README.md
```

## Funcionamento do laboratório

### Criptografia

O arquivo `encrypter.py` realiza as seguintes operações:

1. Abre o arquivo fictício `teste.txt`.
2. Lê seu conteúdo em modo binário.
3. Utiliza AES no modo CTR para criptografar os dados.
4. Remove o arquivo original.
5. Cria o arquivo `teste.txt.ransomwaretroll`.

### Descriptografia

O arquivo `decrypter.py` realiza o processo inverso:

1. Abre o arquivo `teste.txt.ransomwaretroll`.
2. Utiliza a mesma chave de criptografia.
3. Descriptografa o conteúdo.
4. Remove o arquivo criptografado.
5. Recria o arquivo `teste.txt`.

## Preparação do ambiente

Clone o repositório:

```bash
git clone https://github.com/FDavidPereira/cibersecurity-desafio-ransomware.git
```

Entre na pasta:

```bash
cd cibersecurity-desafio-ransomware
```

Crie um ambiente virtual:

```bash
python3 -m venv .venv
```

Ative o ambiente:

```bash
source .venv/bin/activate
```

Instale a biblioteca necessária:

```bash
python -m pip install pyaes
```

## Execução

Antes de executar, confirme que o arquivo `teste.txt` contém somente informações fictícias:

```bash
cat teste.txt
```

Execute a criptografia:

```bash
python encrypter.py
```

Verifique o arquivo criado:

```bash
ls -lah
```

Resultado esperado:

```text
teste.txt.ransomwaretroll
```

Execute a descriptografia:

```bash
python decrypter.py
```

Confira o conteúdo recuperado:

```bash
cat teste.txt
```

## Análise técnica

O projeto utiliza uma chave AES de 16 bytes:

```python
key = b"testeransomwares"
```

Uma chave de 16 bytes corresponde ao **AES-128**.

O modo CTR transforma o AES em uma cifra de fluxo. Para recuperar corretamente o conteúdo, o processo de descriptografia precisa utilizar a mesma chave e o mesmo estado inicial do contador.

## Limitações identificadas

Este código é uma demonstração simplificada e não deve ser considerado uma implementação criptográfica segura.

Principais limitações:

- A chave está escrita diretamente no código.
- O arquivo original é removido antes da confirmação de que o novo arquivo foi salvo corretamente.
- Não existe tratamento adequado de erros.
- Uma chave incorreta pode gerar conteúdo inválido.
- O modo CTR não fornece verificação de integridade.
- Um arquivo existente pode ser sobrescrito.
- O arquivo completo é carregado na memória.

## Boas práticas adotadas

- Utilização de máquina virtual isolada.
- Execução como usuário comum, sem privilégios de `root`.
- Uso exclusivo de arquivo fictício.
- Criação de snapshot antes do laboratório.
- Separação entre a rede do laboratório e a rede externa.
- Não utilização em arquivos ou equipamentos de terceiros.

## Prevenção contra ransomware

Algumas medidas importantes de prevenção incluem:

- Manter backups periódicos e testados.
- Atualizar sistemas e aplicações.
- Utilizar proteção de endpoint.
- Aplicar o princípio do menor privilégio.
- Monitorar alterações incomuns em arquivos.
- Bloquear anexos e executáveis suspeitos.
- Treinar usuários contra phishing e engenharia social.
- Segmentar redes corporativas.
- Manter planos de resposta a incidentes.

## Aprendizados

Este laboratório permitiu compreender como a criptografia pode impedir o acesso ao conteúdo de um arquivo e como a mesma chave pode ser utilizada para recuperá-lo.

Também foi possível observar que o desenvolvimento seguro exige:

- proteção das chaves;
- validação de integridade;
- tratamento de exceções;
- controle de permissões;
- preservação dos dados em caso de falha.

## Autor

**David Pereira**

- GitHub: [FDavidPereira](https://github.com/FDavidPereira)

---

Projeto desenvolvido exclusivamente para aprendizado de cibersegurança em ambiente controlado e autorizado.
