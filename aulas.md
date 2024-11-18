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

# Aula 08 - Eventos pt.2 👾

## 🎬 Roteiro

* Eventos
    * Teclado
    * Mouse
    * Drag
* ActionChains

### Teclado - Keyboard Events;

Existem 3* tipos de eventos disparados por teclado

* keyup
* keydown
* accesskey

![Frame 14](https://github.com/user-attachments/assets/115d063f-a5d4-4166-ae8e-aa99322b861b)

E também temos vários atributos, dos quais vou destacar 3 que considero mais importantes
* key(Valor da tecla)

* Atributos de teclas
    * shiftKey
    * altKey
    * metaKey
    * ctrlKey
 
* getModifierState()
    * CapsLock
    * shift
    * meta
    * os

Eventos, em grande maioria, dependem de interações do usuário. Nós podemos interagir com o browser de várias maneiras:

* Mouse
* Teclado
* Touch*

![image](https://github.com/user-attachments/assets/41fcd081-cdd5-48a1-9d69-b1c1e5ee9f9e)
![image](https://github.com/user-attachments/assets/0b4365cf-2716-471d-877d-d7b4cd409fd7)

## Action Chains - Low-level API 💡

### Cadeias de ações

Action Chains são maneiras de automatizar ações de baixo nível. Por exemplo, como uma tecla é pressionada ?

* key Down
* key Up

### Descrevendo ações

![image](https://github.com/user-attachments/assets/feff73a2-2b8a-4a11-a7de-479f6924f430)

![image](https://github.com/user-attachments/assets/ac61cc2d-b286-4c1c-94f8-5c8132b29494)

![image](https://github.com/user-attachments/assets/105637e8-f595-46f0-a337-05ca02ce7c4f)

![image](https://github.com/user-attachments/assets/5482d19d-a20b-4a08-bc54-6375b689ceb9)

![image](https://github.com/user-attachments/assets/db83417b-3e4e-43c8-b4e0-24d46c93d7a7)

## Eventos de Mouse 🖱️

Tipos de eventos disparados por mouse

* mouseenter
* mouseleave
* click
* dbclick
* conxtmenu

Atributos de ação

* shiftKey
* altKey
* metaKey
* ctrlKey

![image](https://github.com/user-attachments/assets/906a7f54-aca6-43e3-971c-88fd997cfeaf)

# Aula 09 - Waits ⏳

## Roteiro 🎬

* Carregamento da página
    * Normal
    * Async
    * Defer
 
* Tipos de esperas
    * Implícita
    * Explicita
 
* Wait
* By
* Locators
* Esperas personalizadas
  

