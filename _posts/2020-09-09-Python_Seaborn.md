---
layout: post
title: Seaborn library
---

데이터 분석 공부를 시작한지 3개월 정도 된 것 같다.
마케터로 5년 넘게 근무하면서 콘텐츠와 광고 성과 지표 정도만 읽었기 때문에 실제로 데이터 분석을 하며 어떤 상황에서 어떤 그래프를 그려야 하는지
감이 잘 안왔었는데 이번 강의를 통해 많이 정리된 기분이다.

1. 기초통계량이 같다면 Data set이 같다?
-데이터셋의 기초통계량만 볼 것이 아니라, 실제 시각화를 통해 각 데이터들이 어떤 특성을 갖는지 확인을 해야한다.

1-1. 수치형데이터 X 수치형데이터
-scatterplot / lmplot / jointplot을 사용

1-2. 수치형데이터 X 카테고리형 데이터
-boxplot / violinplot / barplot / heatmap을 사용

1-3. 수치형 데이터 X 위치 정보
-folium library를 사용하여 지도 시각화


2. Seaborn의 기본형태
-seaborn을 sns로 칭한다면,
sns.그래프명(data = 데이터프레임, x = 'x축에 들어갈 데이터 컬럼', y = 'y축에 들어갈 데이터 컬럼', hue = '구분할 카테고리 컬럼')

2-1. scatterplot은 산점도 형태로 기본적으로 점으로 표기되며, 수치형 데이터 간의 회귀 여부를 알 수 있다.

2-2. lmplot 또한 scatterplot과 마찬가지로 수치형 데이터 간의 회귀 여부를 알 수 있고, 회귀선을 함께 그려준다.

2-3. jointplot의 경우 kind 인자에 어떤 값을 주는지에 따라 다른 그래프를 보여준다.
     kind = 'kde'일 경우 밀도 그래프를 그릴 수 있다.
     kind = 'regg'일 경우 회귀 그래프를 그릴 수 있다.
     kind = 'hex'일 경우 kde와 달리 색을 농도로만 밀도를 표기한다.
     
2-4. pairplot은 모든 수치형 데이터에서 두개의 컬럼씩 선택하여 그 관계를 시각화 해준다.
     모든 수치형 데이터를 그리기 때문에 x축과 y축은 따로 지정해주지 않아도 된다.
     hue option을 쓸 수 있다.
     
2-5. boxplot은 카테고리 별 데이터 위치와 기초통계량을 시각화한다.
     다만, 특정 기준에 따른 데이터 분포를 볼 수는 있으나, 데이터 개수를 표현하지 않기 때문에 카테고리마다 데이터 수가 다르거나,
     적을 경우에는 해석에 오류가 있을 수 있다. 이를 방지하기 위해 swarmplot으로 데이터 개수까지 확인한다.
     
2-6. swarmplot은 boxplot의 데이터 분포를 개수로 확인할 수 있는 그래프이며, dodge = True 인자를 통해 hue로 구분한 데이터를 따로 그릴 수 있다.

2-7. heatmap은 수많은 데이터들 중에서 의미 있는 데이터를 골라내기 위해 사용하는 그래프로 sns.heatmap(data = 데이터프레임)의 형식으로 그릴 수 있다.
     수치형으로만 이루어진 데이터 프레임으로 그릴 수 있으며, annot option을 통해 heatmap안에 값을 표기할 수 있다.
     fmt option을 통해 값의 소수점 자리를 설정 할 수도 있으며, cmap으로 heatmap의 색상도 변경할 수 있다.
     (추천 색상 : Reds, Blues, vlag, Pastel1, RdBu_r
     
 
3. 지도 그래프 그리기(folium library)
지도 그래프는 기본적으로 위도, 경도 데이터를 이용해 지도를 그린 후 그 위에 데이터를 추가하는 형식으로 사용한다.

3-1. 지도생성 : folium.Map(location = [위도, 경도], zoom_start = 확대정도)의 기본 형태를 가지는데, 이 때 zoom_start는
              지정한 위도와 경도를 중심으로 확대 범위를 설정하는 것이다.(확대 정도는 숫자로 입력)
              
3-2. 마커추가 : folium.Marker([위도,경도]).add_to(지도 변수명)을 기본형태로 띄며 마우스 오버시 나타날 정보, 마우스 클릭시 나타날 정보를 추가할 수 있다.
              마우스 오버시 나타날 정보 추가 = folium.Marker([위도,경도], tooltip = '정보내용').add_to(지도 변수명)
              마우스 클릭시 나타날 정보 추가 = folium.Marker([위도,경도], popup = '정보내용').add_to(지도 변수명)
              
3-3. 미니맵 추가 : 미니맵은 folium library의 plugins에서 따로 불러온다.(from folium.plugins import MiniMap)
                변수 = MiniMap() %>% 변수.add_to(지도 변수명) 으로 추가 할 수 있다.
                
3-4. 클러스터 마커 : 클러스터 마커는 마커들이 동일 위치에 겹쳐서 많을 때 모아서 보여주는 기능이며,
                 from folium.plugins import MarkerCluster를 통해 불러와 사용한다.
                 변수 = MarkerCluster() %>% 변수.add_to(지도 변수명) 으로 사용한다.
              
![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.
