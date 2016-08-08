## 160804
* ==Title==: 
Tutorial: Event Processing Under Uncertainty (2012)

* ==Author== :
Alexander Artikis ,Opher Etzion , Zohar Feldman , Fabiana Fournier

* ==Intro== :  
 빅데이터는 가트너 2012에서 트렌드 테크놀로지로 뽑힘. 빅 데이터는 다음 네가지의 특성을 가진다.
  1. Volume (data at rest)
  2. Velocity (data in motion)
  3. Variety (data in many forms)
  4. Veracity (data in doubt : uncertainty in the data)
  
 또한 빅데이터의 발전을 이끄는 원동력으로 다음의 것들이 있다.
  1. IoT와 같은 기술로 인한 계측화 (데이터의 발생)
  2. 저렴한 저장장치
  3. 센싱 기술의 삶의로의 스며듦 (e.g. 스마트폰)
  4. broadband connectivity (e.g. networked sensor nodes)
  5. 비즈니스 전략으로의 소셜 네트워크 사용 등

 이런 다양한 데이터 인풋을 저장하고 실시간으로 인지할 필요가 있음은 당연했고, 이는 recognition system that detect situations or events of special significance 를 통해 해결되었다. 하지만 대부분의 EPS(이벤트 처리 시스템)는 reasoning algorithm 의 efficiency에만 신경을 쓰고 있다. However, these don't take into account the various types of uncertainty that exist in most applications.센서나 소셜 미디어로부터의 데이터는 고유의 불확실성(uncertainty)을 가지고 있다.많은 현재의(state-of-the-art) 시스템들에서는 데이터가 정확하다고 가정하거나, 혹은 처리전에 cleanse 과정을 거친다고 가정한다. 하지만 이는 시간적 제한으로 인해 불가능하다. 
 
 이 논문에서는 common types of uncertainty in event processing 을 소개하고, 이를 다루는 방법에 대해 소개한다. (특히 AI 관련하여 연구가 많이 되고 있다 : AI-based event processing system that support probabilistic reasoning)

* ==Background== :
 1. Event Processing Constructs
  [15]에서의 Event Processing Language 기반으로 작성되었다. 이에 대해 간략히 소개한다.
   * **Event Type** : a specification for a set of event objects that have the same semantic intent and the same structure.<br/>모든 event object 는 event type 의 instance로 간주된다. event type은 producer로 부터 직접 발생한 raw event 를 나타낼수도 있고, Event Processing Agent 로부터 derived 된 derived event를 나타낼 수도 있다. 또한, 이벤트는 simple event 일 수도 있고, composite event 일 수도 있다. 
   * **EPA** : 주어진 input event 에 대해서, 특정 logic을 적용하여 a set of output (derived) event를 만들어낸다. 
   * **Context** : a named specification of conditions that groups event instances. 몇가지 context dimension이 존재하지만, 여기서는 자주 사용되는 두 가지를 사용한다(temporal / segmentation-oriented) temporal context는 하나 이상의 time interval을 가질 수 있다. 각 time interval 은 context partition 에 대응되고, interval 안에서 발생한 event를 포함한다. segmentation-oriented context는 attribute 나 attribute의 묶음으로 구분하기 위해서 사용한다. (각 유저가 id를 가진 이벤트 스트림의 이벤트를 생각해보면 된다. 이 경우 segentation-oriented context를 통해서 유저별로 tracking이 가능해진다.)
   * **EPN(Event Processing Network)**
   ![Event Processing Network](./EPN.jpg)

 2. Event Processing Agents
 다양한 타입의 agent들이 있지만, 몇 가지만 소개한다.(섹션 3을 설명하기에 충분한 정도만)
   1. Filter agent: excludes unwanted event instances (so, does not transform input event)
   2. Split agent: single event를 받아서 collection of events 를 만들어냄.(복제할 수도 있고, 또는 subset 일 수도 있고..)
   3. Pattern matching: all, sequence, threshold, absence, any, count, top-k, 등등이 있을 수 있다. Pattern policies 라는 걸 이용해서 fine-tune 할 수 있다. Pattern filter(stateless)와 Pattern assertion(stateful)??

* ==Scenario(Illustrative example)== :
 Visual surveillance system에서의 crime detection
 목적(goal) : to detect and alert in real-time possible occurrences of crimes
 ![Event types](./EventType.jpg)
 ![crime event processing network](./fig2.jpg)
 ![Event processing agent types](./table2.jpg)
 어떤 사람이 잠재적 범죄장소에 하루에 다섯번 이상 나타나면 crime으로 간주한다. 또한 3일 이내에 범죄 의심이 10건 이상 일어나는 장소를 범죄 위험 지역으로 지정하여 알린다.(한달 단위로 가장 의심되는 지역 top3) 그리고 시민의 제보와의 매칭도 확인한다. 

* ==Uncertainty types== :
 EPS 에서는 다음의 다양한 종류의 uncertainty를 다루어야 한다.
 1. Incomplete event streams (e.g. 이미지 프로세싱 시스템에서의 human activity detecting 실패)
 2. Insufficient event dictionary (e.g. 이미지 프로세싱 시스템이 범죄에 해당하는 모든 종류의 activity를 인지하지는 못하기 때문에)
 3. Erroneous event recognition (e.g. 시민으로부터의 제보 시간이 정확하지 않을 수 있다)
 4. Inconsistent event annotation (패턴 인식에서 composite event 를 위한 pattern 을 정의할 때, domain expert 에 의해서 manual하게 이루어지거나 머신러닝 기술을 이용할 수 밖에 없는데, 대부분의 경우 일관성이 없을 수 있다.)
 5. Imprecise event patterns (e.g. it may not be possible to precisely identify all conditions in which a crime of a particular type is said to take place.)

 간단하게 정리해보면
 1. Uncertainty in the event input
 2. (certainty in the event input and) uncertainty in the composite event pattern
 3. uncertainty in both input and pattern

<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>



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