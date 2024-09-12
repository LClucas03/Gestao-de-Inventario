# Gestao-de-Inventario

CRIAR BANCO DE DADOS EmployeeManagement;
USE Gestão de Funcionários;
CRIAR TABELA Departamentos (
    department_id INT INCREMENTO AUTOMÁTICO CHAVE PRIMÁRIA,
    nome_do_departamento VARCHAR(100) ÚNICO NÃO NULO
);
CRIAR TABELA Funcionários (
    employee_id INT INCREMENTO AUTOMÁTICO CHAVE PRIMÁRIA,
    first_name VARCHAR(50) NÃO NULO,
    sobrenome VARCHAR(50) NÃO NULO,
    e-mail VARCHAR(100) ÚNICO NÃO NULO,
    telefone VARCHAR(20),
    hire_date DATA NÃO NULA,
    departamento_id INT,
    CHAVE ESTRANGEIRA (department_id) REFERÊNCIAS Departamentos(department_id)
);
CRIAR TABELA Salários (
    salary_id INT INCREMENTO AUTOMÁTICO CHAVE PRIMÁRIA,
    funcionário_id INT,
    quantidade DECIMAL(10, 2) NÃO NULO,
    data_efetiva DATA NÃO NULA,
    CHAVE ESTRANGEIRA (employee_id) REFERÊNCIAS Funcionários(employee_id)
);
INSERIR EM Departamentos (department_name)
VALORES ('RH'), ('Finanças'), ('Engenharia');
INSERIR EM Funcionários (nome, sobrenome, e-mail, telefone, data de contratação, id do departamento)
VALORES ('Alice', 'Smith', 'alice.smith@example.com', '555-1234', '2024-01-15', 1),
       ('Bob', 'Johnson', 'bob.johnson@example.com', '555-5678', '2024-03-22', 2),
       ('Charlie', 'Williams', 'charlie.williams@example.com', '555-8765', '2024-06-10', 3);
INSERIR EM Salários (id_funcionário, valor, data_efetiva)
VALORES (1, 50000.00, '2024-01-15'),
       (2, 60000.00, '2024-03-22'),
       (3, 70000.00, '2024-06-10');
SELECIONE * DE Funcionários;
SELECIONE e.employee_id, e.first_name, e.last_name, d.department_name
DE Funcionários e
JUNTE-SE Departamentos d ON e.department_id = d.department_id;
SELECIONE e.primeiro_nome, e.sobrenome, s.valor, s.data_efetiva
DE Salários s
JUNTE-SE Funcionários e ON s.employee_id = e.employee_id
ONDE e.email = 'alice.smith@example.com';
SELECIONE e.primeiro_nome, e.sobrenome, s.valor, s.data_efetiva
DE Funcionários e
JUNTE Salários s ON e.employee_id = s.employee_id;
ATUALIZAÇÃO Funcionários
DEFINIR departamento_id = 2
ONDE e-mail = 'bob.johnson@example.com';
ATUALIZAÇÃO Funcionários
DEFINIR departamento_id = 2
ONDE e-mail = 'bob.johnson@example.com';
ATUALIZAÇÃO Salários
Valor definido = 55000,00
ONDE employee_id = 1 E effective_date = '2024-01-15';
EXCLUIR DE Funcionários
ONDE e-mail = 'charlie.williams@example.com';
EXCLUIR DE Departamentos
ONDE nome_do_departamento = 'Finanças';
