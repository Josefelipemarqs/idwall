<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Redirecionamento</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
        }

        #cpfForm {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            text-align: center;
            width: 300px;
        }

        h2 {
            margin-bottom: 20px;
            font-size: 20px;
            color: #333;
        }

        input[type="text"] {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 16px;
        }

        button {
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            background-color: #007bff;
            color: white;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        button:hover {
            background-color: #0056b3;
        }

        #sdkContainer {
            display: none;
            text-align: center;
        }
    </style>
    <script>
        // Redireciona de 127.0.0.1 para localhost
        if (window.location.hostname === '127.0.0.1') {
            window.location.href = window.location.href.replace('127.0.0.1', 'localhost');
        }
    </script>
</head>
<body>
    <div id="cpfForm">
        <h2>Insira o CPF ou Nº de telefone</h2>
        <input type="text" id="cpfInput" placeholder="Digite aqui" maxlength="11" required>
        <button id="submitCpf">Enviar</button>
    </div>

    <div id="sdkContainer">
        <script src="https://sdkweb-lib.idwall.co/index.js"></script>
        <div data-sdk-dynamic-link></div>
        <script>
            function initializeSDK(profileRef) {
                idwSdkDynamicLink({
                    token: 'U2FsdGVkX1/c3QwKTpYAvmRHKHuyVcawb4xX/jZkPLogJq00Lw==',
                    profileRef: profileRef,
                    onRender: () => {
                        console.log('it renders!');
                    },
                    onComplete: ({ token }) => {
                        console.log(token);
                    }
                });
            }

            document.getElementById('submitCpf').addEventListener('click', function() {
                const cpf = document.getElementById('cpfInput').value;
                if (cpf) {
                    document.getElementById('cpfForm').style.display = 'none';
                    document.getElementById('sdkContainer').style.display = 'block';
                    initializeSDK(cpf);
                } else {
                    alert('Por favor, insira um CPF válido.');
                }
            });
        </script>
    </div>
</body>
</html>
