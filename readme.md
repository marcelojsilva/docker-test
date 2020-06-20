## Comandos docker

Executar ubuntu e entrar direto no bash
```bash
docker run -it ubuntu /bin/bash
```

Executar nginx detached redirecionando porta 8080 para 80 no container
```bash
docker run -d -p 8080:80 nginx
```

Listar containers rodando
```bash
docker ps
```

Listar todos containers
```bash
docker ps -a
```

Remover container (-f força remoção mesmo se rodando)
```bash
docker rm <id do container> ou <nome> -f
```

Executar bash no container
```bash
docker exec -it <nome> bash
```

Listar imagens
```bash
docker images
```

Remover imagens
```bash
docker rmi <nome>
```

### Criando um container Hello World com Python Flask

*index.py*
```python
from flask import Flask
app = Flask(__name__)
@app.route("/")
def hello():
	return "Hello World!"
if __name__ == "__main__":
	app.run(host="0.0.0.0", port=int("5000"), debug=True)
```
*requirements.txt*
```ptyhon
flask
```

*Dockerfile*
```docker
FROM python:3
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
EXPOSE 5000
CMD python ./index.py
```

Criando a imagem
```bash
docker build -t mjsdock/helloflaskcontainer:latest .
```

Rodando a imagem
```bash
docker run -p 5000:5000 mjsdock/helloFlaskContainer:latest
```

Publicando imagem
```bash
docker login -u mjsdock #Quando não foi feito login anteriormente
docker push mjsdock/helloFlaskContainer:latest
```