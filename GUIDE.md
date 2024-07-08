# INTRODUCCIÓN
Este documento es el resultado de una investigación continua sobre las herramientas de personalización del entorno de trabajo que 
cumplen unos requisitos que siguen un criterio totalmente personal. El único objetivo de este documento es el de recopilar en un único 
lugar todo el proceso de configuración de principio a fin de mi entorno de trabajo, y compartirlo con todas aquellas personas que se 
interesan por el.

# OBJETIVO
La creación de este documento pretende dar solución a los siguientes requisitos:
- Disponer de un entorno de trabajo en el que pueda hacer la mayoría de las cosas utilizando la terminal y el teclado.
- Se deben poder renderizar imágenes en la propia terminal.
- El entorno debe tener la posibilidad de dividirse en ventanas/paneles para poder realizar multiples tareas.
- Debe poder guardar las sesiones de trabajo para no empezar de cero en caso de que la terminal se cierre por accidente.
- Realizar una instalación minimalista, con lo estrictamente necesario. Por ejemplo:
    Prefiero instalar Zsh y no Oh My Zsh para instalar manualmente solamente aquellos plugins que sí utilizaré.
    Al instalar una fuente solo instalo la versión que utilizo (Regular) y no el pack completo (Regular, Bold, Bolditalic, Italic).
 

# CONFIGURACIÓN FINAL

- Distribución -> `Debian 12` (Driven by the community)
- Shell -> `Zsh` (By Paul Falstad)
- Emulador de terminal -> `Wezterm` (By [Wez Furlong](https://github.com/wez))
- Fuente -> `Hack Nerd Font` (By [Chris Simpkins](https://github.com/chrissimpkins))
- Multiplexor -> `Tmux` (Driven by the community)
- Editor-> `Neovim` (Driven by the community)

# PROCEDIMIENTO

## Instalación del shell
Me he decantado por la utilización de la shell Zsh en lugar de la que mi distribución trae por defecto (Bash) debido a que es más
configurable, y puedes personalizarla mediante la instalación y/o configuración de plugins sin necesidad de sustituir la propia shell.

En mi caso, instalaré los plugin de manera manual, aunque se podrían instalar con un gestor de plugins como es el "Oh my Zsh".

Para cambiar de la shell por defecto (Bash) a la shell Zsh, bastará con ejecutar los siguientes comandos:

```
sudo apt update
```
```
sudo apt upgrade
```
```
sudo apt install zsh
```

En el siguiente comando se ha de sustituir USUARIO por aquel del que se desee cambiar la shell.

```
chsh -s /bin/zsh USUARIO
```

>[!NOTE]
>Utiliza el siguiente comando si deseas utilizar zsh como root.

```
sudo chsh -s /bin/zsh root
```

>[!NOTE]
>Utiliza el siguiente comando si lo que deseas es cambiar la shell para todos los usuarios. Quita la opción -s. Así zsh pasará a ser la shell por defecto.

```
chsh /bin/zsh
```

En mi caso he configurado la shell Zsh para mi usuario y para root.
Tened en cuenta que una vez realizado este paso, el Prompt pasa a verse bastante feo, y es por ello que más adelante, tras instalar el 
emulador de terminal Wezterm, procederemos a instalar el plugin Powerlevel10k para que dicho Promt sea mucho más descriptivo y util.

## Instalación del emulador de terminal

En mi caso me he decantado por Wezterm, un emulador de terminal cross-platform con renderizado de GPU creado por @Wez en el lenguaje
Rust. Además a este emulador se puede complementar con scripts en el lenguaje Lua.
Hay alternativas muy populares que cumplían mis requisitos (Alakrity, Kitty...)

Esta decisión fue tomada por la necesidad de poder renderizar imágenes en la terminal, además de poder personalizar el prompt mediante
la utilización del plugin powerlevel10k para la shell zsh.

Para instalar el emulador seguiremos los siguientes pasos:

  ```
  curl -fsSL https://apt.fury.io/wez/gpg.key | sudo gpg --yes --dearmor -o /usr/share/keyrings/wezterm-fury.gpg
  ```
  ```
  echo 'deb [signed-by=/usr/share/keyrings/wezterm-fury.gpg] https://apt.fury.io/wez/ * *' | sudo tee /etc/apt/sources.list.d/wezterm.list`
  ```
  ```
  sudo apt update
  ```
  ```
  sudo apt install wezterm`
  ```

Hemos de tener en cuenta que al instalar el emulador Wezterm se instala por defecto el conjunto de fuentes de Nerd Font.

## Instalación de la fuente
En este punto debemos decidir que fuente queremos. En mi caso la fuente que más me gusta es "Hack Nerd Font", aunque "Fira Code" me parece muy buena para desarrollo.

Prefiero "Hack Nerd Font" porque no es tan sofisticada en las letras "g" o "r", lo cual agradezco para administración de sistemas y redes. Y en cuanto a las ligaduras, tampoco soy un fanático de las mismas, ya que en realidad me es igual usarlas o no, y si me apuras te diría que prefiero no usarlas porque no me importa tanto la estética. Y prefiero ver claro que símbolos se están usando en los scripts y regex.

Para instalar la fuente elegida seguimos los siguientes pasos:
- Elegimos la fuente a utilizzar en la web Nerd Fonts.
- Previsualizamos la fuente a utilizar en la web [Programming Fonts](https://www.programmingfonts.org/#hack) para asegurarnos.
- Vamos al repositorio de Nerd Fonts (https://github.com/ryanoasis/nerd-fonts)
- Clicamos en "Hack Nerd Fonts" para que nos lleve al repositorio de la fuente [Hack Nerd Font](https://github.com/ryanoasis/nerd-fonts/tree/master/patched-fonts/Hack)
  Aunque el repositorio de la fuente [Hack](https://github.com/source-foundry/Hack) es el original creado por [Chris Simpkins](https://github.com/chrissimpkins).
- Seguidamente clicamos en estilo de fuente que más nos guste, en mi caso Regular.
- Lo siguiente que haremos será clicar en el tipo de Regular que queremos, en mi caso la [Regular](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/Hack/Regular/HackNerdFont-Regular.ttf)
- Una vez situados en dicha página podemos clicar en los 3 punto y descarga o utilizar el atajo ```Ctrl+Shift+S```.
- Seleccionamos la carpeta Downloads.
- Creamos una carpeta nueva en ~/.local/share llamada "fonts" con el comando:

  ```
  mkdir ~/.local/share/fonts
  ```

- Movemos el fichero descargado con formato `.ttf` a dicha carpeta con el comando:

  ```
  mv ~/Downloads/HackNerdFonts-Regular.ttf ~/.local/share/fonts
  ```

- Añadimos la fuente al fichero de configuración del emulador `~/.wezterm.lua` mediante el siguiente código:

  ```
  config.font = wezterm.font 'Hack Nerd Font'
  ```

## Instalación del Multiplexor
A pesar de que el propio emulador de terminal Wezterm posee una función de multiplexación de ventanas mediante una característica conocida como `Dominios`, considero que no es tan buena como las `Sesiones` del multiplexor Tmux, ya que estas últimas permiten desacoplar `detatch`o acoplar `attatch` la sesión, pudiendo cerrar por completo la terminal y al abrirla de nuevo, se puede recuperar la sesión de trabajo. Además se pueden tener varias sesiones al mismo tiempo, lo cual ofrece una versatilidad enorme a la hora de trabajar.

Para la instalación de Tmux seguiremos los siguientes pasos:
- Primero instalamos las bibliotecas necesarias para que Tmux funcione correctamente mediante los siguientes comandos: 

  ```
  sudo apt install -y build-essential bison pkg-config libevent-dev libncurses-dev
  ```

- Seguidamente procederemos a instalar Tmux utilizando los siguientes comandos: 

  ```
   sudo git clone https://github.com/tmux/tmux.git
  ```
  ```
    cd tmux
  ```
  ```
    sudo sh autogen.sh
  ```
  ```
    sudo ./configure
  ```
  ```
    sudo make && sudo make install
  ```
  

## Instalación del editor de texto.
Como editor de texto he decidido utilizar Neovim debido a las posibilidades que ofrece a la hora de configurarlo. Siendo posible utilizar el lenguaje Lua para añadir funcionalidades a tu gusto.

Entre las opciones de instalación prefiero la [instalación desde la fuente](https://github.com/neovim/neovim/blob/master/BUILD.md), es decir, el repositorio de [Neovim](https://github.com/neovim/neovim/tree/master) en GitHub

He de decir que me gusta instalar la versión estable `stable` por lo que es importante cambiar a dicha rama antes de proceder con la instalación.

Para instalarlo simplemente seguiremos los pasos documentados en el repositorio oficial.
