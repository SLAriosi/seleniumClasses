# seleniumClasses

Aulas sobre Selenium com Python assistindo e estudando as aulas do Dunossauro (Eduardo Mendes) no YouTube.

## Ferramentas Utilizadas

<span>
    <img src="https://github.com/SLAriosi/svgTools/blob/main/Selenium.png" width="40" height="40" alt="Selenium" />
    <img src="https://github.com/SLAriosi/svgTools/blob/main/Python.png" width="40" height="40" alt="Python" />
</span>

## Conteúdo

- [Introdução ao Selenium](#introdução-ao-selenium)
- [Configuração do Ambiente](#configuração-do-ambiente)
- [Navegação Básica](#navegação-básica)
- [Interação com Elementos](#interação-com-elementos)
- [Esperas Explícitas e Implícitas](#esperas-explícitas-e-implícitas)
- [Execução de Scripts JavaScript](#execução-de-scripts-javascript)
- [Manipulação de Janelas e Frames](#manipulação-de-janelas-e-frames)
- [Captura de Screenshots](#captura-de-screenshots)
- [Testes Automatizados](#testes-automatizados)
- [Boas Práticas](#boas-práticas)
- [Projetos Avançados](#projetos-avançados)

## Aula 07 - Eventos

Nesta aula, abordamos os eventos no Selenium, como interagir com elementos da página e como automatizar testes de forma eficiente.

## Introdução ao Selenium

O Selenium é uma ferramenta poderosa para automação de navegadores web. Ele permite que você controle um navegador programaticamente, simulando ações de um usuário real.

## Configuração do Ambiente

Para começar, você precisará instalar o Selenium e o driver do navegador que deseja usar. Aqui está um exemplo de como instalar o Selenium e o ChromeDriver:

pip install selenium

Baixe o ChromeDriver em [ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/) e adicione-o ao seu PATH.

## Navegação Básica

Exemplo de código para abrir uma página web:

from selenium import webdriver

browser = webdriver.Chrome()
browser.get('https://www.example.com')

## Interação com Elementos

Exemplo de código para interagir com elementos da página:

element = browser.find_element_by_name('q')
element.send_keys('Selenium')
element.submit()

## Esperas Explícitas e Implícitas

Exemplo de código para usar esperas explícitas:

from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

element = WebDriverWait(browser, 10).until(
    EC.presence_of_element_located((By.ID, 'myElement'))
)

## Execução de Scripts JavaScript

Exemplo de código para executar scripts JavaScript:

browser.execute_script("alert('Hello, World!');")

## Manipulação de Janelas e Frames

Exemplo de código para manipular janelas e frames:

browser.switch_to.window(browser.window_handles[1])
browser.switch_to.frame('myFrame')

## Captura de Screenshots

Exemplo de código para capturar screenshots:

browser.save_screenshot('screenshot.png')

## Testes Automatizados

Exemplo de código para criar testes automatizados:

import unittest

class TestExample(unittest.TestCase):
    def setUp(self):
        self.browser = webdriver.Chrome()

    def test_example(self):
        self.browser.get('https://www.example.com')
        self.assertIn('Example Domain', self.browser.title)

    def tearDown(self):
        self.browser.quit()

if __name__ == '__main__':
    unittest.main()

## Boas Práticas

- Use esperas explícitas para garantir que os elementos estejam presentes antes de interagir com eles.
- Mantenha seu código organizado e modular.
- Capture logs e screenshots para facilitar a depuração.

## Projetos Avançados

- Automação de testes de regressão.
- Web scraping avançado.
- Integração com frameworks de testes como pytest.

## Contribuição

Sinta-se à vontade para contribuir com este repositório enviando pull requests ou abrindo issues.

## Licença

Este projeto está licenciado sob a licença MIT - veja o arquivo LICENSE para mais detalhes.
