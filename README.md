# 🎮 Game App - Projeto Spring Boot

## 📋 Descrição

Aplicação web desenvolvida em **Spring Boot 3.3.4** com autenticação e autorização usando **Spring Security**. O projeto implementa um sistema de dashboard com rotas protegidas por autenticação, utilizando **Thymeleaf** como template engine.

Este projeto foi desenvolvido como atividade da disciplina **Java Advanced** da FIAP, focando na correção de erros em código legado e implementação de segurança.

---

## 🚀 Tecnologias Utilizadas

- **Java 17**
- **Spring Boot 3.3.4**
- **Spring Security 6.3**
- **Thymeleaf**
- **Maven**
- **Tomcat Embed 10.1.31**

---

## 📂 Estrutura do Projeto

```
CP-Java/
├── src/
│   ├── main/
│   │   ├── java/org/example/
│   │   │   ├── GameApplication.java          # Classe principal
│   │   │   ├── web/
│   │   │   │   └── GameController.java       # Controller MVC
│   │   │   └── config/
│   │   │       └── SecurityConfig.java       # Configuração de segurança
│   │   └── resources/
│   │       ├── templates/
│   │       │   ├── dashboard.html            # Página principal
│   │       │   └── login.html                # Página de login
│   │       └── application.properties        # Configurações da aplicação
│   └── test/
│       └── java/org/example/
├── pom.xml
└── README.md
```

---

## 🔧 Configuração e Instalação

### **Pré-requisitos**

- Java 17 ou superior
- Maven 3.8+
- IDE (IntelliJ IDEA, Eclipse, VS Code)

### **Clonar o Repositório**

```bash
git clone https://github.com/Vinicius-A-Siqueira/CP5-JAVA-2025/
cd CP-Java
```

### **Compilar o Projeto**

```bash
mvn clean install
```

### **Executar a Aplicação**

```bash
mvn spring-boot:run
```

Ou executar o JAR compilado:

```bash
java -jar target/game-app-1.0.0.jar
```

A aplicação estará disponível em: **http://localhost:8080**

---

## 🔐 Credenciais de Acesso

| Usuário | Senha | Permissão |
|---------|-------|-----------|
| `admin` | `123` | USER      |

---

## 🛣️ Rotas da Aplicação

| Método | Rota | Proteção | Descrição |
|--------|------|----------|-----------|
| `GET` | `/` | ❌ Pública | Dashboard principal |
| `GET` | `/login` | ❌ Pública | Página de login |
| `POST` | `/do-something` | ✅ Protegida | Altera estado do servidor (requer autenticação) |

---

## 🎯 Funcionalidades

### ✅ **Implementadas**

- [x] Dashboard com listagem de itens
- [x] Sistema de autenticação com Spring Security
- [x] Proteção de rotas que alteram estado do servidor
- [x] Criptografia de senhas com BCrypt
- [x] Templates Thymeleaf responsivos
- [x] Gerenciamento de sessão
- [x] Logout funcional

### 🔒 **Segurança**

- **BCryptPasswordEncoder** com força de 12 rounds
- **CSRF Protection** habilitada por padrão
- **Session Management** com fixação de sessão
- Apenas rotas POST que alteram estado requerem autenticação
- Headers de segurança configurados

---

## 🧪 Testes

### **Testar Rota Pública**

```bash
curl http://localhost:8080/
```

**Resultado esperado:** Status 200 (Dashboard visível)

### **Testar Rota Protegida SEM Autenticação**

```bash
curl -i http://localhost:8080/do-something
```

**Resultado esperado:** Status 302 (Redirect para `/login`)

### **Testar Login**

1. Acesse: `http://localhost:8080/login`
2. Digite:
   - Usuário: `admin`
   - Senha: `123`
3. Clique em **"Entrar"**
4. Será redirecionado para o dashboard
5. Teste o botão **"Fazer Algo"** (POST protegido)

---

## 🐛 Erros Corrigidos

Este projeto foi desenvolvido a partir de um código com erros intencionais. Os seguintes problemas foram corrigidos:

### **GameController.java**

| Erro | Correção |
|------|----------|
| `@RestController` | `@Controller` (para retornar views) |
| `@GetMappin` | `@GetMapping` (falta letra "g") |
| `return "dashbord"` | `return "dashboard"` (typo) |
| `@GetMapping("/do-something")` | `@PostMapping("/do-something")` (altera estado) |
| Falta `pageTitle` no método `home()` | Adicionado atributo |

### **login.html**

| Erro | Correção |
|------|----------|
| `th:text="${pageTitle"` | `th:text="${pageTitle}"` (falta fechar) |
| `th:action="@{/login"` | `th:action="@{/login}"` (falta fechar) |
| `th:field` sem DTO | Removido, usando `name` |
| `type="submti"` | `type="submit"` (typo) |

### **dashboard.html**

| Erro | Correção |
|------|----------|
| `th:text="${pageTitle"` | `th:text="${pageTitle}"` (falta fechar) |
| `th:texts=` | `th:text=` (typo) |
| `th:text="${now.toString()} )"` | `th:text="${now.toString()}"` (parêntese extra) |
| `th:each="item ${itens}"` | `th:each="item : ${itens}"` (falta dois-pontos) |
| `<div>` sem fechar | Adicionado `</div>` |

---

## 📦 Dependências Principais

```xml
<dependencies>
    <!-- Spring Boot Web -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    
    <!-- Thymeleaf -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-thymeleaf</artifactId>
    </dependency>
    
    <!-- Spring Security -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
    
    <!-- DevTools (hot reload) -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
        <optional>true</optional>
    </dependency>
</dependencies>
```

---

## 🔍 Verificar Vulnerabilidades

```bash
# Verificar dependências
mvn dependency:tree

# Verificar vulnerabilidades com OWASP
mvn dependency-check:check
```

---

## 📝 Configurações (application.properties)

```properties
server.port=8080
spring.application.name=game-app
spring.thymeleaf.cache=false
logging.level.root=INFO
logging.level.org.example=DEBUG
```

---

## 🏆 Desafio Bônus (Ponto Extra)

✅ **Spring Security implementado com:**

- Proteção de rotas que alteram estado do servidor (`POST /do-something`)
- Autenticação form-based com redirecionamento
- Criptografia de senhas com BCrypt
- Gerenciamento de sessão seguro
- Configuração de usuário em memória (InMemoryUserDetailsManager)

---

## 👨‍💻 Autor

**Projeto desenvolvido como atividade acadêmica da FIAP**

Disciplina: Java Advanced  
Professor: Prof. Me. Orlando C. Patriarcha

---

## 📄 Licença

Este projeto é de uso acadêmico e educacional.

---

## 🤝 Como Contribuir

1. Fork o projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

---

## 📞 Suporte

Para dúvidas ou problemas, abra uma issue no repositório.

---

**🎮 Lets Play a Game! Todos os erros foram corrigidos e o código está 100% funcional!** ✅
