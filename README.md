# Projeto de Banco de Dados Universitário

Este projeto apresenta a modelagem de um banco de dados relacional voltado para o gerenciamento acadêmico de uma universidade. O modelo contempla entidades como alunos, cursos, professores, disciplinas, turmas e provas, permitindo organizar informações acadêmicas e apoiar análises sobre desempenho, estrutura curricular e relacionamento entre professores e cursos.

## Objetivo do Projeto

O objetivo principal deste projeto é criar uma estrutura de banco de dados capaz de representar o funcionamento básico de uma instituição de ensino superior, considerando:

- Cadastro de alunos
- Cadastro de cursos de graduação
- Cadastro de professores
- Associação entre professores e cursos
- Cadastro de disciplinas vinculadas a cursos
- Cadastro de turmas por disciplina e professor
- Cadastro de provas aplicadas por disciplina
- Relacionamento entre as principais entidades acadêmicas

A modelagem foi desenvolvida com foco em organização, integridade referencial e possibilidade de expansão para análises acadêmicas mais completas.

## Tecnologias Utilizadas

- Banco de Dados Oracle
- SQL
- Modelagem Relacional
- Diagrama Entidade-Relacionamento

## Estrutura do Banco de Dados

O banco de dados é composto pelas seguintes tabelas:

- Aluno
- Curso
- Professor
- Prova
- professorcurso
- Disciplina
- Turma

## Descrição das Tabelas

### Tabela Aluno

A tabela `Aluno` armazena as informações dos estudantes cadastrados na instituição.

Campos principais:

- `idAluno`: identificador único do aluno
- `nomeAluno`: nome completo do aluno
- `cpfAluno`: CPF do aluno
- `dataNascimentoAluno`: data de nascimento
- `anoInicioGraduacao`: ano de ingresso na graduação
- `mediaAluno`: média geral do aluno
- `idCursoGraduacao`: chave estrangeira que referencia o curso do aluno

Relacionamento:

- Um curso pode possuir vários alunos.
- Cada aluno está associado a um curso de graduação.

### Tabela Curso

A tabela `Curso` armazena os dados dos cursos de graduação oferecidos pela instituição.

Campos principais:

- `idGraduacao`: identificador único do curso
- `cursoGaduacao`: nome do curso de graduação
- `areaAtuacao`: área de conhecimento ou atuação do curso
- `tempoPeriodosTotal`: duração total do curso em períodos

Relacionamentos:

- Um curso pode possuir vários alunos.
- Um curso pode possuir várias disciplinas.
- Um curso pode estar associado a vários professores por meio da tabela `professorcurso`.

### Tabela Professor

A tabela `Professor` armazena os dados dos professores da instituição.

Campos principais:

- `idProfessor`: identificador único do professor
- `nomeProfessor`: nome completo do professor
- `dataNascimentoProfessor`: data de nascimento
- `dataContratacao`: data de contratação

Relacionamentos:

- Um professor pode estar associado a vários cursos.
- Um professor pode lecionar várias turmas.
- Um professor pode ser responsável por várias provas.

### Tabela professorcurso

A tabela `professorcurso` é uma tabela de junção utilizada para representar o relacionamento muitos-para-muitos entre professores e cursos.

Campos principais:

- `idProfessorCurso`: identificador único da associação
- `idProfessor`: chave estrangeira para a tabela `Professor`
- `idGraduacao`: chave estrangeira para a tabela `Curso`
- `dataInicio`: data de início do vínculo entre professor e curso
- `dataFim`: data de fim do vínculo entre professor e curso

Relacionamento:

- Um professor pode lecionar em vários cursos.
- Um curso pode possuir vários professores.

Essa tabela evita redundância de dados e permite registrar o histórico de vínculo dos professores com os cursos.

### Tabela Disciplina

A tabela `Disciplina` armazena as disciplinas pertencentes aos cursos de graduação.

Campos principais:

- `idDisciplina`: identificador único da disciplina
- `nomeDisciplina`: nome da disciplina
- `cargaHoraria`: carga horária da disciplina
- `periodoSugerido`: período recomendado para cursar a disciplina
- `idCursoGraduacao`: chave estrangeira que referencia o curso ao qual a disciplina pertence

Relacionamento:

- Um curso pode possuir várias disciplinas.
- Cada disciplina pertence a um curso.

### Tabela Turma

A tabela `Turma` representa a oferta de uma disciplina em determinado ano, semestre, turno e sala.

Campos principais:

- `idTurma`: identificador único da turma
- `idDisciplina`: chave estrangeira para a tabela `Disciplina`
- `idProfessor`: chave estrangeira para a tabela `Professor`
- `anoLetivo`: ano em que a turma foi ofertada
- `semestre`: semestre letivo
- `turno`: turno da turma
- `sala`: sala onde a turma ocorre

Relacionamentos:

- Uma disciplina pode possuir várias turmas.
- Um professor pode lecionar várias turmas.
- Cada turma está associada a uma disciplina e a um professor.

### Tabela Prova

A tabela `Prova` armazena informações sobre as avaliações aplicadas nas disciplinas.

Campos principais:

- `idProva`: identificador único da prova
- `dataAplicacaoProva`: data de aplicação da prova
- `idDisciplina`: chave estrangeira para a tabela `Disciplina`
- `qtdeQuestoes`: quantidade de questões da prova
- `idProfessor`: chave estrangeira para a tabela `Professor`
- `tipoProva`: tipo da avaliação
- `pesoProva`: peso da prova na composição da média

Relacionamentos:

- Uma disciplina pode possuir várias provas.
- Um professor pode ser responsável por várias provas.

## Relacionamentos do Modelo

O modelo possui os seguintes relacionamentos principais:

```text
Curso 1:N Aluno
Curso 1:N Disciplina
Professor N:N Curso
Disciplina 1:N Turma
Professor 1:N Turma
Disciplina 1:N Prova
Professor 1:N Prova
