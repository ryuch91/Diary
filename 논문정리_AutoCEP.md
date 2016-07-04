## 160630
- Title: 
Doctoral Symposium: Automatic Learning of Predictive Rules for Complex Event Processing 

- Author:
Raef Mousheimish, Yehia Taher, Karine Zeitouni

- Abstract:
  shapelet 이라는 early classification on time series 방식의 data mining 기법을 적용해서,
historical data로부터 shapelet을 얻어내고, 이를 CEP engine 의 rule 에 자동으로 추가해주는 시스템 설계
  
  독특한 점은 data mining 쪽의 연구에서는 shapelet 분야가 최근의 연구라서, 이 다수의 dimension (source)로 부터 multrivariate shapelet extraction을 sequence constraint나 time window 관련하여 하는 연구가 거의 없어서 직접 Multidimensional Shapelet Learning 기법을 제안했다는 것(직접 구현 및 실현하지는 않았다)

  사용된 기술들은 sequence mining technique으로 'enumeration tree', 관계 있는 shapelet 만 사용하기 위해 사용된 'sub-tree pruning mechanism'

- Critics:
  shaplet 을 이용한 방법은 빠른 초반 룰 생성에는 좋지만, 이후에 더 데이터(historical)가 쌓이면 룰에 대한 정확도와 신뢰도를 높이기 위해서, 다른 learing technique을 추가로 사용해주는게 좋지 않을까?
  
  multivarate shapelet에 대해서는 어떤 결과도 없음. 제시일 뿐.(univariate에 대해서는 실제 코드를 올려놓음 : https://goo.gl/JtZctT )

- Quotes:
```
Every happening in the real world could be represented as an event [8] 
```
``[8] : D.Luckham and R.Schulte. Event Processing glossary-version 1.1. Event Processing Technical Society, 2, 2008``
```
As pointed out by some researched in the domain [4,3], exploiting the high performance of CEP for predictive purposes will be extremely beneficial in different real-life applications, and going from reactive towards proactive event-driven systems would be a major technological advancement that the CEP could achieve.
```
``[5] : M.F.Ghalwash et al., Early classification of multivariate temporal observations by extraction of interpretable shapelets. BMC bioinformatics, 13(1):1, 2012 `` 
``[4] : L.J.Fulop et al., Predictive complex event processing: a conceptual framework for combining complex event processing and predictive analytics. 2012
``
```
However, and until this day, it remains considerably difficult to integrate CEP in predictive contexts, and its main usage is still the detection, not the prediction of situations.
```
``` 
It remains a challenging and tedious task for humans to manually write rules that can predict these situations
```
```
Few and recent efforts that tackled the problem of automatic rule generation are discussed in [9,10,11,13,12]. However, they either make the unrealistic assumption of having one and only one rule that could lead to a specific situation [9,10], or they are very user-centric and can not learn complete rules [11,13,12]. Furthermore, one of the major drawbacks is that they cannot handle periodic events
```
``
[9] : A.Margara et al., Towards automated rule learning for complex event processing. Technical report, 2013.
``
``
[10] : A.Margara et al., Learning from the past: automated rule generation for complex event processing . DEBS 2014, p.47-58.
``
``
[11] : C.Mutshler. Learning event detection rules with noise hidden markov models. In AHS, 2012
``
``
[12] : S. Sen. An approach for iterative event pattern recommendation. DEBS 2010
``
``
[13] : Y.Turchin. Tuning complex event processing rules using the prediction-correlation paradigm. DEBS 2009. 
``