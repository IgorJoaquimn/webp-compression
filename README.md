# webp-compression
O objetivo deste trabalho é comprimir uma imagem passada como entrada. O método desenvolvido pode ser com ou sem perdas [reference](https://developers.google.com/speed/webp/docs/compression)

## Definição do Pipeline de Compressão

O pipeline de compressão no formato WebP segue uma série de etapas projetadas para reduzir eficientemente o tamanho dos dados da imagem.
1. Primeiramente, a imagem é dividida em blocos menores chamados macroblocos, que são mais fáceis de processar individualmente.
2. Em seguida, a compressão preditiva é aplicada, onde os valores dos pixels são preditos com base nos valores dos pixels vizinhos, resultando em predições de pixels.
3. A diferença entre os valores reais dos pixels e os valores preditos é calculada, gerando os resíduos (residuals).
4. Esses resíduos são então submetidos à codificação por transformada (transform coding) utilizando a Transformada Cosseno Discreta (DCT), que converte os dados de espaço de imagem para espaço de frequência, concentrando a maior parte da informação útil em poucos coeficientes.
5. Posteriormente, esses coeficientes são quantizados, reduzindo a precisão de alguns deles para permitir uma compressão mais eficiente.
6. Finalmente, os coeficientes quantizados são codificados utilizando a codificação entrópica aritmética (Arithmetic entropy encoding), que reduz ainda mais o tamanho dos dados ao eliminar redundâncias estatísticas.

## Uso

No contexto do encoding preditivo, as imagens preditas são geradas usando algoritmos que tentam prever um bloco de pixels com base em pixels vizinhos. As predições podem ser feitas de várias maneiras, como predição horizontal (H_PRED), predição vertical (V_PRED), predição de média (DC_PRED), predição de média temporal (TM_PRED), entre outras. Cada uma dessas técnicas de predição tenta estimar os valores dos pixels com base em padrões específicos na imagem.
![image](https://github.com/IgorJoaquimn/webp-compression/assets/92036904/29ce07fa-0c2f-4365-8568-baff2cfeba58)

O histograma das variações dos macroblocos nos fornece informações sobre a distribuição dos detalhes na imagem. Com base nessa distribuição, podemos selecionar thresholds apropriados para a quantização. Esses thresholds determinam a quantidade de detalhes que serão preservados ou descartados durante a compressão da imagem.

## Compressão

Este algoritmo de compressão segue o pipeline mencionado acima, realizando as seguintes etapas:

1. Predição dos pixels utilizando algoritmos de predição preditiva como H_PRED, V_PRED, DC_PRED, TM_PRED.
2. Cálculo dos resíduos (diferenças entre os valores reais dos pixels e os valores preditos).
3. Aplicação da transformada DCT (Discrete Cosine Transform) aos resíduos.
4. Quantização dos coeficientes da transformada DCT.
5. Codificação dos coeficientes quantizados usando codificação de entropia aritmética.

O tamanho do arquivo residual é determinado pelo número de bits necessários para representar os coeficientes quantizados. A taxa de compressão (sem considerar o cabeçalho) é calculada dividindo o número de bits originais pelo número de bits residuais.

## Decompressão

A decompressão segue o processo inverso da compressão. Os coeficientes quantizados são desquantizados, e a transformada inversa DCT é aplicada para recuperar os resíduos. Em seguida, as predições de pixel são adicionadas aos resíduos para reconstruir a imagem comprimida.

Finalmente, é realizada uma comparação entre a imagem original e a imagem decomprimida para avaliar a qualidade da compressão.
![image](https://github.com/IgorJoaquimn/webp-compression/assets/92036904/e9e83043-65c3-41e7-8369-82330554111a)


## Como Executar

Para executar o código, é necessário ter Python instalado no ambiente. É recomendado utilizar um ambiente virtual para instalar as dependências e evitar conflitos com outras bibliotecas do sistema.

Execute o notebook TP ICV.ipynb para comprimir uma imagem específica. Certifique-se de instalar todas as bibliotecas necessárias listadas no início do notebook antes de executar o código.

