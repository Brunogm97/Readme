```python
!pip install Flask

```

    Requirement already satisfied: Flask in c:\users\bruno\anaconda3\lib\site-packages (2.2.2)
    Requirement already satisfied: Werkzeug>=2.2.2 in c:\users\bruno\anaconda3\lib\site-packages (from Flask) (2.2.3)
    Requirement already satisfied: Jinja2>=3.0 in c:\users\bruno\anaconda3\lib\site-packages (from Flask) (3.1.2)
    Requirement already satisfied: itsdangerous>=2.0 in c:\users\bruno\anaconda3\lib\site-packages (from Flask) (2.0.1)
    Requirement already satisfied: click>=8.0 in c:\users\bruno\anaconda3\lib\site-packages (from Flask) (8.0.4)
    Requirement already satisfied: colorama in c:\users\bruno\anaconda3\lib\site-packages (from click>=8.0->Flask) (0.4.6)
    Requirement already satisfied: MarkupSafe>=2.0 in c:\users\bruno\anaconda3\lib\site-packages (from Jinja2>=3.0->Flask) (2.1.1)
    


```python
# Conversor de Anos-Luz para Quilômetros

Esta é uma API simples em .NET que converte distâncias de anos-luz para quilômetros e vice-versa.

## Como usar

Para converter uma distância, faça uma requisição GET para os endpoints `/converter?value=<valor>&unit=<unidade>`, onde:
- `value` é o valor a ser convertido
- `unit` é a unidade de medida (`km` para quilômetros ou `anos-luz` para anos-luz)

Exemplo de requisição:
    
    GET /converter?value=1&unit=km
    

## Exemplos de Resposta

- Sucesso (200 OK):


```


```python
using Microsoft.AspNetCore.Mvc;
using System;

namespace ConversorDeUnidades.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class ConverterController : ControllerBase
    {
        [HttpGet]
        public ActionResult<object> Get(double value, string unit)
        {
            if (value < 1 || !ModelState.IsValid || (unit != "km" && unit != "anos-luz"))
            {
                return BadRequest(new
                {
                    statusCode = 400,
                    errorMessage = "Valor inválido ou unidade inválida",
                    dateTime = DateTime.UtcNow,
                    value = 0.0
                });
            }

            double result = unit == "km" ? value * 9.461e12 : value / 9.461e12;

            return Ok(new
            {
                statusCode = 200,
                errorMessage = "",
                dateTime = DateTime.UtcNow,
                value = result
            });
        }
    }
}

```


```python
from flask import Flask, request, jsonify
import datetime

app = Flask(__name__)

@app.route('/netcon/api/v1/converter', methods=['GET'])
def converter():
    try:
        if 'km' in request.args:
            km = float(request.args.get('km'))
            anos_luz = km / 9.461e12
            return jsonify({
                'statusCode': 200,
                'errorMessage': None,
                'dateTime': datetime.datetime.now().strftime("%d/%m/%Y %H:%M:%S"),
                'value': anos_luz
            }), 200
        elif 'anos-luz' in request.args:
            anos_luz = float(request.args.get('anos-luz'))
            km = anos_luz * 9.461e12
            return jsonify({
                'statusCode': 200,
                'errorMessage': None,
                'dateTime': datetime.datetime.now().strftime("%d/%m/%Y %H:%M:%S"),
                'value': km
            }), 200
        else:
            return jsonify({
                'statusCode': 400,
                'errorMessage': 'Parâmetro inválido',
                'dateTime': datetime.datetime.now().strftime("%d/%m/%Y %H:%M:%S"),
                'value': None
            }), 400
    except ValueError:
        return jsonify({
            'statusCode': 400,
            'errorMessage': 'Valor inválido',
            'dateTime': datetime.datetime.now().strftime("%d/%m/%Y %H:%M:%S"),
            'value': None
        }), 400

if __name__ == '__main__':
    app.run()

with open('README.md', 'w') as arquivo:
    arquivo.write(conteudo)

print("Arquivo README.md salvo com sucesso!")
```
