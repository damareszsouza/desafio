# desafio
desafio django - propostas de empréstimos 
rascunho teste 1 

Criação do Projeto Django:
Executar o comandodjango-admin startproject nome_do_projetopara criar o projeto Django.

Executar o comandopython manage.py startapp propostaspara criar um novo aplicativo

Definição do Modelo
Dentemodels.pydo aplicativo "propostas

Pitão

from django.db import models

class Proposta(models.Model):
    nome = models.CharField(max_length=100)
    cpf = models.CharField(max_length=14)
    valor_solicitado = models.DecimalField(max_digits=10, decimal_places=2)
    status = models.CharField(max_length=20, choices=[('pendente', 'Pendente'), ('aprovada', 'Aprovada'), ('negada', 'Negada')], default='pendente')
    data_criacao = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.nome
Criação das
Dentro doviews.pyfazer aplicativo

from django.shortcuts import render, redirect
from .models import Proposta

def listar_propostas(request):
    propostas = Proposta.objects.all()
    return render(request, 'propostas/listar_propostas.html', {'propostas': propostas})

def criar_proposta(request):
    if request.method == 'POST':
        nome = request.POST['nome']
        cpf = request.POST['cpf']
        valor_solicitado = request.POST['valor_solicitado']
        proposta = Proposta(nome=nome, cpf=cpf, valor_solicitado=valor_solicitado)
        proposta.save()
        return redirect('listar_propostas')
    return render(request, 'propostas/criar_proposta.html')
Configuração das URLs
Dentrourls.pydo projeto, anúncio


from django.urls import path
from propostas.views import listar_propostas, criar_proposta

urlpatterns = [
    path('propostas/', listar_propostas, name='listar_propostas'),
    path('propostas/nova/', criar_proposta, name='criar_proposta'),
]
Criação dos Templates HTML:
C

listar_propostas.html:

HTML


{% for proposta in propostas %}
  <p>{{ proposta.nome }}</p>
  <p>{{ proposta.valor_solicitado }}</p>
  <p>{{ proposta.status }}</p>
  <hr>
{% empty %}
  <p>Nenhuma proposta encontrada.</p>
{% endfor %}
criar_proposta.html:

HTML

<form method="post" action="{% url 'criar_proposta' %}">
  {% csrf_token %}
  <label for="nome">Nome:</label>
  <input type="text" id="nome" name="nome" required>
  <br>
  <label for="cpf">CPF:</label>
  <input type="text" id="cpf" name="cpf" required>

  
  <br>
  <label for="valor_solicitado">Valor Solicitado:</label>
  <input type="number" id="valor_solicitado" name="valor_solicitado" required>
  <br>
  <input type="submit" value="Enviar">
</form>
Certifique-sesettings.pydo seu projeto Django

interface de preenchimento de propostas em uma interface à parte (pode ser usada em um framework web como ReactJS, VueJS, Angular ou mesmo apenas HTML com CSS e JS)

# formularios separados 

HTML

<!DOCTYPE html>
<html>
<head>
  <title>Preenchimento de Propostas</title>
  <link rel="stylesheet" type="text/css" href="style.css">
</head>
<body>
  <h1>Preenchimento de Propostas</h1>
  <form id="propostaForm">
    <label for="nome">Nome:</label>
    <input type="text" id="nome" required>
    <br>
    <label for="cpf">CPF:</label>
    <input type="text" id="cpf" required>
    <br>
    <label for="valor_solicitado">Valor Solicitado:</label>
    <input type="number" id="valor_solicitado" required>
    <br>
    <button type="submit">Enviar</button>
  </form>

  <script src="script.js"></script>
</body>
</html>
Neste exemplo, criamos um formulário HTML

Você também pode criar um arquivo CSS separado (por exemplo, "style.css") para estilizar a interface de acordo com suas preferências:

css


body {
  font-family: Arial, sans-serif;
  margin: 20px;
}

h1 {
  text-align: center;
}

form {
  margin-top: 20px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input, button {
  padding: 5px;
  margin-bottom: 10px;
}

button {
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}

button:hover {
  opacity: 0.8;
}


javascript


document.getElementById('propostaForm').addEventListener('submit', function(event) {
  // Impede que o formulário seja enviado normalmente
  event.preventDefault();

  // Obtém os valores dos campos do formulário
  var nome = document.getElementById('nome').value;
  var cpf = document.getElementById('cpf').value;
  var valor_solicitado = document.getElementById('valor_solicitado').value;

  // Envia os dados para a API ou realiza outras ações necessárias
  // ...

  // Limpa os campos do formulário
  document.getElementById('nome').value = '';
  document.getElementById('cpf').value = '';
  document.getElementById('valor_solicitado').value = '';
});
