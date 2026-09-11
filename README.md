### 1 Problemas encontrados
#### Defesa do código

#### 1.1 Definição da classe Serviços feita em app.py

Essa classe deveria ter sido escrita em models.py ou em um arquivo python separado. Considerado erradop pois a definição de classes que representem entidades deve ser feita na camada Models.

#### 1.2 Rotas no App.py

O app.py deve ser prioritariamente para instanciar o Flask e registrar algumas ferramentas. Essas rotas que estão nele deveriam estar separadas por camadas/blueprints. Ex: login e logout em `blueprints/auth`, serviços em `blueprints/servicos`

#### 1.3 Templates misturados

Apesar de haver uma separação dos arquivos HTML(templates) em uma pasta única, o recomendado é que eles também fiquem separados nos blueprints. Ex: 

auth/templates
- /auth
- - login.html
- - logout.html

#### 1.4 Models em um arquivo único

Apesar de entender que R10(Romerito) utilizou um único arquivo models.py para realizar a prova, o ideal ainda seria separar os models por blueprints ao invés de deixá-los todos compartilhados.

### 2 Localização da camada Model e Controllers

A camada model é o arquivo único models.py, pois foi o que foi dado como base para a avaliação. 
Trecho do model:
servicos = [
    {"id": 1, "descricao": "Troca de tela do celular", "categoria": "Eletrônico", "prazo": "3 dias úteis", "valor": 250.00},
    {"id": 2, "descricao": "Calibragem de bicicleta", "categoria": "Mecânico", "prazo": "1 dia útil", "valor": 80.00},
    {"id": 3, "descricao": "Reparo de placa-mãe", "categoria": "Eletrônico", "prazo": "5 dias úteis", "valor": 450.00},
    {"id": 4, "descricao": "Instalação de interruptor", "categoria": "Elétrico", "prazo": "2 dias úteis", "valor": 120.00},
    {"id": 5, "descricao": "Conserto de ventilador", "categoria": "Elétrico", "prazo": "2 dias úteis", "valor": 90.00},
]

Os controllers eram os arquivos routes.py de cada blueprint
Trecho do auth:
@auth_bp.route("/logout")
def logout():
    session.pop("usuario", None)
    return redirect(url_for("servicos.index"))

### 3 url_for

O url_for do login precisava de um ajuste, pois ele fazia o redirecionamento para uma rota chamada 'painel' que não existia. Os endpoints precisavam ter o '@app' trocado por '@nome_blueprint_bp.route'. De resto, nas referências só era preciso ser colocado o nome do blueprint, seguido por um ponto (.) e o nome da rota que desejava ser acessada.
