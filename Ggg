<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contratos según Borda - Práctica Interactiva</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
      background-color: #f4f4f4;
    }
    h1, h2 {
      text-align: center;
    }
    .contract-section {
      background: #fff;
      padding: 20px;
      margin-bottom: 30px;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    .question {
      margin: 10px 0;
    }
    .options label {
      display: block;
      margin: 5px 0;
      cursor: pointer;
    }
    .btn {
      padding: 10px 20px;
      margin-top: 10px;
      background-color: #007bff;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
    .btn:hover {
      background-color: #0056b3;
    }
    .result {
      margin-top: 10px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <h1>Práctica Interactiva de Contratos</h1>
  <p style="text-align:center">Basado en el Manual de Contratos de Borda (Edición 2020)</p>

  <div id="questions-container"></div>

  <script>
    const contratos = [
      {
        nombre: "Leasing",
        preguntas: [
          {
            tipo: "vf",
            pregunta: "En el contrato de leasing, el dador entrega un bien para uso y goce con opción de compra al final.",
            respuesta: true
          },
          {
            tipo: "mc",
            pregunta: "¿Cuál es un carácter esencial del leasing?",
            opciones: ["Es gratuito", "Incluye opción de compra", "Es siempre verbal"],
            respuesta: "Incluye opción de compra"
          }
        ]
      },
      {
        nombre: "Obra",
        preguntas: [
          {
            tipo: "vf",
            pregunta: "En el contrato de obra, el contratista se obliga a realizar una obra a cambio de un precio.",
            respuesta: true
          },
          {
            tipo: "mc",
            pregunta: "¿Cuál es un elemento esencial del contrato de obra?",
            opciones: ["La entrega de dinero en préstamo", "La realización de una obra determinada", "El depósito de bienes"],
            respuesta: "La realización de una obra determinada"
          }
        ]
      },
      {
        nombre: "Servicio",
        preguntas: [
          {
            tipo: "vf",
            pregunta: "En el contrato de servicios, el prestador se obliga a realizar tareas sin resultado determinado.",
            respuesta: true
          },
          {
            tipo: "mc",
            pregunta: "¿Cuál es un carácter del contrato de servicios?",
            opciones: ["Es intuitu personae", "Es real", "Es gratuito siempre"],
            respuesta: "Es intuitu personae"
          }
        ]
      },
      {
        nombre: "Mutuo",
        preguntas: [
          {
            tipo: "vf",
            pregunta: "El mutuo es siempre gratuito.",
            respuesta: false
          },
          {
            tipo: "mc",
            pregunta: "El mutuo implica la entrega de: ",
            opciones: ["Bienes no fungibles", "Bienes fungibles para consumo", "Una cosa en depósito"],
            respuesta: "Bienes fungibles para consumo"
          }
        ]
      },
      {
        nombre: "Comodato",
        preguntas: [
          {
            tipo: "vf",
            pregunta: "El comodato es un préstamo gratuito de uso de cosas no fungibles.",
            respuesta: true
          },
          {
            tipo: "mc",
            pregunta: "Obligación principal del comodatario es:",
            opciones: ["Conservar y restituir la cosa", "Pagar intereses", "Transferir la propiedad"],
            respuesta: "Conservar y restituir la cosa"
          }
        ]
      },
      {
        nombre: "Depósito",
        preguntas: [
          {
            tipo: "vf",
            pregunta: "En el depósito, el depositario se obliga a guardar la cosa y devolverla cuando se le pida.",
            respuesta: true
          },
          {
            tipo: "mc",
            pregunta: "¿Cuál es una obligación esencial del depositante?",
            opciones: ["Custodiar la cosa", "Pagar el precio si es oneroso", "Usar la cosa"],
            respuesta: "Pagar el precio si es oneroso"
          }
        ]
      },
      {
        nombre: "Donación",
        preguntas: [
          {
            tipo: "vf",
            pregunta: "La donación es un contrato unilateral por el cual se transfiere gratuitamente un bien.",
            respuesta: true
          },
          {
            tipo: "mc",
            pregunta: "¿Cuál es un requisito esencial de la donación?",
            opciones: ["La causa onerosa", "La aceptación del donatario", "La entrega inmediata"],
            respuesta: "La aceptación del donatario"
          }
        ]
      }
    ];

    const container = document.getElementById('questions-container');

    contratos.forEach(contrato => {
      const section = document.createElement('div');
      section.className = 'contract-section';
      section.innerHTML = <h2>${contrato.nombre}</h2>;

      contrato.preguntas.forEach((q, index) => {
        const div = document.createElement('div');
        div.className = 'question';

        if(q.tipo === 'vf') {
          div.innerHTML = `
            <p>${q.pregunta}</p>
            <div class="options">
              <label><input type="radio" name="${contrato.nombre}-${index}" value="true"> Verdadero</label>
              <label><input type="radio" name="${contrato.nombre}-${index}" value="false"> Falso</label>
            </div>
            <button class="btn" onclick="checkAnswer('${contrato.nombre}-${index}', '${q.respuesta}')">Responder</button>
            <div class="result" id="result-${contrato.nombre}-${index}"></div>
          `;
        } else {
          let opts = q.opciones.map(opt => <label><input type="radio" name="${contrato.nombre}-${index}" value="${opt}"> ${opt}</label>).join('');
          div.innerHTML = `
            <p>${q.pregunta}</p>
            <div class="options">${opts}</div>
            <button class="btn" onclick="checkAnswer('${contrato.nombre}-${index}', '${q.respuesta}')">Responder</button>
            <div class="result" id="result-${contrato.nombre}-${index}"></div>
          `;
        }

        section.appendChild(div);
      });

      container.appendChild(section);
    });

    function checkAnswer(name, correctAnswer) {
      const radios = document.getElementsByName(name);
      let selected = null;
      for(const r of radios) {
        if(r.checked) selected = r.value;
      }
      const resultDiv = document.getElementById('result-' + name);
      if(selected === null) {
        resultDiv.innerHTML = "Seleccioná una opción.";
        resultDiv.style.color = "orange";
      } else if(selected == correctAnswer) {
        resultDiv.innerHTML = "¡Correcto!";
        resultDiv.style.color = "green";
      } else {
        resultDiv.innerHTML = "Incorrecto.";
        resultDiv.style.color = "red";
      }
    }
  </script>
</body>
</html>
