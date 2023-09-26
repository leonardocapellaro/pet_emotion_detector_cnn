# pet_emotion_detector_cnn

Classificador de emoções de pets utilizando redes neurais convolucionais. 

## Preparação dos dados
### Base de dados
Para o treinamento do classificador, a base [Dog Emotions Prediction](https://www.kaggle.com/datasets/devzohaib/dog-emotions-prediction?resource=download)
foi utilizada como ponto de partida.
Como primeiro passo, a face de cada animal foi recortada utilizando a biblioteca dlib com um [modelo](https://github.com/kairess/dog_face_detector)
treinado para reconhecer faces de animais disponibilizado por @kairess. Feito isso, foi
realizada uma curadoria manual nas classes, excluindo imagens ruidosas e remanejando imagens que
estavam em classes incorretas.

### Data augmentation
Foi realizado um data augmentation nos dados de treinamento de 10 para 1, ou seja, para cada imagem foram geradas outras 10
derivadas utilizando a biblioteca ImageDataGenerator. Cada imagem foi redimensionada para ter 250x250 de tamanho.

## Treinamento do Modelo
Foram utilizados dois modelos principais, o Densenet121 e o Densenet201. Para cada um deles foram utilizadas as seguintes técnicas:

- EarlyStopping: Baseado na acurácia de validação, foi configurada uma paciência de 15 épocas para o modelo parar caso não tenha ocorrido nenhuma evolução nessa métrica.
- As camadas base dos Dense foram congeladas para evitar retreino.
- Foram utilizadas a camada base, uma flatten, uma camada densa com 512 neurônios, um dropout de 50% para esta camada e uma camada de saída com 4 neurônios, um para cada classe.
- Foi utilizado um decaimento de learning rate por época, iniciando em 1e-3 e terminando em 1e-5.

## Aplicação do modelo
Dada uma imagem a ser classificada em formato aceito pelo image do keras, o código para classificação faz uma busca por animais, recorta o rosto e aplica no modelo treinando anteriormente,
classificando o humor do animal em "angry", "happy", "sad" ou "realxed".
