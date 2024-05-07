### Português:

# Instalação do Micro XRCE-DDS Agent

O Micro XRCE-DDS Agent pode ser instalado no computador auxiliar usando um pacote binário, construído e instalado a partir do código-fonte ou construído e executado de dentro de um espaço de trabalho ROS 2. Todos esses métodos buscam todas as dependências necessárias para se comunicar com o cliente (como o FastCDR).

## Instalação Autônoma a Partir do Código-Fonte
No Ubuntu, você pode construir a partir do código-fonte e instalar o Agente autonomamente usando os seguintes comandos:

```
git clone https://github.com/eProsima/Micro-XRCE-DDS-Agent.git
cd Micro-XRCE-DDS-Agent
mkdir build
cd build
cmake ..
make
sudo make install
sudo ldconfig /usr/local/lib/
```
Para iniciar o agente com configurações para se conectar ao cliente uXRCE-DDS em execução no simulador:

```
MicroXRCEAgent udp4 -p 8888
```

## Construir/Executar dentro de um Espaço de Trabalho ROS 2
O agente pode ser construído e lançado dentro de um espaço de trabalho ROS 2 (ou construído autonomamente e lançado a partir de um espaço de trabalho). Você deve ter instalado o ROS 2 seguindo as instruções no Guia do Usuário ROS 2.

Para construir o agente dentro do ROS:

Crie um diretório de espaço de trabalho para o agente:

```
mkdir -p ~/px4_ros_uxrce_dds_ws/src
```
Clone o código-fonte do Micro-XRCE-DDS-Agent da eProsima para o diretório /src (o ramo principal é clonado por padrão):

```
cd ~/px4_ros_uxrce_dds_ws/src
git clone https://github.com/eProsima/Micro-XRCE-DDS-Agent.git
```
Configure o ambiente de desenvolvimento ROS 2 e compile o espaço de trabalho usando colcon:

```
source /opt/ros/humble/setup.bash
colcon build
```

Isso compila todas as pastas sob /src usando a cadeia de ferramentas fornecida.

Para executar o agente Micro XRCE-DDS no espaço de trabalho:

Configure o local_setup.bash para disponibilizar os executáveis no terminal (também setup.bash se estiver usando um novo terminal).

```
source /opt/ros/humble/setup.bash
source install/local_setup.bash
```
Inicie o agente com configurações para se conectar ao cliente uXRCE-DDS em execução no simulador:

```
MicroXRCEAgent udp4 -p 8888
```

## Iniciando Agente e Cliente
### Iniciando o Agente
O agente é usado para se conectar ao cliente por meio de um canal específico, como UDP ou uma conexão serial. As configurações do canal são especificadas quando o agente é iniciado, usando opções de linha de comando. Estas são documentadas no guia do usuário da eProsima: Micro XRCE-DDS Agent > Agent CLI. Note que o agente suporta muitas opções de canal, mas o PX4 suporta apenas conexões UDP e serial.

Por exemplo, o simulador PX4 executa o cliente uXRCE-DDS sobre UDP na porta 8888, então para se conectar ao simulador você iniciaria o agente com o comando:

```
MicroXRCEAgent udp4 -p 8888
```
Ao trabalhar com hardware real, a configuração depende do hardware, sistema operacional e canal. Por exemplo, se estiver usando a porta serial UART0 do RasPi, você pode se conectar usando este comando (com base nas informações em Documentação do Raspberry Pi > Configurando UARTS):

```
sudo MicroXRCEAgent serial --dev /dev/AMA0 -b 921600
```
Para mais informações, consulte a Documentação de Middleware do PX4 https://docs.px4.io/main/en/middleware/uxrce_dds.html.

***

### English:
# Micro XRCE-DDS Agent Installation
The Micro XRCE-DDS Agent can be installed on the companion computer using a binary package, built and installed from source, or built and run from within a ROS 2 workspace. All of these methods fetch all the dependencies needed to communicate with the client (such as FastCDR).

## Install Standalone from Source
On Ubuntu, you can build from source and install the Agent standalone using the following commands:

```
git clone https://github.com/eProsima/Micro-XRCE-DDS-Agent.git
cd Micro-XRCE-DDS-Agent
mkdir build
cd build
cmake ..
make
sudo make install
sudo ldconfig /usr/local/lib/
```
To start the agent with settings for connecting to the uXRCE-DDS client running on the simulator:

```
MicroXRCEAgent udp4 -p 8888
```
## Build/Run within ROS 2 Workspace
The agent can be built and launched within a ROS 2 workspace (or built standalone and launched from a workspace). You must already have installed ROS 2 following the instructions in the ROS 2 User Guide.

To build the agent within ROS:

Create a workspace directory for the agent:

```
mkdir -p ~/px4_ros_uxrce_dds_ws/src
```
Clone the source code for the eProsima Micro-XRCE-DDS-Agent to the /src directory (the main branch is cloned by default):

```
cd ~/px4_ros_uxrce_dds_ws/src
git clone https://github.com/eProsima/Micro-XRCE-DDS-Agent.git
```
Source the ROS 2 development environment, and compile the workspace using colcon:

```
source /opt/ros/humble/setup.bash
colcon build
```
This builds all the folders under /src using the sourced toolchain.

To run the Micro XRCE-DDS agent in the workspace:

Source the local_setup.bash to make the executables available in the terminal (also setup.bash if using a new terminal).
```
source /opt/ros/humble/setup.bash
source install/local_setup.bash
```
Start the agent with settings for connecting to the uXRCE-DDS client running on the simulator:

```
MicroXRCEAgent udp4 -p 8888
```
## Starting Agent and Client
### Starting the Agent
The agent is used to connect to the client over a particular channel, such as UDP or a serial connection. The channel settings are specified when the agent is started, using command line options. These are documented in the eProsima user guide: Micro XRCE-DDS Agent > Agent CLI. Note that the agent supports many channel options, but PX4 only supports UDP and serial connections.

For example, the PX4 simulator runs the uXRCE-DDS client over UDP on port 8888, so to connect to the simulator you would start the agent with the command:

```
MicroXRCEAgent udp4 -p 8888
```
When working with real hardware, the setup depends on the hardware, OS, and channel. For example, if you're using the RasPi UART0 serial port, you might connect using this command (based on the information in Raspberry Pi Documentation > Configuring UARTS):

```
sudo MicroXRCEAgent serial --dev /dev/AMA0 -b 921600
```
For more information, consult PX4 Middleware Documentation https://docs.px4.io/main/en/middleware/uxrce_dds.html.

