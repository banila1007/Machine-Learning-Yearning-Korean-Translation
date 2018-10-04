## 43 Artificial data synthesis

개발중인 음성인식 시스템이 마치 자동차 안에서 녹음된 오디오 클립과 같은 형태의 데이터를 더 많이 요구한다. 운전을 하면서 더 많은 데이터를 수집하는 것 대신에, 더 쉽게 데이터를 얻을 방법이 있다: 인공적으로 합성하는 것이다.

거대한 양의 자동차/길가의 노이즈 오디오 클립을 수집했다고 가정해보자. 이러한 데이터는 몇몇 웹사이트로부터 다운로드 할 수 있다. 이때, 조용한 방에서 몇몇 사람들이 이야기를 하는 오디오 데이터가 포함된 큰 사이즈의 학습 데이터셋도 가지고 있다고 가정해보자. 만약에 사람들이 이야기하는 오디오 클립을 자동차/길가의 노이즈 오디오 클립에 "추가" 할 수 있다면, 마치 그 사람들이 노이즈가 낀 자동차 소리 속에서 이야기하는 것 같은 형태의 오디오 클립을 얻을 수 있게된다. 이러한 과정을 사용해서, 거대한 데이터가 마치 자동차 안에서 녹음된것 처럼 "합성" 할 수 있게 된다.

좀 더 일반화 해보자. 인공적인 데이터 합성이 개발 데이터셋에 합리적으로 매칭되는 거대한 데이터셋을 생성해낼 수 있는 몇몇 환경이 있을 것이다. 고양이 이미지 감지 알고리즘을 두번째 예로 들어 보겠다. 개발 데이터셋에는 학습 데이터셋보다 모션 블러 (잔상)이 나타난 이미지가 많이 포함 될 수 있다. 왜냐하면, 사용자들은 사진을 촬영할때 그들의 스마트폰을 미세하게 움직이곤 하기 때문이다. 인터넷에서 모아진 학습데이터에서 잔상이 없는 이미지를 선택할 수 있고, 이 이미지들에게 시뮬레이션적으로 모션 블러 효과를 추가할 수 있을 것이다. 이렇게 개발 데이터셋에 더욱 유사한 이미지를 만들어낼 수 있게된다.

인공적인 데이터 합성은 몇몇 도전적인 과제가 될 수 있음을 알아두자: 때로는, 컴퓨터 보다는 사람이 판단하기에 더 실제같은 합성 데이터를 만들어 내는 것이 더 쉬울지도 모른다. 예를 들어서, 1,000시간 분량의 음성에 대한 학습 데이터셋이 있지만, 자동차 노이즈 소리는 1시간 분량만이 준비되어 있다고 가정해보자. 학습 데이터의 1,000시간의 음성 데이터와 자동차 노이즈 소리의 1시간을 반복적으로 사용해서, 동일한 차 노이즈 소리가 계속 반복되어 나타나는 합성된 데이터셋을 만들어내게 될 수 있다. 실제 사람이 들어 보기에, 어떤 차이를 파악해 내기가 어려울 수 있지만, 학습 알고리즘 입장에서 보면 1시간의 자동차 노이즈 소리에 대하여 "과적합"이 발생할 수도 있는 것이다. 그렇기 때문에, 다른 형태의 자동차 노이즈 소리가 녹음된, 새로운 오디오 클립에 대해서는 일반화되기 어렵다.

비슷한 예를 들어보면, 1,000시간의 자동차 노이즈 소리가 녹음되어 있지만, 이 데이터는 10개의 다른 자동차들로 부터만 녹음되는 상황이 있을 수 있다. 이러한 경우에는, 알고리즘이 이 10개의 자동차에 대해서 "과적합"될 가능성이 생긴다. 불행하게도 이러한 문제점들은 알아채기가 꽤나 힘들다.

<div style="text-align:center;">
  <img src="../img/43_1.PNG" style="text-align:center;"/>
</div>

한가지의 예를 더 들어보자. 자동차를 인식하는 컴퓨터 비젼 시스템을 만들고 있다고 가정해보자. 또한, 비디오 게임 회사와 파트너를 맺었는데, 이 회사는 여러가지 자동차 모델을 컴퓨터 그래픽화 하였다. 알고리즘을 학습시키기 위해서, 합성된 자동차 이미지를 생성하기 위한 모델을 사용할 수 있다. 비록 합성된 이미지가 매우 현실적으로 생겼다고 해도, 이러한 접근방식은 별로 잘 작동하지는 못할 것이다. 전체 비디오 게임을 통틀어서 ~20개 정도 만의 자동차 디자인을 가지고 있을지도 모른다. 자동차를 3D 모델링 하는건 매우 비싼 비용이 들기 때문이다; 만약 게임을 해본적이 있다면, 동일한 종류의 자동차를 보고 또 본다는 것을 눈치채기 힘들 수 있다. 아마도 색깔을 달리했기 때문일 것이다. 이러한 데이터는 사람에게 매우 현실적으로 보일 수 있다. 하지만, 개발/테스트 데이터셋에서 마주하게 될 가능성이 높은 실제 도로에 있는 모든 종류의 자동차들과 비교해보면, 이렇게 20개 종류로 합성된 자동차는 단지 실세계에 존재하는 자동차 분포의 극소한 부분만을 반영한다. 그렇기 때문에, 만약 100,000개의 학습 예제 데이터가 모두 이 20개의 자동차로부터 구성된 것이라면, 개발중인 시스템은 "과적합"될 것이고, 다른 종류의 자동차 디자인들을 포함하는 개발/테스트 데이터셋에 대하여 일반화 되는데 실패할 것이다.

데이터를 합성할 때, 정말로 대표할 수 있는 데이터를 합성하는 것인가에 대하여 생각해봐야 한다. 학습 알고리즘으로 하여금 합성된 것과 비-합성된 것을 구분하는 능력을 갖추게 만드는 합성된 데이터의 속성이 생기는 것을 피하도록 노력해야 한다. 모든 합성된 데이터가 20개의 자동차 디자인 중 한가지 종류로 부터 생성 되었거나, 모든 합성된 오디오 데이터가 단지 1시간의 자동차 노이즈 소리로 부터 생성 되는 경우와 같은 것 말이다. 하지만, 이 조언의 내용을 지키기는 사실상 힘들다.

데이터 합성에 관해서 일할때, 내가 속했던 팀은 합성된 데이터가 의미있는 영향을 주게끔 하기 위해서, 실제 데이터 분포와 최대한 가까운 정도의 디테일을 가진 합성 데이터를 만들어 내는데 수주(weeks)의 시간이 걸렸었다. 하지만, 디테일에 대한 것을 올바르게 얻을 수만 있다면, 이전보다 훨씬 큰 학습 데이터셋에 어느순간 접근하는것이 가능해질 것이다.