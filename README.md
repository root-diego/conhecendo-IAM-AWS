# 🔐 Documentação: Introdução ao AWS Identity and Access Management (IAM)

Este repositório contém minha documentação prática do laboratório **“Introdução ao AWS IAM”**, realizado como parte das atividades do programa **AWS re/Start - Escola da Nuvem ☁️**.

O objetivo do laboratório foi compreender o gerenciamento de usuários, grupos e permissões na AWS, aplicando o princípio do menor privilégio e testando na prática os efeitos das políticas.

---

## 🧠 Habilidades Adquiridas

* Criação e configuração de políticas de senha no IAM
* Exploração de usuários e grupos IAM pré-criados
* Identificação de políticas gerenciadas e inline
* Associação de usuários a grupos específicos
* Teste prático de permissões com login de diferentes usuários

---

## 🛠️ Tecnologias Utilizadas

<div align="left">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/amazonwebservices/amazonwebservices-original-wordmark.svg" width="60" height="60" alt="AWS"/>

---

## 📁 Estrutura do Repositório

`conhecendo-IAM-AWS`

```
├── imagens/
│   ├── 01-politica-senha.png
│   ├── 02-politica-senha-pt2.png
│   ├── 03-user-01-summary.png
│   ├── 04-politica-ec2-support.png
│   ├── 05-s3-support-user.png
│   ├── 06-ec2-support-user.png
│   ├── 07-ec2-admin-user.png
│   ├── 08-login-user-01.png
│   ├── 09-login-user-02.png
│   ├── 10-login-user-03.png
│   ├── 11-11-funcionamento-politicas.png
└── README.md
```

---

## 🧩 Cenário do Laboratório

O ambiente de laboratório forneceu 3 usuários IAM e 3 grupos com permissões distintas para realizar testes práticos:

| Usuário  | Grupo IAM     | Permissões                                          |
| :------- | :------------ | :-------------------------------------------------- |
| `user-1` | `S3-Support`  | Leitura de buckets e objetos no Amazon S3           |
| `user-2` | `EC2-Support` | Visualização de instâncias EC2 (read-only)          |
| `user-3` | `EC2-Admin`   | Controle total sobre instâncias EC2 (inline policy) |

---

## 🖥️ Etapas Realizadas

### 1. Criando e Aplicando a Política de Senhas

No console do **IAM**, foi configurada uma política de senha para toda as contas da AWS:

* **Tamanho mínimo:** 10 caracteres
* **Exigir:** letras maiúsculas, minúsculas, números e caracteres especiais
* **Permitir alteração de senha pelo usuário**
* **Expiração:** 90 dias
* **Evitar reuso das últimas:** 5 senhas anteriores

#### Tela de configuração:

![Política de Senha](01-politica-senha.png)

![Política de Senha](02-politica-senha-pt2.png)


---

### 2. Explorando Usuários e Grupos

Acesse o menu **Users** e selecione `user-1` para visualizar suas permissões.
Observe que o usuário não possui políticas diretas aplicadas.

![User-1 summarry](03-user-01-summary.png)

Depois, em **User groups**, analise os grupos disponíveis:

* `EC2-Admin`
* `EC2-Support`
* `S3-Support`

Cada grupo possui diferentes tipos de políticas:

* `S3-Support`: política gerenciada **AmazonS3ReadOnlyAccess**
* `EC2-Support`: política gerenciada **AmazonEC2ReadOnlyAccess**
* `EC2-Admin`: política **inline** com permissões de controle total em EC2

#### Exemplo de tela de permissões do grupo EC2-Support:

![Permissões EC2-Support](04-politica-ec2-support.png)


---

### 3. Associando Usuários aos Grupos

Cada usuário foi adicionado ao seu respectivo grupo:

| Usuário  | Grupo Adicionado |
| :------- | :--------------- |
| `user-1` | `S3-Support`     |
| `user-2` | `EC2-Support`    |
| `user-3` | `EC2-Admin`      |

#### Tela de adição de usuários a grupos:

![Adição usuario](05-s3-support-user.png)
![Adição usuario](06-ec2-support-user.png)
![Adição usuario](07-ec2-admin-user.png)

---

### 4. Testando as Permissões de Cada Usuário

Para os testes, foi utilizado o **IAM user sign-in link** da conta em janelas anônimas separadas.

#### 🔹 user-1 (S3-Support)

* ✔Acesso bem-sucedido ao **Amazon S3**
* ✔Conseguiu listar e visualizar buckets
* ❌Tentativa de acessar EC2 resultou em **Access Denied**

![Login usuario](08-login-user-01.png)

---

#### 🔹 user-2 (EC2-Support)

* ✔Acesso ao **Amazon EC2** autorizado apenas para visualização
* ❌Não foi possível parar ou iniciar instâncias

![Login usuario](09-login-user-02.png)

---

#### 🔹 user-3 (EC2-Admin)

* ✔Permissão total sobre instâncias EC2 (inline policy)
* ✔Conseguiu parar e iniciar instâncias

![Login usuario](10-login-user-03.png)

---

## 🧩 Resultado Final

O teste prático confirmou o funcionamento correto das políticas IAM:

![Funcionamento das Politicas do IAM](11-funcionamento-politicas.png)

---

## 🔐 Lições Aprendidas

* Aplicar o **princípio do menor privilégio** garante segurança e controle.
* Políticas **inline** são úteis para exceções específicas.
* O **IAM** centraliza o controle de autenticação e autorização de recursos.
* O uso de **grupos** facilita o gerenciamento em larga escala.
* Políticas de senha fortes reduzem riscos de comprometimento de contas.

---

⚠️ ***Observação***

Este laboratório foi executado em um **ambiente sandbox da AWS**, com tempo limitado de uso (cerca de 3h). Após o encerramento, os recursos são automaticamente removidos.

Este laboratório foi realizado em um **ambiente sandbox da AWS**, disponibilizado apenas para fins educacionais. Nesse tipo de ambiente, o acesso é temporário e os **recursos são automaticamente encerrados e excluídos ao final da sessão**.

Informações como **Account ID ou nome do usuário do laboratório podem aparecer nos prints**, mas **não representam risco de segurança**, pois não pertencem a uma conta real e não permitem qualquer acesso externo.
