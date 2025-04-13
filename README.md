# Sistema de Controle de Biblioteca - Projeto em C

## **Descrição:**
Este sistema foi desenvolvido para gerenciar o acervo de livros de uma biblioteca corporativa. O objetivo é automatizar o processo de controle de empréstimos, aquisições, devoluções e a baixa de exemplares, substituindo o processo manual utilizado atualmente. O sistema permite registrar novos livros e usuários, controlar empréstimos e devoluções, localizar exemplares e usuários, e gerar relatórios sobre o acervo, empréstimos e pendências.

### **Funcionalidades:**
- **Cadastro de Livros:** Registra informações dos livros como título, autor, editora, ano de publicação, entre outros.
- **Cadastro de Usuários:** Registra informações dos usuários como nome, endereço, telefone e número de crachá da empresa.
- **Controle de Empréstimos:** Permite registrar o empréstimo de livros para os usuários e controlar a devolução.
- **Localização de Exemplares e Usuários:** O sistema permite procurar livros e usuários por diferentes critérios, como título, autor e nome do usuário.
- **Geração de Relatórios:** O sistema pode gerar relatórios sobre o acervo, usuários, empréstimos, pendências e livros publicados em um período específico.

## **Mecanismos Utilizados:**

### **Estruturas de Dados:**
- **Listas Encadeadas:** O sistema utiliza listas encadeadas para armazenar os dados dos livros, usuários e empréstimos. Cada lista encadeada é composta por nós que armazenam os dados e ponteiros para o próximo elemento da lista. Isso facilita a inserção, remoção e manipulação dos dados de forma dinâmica.
  
### **Persistência de Dados:**
- **Arquivos Binários:** Para garantir a persistência dos dados, o sistema utiliza arquivos binários. Ao final de cada execução, todos os dados (livros, usuários e empréstimos) são salvos em arquivos binários específicos. Quando o programa é reiniciado, os dados são carregados desses arquivos para as respectivas listas encadeadas.
- **Arquivos CSV:** Relatórios podem ser exportados para arquivos CSV, que podem ser abertos no Excel para análise ou arquivamento.

### **Relatórios:**
- **Relatório de Acervo:** Lista todos os livros registrados na biblioteca.
- **Relatório de Usuários:** Exibe informações sobre todos os usuários cadastrados.
- **Relatório de Empréstimos:** Mostra todos os empréstimos realizados e suas respectivas datas de devolução.
- **Relatório de Pendências:** Exibe os livros que foram emprestados e ainda não devolvidos.
- **Relatório de Livros por Ano:** Gera um relatório de livros publicados em uma faixa de ano específica.

### **Tecnologias Utilizadas:**
- **C** para implementação do sistema.
- **Listas Encadeadas** para estrutura de dados dinâmicas.
- **Arquivos Binários** para persistência de dados.
- **Arquivos CSV** para exportação de relatórios.

---

## **Como Rodar o Projeto Localmente:**

### **Pré-requisitos:**
- **Compilador GCC**: Certifique-se de ter o compilador GCC instalado para compilar programas em C.
- **Editor de Texto**: Você pode usar qualquer editor de texto como Visual Studio Code, Sublime Text ou até o Vim para escrever o código.

### **Passos:**
1. Clone este repositório para o seu computador:
   ```bash
   git clone https://github.com/seuusuario/Sistema-Biblioteca-C.git
2. Navegue até o diretório do projeto:
   ```bash
   cd Sistema-Biblioteca-C
3. Compile o programa:
   ```bash
   gcc -o sistema_biblioteca sistema_biblioteca.c
4. Execute o programa:
   ```bash
   ./sistema_biblioteca
---
### **Como Usar:** 
---
- **Cadastrar Usuários:** Você pode cadastrar novos usuários no sistema da biblioteca.

- **Cadastrar Livros:** Você pode registrar novos livros com detalhes como título, editora, autor, etc.

* **Empréstimo e Devolução de Livros:** Os usuários podem pegar emprestado e devolver livros.

- **Gerar Relatórios:** Você pode gerar relatórios sobre o acervo da biblioteca, lista de usuários, empréstimos, e livros pendentes. Estes podem ser exportados como arquivos .csv para o Excel.
---
## **Arquivos Binários:**
- **Usuários:** ```bash usuarios.bin ```

- **Livros:** ```bash livros.bin```

- **Empréstimos:** ```bash emprestimos.bin```

Quando o programa for encerrado, todos os dados serão salvos nesses arquivos binários. Ao reiniciar o programa, ele irá carregar os dados desses arquivos para as listas encadeadas.

---
## **Tecnologias Utilizadas:**
 - C para implementação.

- GCC (GNU Compiler Collection) para compilar o programa.

- Manipulação de Arquivos Binários para persistência de dados.

- Formato CSV para exportação de relatórios.
---
Se precisar de ajuda com a compilação ou execução do programa, sinta-se à vontade para abrir uma issue ou entrar em contato diretamente. Aproveite o uso do Sistema de Controle de Biblioteca!

---

# Library Management System - C Project

## **Description:**
This system was developed to manage the book collection of a corporate library. The objective is to automate the processes of loan control, acquisitions, returns, and item disposal, replacing the manual processes currently used. The system allows registering new books and users, controlling loans and returns, locating items and users, and generating reports on the collection, loans, and pending items.

### **Features:**
- **Book Registration:** Registers book information such as title, author, publisher, publication year, and more.
- **User Registration:** Registers user information such as name, address, phone number, and employee ID.
- **Loan Control:** Allows registering book loans to users and controlling returns.
- **Item and User Location:** The system allows searching for books and users by different criteria, such as title, author, and user name.
- **Report Generation:** The system can generate reports on the collection, users, loans, pending items, and books published within a specific year range.

## **Mechanisms Used:**

### **Data Structures:**
- **Linked Lists:** The system uses linked lists to store book, user, and loan data. Each linked list consists of nodes that store data and pointers to the next item in the list. This facilitates the dynamic insertion, removal, and manipulation of data.

### **Data Persistence:**
- **Binary Files:** To ensure data persistence, the system uses binary files. At the end of each session, all data (books, users, and loans) are saved in specific binary files. When the program is restarted, data is loaded from these files into their respective linked lists.
- **CSV Files:** Reports can be exported to CSV files, which can be opened in Excel for analysis or archiving.

### **Reports:**
- **Collection Report:** Lists all the books registered in the library.
- **User Report:** Displays information about all registered users.
- **Loan Report:** Shows all loans made and their respective return dates.
- **Pending Report:** Displays books that were borrowed and have not yet been returned.
- **Books by Year Report:** Generates a report of books published within a specific year range.

### **Technologies Used:**
- **C** for implementing the system.
- **Linked Lists** for dynamic data structures.
- **Binary Files** for data persistence.
- **CSV Files** for exporting reports.

---

## **How to Run the Project Locally:**

### **Prerequisites:**
- **GCC Compiler:** Ensure you have the GCC compiler installed to compile C programs.
- **Text Editor:** You can use any text editor like Visual Studio Code, Sublime Text, or even Vim to write the code.

### **Steps:**
1. Clone this repository to your computer:
   ```bash
   git clone https://github.com/yourusername/Library-System-C.git
2. Navigate to the project directory:
   ```bash
   cd Library-System-C
3. Compile the program:
   ```bash
   gcc -o library_system library_system.c
4. Run the program:
   ```bash
   ./library_system
---
## **How to Use:**
- **Register Users:** You can register new users in the library system.

- **Register Books:** You can register new books with details such as title, publisher, author, etc.

- **Loan and Return Books:** Users can borrow and return books.

- **Generate Reports:** You can generate reports on the library's collection, user list, loans, and pending books. These can be exported as .csv files for Excel.
---
## **Binary Files:**
- **Users:** ```bash users.bin```

- **Books:** ```bash books.bin```

- **Loans:** ```bash loans.bin```

When the program is closed, all data will be saved to these binary files. Upon restarting the program, it will load data from these files into the linked lists.

---
## **Technologies Used:**

- C for implementation.

- GCC (GNU Compiler Collection) for compiling the program.

- Binary File Handling for data persistence.

- CSV Format for report export.

If you need help with compiling or running the program, feel free to open an issue or contact me directly. Enjoy using the Library Management System!
