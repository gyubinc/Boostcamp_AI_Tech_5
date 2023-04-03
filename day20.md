# 4) LSTM, GRU
---

## Long Shor-Term Memory(LSTM)

Core idea: pass cell state information straightly without any transformation

매 time step마다 변화하는 h를 short term memory cell state 를 Long memory로 표현

$h_t = f_w(x_t, h_{t-1})$

${C_t, h_t} = LSTM(x_t, C_{t-1}, h_{t-1})$

cell state = 정보를 담고있는 벡터

hidden state = cell state vector를 가공을 통해 노출할 정보만을 담은 벡터

i: input gate, wheter to write to cell

f: Forget gate, Whether to erase cell

o: Output gate, How much to reveal cell

g: Gate gate, How much to write to cell

x의 dimension h x 1, h의 dimension h x 1, weight의 dimension을 4h x 2h로 가정하면 w * (x,g)를 해서 나온 4h x 1차원의 벡터의 h x 1 네 부분을 각각 (sigmoid, sigmoid, sigmoid, tanh)를 통과시켜 나온 벡터가 바로 (i, f, o, g)임

sigmoid 함수를 거친 i, f, o는 0~1 사이의 값으로 어떤 값과 element-wise product가 이루어졌을때 해당 값을 몇 % 저장할 것인가와 같은 의미를 가지고

tanh함수의 경우 vanila rnn에서 선형결합 후 tanh를 이용해 hidden state를 -1~1사이로 담았던 것과 같은 유의미한 정보를 표현

## Forget gate

$f_t = \sigma(W_f*[h_{t-1}, x_t] + b) $

* 위의 f: forget gate

만약 이전의 Cell state의 값이 [3, 5, -2] 였고

ft의 값이 [0.7, 0.4, 0.8]로 계산되었다면

Cell state를 [2.1, 2.0, -1.6]으로 업데이트됨

* 각각 30% 60% 20%의 정보를 forget했다

## Input gate & Gate gate

Generate information to be added and cut it by input gate

$i_t = \sigma(W_i*[h_{t-1}, x_t] + b_i)$

* Input gate

$\widetilde{C_t}$ = tanh(Wc * [ht-1, xt] + bc)

* Output gate

Generate new cell state by adding current information to previous cell state

$C_t = f_t*C_{t-1} + i_t*\widetilde{C_t}$

* Forget gate를 통과한 $f_t*C_{t-1}$에 더해주는 과정

## Gate gate를 바로 더하지 않고 Input gate를 곱하는 이유

한 번에 더해주고자 하는 값을 구하는 것이 어려워 조금 더 큰 Gate gate를 생성한 후 Input gate를 곱해줘서 정보를 덜어내는 형태로 2단계를 만든다

## Output gate

$o_t = \sigma(W_o[h_{t-1}, x_t] + b_0)$

$h_t = o_t * tanh(C_t)$

앞서 계산한 Cell state에 tanh를 적용해서 -1 ~ 1 사이의 벡터로 변경하고 output gate를 곱해 filtering한 후 hidden state를 만들어낸다

## Cell state와 hidden state의 역할

만약 "I go 라는 단어들이 주어지고 home" 라고 예측해야 한다면, 

hidden state의 역할은 바로 다음 단어인 home을 예측하는 것이고 Cell state는 "를 닫아야 한다는 정보를 담고 있다고 볼 수 있다.

결국 Cell state는 나중에 필요하지만 현재는 필요하지 않은 정보를 저장하고 있다고 볼 수 있다.

## Gated Recurrent Unit(GRU)

LSTM에 비해 적은 메모리 요구량, 빠른 계산 시간

Cell state와 hidden state 를 통합해 하나의 hidden state를 만들어서 사용하면서 용도는 Cell state와 유사하게 사용

$z_t = \sigma(W_z*[h_{t-1}, x_t])$

$\gamma_t = \sigma(W_r*[h_{t-1}, x_t])$

$\widetilde{h_t} = tanh(W*[\gamma*h_{t-1}, x_t])$

**LSTM**

$C_t = f_t*C_{t-1} + i_t*\widetilde{C_t}$

**GRU**

$h_t = (1 - z_t)*h_{t-1} + z_t*\widetilde{h_t}$

LSTM의 it를 zt로 사용하며 ft를 1-zt의 가중평균 형태로 표현해서 일원화

## Backpropagation in LSTM,GRU

Uninterrupted gradient flow

* Whh를 계속 곱하는 것이 아니고 항상 변하는 forget gate를 곱하고 덧셈을 통해 정보를 만들어주기 때문에 gradient vanishing 해결

* 멀리 있는 time step까지 long term dependency 문제 해결

## Summary on RNN/LSTM/GRU

1. RNNs allow a lot of flexibility in architecture design

2. Vanila RNNs are simple but don't work very well

3. Backward flow of gradients in RNN can explode or vanish

4. Common to use LSTM or GRU: their additive interactions improve gradient flow