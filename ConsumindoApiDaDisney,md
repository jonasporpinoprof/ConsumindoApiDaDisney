# ConsumindoApiDaDisney


Para consumir a API da Disney e exibir os nomes dos personagens e os filmes relacionados, você pode utilizar a biblioteca `requests` do Python para fazer uma requisição GET e manipular os dados da resposta JSON.

Aqui está um exemplo simples de como fazer isso:

```python
import requests

# URL da API para o personagem específico
url = "https://api.disneyapi.dev/character/18"

# Fazer a requisição GET para a API
response = requests.get(url)

# Verificar se a requisição foi bem-sucedida
if response.status_code == 200:
    # Converter a resposta para JSON
    data = response.json()
    
    # Extrair o nome do personagem
    name = data['data']['name']
    
    # Extrair os filmes em que o personagem aparece
    films = data['data']['films']
    
    # Exibir o nome do personagem e seus filmes
    print(f"Personagem: {name}")
    if films:
        print("Filmes:")
        for film in films:
            print(f"- {film}")
    else:
        print("Este personagem não aparece em nenhum filme.")
else:
    print(f"Erro ao acessar a API. Status code: {response.status_code}")
```

### Explicação:
- Usamos a biblioteca `requests` para fazer uma requisição HTTP.
- Verificamos o status da resposta para garantir que a requisição foi bem-sucedida (código 200).
- A resposta JSON é convertida em um dicionário Python para facilitar a manipulação dos dados.
- Extraímos o nome do personagem e a lista de filmes do campo `data`.
- Os filmes são exibidos em formato de lista. Se o personagem não tiver filmes listados, exibimos uma mensagem apropriada.

Você pode modificar o código para consumir outros endpoints ou tratar diferentes personagens.


Você pode combinar o código que consome a API com a interface gráfica criada usando `Tkinter`. Além disso, para exibir a imagem do personagem a partir da `imageUrl`, podemos utilizar a biblioteca `PIL` (Pillow) para carregar e mostrar a imagem no `Tkinter`.

# Mostrar nome do personagem, filme e imagem

Aqui está um exemplo de como integrar tudo isso:

1. Consome a API.
2. Exibe o nome do personagem e os filmes.
3. Exibe a imagem do personagem.

Instale a biblioteca Pillow, se ainda não tiver:
```bash
pip install pillow
```
A falha na exibição da imagem no `Tkinter` pode ocorrer devido a dois problemas comuns:

1. O redimensionamento da imagem com `Image.ANTIALIAS` foi depreciado nas versões mais recentes do `Pillow`.
2. O formato da imagem retornada pela API pode ser incompatível ou não estar sendo carregado corretamente.

Aqui está o código ajustado para garantir que a imagem seja exibida corretamente. Vamos remover a constante `Image.ANTIALIAS` e garantir que o formato da imagem seja compatível:

```python
import requests
import tkinter as tk
from tkinter import messagebox
from PIL import Image, ImageTk
from io import BytesIO

# Função para buscar dados do personagem da API
def buscar_personagem():
    url = "https://api.disneyapi.dev/character/18"
    
    try:
        response = requests.get(url)
        response.raise_for_status()  # Levanta exceção para status codes de erro
        
        data = response.json()
        
        # Extrair nome e filmes do personagem
        name = data['data']['name']
        films = data['data']['films']
        image_url = data['data']['imageUrl']
        
        # Atualizar os rótulos na janela
        label_nome.config(text=f"Personagem: {name}")
        
        # Exibir a lista de filmes
        if films:
            filmes_text = "\n".join(films)
        else:
            filmes_text = "Este personagem não aparece em nenhum filme."
        
        label_filmes.config(text=f"Filmes:\n{filmes_text}")
        
        # Exibir a imagem
        carregar_imagem(image_url)
        
    except requests.exceptions.RequestException as e:
        messagebox.showerror("Erro", f"Erro ao acessar a API: {e}")

# Função para carregar e exibir a imagem do personagem
def carregar_imagem(url):
    try:
        response = requests.get(url)
        response.raise_for_status()
        
        # Carregar a imagem da URL
        image_data = response.content
        image = Image.open(BytesIO(image_data))
        
        # Redimensionar a imagem para caber na interface
        image = image.resize((200, 200))  # Sem usar o Image.ANTIALIAS, que foi removido
        
        # Converter para um formato compatível com Tkinter
        img_tk = ImageTk.PhotoImage(image)
        
        # Atualizar o rótulo da imagem
        label_imagem.config(image=img_tk)
        label_imagem.image = img_tk  # Necessário manter a referência para não perder a imagem
        
    except requests.exceptions.RequestException as e:
        messagebox.showerror("Erro", f"Erro ao carregar a imagem: {e}")

# Criar a janela principal
root = tk.Tk()
root.title("Disney Personagens")
root.geometry("400x500")

# Criar rótulos para exibir os dados
label_nome = tk.Label(root, text="Personagem: ", font=("Arial", 14))
label_nome.pack(pady=10)

label_filmes = tk.Label(root, text="Filmes:", font=("Arial", 12), justify=tk.LEFT)
label_filmes.pack(pady=10)

# Rótulo para exibir a imagem
label_imagem = tk.Label(root)
label_imagem.pack(pady=20)

# Botão para buscar os dados do personagem
btn_buscar = tk.Button(root, text="Buscar Personagem", command=buscar_personagem)
btn_buscar.pack(pady=20)

# Iniciar o loop da janela
root.mainloop()
```

### Depois de um erro no carregamento da imagem foram feitas as seguintes mudanças:
1. **Redimensionamento da imagem**: O uso de `Image.ANTIALIAS` foi removido, pois essa constante foi descontinuada nas versões mais recentes do `Pillow`. Agora o redimensionamento está funcionando sem ela.
2. **Referência da imagem**: Mantive a referência para a imagem (`label_imagem.image = img_tk`) para evitar que o Python colete o objeto de imagem.

Testando essas modificações, a imagem do personagem deve ser exibida corretamente na interface `Tkinter`.

# Mostrar personagens com entrada de id pelo usuário

Ids disponíveis:

( 112 )( 18 )( 16 )( 45 )( 7 )( 12 )( 36 )( 139 )( 152 )( 181 )( 204 )( 215 )( 293 )( 295 )( 310 )( 327 )( 336 )( 337 )( 342 )( 347 )( 350 )( 364 )( 380 )( 384 )( 404 )( 410 )( 440 )( 442 )( 450 )( 469 )( 474 )( 490 )( 500 )( 529 )( 543 )( 566 )( 157 )( 189 )( 206 )( 207 )( 223 )( 241 )( 247 )( 268 )( 278 )( 285 )( 291 )( 303 )( 322 )( 351 )

Aqui está o código atualizado que inclui uma `Entry` (campo de entrada) para que o usuário possa digitar o ID do personagem. A função `buscar_personagem()` foi modificada para buscar o personagem com base no ID fornecido pelo usuário.

```python
import requests
import tkinter as tk
from tkinter import messagebox
from PIL import Image, ImageTk
from io import BytesIO

# Função para buscar dados do personagem da API com base no ID inserido pelo usuário
def buscar_personagem():
    character_id = entry_id.get()  # Obter o ID do personagem inserido pelo usuário
    
    if not character_id.isdigit():
        messagebox.showerror("Erro", "Por favor, insira um ID válido (número).")
        return
    
    url = f"https://api.disneyapi.dev/character/{character_id}"
    
    try:
        response = requests.get(url)
        response.raise_for_status()  # Levanta exceção para status codes de erro
        
        data = response.json()
        
        # Verificar se há dados no campo 'data'
        if not data.get('data'):
            messagebox.showerror("Erro", "Personagem não encontrado.")
            return
        
        # Extrair nome e filmes do personagem
        name = data['data']['name']
        films = data['data']['films']
        image_url = data['data']['imageUrl']
        
        # Atualizar os rótulos na janela
        label_nome.config(text=f"Personagem: {name}")
        
        # Exibir a lista de filmes
        if films:
            filmes_text = "\n".join(films)
        else:
            filmes_text = "Este personagem não aparece em nenhum filme."
        
        label_filmes.config(text=f"Filmes:\n{filmes_text}")
        
        # Exibir a imagem
        carregar_imagem(image_url)
        
    except requests.exceptions.RequestException as e:
        messagebox.showerror("Erro", f"Erro ao acessar a API: {e}")

# Função para carregar e exibir a imagem do personagem
def carregar_imagem(url):
    try:
        response = requests.get(url)
        response.raise_for_status()
        
        # Carregar a imagem da URL
        image_data = response.content
        image = Image.open(BytesIO(image_data))
        
        # Redimensionar a imagem para caber na interface
        image = image.resize((200, 200))  # Sem usar o Image.ANTIALIAS, que foi removido
        
        # Converter para um formato compatível com Tkinter
        img_tk = ImageTk.PhotoImage(image)
        
        # Atualizar o rótulo da imagem
        label_imagem.config(image=img_tk)
        label_imagem.image = img_tk  # Necessário manter a referência para não perder a imagem
        
    except requests.exceptions.RequestException as e:
        messagebox.showerror("Erro", f"Erro ao carregar a imagem: {e}")

# Criar a janela principal
root = tk.Tk()
root.title("Disney Personagens")
root.geometry("400x600")

# Rótulo para o ID do personagem
label_id = tk.Label(root, text="Digite o ID do personagem:", font=("Arial", 12))
label_id.pack(pady=10)

# Campo de entrada para o ID do personagem
entry_id = tk.Entry(root, font=("Arial", 12))
entry_id.pack(pady=10)

# Botão para buscar os dados do personagem
btn_buscar = tk.Button(root, text="Buscar Personagem", command=buscar_personagem)
btn_buscar.pack(pady=10)

# Criar rótulos para exibir os dados
label_nome = tk.Label(root, text="Personagem: ", font=("Arial", 14))
label_nome.pack(pady=10)

label_filmes = tk.Label(root, text="Filmes:", font=("Arial", 12), justify=tk.LEFT)
label_filmes.pack(pady=10)

# Rótulo para exibir a imagem
label_imagem = tk.Label(root)
label_imagem.pack(pady=20)

# Iniciar o loop da janela
root.mainloop()
```

### O que foi alterado:
1. **Campo de entrada (`Entry`)**: Adicionamos uma `Entry` para que o usuário possa digitar o ID do personagem que deseja buscar. 
2. **Validação do ID**: Verificamos se o valor inserido é um número antes de tentar buscar os dados. Caso contrário, exibimos uma mensagem de erro.
3. **Uso do ID**: O ID fornecido pelo usuário é passado na URL da requisição à API.

Agora, o usuário pode digitar o ID do personagem na interface, e ao clicar em "Buscar Personagem", os dados (nome, filmes e imagem) do personagem correspondente serão exibidos.
