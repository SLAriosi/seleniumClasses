# Aula 07 - Eventos 💫

## 🔄 Change / onChange

O evento de mudança (`change`) é desencadeado quando um elemento perde o foco (`blur`). O elemento será analisado e, caso alguma mudança tenha ocorrido durante o período de foco, o evento será disparado.

**Exemplo:** Você clica no botão de input de algum formulário, ele entra em foco, você pode digitar e fazer o que quiser lá. Na hora que você clicar fora dele, o evento `change` verificará essa alteração e será disparado (caso tenha alguma alteração no input).

## Eventos + Selenium <img src="https://github.com/SLAriosi/svgTools/blob/main/Selenium.png" width="30" height="30" />

### Observando os eventos

A biblioteca do Selenium conta com um mecanismo para observar eventos: um `EventListener` (Escutador de eventos). A implementação dele é baseada em um padrão de projeto chamado **Template Method**.

A ideia principal é fazer uma ação "antes" e/ou "depois" de alguma determinada ação do WebDriver.

"Antes" e "Depois" geralmente são conhecidos como **Hooks**. Vamos usar o método `click` como exemplo.

```plaintext
|  Estado anterior ao |                                     | Estado posterior ao |                                      
|        click        |                                     |        click        |  
+---------------------+       +---------------------+       +---------------------+
|                     |       |                     |       |                     |
|         WE          |  <--> |        Click        |  <--> |          WE         |
|                     |       |                     |       |                     |
+---------------------+       +---------------------+       +---------------------+
```

## EventListener 📢

O objetivo do **EventListener** é observar o estado do WD em todos os momentos. Antes e depois de uma ação ser executada;

**Por exemplo:** Todas as vezes em que o **click** for chamado podemos observar o estado do dom, de um único elemento, fazer logs, etc...

| WE   |    <-    CLICK     ->  | WE                           |
| :---------- | :--------- | :---------------------------------- |
| `.before_click()` | `.click()` | `.after_click()` |

```python
from selenium.webdriver import Chrome
from.selenium.webdriver.support.events import (
    AbstractEventListener, EventFiringWebDriver()
  )

class Escuta(AbstractEventListener):
  def after_navigate_to(self, url, webdriver):
    print(url)

  def after_navigate_back(self, url, webdriver):
    print('voltando')

  def before_click(self, elemento, driver):
    print(
      f'Tag {elemento.tag_name}: Texto: {elemento.text}: Antes de clicar'
    )

  def after_click(self, elemento, driver):
    print(
      f'Tag {elemento.tag_name}: Texto: {elemento.text}: Depois de clicar'
    )

browser = Chrome()

rapi_10_browser = EventFiringWebDriver(browser, Escuta())

browser.get('https://selenium.dunossauro.live/aula_07_d')
input_de_texto = rapi_10_browser.find_element_by_tag_name('input')
span = rapi_10_browser.find_element_by_tag_name('span')
p = rapi_10_browser.find_element_by_tag_name('p')

input_de_texto.click()
print('Tô clicãnû')

browser.quit()
```

## Event Firing 🔥
O disparador de eventos é uma "burocracia" do selenium para usar um Listener.

Ele constrói um *wrapper** do webdriver e dispara os eventos para o Listener. 



* (wrapper = envólucro, uma caixa, onde fica quardado o webdriver para disparar os eventos que aconteceram para o Listener).
