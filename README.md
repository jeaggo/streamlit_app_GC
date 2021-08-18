Ejemplo para ejecutar una aplicación de streamlit a través de Google Colaboratory (GC)

Paso 1 - Estando en tu Google Colaboratory, lo primero que tenemos que hacer es instalar streamlit
# !pip install streamlit
Nota: Cuando lo instales es posible que al final te salga un mensaje de advertencia, si es así, es necesario reiniciar el GC y volver a instalar streamlit

Paso 2 - Ahora vamos a cargar una máquina virtual que tenga instalado Ngrok, para lo cual hay que ejecutar la siguiente instrucción
# !wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip

Paso 3 - Una vez que obtenemos la máquina virtual con linux y ngrok, el siguiente paso es cargar esta máquina virtual en nuestro archivo de GC
# !unzip ngrok-stable-linux-amd64.zip

Paso 4 - Posteriormente le indicaremos a Ngrok que estará utilizando el puerto 8501 para visualizar nuestra aplicación y esta instrucción nos ayudará a inicializar el puerto 8501
# get_ipython().system_raw('./ngrok http 8501 &')

Paso 5 - Una vez inicializado el puerto, ahora vamos a crear un tunel para que pueda generarse un enlace que nos permita visualizar nuestra aplicación
# !curl -s http://localhost:4040/api/tunnels | python3 -c \
#    'import sys, json; print("Execute the next cell and the go to the following URL: " +json.load(sys.stdin)["tunnels"][0]["public_url"])'
Nota: Una vez que ejecutaron la instrucción anterior, verán que aparece un URL que es el que vamos a dar clic para visualizar nuestra aplicación, pero primero tenemos que ejecutar nuestra aplicación

Paso 6 - El siguiente paso, es copiar en una celda el archivo .py que contiene el código de nuestra aplicación y en la primera línea, hay que poner la siguiente instrucción
# %%writefile app.py
Nota: Esta instrucción hará que nuestro código se cargue como un archivo denominado app.py en nuestro GC. Puedes probar copiando el código que está en este git

Paso 7 - Una vez cargado el archivo ahora vamos a proceder a ejecutarlo con el comando streamlit para que se visualice el contenido del mismo, para esto en una nueva celda, hay que colocar la siguiente instrucción
# !streamlit run /content/app.py

Nota: Aunque te aparezcan los direcciones de internet (url), recuerda que para poder visualizar tu aplicación, es necesario dar click en el enlace (url) que te apareció en la celda en donde activamos el tunel de Ngrok
