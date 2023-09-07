# projetoKotlinDIO
// Classe que representa um aluno
data class Aluno(val nome: String, val matricula: String) {
    val cursosMatriculados = mutableListOf<Curso>()

    fun matricularEmCurso(curso: Curso) {
        cursosMatriculados.add(curso)
        curso.adicionarAluno(this)
    }
}

// Classe que representa um curso
data class Curso(val nome: String, val codigo: String, val cargaHoraria: Int) {
    val alunosMatriculados = mutableListOf<Aluno>()

    fun adicionarAluno(aluno: Aluno) {
        alunosMatriculados.add(aluno)
    }

    fun calcularCusto(): Double {
        // Aqui você pode implementar a lógica para calcular o custo do curso
        // Por exemplo, considerando um valor por hora de aula
        val valorPorHora = 10.0 // Altere para o valor desejado
        return cargaHoraria * valorPorHora
    }
}

// Classe que representa uma formação educacional
data class FormacaoEducacional(val nome: String) {
    val cursos = mutableListOf<Curso>()

    fun adicionarCurso(curso: Curso) {
        cursos.add(curso)
    }

    fun calcularCargaHorariaTotal(): Int {
        return cursos.sumBy { it.cargaHoraria }
    }

    fun calcularCustoTotal(): Double {
        return cursos.sumByDouble { it.calcularCusto() }
    }
}

fun main() {
    // Criando alguns alunos
    val aluno1 = Aluno("João", "123")
    val aluno2 = Aluno("Maria", "456")

    // Criando alguns cursos
    val curso1 = Curso("Programação em Kotlin", "KOT-101", 40)
    val curso2 = Curso("Banco de Dados", "DB-201", 30)

    // Matriculando alunos nos cursos
    aluno1.matricularEmCurso(curso1)
    aluno2.matricularEmCurso(curso1)
    aluno2.matricularEmCurso(curso2)

    // Criando uma formação educacional
    val formacao = FormacaoEducacional("Desenvolvimento de Software")

    // Adicionando cursos à formação educacional
    formacao.adicionarCurso(curso1)
    formacao.adicionarCurso(curso2)

    // Imprimindo informações sobre a formação educacional
    println("Formação Educacional: ${formacao.nome}")
    println("Carga Horária Total: ${formacao.calcularCargaHorariaTotal()} horas")
    println("Custo Total da Formação: R$ ${formacao.calcularCustoTotal()}")

    // Imprimindo informações sobre os cursos e alunos matriculados
    println("\nCursos da Formação:")
    for (curso in formacao.cursos) {
        println("Nome do Curso: ${curso.nome}")
        println("Carga Horária: ${curso.cargaHoraria} horas")
        println("Alunos Matriculados:")
        for (aluno in curso.alunosMatriculados) {
            println("- ${aluno.nome}")
        }
        println("Custo do Curso: R$ ${curso.calcularCusto()}\n")
    }
}
