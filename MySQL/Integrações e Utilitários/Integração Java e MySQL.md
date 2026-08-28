# Integração Java e MySQL via JDBC

Para conectar uma aplicação **Java** a uma base de dados **MySQL**, utilizamos a API padrão **JDBC (Java Database Connectivity)** juntamente com o driver oficial **MySQL Connector/J**.

---

## 1. Dependência Maven (`pom.xml`)

```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
    <version>8.4.0</version>
</dependency>
```

---

## 2. Estrutura de Conexão com o Banco de Dados

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class ConexaoFabrica {
    private static final String URL = "jdbc:mysql://localhost:3306/empresa_db?useSSL=false&serverTimezone=UTC&characterEncoding=UTF-8";
    private static final String USUARIO = "root";
    private static final String SENHA = "senha_segura";

    public static Connection obterConexao() throws SQLException {
        return DriverManager.getConnection(URL, USUARIO, SENHA);
    }
}
```

---

## 3. Consulta Segura com `PreparedStatement` e `ResultSet`

> [!tip] 💡 Segurança contra SQL Injection
> Nunca concatene variáveis diretamente no texto da query SQL. Utilize sempre **`PreparedStatement`** com parâmetros parametrizados (`?`).

```java
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;

public class ClienteDAO {

    public void buscarClientesPorCidade(String cidadeFiltro) {
        String sql = "SELECT cliente_id, nome, email, limite_credito FROM clientes WHERE cidade = ? ORDER BY nome ASC";

        // Uso do try-with-resources para fechamento automático de conexões e recursos
        try (Connection conexao = ConexaoFabrica.obterConexao();
             PreparedStatement stmt = conexao.prepareStatement(sql)) {

            stmt.setString(1, cidadeFiltro);

            try (ResultSet rs = stmt.executeQuery()) {
                while (rs.next()) {
                    int id = rs.getInt("cliente_id");
                    String nome = rs.getString("nome");
                    String email = rs.getString("email");
                    double limite = rs.getDouble("limite_credito");

                    System.out.printf("ID: %d | Nome: %s | E-mail: %s | Limite: R$ %.2f%n", 
                                      id, nome, email, limite);
                }
            }

        } catch (SQLException e) {
            System.err.println("Erro ao consultar o banco de dados: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

---

## 4. Inserção de Registros com Transação

```java
public void inserirCliente(String nome, String email, double limite) {
    String sql = "INSERT INTO clientes (nome, email, limite_credito) VALUES (?, ?, ?)";

    try (Connection conexao = ConexaoFabrica.obterConexao()) {
        conexao.setAutoCommit(false); // Inicia transação

        try (PreparedStatement stmt = conexao.prepareStatement(sql)) {
            stmt.setString(1, nome);
            stmt.setString(2, email);
            stmt.setDouble(3, limite);

            stmt.executeUpdate();
            conexao.commit(); // Confirma transação
            System.out.println("Cliente cadastrado com sucesso!");
        } catch (SQLException e) {
            conexao.rollback(); // Reverte em caso de falha
            throw e;
        }

    } catch (SQLException e) {
        System.err.println("Erro na inserção: " + e.getMessage());
    }
}
```

---

## Materiais de Apoio
- [Vídeo Tutorial: Aprenda Como Conectar JAVA com Banco de Dados usando JDBC](https://www.youtube.com/watch?v=1v4iiTRFymE)
