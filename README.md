# itv_experiments
Experimentos na pista de motocross







## Planejamento do experimento no ITV (Campinho)


Obter os códigos desse repositório aqui (na nuc do robô):

`git clone https://github.com/adrianomcr/itv_experiments.git`

E dar um:

`catkin build`

Não se esquecer de:

`source devel/setup.bash`

Colocar o robô virado para o Leste, na posição inicial (x, y, yaw) desejada. Usar bússola e mapa* para se orientar com o Leste. A posição que o robô for acionado será setada não como o (x, y) = (0, 0), e sim como (x, y) = (-8.9399, 3.0343), que é o ponto inicial da trajetória dada pelo Dijkstra.

* É bom utilizar um mapa para corrigir o deslocamento do campo magnético da Terra. 

Ligar o robô e checar se o bringup foi executado adequadamente.


Rodar o seguinte launch:

`roslaunch ivt_experiments experimento_itv_control.launch`

Esse launch tem dois nós:
- `pose_constructor` - vai setar o "000" do robô e gerar a pose relativa com base nos dados do GPS e da IMU
- `vec_field_itv.py` - vai esperar uma trajetória e quando recebe-la vai gerar comandos /cmd_vel para o robô

Esperar um tempo (dois segundos pelo menos). Isso serve para o código setar o 000. Esse um tempinho significa: "O código a seguir não deve ser chamado no mesmo launch dos nós acima, e sim depois."

Rodar o launch que chama o código que vai ler uma trajetória de um arquivo txt. (* Obs: Este comando deve ser executado de dentro do catkin workspace que contem o package itv_experriments Ex:/home/espeleo/catkin_ws/)

`roslaunch itv_experiments experimento_itv_traj.launch`

Dentro deste launch (acima) uma das quatro trajetórias pode ser escolhida. Pode-se também escolher a velocidade desejada para o robô.

Alternativamente ao último comando, pode-se utilizar:

`rosrun itv_experiments dijkstra_trajectories_itv.py TRAJ_TYPE`

- `TRAJ_TYPE = 1`  =>  Dijkstra Points Combined
- `TRAJ_TYPE = 2`  =>  Dijkstra Points Energy
- `TRAJ_TYPE = 3`  =>  Dijkstra Points Shortest
- `TRAJ_TYPE = 4`  =>  Dijkstra Points Transversal



## Rosbag


Para salvar todos os tópicos em bags de 30 segundos:

`rosbag record -a --split --duration=30`


Para salvar todos os tópicos em bags de 1 minuto:

`rosbag record -a --split --duration=1m`
